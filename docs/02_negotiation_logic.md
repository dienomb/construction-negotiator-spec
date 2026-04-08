# Negotiation Logic

## Framework: Harvard Principled Negotiation

The system is built on the four principles from *Getting to Yes* (Fisher & Ury):

| Principle | How the AI Applies It |
|-----------|----------------------|
| **Separate people from the problem** | Emails are framed around project needs and market conditions, not personal pressure. |
| **Focus on interests, not positions** | The AI identifies likely supplier interests (steady work, fast payment, repeat business) and constructs offers around them. |
| **Invent options for mutual gain** | Proposes trade-off packages rather than single-variable haggling (e.g., "I can't move on price but can offer 14-day payment terms"). |
| **Insist on objective criteria** | References market benchmarks, published index prices, or previous deal data to anchor positions. |

---

## Trade-Off Matrix

Every negotiation involves balancing multiple variables. The system tracks a **trade-off matrix** for each negotiation:

| Variable | Weight (default) | User-adjustable? | Notes |
|----------|-----------------|-----------------|-------|
| Unit price | High | Yes | Primary objective in most negotiations |
| Lead time / delivery date | Medium | Yes | Critical on time-sensitive projects |
| Payment terms (days) | Medium | Yes | Directly impacts cash flow |
| Warranty / defect liability | Low | Yes | Important for high-risk materials/equipment |
| Minimum order quantity | Low | Yes | Affects smaller projects |
| Scope inclusions/exclusions | High | Yes | Especially relevant for subcontract scope |

The AI uses the user-defined weights to evaluate counter-offer packages holistically rather than optimising on price alone.

---

## BATNA (Best Alternative to a Negotiated Agreement)

Before each negotiation begins, the user (or the system based on historical data) sets:

- **Target price** — the ideal outcome.
- **BATNA price** — the walk-away point; if no agreement is reached above this value, the system recommends rejecting.
- **BATNA alternative** — the fallback supplier or option if this negotiation fails.

The AI will never recommend accepting a deal below the BATNA without explicit user override and confirmation.

---

## Concession Strategy

The system supports configurable concession patterns:

### 1. Diminishing Concessions (default)
Make larger concessions early to signal good faith, smaller ones later to signal a hard limit.

```
Round 1: -5%  →  Round 2: -3%  →  Round 3: -1%  →  Final: hold
```

### 2. Anchor High
Open with an aggressive position, then make a single meaningful concession to land near target.

```
Open: -15%  →  Concession: +8%  →  Final position: -7%
```

### 3. Split the Difference
Signal willingness to meet in the middle when negotiations are near the target zone.

### 4. Variable-Swap
Concede on one variable to hold firm on another (e.g., accept longer lead time to maintain price).

---

## Decision Tree

The AI follows this decision tree during each negotiation cycle:

```
START: New supplier response received
│
├─ Is quoted price within BATNA?
│   ├─ YES → Is it within target?
│   │         ├─ YES → Recommend ACCEPT
│   │         └─ NO  → Generate counter-offer (aim for target, using concession strategy)
│   └─ NO  → Is there a trade-off package that brings total value above BATNA?
│             ├─ YES → Propose trade-off package
│             └─ NO  → Recommend REJECT / escalate to user
│
├─ Has the supplier not responded within the follow-up window?
│   └─ YES → Trigger follow-up email (up to max_follow_ups config)
│
└─ Has max negotiation rounds been reached?
    └─ YES → Present final position; flag for user decision
```

---

## Negotiation Round Limits

| Setting | Default | Notes |
|---------|---------|-------|
| `max_rounds` | 4 | Maximum back-and-forth cycles before escalation |
| `follow_up_wait_days` | 3 | Days before sending a follow-up to non-responsive supplier |
| `max_follow_ups` | 2 | Maximum follow-up emails before marking as unresponsive |

---

## Tone & Relationship Considerations

| Relationship Tier | Recommended Tone | Aggression Level |
|-------------------|-----------------|-----------------|
| New supplier | Professional, formal | Moderate — establish credibility |
| Preferred supplier | Collaborative, direct | Lower — preserve relationship |
| Spot/transactional supplier | Business-like, firm | Higher — price-focused |
| Strategic partner | Consultative | Low — focus on mutual value |

The AI automatically adjusts email language and concession aggressiveness based on the assigned relationship tier.
