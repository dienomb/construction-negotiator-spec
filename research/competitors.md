# Competitor Research

## Overview

Three primary AI-powered procurement / negotiation platforms were identified as the most relevant comparators: **Pactum**, **LightSource.ai**, and **Zepth**. Each targets slightly different segments and use cases.

---

## 1. Pactum

**Website:** pactum.com  
**Founded:** 2019  
**HQ:** San Francisco, CA (Estonian founders)  
**Stage:** Series B (~$55M raised as of 2023)

### What They Do
Pactum is an autonomous negotiation AI platform used by large enterprises (Walmart, Maersk, Home Depot) to negotiate commercial terms with long-tail suppliers at scale. The system conducts fully autonomous multi-round negotiations via structured chatbot interactions, targeting payment terms, pricing, and contract conditions.

### Key Strengths
- Proven at Fortune 500 scale (Walmart public case study).
- Fully autonomous negotiation (no human in the loop for standard negotiations).
- Reported outcomes: 3–5% cost savings; 2–3× supplier engagement vs. manual.
- Sophisticated multi-variable optimisation using game theory and Nash bargaining.
- Well-funded and credible.

### Key Weaknesses
- Enterprise-only; minimum contract sizes make it inaccessible to SMBs.
- Not construction-specific; lacks BOQ import, project-based context, or subcontract scope handling.
- Supplier interaction is via a dedicated Pactum portal/chatbot, not email — requires supplier adoption, which is a barrier for smaller construction suppliers.
- No Gmail/Outlook integration for native email-based negotiation.

### Pricing
Not public; enterprise contracts only. Estimated $50K–$500K+ ACV.

### Relevance to Us
Pactum validates the market for AI negotiation automation at scale. Their limitation is that they are built for large enterprises with structured supplier portals — not for construction SMBs who negotiate via email with local subcontractors and material suppliers.

---

## 2. LightSource.ai

**Website:** lightsource.ai  
**Founded:** 2021  
**HQ:** San Francisco, CA  
**Stage:** Series A (~$26M raised as of 2023)

### What They Do
LightSource is a strategic sourcing and supplier discovery platform with AI-powered RFQ management and supplier recommendations. It focuses on manufacturing procurement (electronics, mechanical components) rather than construction. Key features include supplier search, RFQ automation, and quote comparison.

### Key Strengths
- Strong supplier discovery and RFQ workflow.
- AI-powered supplier matching and recommendation.
- Clean UI; well-suited to category managers doing strategic sourcing.
- Integration with procurement workflows.

### Key Weaknesses
- Not a negotiation platform — it handles RFQ and quote comparison but does not automate counter-offers or multi-round negotiations.
- Manufacturing-focused (PCBs, machined parts); no construction-specific features.
- No email-based negotiation; no Harvard-framework logic.
- No subcontract scope management (construction labour, trades).

### Pricing
Not public; estimated $15K–$60K ACV for SMB/mid-market manufacturing.

### Relevance to Us
LightSource shows strong demand for AI-assisted sourcing in manufacturing. The gap: construction firms need a negotiation engine (counter-offers, concessions, BATNA tracking), not just RFQ + quote comparison. Our product fills this gap for the construction vertical.

---

## 3. Zepth

**Website:** zepth.com  
**Founded:** 2017  
**HQ:** Dubai, UAE  
**Stage:** Series A

### What They Do
Zepth is a construction project management and procurement platform focused on the Middle East and emerging markets. It covers project scheduling, procurement workflows, vendor management, and document control. Not AI-native; procurement is workflow-based rather than AI-driven.

### Key Strengths
- Deep construction vertical focus (site management, BOQ, vendor approvals).
- Strong in Middle East/GCC markets (regulatory, local compliance features).
- Procurement module handles purchase requisitions, vendor comparison, PO issuance.

### Key Weaknesses
- No AI negotiation capability; vendor management is manual and form-based.
- Limited to structured procurement workflows; no conversational/email-based negotiation.
- Geographic focus limits TAM for global expansion.
- Legacy UX; less intuitive than modern SaaS tools.

### Pricing
Not public; project-based licensing. Estimated $10K–$50K per implementation.

### Relevance to Us
Zepth confirms that the construction vertical needs dedicated procurement tooling. The gap: Zepth is a project management tool with a procurement module — it doesn't negotiate. We are a negotiation-first platform that can eventually integrate with tools like Zepth (or Procore) as a negotiation layer.

---

## Competitive Positioning Summary

| Capability | Pactum | LightSource | Zepth | **Us (v1)** |
|-----------|--------|-------------|-------|-------------|
| AI negotiation (multi-round) | ✅ | ❌ | ❌ | ✅ |
| Email-native (Gmail/Outlook) | ❌ | ❌ | ❌ | ✅ |
| Construction-specific | ❌ | ❌ | ✅ | ✅ |
| SMB pricing | ❌ | Partial | Partial | ✅ |
| Harvard negotiation framework | ✅ | ❌ | ❌ | ✅ |
| BOQ / project context | ❌ | ❌ | ✅ | ✅ |
| Subcontract scope handling | ❌ | ❌ | Partial | ✅ |
| BATNA / concession tracking | ✅ | ❌ | ❌ | ✅ |

### Our Differentiated Position
**We are the only email-native, construction-specific AI negotiation platform built for SMBs.**

- Unlike Pactum: we work via email (no supplier portal adoption required) and serve SMBs at accessible price points.
- Unlike LightSource: we automate the full negotiation cycle (counter-offers, concessions), not just RFQ.
- Unlike Zepth: we are negotiation-first, AI-native, and not tied to project management workflows.
