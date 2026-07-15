---
description: Customer-evidence-ranked sprint backlog
argument-hint: [feature-area]
allowed-tools: Read
---

Generate a customer-evidence-ranked sprint backlog using feedback from ~~feedback tool.

Parse $ARGUMENTS:
- No args → all themes, auto-categorized
- Feature area (e.g. `"Analytics"`) → scoped to that area

Apply the `product-prioritization` and `severity-classification` skills throughout.

**Step 1: Surface top themes**
Identify the 10–15 most prominent feedback themes from the last 30 days. Count distinct affected accounts for each.

**Step 2: Score each theme**
Apply the urgency scoring formula from the `product-prioritization` skill:
- Recency (25%) — how recently has this been mentioned?
- Velocity (25%) — is it growing, stable, or declining?
- Account Tier (20%) — enterprise or SMB concentration?
- Volume (15%) — distinct account count
- Coverage Gap (15%) — is there existing work planned for this?

**Step 3: Surface bugs separately**
Using the `severity-classification` skill, identify any P0 or P1 bugs from the same period. These appear at the top of the backlog regardless of urgency score.

**Step 4: Identify the "Sleeper"**
Flag one theme that has a lower current volume but is accelerating — worth tracking as a potential future P1.

**Step 5: Format the backlog**

```
## P0/P1 Bugs (top of sprint, non-negotiable)
[List any P0/P1 bugs with blast radius]

## Top Themes by Urgency Score
| Rank | Theme | Urgency Score | Distinct Accounts | Trend | Recommendation |
|------|-------|---------------|-------------------|-------|----------------|

## Sleeper to Watch
[One theme with growth signal]
```

For each top theme, include 1–2 supporting quotes and a one-sentence rationale for the score.

Apply the `customer-evidence-synthesis` skill for quote selection. End with a limitations section.
