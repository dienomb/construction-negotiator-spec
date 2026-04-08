# Workflows — Step-by-Step Flows

## Overview

The system supports three primary workflow types:

1. **Outreach Flow** — from job setup to first supplier contact.
2. **Negotiation Flow** — from first response to agreed deal.
3. **Close & Record Flow** — from agreement to deal archive.

---

## Flow 1: Outreach

```
1. User creates or selects a Project
       │
2. User creates a new Negotiation within the project
   - Selects supplier (existing or new)
   - Sets category (e.g., "structural steel")
   - Uploads or pastes quote request details (scope, BOQ line items, delivery date)
   - Sets target price and BATNA price
   - Chooses concession strategy and tone
       │
3. System generates initial outreach email
   - AI selects the best-fit template for the category and relationship tier
   - Populates with project context, scope summary, and requested terms
   - User reviews and edits (optional)
       │
4. User approves and sends
   - Email dispatched via connected Gmail/Outlook account
   - Negotiation status → "outreach"
   - Follow-up timer started (configurable, default 3 days)
       │
5. If no reply within follow-up window:
   - System sends automated follow-up (up to max_follow_ups)
   - Each follow-up logged as a Message record
```

---

## Flow 2: Negotiation

```
1. Inbound supplier email received (via connected email account)
       │
2. System parses the email
   - Extracts quoted price, payment terms, lead time, and any exclusions
   - Updates negotiation record with `initial_quoted_price` and parsed trade-off values
   - Negotiation status → "in_progress"
       │
3. AI evaluates the quote
   - Checks against target price and BATNA
   - Runs trade-off matrix analysis (weighted score)
   - Selects concession strategy appropriate for the current round
       │
4. AI generates counter-offer
   - Drafts counter-offer email with rationale
   - Suggests alternative trade-off packages if a straight price counter is unlikely to succeed
   - Flags if any proposed terms breach company negotiation policy
       │
5. User reviews counter-offer
   - Can accept AI recommendation, edit, or override entirely
   - Can adjust weights/trade-off priorities before approving
       │
6. Counter-offer sent; round counter incremented
       │
7. Repeat from step 1 until:
   a. Agreement reached → continue to Flow 3
   b. BATNA breached → system recommends rejection; user decides
   c. Max rounds reached → system flags for user decision
   d. Supplier unresponsive → marked as "abandoned" after max follow-ups
```

---

## Flow 3: Close & Record

```
1. User accepts a supplier proposal (or supplier accepts our final offer)
       │
2. System updates negotiation status → "agreed"
   - Records agreed_price, agreed terms in trade_offs table
   - Calculates savings_achieved (initial quote vs. agreed price)
       │
3. Deal record created
   - agreed_price, payment_terms_days, lead_time_days populated
   - User optionally uploads signed PO or contract document
       │
4. Confirmation email generated and sent to supplier
   - Summarises all agreed terms
   - Logged as final outbound Message
       │
5. Supplier profile updated
   - discount_range_pct, reliability_score, payment_terms_typical refreshed
   - New deal added to supplier negotiation history
       │
6. Savings and outcome data flows to Reporting dashboard
```

---

## Flow 4: Batch Outreach (Multiple Suppliers)

```
1. User sets up a "competitive tender" negotiation group
   - Selects 2–10 suppliers for the same scope
   - Sets shared scope/BOQ and terms
       │
2. System sends simultaneous outreach to all selected suppliers
   - Each supplier gets an individualised email (tone/relationship-adjusted)
   - Each supplier tracked as a separate Negotiation record
       │
3. As quotes arrive, system aggregates them into a comparison view
   - Side-by-side: price, terms, lead time, total weighted score
       │
4. User selects preferred supplier(s) to continue negotiating
   - Remaining suppliers receive a polite "not successful this time" email
   - System records outcome for all suppliers
```

---

## Flow 5: Approval Workflow (Enterprise)

```
1. AI recommends accepting a deal
       │
2. Deal value > approval threshold configured by admin?
   ├─ NO  → User can accept immediately
   └─ YES → Approval request generated
                │
             3. Notification sent to approver (email + in-app)
                │
             4. Approver reviews deal summary and negotiation history
                │
             5. Approver: APPROVE or REJECT (with reason)
                │
             APPROVE → deal confirmed, supplier notified
             REJECT  → negotiation re-opened or abandoned
```

---

## Status State Machine

```
draft → outreach → in_progress → agreed
                              → rejected
                              → abandoned
outreach → abandoned (no response after max follow-ups)
```

All status transitions are logged with timestamp and acting user.
