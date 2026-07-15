---
description: Monday morning customer intelligence briefing
argument-hint: [pm|cpo|eng|cx]
allowed-tools: Read
---

Generate a weekly customer intelligence memo using data from ~~feedback tool.

Audience: $ARGUMENTS (default: pm). Adjust framing accordingly:
- `pm`: balanced view — themes, priorities, one decision to make
- `cpo`: strategic view — trends, competitive signals, one strategic question
- `eng`: technical view — bugs, regressions, reliability signals, blast radius
- `cx`: customer-facing view — account health, escalations, satisfaction signals

Run the Big 5 scan:

1. **Emerging themes** — What new patterns appeared in the last 7 days that weren't prominent the week before? Look for volume upticks and new vocabulary.

2. **Worsening signals** — Which existing negative themes are getting worse? Prioritize by velocity (rate of change) and account tier concentration.

3. **Enterprise blockers** — Which issues are concentrated in high-tier accounts and represent a blocker (not just friction)? Flag if any involve an account with an open renewal or expansion.

4. **Self-serve friction** — Which issues disproportionately affect lower-touch, smaller-tier customers? These often reflect onboarding gaps or documentation failures.

5. **Decision of the Week** — Identify one prioritization judgment call that the data supports making this week. Frame it as a decision, not a recommendation: "Given X signal, now is the time to decide whether to Y."

Format the output as a structured briefing with a clear header, one section per Big 5 item, and a closing "What to Watch" note for signals that are small today but worth monitoring.

Apply the `customer-evidence-synthesis` and `product-prioritization` skills throughout.

End with a mandatory limitations section: what this memo doesn't cover, what data might be missing, and what would change the analysis if available.
