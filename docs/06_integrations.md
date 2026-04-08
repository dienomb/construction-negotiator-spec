# Integrations

## Overview

The platform integrates with email clients for sending/receiving negotiation messages, and with spreadsheet tools for importing and exporting deal data. Future integrations will connect to construction-specific CRM and ERP platforms.

---

## 1. Gmail Integration

### Purpose
Send outbound negotiation emails and receive inbound supplier replies directly within the platform, without requiring users to switch between tools.

### Method
- **OAuth 2.0** — user authorises the platform to access their Gmail account with the `gmail.send` and `gmail.readonly` scopes.
- The platform stores a refresh token (encrypted at rest); access tokens are fetched on demand.

### Outbound (sending)
- Emails are composed by the AI and approved by the user in the platform UI.
- Sent via the Gmail API (`messages.send`), appearing in the user's Sent folder as if sent manually.
- Thread ID stored in the `messages` table for reply tracking.

### Inbound (receiving)
- Platform polls Gmail via `messages.list` (or webhook via Gmail Push Notifications) for new replies on tracked threads.
- New messages matching a tracked thread ID are fetched, decrypted, and stored as `direction = 'inbound'` records.
- AI parsing prompt (see `05_ai_prompts.md §2`) is triggered automatically on new inbound messages.

### Scopes Required
| Scope | Reason |
|-------|--------|
| `https://www.googleapis.com/auth/gmail.send` | Send outbound emails |
| `https://www.googleapis.com/auth/gmail.readonly` | Read inbound replies |
| `https://www.googleapis.com/auth/gmail.modify` | Mark messages as read |

### Data Privacy
- Email content is stored encrypted in the platform database.
- Users can revoke access at any time; stored tokens are deleted on revocation.
- Email bodies are sent to the AI model (OpenAI/Anthropic) for parsing; no PII beyond the email content is shared.

---

## 2. Microsoft Outlook / Microsoft 365 Integration

### Purpose
Same as Gmail integration for users on the Microsoft ecosystem.

### Method
- **Microsoft OAuth 2.0** (MSAL) with Microsoft Graph API.
- Scopes: `Mail.Send`, `Mail.ReadWrite`.

### Notes
- Functionally identical to Gmail integration; abstracted behind a common `EmailProvider` interface in the backend.
- Exchange Server (on-premise) support is out of scope for v1; may be added in a future release.

---

## 3. Excel / CSV Integration

### Purpose
Allow users to import quote comparisons, BOQs, and supplier lists from spreadsheets, and export deal summaries and savings reports.

### Import: Quote Comparison Sheet

Users can upload an `.xlsx` or `.csv` file with columns:

| Expected Column | Maps To |
|----------------|---------|
| `Supplier Name` | `suppliers.name` |
| `Unit Price` | `negotiations.initial_quoted_price` |
| `Lead Time (days)` | `trade_offs.initial_value` (lead_time) |
| `Payment Terms (days)` | `trade_offs.initial_value` (payment_terms) |
| `Notes` | `messages.body` (first inbound) |

The import wizard allows column mapping if headers differ from expected names.

### Import: Supplier List

Bulk import suppliers with columns: Name, Category, Contact Name, Contact Email, Phone, Relationship Tier.

### Export: Deal Summary

Export a negotiation summary (all rounds, agreed terms, savings) to `.xlsx` or `.pdf`.

### Export: Savings Report

Export an aggregated savings report by project, category, or period to `.xlsx`.

### Implementation Notes
- Use `xlsx` (SheetJS) on the frontend for client-side parsing.
- Server-side validation and normalisation before database write.
- Large imports (>500 rows) are processed asynchronously with a progress indicator.

---

## 4. Future Integration: Procore (CRM / Project Management)

### Purpose
Sync project data and awarded subcontract/purchase order information with Procore, reducing double-entry.

### Planned Flows
- **Inbound from Procore:** Import project details and commitments to create negotiation contexts automatically.
- **Outbound to Procore:** Push agreed deal terms as a draft commitment or budget line item.

### API
- Procore REST API v1.
- OAuth 2.0 with `projects.read`, `commitments.write` scopes.

### Status: Not in v1 — planned for v2.

---

## 5. Future Integration: Sage / ERP

### Purpose
Export agreed purchase orders or subcontract terms directly to accounting/ERP systems.

### Planned Flows
- Create a PO in Sage 300 / Sage Intacct when a deal is agreed.
- Map supplier, amount, payment terms, and project cost code.

### Status: Not in v1 — planned for v2, subject to customer demand.

---

## 6. Future Integration: Slack / Teams Notifications

### Purpose
Send deal alerts, approval requests, and follow-up reminders to Slack or Microsoft Teams channels.

### Planned Flows
- Notify a channel when a supplier replies with a new quote.
- Post approval request to a designated channel.
- Daily digest of open negotiations and pending actions.

### Status: Not in v1 — planned for v2.

---

## Integration Architecture

```
┌─────────────────────────────────────────────────────────┐
│                   Application Backend                   │
│                                                         │
│  EmailService (interface)                               │
│   ├── GmailProvider  ─────────────── Gmail API          │
│   └── OutlookProvider ─────────────  Graph API          │
│                                                         │
│  SpreadsheetService                                     │
│   ├── Import parser (SheetJS)                           │
│   └── Export renderer (xlsx / pdf)                      │
│                                                         │
│  WebhookService (inbound)                               │
│   ├── Gmail Push Notifications                          │
│   └── MS Graph change notifications                     │
│                                                         │
│  [Future] ERP Connector                                 │
│   ├── ProcoreAdapter                                    │
│   └── SageAdapter                                       │
└─────────────────────────────────────────────────────────┘
```

All external API credentials are stored as encrypted secrets in the platform's secrets manager (e.g., AWS Secrets Manager or Vault), never in environment variables committed to source control.
