---
name: product-prioritization
description: >
  This skill should be used when scoring, ranking, or making roadmap recommendations
  from customer feedback data. Auto-loads for /roadmap-review, /sprint-planning,
  /emerging-signals, and any command that produces a prioritized list or an
  Accelerate/Defer/Stop recommendation. Also triggers when someone asks "what should
  we build next", "how do I prioritize this", or "score these against customer data".
version: 0.1.0
---

# Product Prioritization from Customer Feedback

## The Urgency Scoring Formula

When scoring a feedback theme or roadmap item, calculate a composite urgency score from five weighted signals:

| Signal | Weight | What to Measure |
|---|---|---|
| **Recency** | 25% | How recently has this been mentioned? Last 7 days scores highest; 90+ days scores lowest. |
| **Velocity** | 25% | Is the signal growing, stable, or declining? Accelerating signals score highest. |
| **Account Tier** | 20% | Are affected accounts enterprise, mid-market, or SMB? Enterprise concentration increases urgency. |
| **Volume** | 15% | How many distinct accounts are affected? (Never raw ticket count.) |
| **Coverage Gap** | 15% | Is there existing engineering work planned for this? Unaddressed signals score higher. |

Score each signal 1–5, multiply by weight, sum for total urgency score (max 5.0).

**Use urgency score to rank**, not to make the final decision. A score of 4.2 is a reason to look closely, not an automatic "build it."

## Recommendation Labels

When producing roadmap recommendations, use these exact labels:

| Label | Meaning | When to Apply |
|---|---|---|
| **Accelerate** | Pull this forward | Strong signal (4.0+), growing velocity, enterprise concentration |
| **Maintain** | On track | Moderate signal (2.5–3.9), stable trend, current timeline is appropriate |
| **Defer** | Push back | Low or declining signal (<2.5), or signal doesn't match the item's scope |
| **Merge** | Consolidate | Multiple roadmap items address the same underlying customer need |
| **Stop** | Reconsider | No meaningful customer signal, or signal contradicts the assumption behind the item |
| **NEW** | Not on roadmap | Customer signal exists for a theme with no current roadmap coverage |

Always explain the recommendation in one sentence. A recommendation without reasoning is an opinion.

## Anti-Patterns to Avoid

**Single-account distortion.** A single enterprise account submitting high-volume feedback on a niche request should not score as high-urgency. Weight distinct account count, not ticket count. Flag if a signal is highly concentrated in one account.

**Recency bias.** A new theme from the last 14 days is not automatically more important than a persistent theme. Check velocity: is the new theme growing or a one-off spike?

**Loudest voice bias.** Feature requests from customers who submit the most feedback are not necessarily representative. Check whether the signal appears across account tiers and sizes.

**Completeness illusion.** Feedback coverage is never 100%. Low-volume signals do not mean low impact — they may mean customers aren't submitting feedback on this issue. Flag when a signal is low-volume but high-severity.

## Sprint Backlog Scoring

For sprint planning specifically, use a tactical weighting that adds:

- **Severity** (bugs only): P0 bugs always top the list regardless of other scores
- **Customer commitment**: Issues where a specific customer has been promised a fix

Sprint output should always include:
- Top 5–8 themes by urgency score
- Any P0/P1 bugs surfaced from the same period
- One "sleeper" — a lower-volume signal that is accelerating and worth watching

## Prioritization vs. Sequencing

Urgency scoring tells you what matters. It doesn't tell you what to build next, because that depends on:
- Engineering complexity (not in the data)
- Dependencies (not in the data)
- Strategic bets (not in the data)

Always label the output as **prioritization input**, not a sprint plan or roadmap. The PM makes the sequencing decision.
