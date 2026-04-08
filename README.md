# Construction Negotiator — Business Product Spec

Construction Negotiator is a single-user procurement assistant for construction buying. It helps one person manage supplier outreach, collect quotes, run structured negotiations, compare offers, and record final agreements in one place so they can save time, improve buying discipline, and secure better commercial outcomes without juggling email threads and spreadsheets.

## Core Problem

A single buyer often has to manage many supplier conversations at once while also protecting project margins, delivery dates, and supplier relationships. In practice, that work is fragmented across inboxes, spreadsheets, and memory, which makes it hard to compare offers fairly, follow up consistently, and negotiate with confidence.

## Key Capabilities

- Build a project brief once and use it to launch supplier conversations quickly.
- Find and organise suppliers for the relevant trade, material, or package.
- Send clear RFQs and follow-ups without rebuilding each message from scratch.
- Collect and interpret quotes from different email and spreadsheet formats.
- Negotiate on price, lead time, payment terms, and scope using consistent trade-off logic.
- Compare suppliers side by side and log the final deal for future reference.

## Specification Overview

| Spec File | What It Covers | Status |
|---|---|---|
| [docs/01_capabilities.md](docs/01_capabilities.md) | Product capabilities and user value areas | Current |
| [docs/02_negotiation_logic.md](docs/02_negotiation_logic.md) | Business negotiation principles, trade-offs, and guardrails | Current |
| [docs/04_workflows.md](docs/04_workflows.md) | End-to-end user workflow from project setup to agreement logging | Current |
| [docs/06_integrations.md](docs/06_integrations.md) | User-facing integrations for email, spreadsheets, and future connected systems | Current |

## Suggested Additions

- A supplier pre-qualification checklist so the user can filter out weak or risky suppliers before requesting quotes.
- A clear urgency and deadline tracker so late replies and stalled negotiations are easier to manage.
- A simple risk view that highlights unusual exclusions, long lead times, or unfavourable payment terms before agreement.
- A post-award handoff summary so agreed commercial terms can be passed into purchasing or project delivery without rework.
- A reusable supplier performance history so the user can see who consistently responds well, negotiates fairly, and delivers reliably.
