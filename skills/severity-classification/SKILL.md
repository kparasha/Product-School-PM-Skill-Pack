---
name: severity-classification
description: >
  This skill should be used when classifying the severity of customer-reported
  issues, calculating blast radius, or assigning P0/P1/P2 labels to bugs or
  escalations. Auto-loads for /escalation-triage, /bug-triage, and /sprint-planning.
  Also triggers when someone asks "how bad is this", "what's the blast radius",
  "is this a P0", or "how many customers are affected".
---

# Severity Classification

## P0 / P1 / P2 Framework

| Level | Name | Definition | Response |
|---|---|---|---|
| **P0** | Critical | Data loss, security breach, service unavailable for multiple accounts, or a blocking issue for an enterprise account with an active escalation | Interrupt now. Stop other work. |
| **P1** | High | Significant workflow disruption affecting multiple accounts, no workaround available, or a P0-adjacent issue that is contained to one account | Act today. |
| **P2** | Medium | Meaningful friction, workaround exists, or a persistent complaint that is growing in volume | Add to weekly review. |
| **No action** | Low | Cosmetic issue, single account with no tier weight, or declining signal | Log and monitor. |

## Blast Radius Calculation

Blast radius = the scope of customer impact. Always calculate in terms of **distinct affected accounts**, not ticket count.

Steps:
1. Count distinct companies or users reporting the issue
2. Classify by account tier (enterprise, mid-market, SMB, free/trial)
3. Note if any affected account has an open renewal, expansion, or active executive relationship
4. Note if the issue is concentrated (one account driving most volume) or distributed (many accounts, each with a few mentions)

**Concentrated signals** (>50% of mentions from one account) should be flagged. A concentrated P0 may be a P1 in practice, because it may reflect one account's unusual environment rather than a systemic issue.

**Distributed signals** (spread across 5+ accounts with no single dominant source) are more reliable indicators of a real product issue.

## Calibration Rules

**Do not auto-P0 based on emotional language.** "This is completely broken" and "I can't use this at all" are common in customer feedback for issues that are P2. Use the framework, not the tone.

**Data loss or security issues are always P0**, even if only one account reports them, because the risk to other accounts is real and latent.

**Enterprise accounts do not automatically make an issue P0.** Enterprise concentration raises urgency score, but the P0 threshold requires active impact (not just a complaint) and a blocking-level disruption.

**Growing signals can upgrade severity.** A P2 with accelerating velocity (doubling month-over-month) should be flagged as "P2 / watch for upgrade."

## False Positive Prevention

Common false positives to check before classifying P0:

- **Feature requests framed as bugs.** "This doesn't work the way I expect" is often a feature request. If the product behaves as designed, this is not a bug — reclassify as a feature request.
- **One-off environment issues.** A bug that only occurs in one account's configuration may reflect their setup, not a product defect. Label as HYPOTHESIS until reproduced independently.
- **Noise from migration or onboarding.** New accounts often submit high volumes of feedback during onboarding. Check account age before classifying severity.

## Output Format for Bug Triage

When producing a bug triage output, structure each cluster as:

```
**[TITLE]** — P0/P1/P2
Blast radius: N distinct accounts (tier distribution)
Description: What customers report happening
Reproduction HYPOTHESIS: [your inference of root cause]
Recommended next step: [specific action]
Representative quote: "[quote]" — [account tier], [date]
```
