# Data Model

## Overview

The database is relational (PostgreSQL). The core entities are: **Companies**, **Suppliers**, **Projects**, **Negotiations**, **Messages**, and **Deals**.

---

## Entity Relationship Diagram (text)

```
Company
  └─< Project
  └─< Supplier

Supplier
  └─< SupplierContact
  └─< NegotiationHistory (aggregate view)

Project
  └─< Negotiation
        └─< Message
        └─< Deal
        └─< TradeOff
```

---

## Tables

### `companies`
Represents the customer (the contractor firm using the platform).

| Column | Type | Notes |
|--------|------|-------|
| `id` | UUID PK | |
| `name` | TEXT | |
| `subscription_tier` | ENUM | `free`, `pro`, `enterprise` |
| `negotiation_policy` | JSONB | Company-wide rules (see Capabilities §8) |
| `created_at` | TIMESTAMPTZ | |

---

### `users`
People within a company who use the platform.

| Column | Type | Notes |
|--------|------|-------|
| `id` | UUID PK | |
| `company_id` | UUID FK → companies | |
| `email` | TEXT UNIQUE | |
| `full_name` | TEXT | |
| `role` | ENUM | `admin`, `negotiator`, `viewer` |
| `created_at` | TIMESTAMPTZ | |

---

### `projects`
A construction project, which provides context for one or more negotiations.

| Column | Type | Notes |
|--------|------|-------|
| `id` | UUID PK | |
| `company_id` | UUID FK → companies | |
| `name` | TEXT | |
| `description` | TEXT | |
| `start_date` | DATE | |
| `end_date` | DATE | |
| `budget` | NUMERIC(15,2) | Overall project budget |
| `status` | ENUM | `active`, `completed`, `archived` |
| `created_by` | UUID FK → users | |
| `created_at` | TIMESTAMPTZ | |

---

### `suppliers`
External suppliers, vendors, or subcontractors.

| Column | Type | Notes |
|--------|------|-------|
| `id` | UUID PK | |
| `company_id` | UUID FK → companies | Scoped to customer company |
| `name` | TEXT | |
| `category` | TEXT | e.g., `concrete`, `steel`, `electrical` |
| `relationship_tier` | ENUM | `new`, `preferred`, `transactional`, `strategic` |
| `payment_terms_typical` | INT | Typical days (e.g., 30, 60) |
| `discount_range_pct` | NUMRANGE | Historical discount range offered |
| `reliability_score` | NUMERIC(3,2) | 0.00–1.00 |
| `price_competitiveness_score` | NUMERIC(3,2) | 0.00–1.00 |
| `notes` | TEXT | |
| `created_at` | TIMESTAMPTZ | |

---

### `supplier_contacts`
Individual contacts at a supplier company.

| Column | Type | Notes |
|--------|------|-------|
| `id` | UUID PK | |
| `supplier_id` | UUID FK → suppliers | |
| `name` | TEXT | |
| `email` | TEXT | |
| `phone` | TEXT | |
| `is_primary` | BOOLEAN | |
| `created_at` | TIMESTAMPTZ | |

---

### `negotiations`
A single negotiation thread between the company and a supplier, within a project.

| Column | Type | Notes |
|--------|------|-------|
| `id` | UUID PK | |
| `project_id` | UUID FK → projects | |
| `supplier_id` | UUID FK → suppliers | |
| `created_by` | UUID FK → users | |
| `status` | ENUM | `draft`, `outreach`, `in_progress`, `agreed`, `rejected`, `abandoned` |
| `category` | TEXT | Material/scope category |
| `target_price` | NUMERIC(15,2) | |
| `batna_price` | NUMERIC(15,2) | Walk-away point |
| `batna_alternative` | TEXT | Description of fallback option |
| `initial_quoted_price` | NUMERIC(15,2) | First quote received |
| `agreed_price` | NUMERIC(15,2) | NULL until deal is closed |
| `savings_achieved` | NUMERIC(15,2) | Computed: `initial_quoted_price - agreed_price` |
| `rounds_completed` | INT | |
| `concession_strategy` | ENUM | `diminishing`, `anchor_high`, `split_difference`, `variable_swap` |
| `tone` | ENUM | `formal`, `professional`, `collaborative` |
| `started_at` | TIMESTAMPTZ | |
| `closed_at` | TIMESTAMPTZ | |

---

### `messages`
Individual emails/messages within a negotiation thread.

| Column | Type | Notes |
|--------|------|-------|
| `id` | UUID PK | |
| `negotiation_id` | UUID FK → negotiations | |
| `direction` | ENUM | `outbound` (to supplier), `inbound` (from supplier) |
| `sender_email` | TEXT | |
| `recipient_email` | TEXT | |
| `subject` | TEXT | |
| `body` | TEXT | |
| `sent_at` | TIMESTAMPTZ | |
| `parsed_price` | NUMERIC(15,2) | AI-extracted price from inbound message |
| `parsed_terms` | JSONB | AI-extracted terms (lead time, payment, etc.) |
| `ai_reasoning` | TEXT | AI explanation of why this message was generated |
| `template_id` | UUID FK → message_templates | NULL if custom |

---

### `trade_offs`
Tracks the variable-level trade-off state for each negotiation.

| Column | Type | Notes |
|--------|------|-------|
| `id` | UUID PK | |
| `negotiation_id` | UUID FK → negotiations | |
| `variable` | TEXT | e.g., `payment_terms`, `lead_time`, `warranty` |
| `weight` | NUMERIC(3,2) | User-defined importance weight |
| `initial_value` | TEXT | Supplier's initial position |
| `target_value` | TEXT | Buyer's target |
| `agreed_value` | TEXT | NULL until resolved |
| `updated_at` | TIMESTAMPTZ | |

---

### `message_templates`
Reusable email templates for outreach, follow-ups, counters.

| Column | Type | Notes |
|--------|------|-------|
| `id` | UUID PK | |
| `company_id` | UUID FK → companies | NULL = system template |
| `name` | TEXT | |
| `type` | ENUM | `initial_outreach`, `follow_up`, `counter_offer`, `acceptance`, `rejection` |
| `tone` | ENUM | `formal`, `professional`, `collaborative` |
| `subject_template` | TEXT | Handlebars/Jinja variables supported |
| `body_template` | TEXT | |
| `created_at` | TIMESTAMPTZ | |

---

### `deals`
Finalised deal record, created when a negotiation reaches `agreed` status.

| Column | Type | Notes |
|--------|------|-------|
| `id` | UUID PK | |
| `negotiation_id` | UUID FK → negotiations | |
| `agreed_price` | NUMERIC(15,2) | |
| `agreed_payment_terms_days` | INT | |
| `agreed_lead_time_days` | INT | |
| `agreed_terms_summary` | TEXT | Free-text summary of all agreed terms |
| `signed_document_url` | TEXT | Link to uploaded signed contract/PO |
| `created_at` | TIMESTAMPTZ | |

---

## Indexes

```sql
CREATE INDEX idx_negotiations_project      ON negotiations(project_id);
CREATE INDEX idx_negotiations_supplier     ON negotiations(supplier_id);
CREATE INDEX idx_negotiations_status       ON negotiations(status);
CREATE INDEX idx_messages_negotiation      ON messages(negotiation_id);
CREATE INDEX idx_messages_direction        ON messages(direction);
CREATE INDEX idx_suppliers_company_cat     ON suppliers(company_id, category);
```
