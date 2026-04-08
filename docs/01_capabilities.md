# Capabilities — Full Feature List

## 1. Supplier Outreach Automation

- **Templated outreach emails** — pre-built, tone-matched templates for initial quote requests, follow-ups, and counter-offers.
- **Batch outreach** — send personalised requests to multiple suppliers simultaneously from a single job/project context.
- **Follow-up scheduling** — automatic reminders and follow-up emails if suppliers have not responded within a configurable window.
- **Response parsing** — extract key values (price, lead time, payment terms, exclusions) from inbound supplier replies using AI.

## 2. Negotiation Engine

- **Harvard Principled Negotiation** — the AI frames positions around interests, not positions; surfaces objective criteria; seeks mutual gains (see `02_negotiation_logic.md`).
- **Trade-off management** — explicit handling of price vs. lead time vs. payment terms vs. warranty/scope.
- **Dynamic counter-offer generation** — AI suggests counter-offer text and rationale based on current gap, BATNA, and supplier history.
- **BATNA tracking** — user defines their Best Alternative to a Negotiated Agreement (walk-away point); system enforces it.
- **Concession strategy** — configurable concession patterns (e.g., diminishing concessions, anchor-high, split-the-difference).

## 3. Deal Tracking & Pipeline

- **Negotiation pipeline view** — kanban-style board showing all active negotiations by stage (Outreach → Response → Counter → Agreed / Dead).
- **Per-negotiation timeline** — full message history, AI reasoning log, and outcome tracking.
- **Outcome recording** — won price, terms, concessions made, time-to-close.
- **Win/loss analysis** — aggregated stats on which strategies, templates, and trade-offs produce the best outcomes per supplier category.

## 4. Supplier Intelligence

- **Supplier profiles** — history of past deals, preferred payment terms, typical discount range, response times.
- **Category benchmarks** — price benchmarks by material category derived from historical deal data.
- **Supplier scoring** — reliability, price competitiveness, and responsiveness scores.
- **Relationship risk flags** — alerts when proposed negotiation tactics may damage a flagged "key relationship" supplier.

## 5. Document & Data Management

- **Excel/CSV import** — import quote sheets, BOQs (bills of quantities), and supplier lists.
- **Contract summary extraction** — upload PDF/DOCX contracts; AI extracts key commercial terms.
- **Audit trail export** — export full negotiation history to PDF or CSV for project records.

## 6. Integrations

- **Gmail / Outlook** — send and receive negotiation emails directly from the platform.
- **Excel** — import quote comparisons; export agreed terms.
- **Future: CRM/ERP** — sync supplier data and deal outcomes to Procore, Sage, or custom ERP (see `06_integrations.md`).

## 7. Reporting & Analytics

- **Savings dashboard** — total cost savings vs. initial quoted price, by project, category, and period.
- **Negotiation velocity** — average time from outreach to agreement.
- **Supplier performance** — which suppliers are easiest to negotiate with, fastest to respond, most likely to discount.
- **AI confidence scores** — per-negotiation model confidence in recommended strategy.

## 8. Configuration & Governance

- **Role-based access** — admin, negotiator, view-only roles.
- **Approval workflows** — deals above a threshold require a second-level approval before acceptance.
- **Company negotiation policy** — define company-wide rules (e.g., always request 2% early-payment discount, never accept >90-day payment terms).
- **Tone settings** — formal, professional, or collaborative — adjustable per supplier category or relationship tier.
