# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repository Is

This is a **business product specification** for Construction Negotiator — an AI-powered procurement assistant for construction buying. There is no application code, no build system, and no tests. The repo contains only Markdown documents, a PDF, and a README.

## Repository Structure

- `docs/` — Product specification documents covering capabilities, negotiation logic, workflows, and integrations
- `client/` — Client-facing materials (partner questionnaire in Spanish, available as `.md` and `.pdf`)
- `README.md` — Product overview and spec file index

## Working With This Repo

- **Language**: Spec docs (`docs/`) are written in English. Client-facing materials (`client/`) are in Spanish.
- **PDF generation**: The partner questionnaire exists as both `cuestionario_socio.md` and `cuestionario_socio.pdf`. When the Markdown source changes, the PDF should be regenerated to stay in sync.
- **Spec numbering**: Doc files use a numbering scheme (`01_`, `02_`, `04_`, `06_`). Gaps exist intentionally — preserve the existing numbering when adding new documents.
- **Suggested Additions sections**: Several docs end with a "Suggested Additions" section listing future enhancements. These are aspirational, not committed scope.

## Domain Context

The product implements **Harvard Principled Negotiation** (Fisher & Ury) as its core framework. Key domain concepts used throughout the specs:

- **BATNA** — Best Alternative to a Negotiated Agreement (the walk-away point)
- **Trade-off matrix** — Weighted variables (price, lead time, payment terms, warranty, MOQ, scope) evaluated holistically
- **Concession strategies** — Diminishing concessions, anchor-high, split-the-difference, variable-swap
- **Relationship tiers** — New, preferred, spot/transactional, strategic partner — each with different tone and aggression levels
- **RFQ** — Request for Quotation, the standard outreach to suppliers

The workflow follows seven stages: Project Setup, Supplier Discovery, Outreach (RFQ), Quote Collection, Autonomous Negotiation, Vendor Comparison/Scoring, Agreement/Deal Logging.
