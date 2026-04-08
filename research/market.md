# Market Research — Size, Opportunity & Pricing

## 1. Market Overview

### Construction Industry Scale
- Global construction output: **~$13.5 trillion** (2024, GlobalData).
- Procurement and materials typically represent **60–70% of project cost** for general contractors.
- That implies **$8–9 trillion** in construction procurement spend annually — even a small improvement in negotiated outcomes represents enormous value.

### Procurement Software Market
- Global construction procurement software market: **~$2.1 billion** (2023), growing at **~11% CAGR** through 2030 (Grand View Research).
- Broader procurement automation software market: **~$9.7 billion** (2023), growing at **~12% CAGR** (MarketsandMarkets).
- AI in procurement: estimated **$6.9 billion** by 2030, growing at **~28% CAGR** from 2023 (Fortune Business Insights).

---

## 2. Target Market Segmentation

### Tier 1 — Small General Contractors (Primary Beachhead)
- **Definition:** $2M–$20M annual revenue; 5–30 employees; 1–3 project managers.
- **Volume:** ~180,000 firms in the US (Census Bureau); ~25,000 in Australia; ~60,000 in the UK.
- **Pain:** No dedicated procurement function; owners/PMs negotiate ad hoc via email.
- **Willingness to pay:** $200–$800/month per firm.
- **SAM (US only):** 180,000 firms × 20% addressable × $400/month avg = **~$172M ARR**.

### Tier 2 — Mid-Size Contractors and Specialty Subcontractors
- **Definition:** $20M–$200M revenue; 30–200 employees; dedicated estimators/PMs.
- **Volume:** ~25,000 firms in the US; ~5,000 in Australia.
- **Pain:** Multiple PMs with inconsistent negotiation outcomes; no institutional memory.
- **Willingness to pay:** $800–$3,000/month per firm.
- **SAM (US only):** 25,000 firms × 25% addressable × $1,500/month avg = **~$112M ARR**.

### Tier 3 — Enterprise / Large GCs (Future)
- **Definition:** $200M+ revenue; formal procurement departments.
- **Note:** Longer sales cycles; potential Pactum territory. Not a primary focus for v1.

### Total Serviceable Addressable Market (US alone)
**~$284M ARR** for Tiers 1–2 in the US.

Adding UK, Australia, and Canada: estimated **~$500M ARR global SAM** for Tiers 1–2.

---

## 3. Go-to-Market Strategy

### Phase 1 (0–12 months): Beachhead
- Target Tier 1 GCs in 1–2 metro markets (e.g., Sydney or Melbourne for AU, or one US city).
- Direct outreach via LinkedIn and construction industry associations (e.g., Master Builders, AGC).
- Offer free trial (3 negotiations) to reduce friction.
- Build 10–20 case studies with measurable savings outcomes.

### Phase 2 (12–24 months): Scale
- Expand to additional metro markets and English-speaking markets (US, UK, CA).
- Add Tier 2 pricing tier and approval workflows.
- Partner with construction accountants, estimating consultants, and project management SaaS (Procore, Buildertrend) for referrals.

### Phase 3 (24–36 months): Platform
- Introduce marketplace features (supplier benchmarks, anonymised deal data).
- ERP/CRM integrations to move up-market toward Tier 3.
- Explore international expansion (Middle East, SE Asia construction boom markets).

---

## 4. Pricing Model

### Subscription Tiers (Monthly, billed annually)

| Tier | Price | Included | Target |
|------|-------|----------|--------|
| **Starter** | $199/month | 1 user; 10 active negotiations; Gmail integration; basic reporting | Solo owner-operators |
| **Pro** | $499/month | 3 users; unlimited negotiations; Gmail + Outlook; full reporting; approval workflows | Small GCs, 5–30 staff |
| **Business** | $1,199/month | 10 users; unlimited negotiations; all integrations; API access; priority support | Mid-size contractors |
| **Enterprise** | Custom | Unlimited users; SSO; SLA; dedicated CSM; ERP integration | Large GCs, $100M+ revenue |

### Value-Based Pricing Rationale
- A 3% saving on a $500K materials package = **$15,000 saved**.
- A $499/month subscription = **$5,988/year**.
- A single successful negotiation on a mid-size project delivers **2.5× ROI** on the annual subscription.
- This makes the value proposition easy to demonstrate and easy for a PM to justify to their principal.

### AI Usage Costs (Internal — not passed through directly)
- Per-negotiation AI cost estimate (parsing + evaluation + 4 rounds drafting):
  - GPT-4o: ~$0.15–$0.40 per negotiation.
  - GPT-4o-mini (parsing only): ~$0.02 per negotiation.
- At 100 negotiations/month per Pro customer, AI cost ≈ **$15–40/month** vs. $499 revenue = healthy margin.

---

## 5. Unit Economics (Pro Tier Illustration)

| Metric | Value |
|--------|-------|
| MRR per customer | $499 |
| Annual contract value | $5,988 |
| Direct AI costs/month | ~$25 |
| Gross margin target | ~80% |
| Target CAC | <$2,000 |
| Target LTV (3yr retention) | ~$18,000 |
| LTV:CAC ratio target | >9:1 |

---

## 6. Key Market Trends

### AI Adoption in Construction
- Construction has historically lagged other industries in software adoption, but **AI adoption is accelerating post-2023** as LLM tools become accessible to non-technical users.
- McKinsey (2024): construction firms using AI in procurement report **12–18% reduction in procurement cycle time** and **4–8% cost savings** on materials.

### Labour Shortages Driving Automation
- Skilled labour shortages across construction markets (US, AU, UK) are forcing firms to do more with fewer administrative staff — creating demand for tools that automate repetitive tasks like supplier outreach and follow-up.

### Margin Pressure
- Construction profit margins are thin (average net margin **2–6%** for general contractors).
- Even a **1–2% improvement in procurement costs** can double or triple net profit on a project — making procurement optimisation a high-priority investment.

### Email-First Communication in Construction
- Unlike enterprise procurement, construction SMBs conduct the vast majority of supplier communication via **email** (not supplier portals or ERPs).
- This is a structural advantage: our Gmail/Outlook-native approach meets users where they already work, minimising adoption friction.

---

## 7. Risks & Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| Pactum moves down-market | Medium | High | Build construction-specific features and SMB pricing that large platforms can't easily replicate |
| Supplier resistance to AI-drafted emails | Medium | Medium | Emails are user-approved; indistinguishable from manually written emails |
| LLM API cost inflation | Low | Medium | Multi-provider routing (OpenAI + Anthropic); prompt optimisation; caching |
| Data privacy concerns (email content) | Medium | High | Strong encryption; clear privacy policy; data residency options for EU |
| Low SMB retention / high churn | Medium | High | Demonstrate measurable savings in onboarding; in-app savings dashboard is the primary retention hook |
