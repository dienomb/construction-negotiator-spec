# Construction Negotiator — Product Spec

## Vision

Build an AI-powered negotiation assistant that helps construction companies, contractors, and procurement teams secure better deals with suppliers — faster, more consistently, and at scale. The system automates outreach, applies proven negotiation frameworks, and learns over time which strategies win.

## Problem

Construction procurement is slow, relationship-dependent, and opaque. Procurement managers spend hours crafting individual supplier emails, negotiating on gut feel, and tracking outcomes across spreadsheets. There is no institutional memory of what worked, no systematic approach to trade-offs, and no way to run concurrent negotiations at scale.

Key pain points:
- **Inconsistent outcomes** — different project managers get wildly different prices from the same suppliers.
- **Time-intensive manual process** — each negotiation is bespoke; no reuse of successful tactics.
- **No data feedback loop** — wins and losses are not recorded in a way that improves future negotiations.
- **Limited leverage** — small/mid-size firms lack the volume to command large-enterprise pricing.
- **Supplier relationship risk** — aggressive tactics can damage long-term relationships if applied clumsily.

## Target User

**Primary:** Procurement managers and project directors at small-to-mid-size general contractors and specialty subcontractors (5–200 employees, $2M–$200M annual revenue).

**Secondary:** Owners and estimators at construction firms who handle their own supplier negotiations without dedicated procurement staff.

**Characteristics:**
- Comfortable with email and basic spreadsheets; not necessarily technical.
- Negotiate with 10–100 suppliers across materials, equipment, and subcontract scope.
- Time-constrained — need automation that feels like a smart assistant, not a tool they have to babysit.
- Value relationships but also need to hit project margins.

## Documentation

| File | Description |
|------|-------------|
| [docs/01_capabilities.md](docs/01_capabilities.md) | Full feature list |
| [docs/02_negotiation_logic.md](docs/02_negotiation_logic.md) | Harvard style, trade-offs, decision tree |
| [docs/03_data_model.md](docs/03_data_model.md) | Database tables, relationships |
| [docs/04_workflows.md](docs/04_workflows.md) | Step-by-step flows (outreach → negotiate → agree) |
| [docs/05_ai_prompts.md](docs/05_ai_prompts.md) | All system prompts, negotiation strategies |
| [docs/06_integrations.md](docs/06_integrations.md) | Gmail, Excel, future CRM/ERP |
| [docs/07_architecture.md](docs/07_architecture.md) | Tech stack, scaling plan |
| [research/competitors.md](research/competitors.md) | Pactum, LightSource, Zepth findings |
| [research/market.md](research/market.md) | Market size, opportunity, pricing |
