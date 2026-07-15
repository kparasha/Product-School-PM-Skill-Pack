---
description: Score roadmap items against customer feedback
argument-hint: [roadmap items to evaluate]
allowed-tools: Read
---

Compare roadmap items against customer feedback from ~~feedback tool and produce a scored recommendation for each.

Parse $ARGUMENTS:
- No args → run a landscape scan: identify the top 10–15 customer feedback themes and check which, if any, have roadmap coverage. This is most useful for quarterly reviews.
- Pasted roadmap items → score each item against the current feedback signal.

Apply the `product-prioritization` skill throughout.

**For each roadmap item (or top feedback theme):**

1. Find matching feedback signal — search for customer mentions of the problem this item addresses, not the solution. Customers describe pain, not features.

2. Calculate urgency score using the formula from `product-prioritization`:
   - Recency, Velocity, Account Tier, Volume, Coverage Gap (each scored 1–5 and weighted)

3. Assign a recommendation label:
   - **Accelerate** — strong signal, high urgency, consider pulling forward
   - **Maintain** — moderate signal, current timeline appropriate
   - **Defer** — low or declining signal, consider pushing back
   - **Merge** — multiple items address the same underlying need
   - **Stop** — no meaningful signal, or signal contradicts the item's assumption
   - **NEW** — a signal exists for a theme with no current roadmap coverage

4. Write one sentence explaining the recommendation.

Format output as a scored table:

| Roadmap Item | Urgency Score | Affected Accounts | Trend | Recommendation | Rationale |
|---|---|---|---|---|---|

For NEW flags (signals without roadmap coverage), describe the unaddressed theme in one paragraph with account count, trend, and a representative quote.

Apply the `customer-evidence-synthesis` skill for all quote selection.

End with a summary of the most important findings (top Accelerate, top Stop, and any NEW flags) and a limitations section.
