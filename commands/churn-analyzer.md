---
description: Pre-churn warning signals or account post-mortem
argument-hint: [account name | blank for market-wide]
allowed-tools: Read
---

Analyze churn patterns using feedback from ~~feedback tool.

Parse $ARGUMENTS:
- No args → market-wide pattern analysis: compare churned accounts vs. healthy accounts
- Account name (e.g. `"Figma"`) → post-mortem on that specific churned account

Apply the `customer-evidence-synthesis` skill throughout. Label all causal inferences as HYPOTHESIS.

---

## Mode 1: Market-Wide Pattern Analysis (no args)

**Step 1: Identify churned and healthy cohorts**
Using available account status data, separate churned accounts from active accounts. Report sample sizes for each cohort.

**Step 2: Compare top themes**
For each cohort, surface the top 10 feedback themes. Compare prevalence: what do churned accounts mention more than healthy accounts?

**Step 3: Pre-churn signal ranking**
Rank themes by predictive correlation: (prevalence in churned accounts) − (prevalence in healthy accounts). Themes with a large positive difference are candidate pre-churn warning signals.

**Step 4: Timing analysis**
For churned accounts, look at the timeline of feedback: when did negative signals appear relative to the churn date? Flag if a pattern emerges (e.g., escalating negative feedback in the 60 days before churn).

**Step 5: At-risk scoring framework**
Based on the above, propose a simple early warning model: "Accounts that exhibit [X, Y, Z] patterns in their feedback are HYPOTHESIS more likely to churn within 90 days."

Format as a signal table with predictive correlation scores, followed by the early warning framework.

---

## Mode 2: Account Post-Mortem (with account name)

**Step 1: Pull the account's full feedback history**
Surface all feedback from this account, ordered chronologically.

**Step 2: Timeline narrative**
Walk through the account's feedback journey: when did they first raise each theme, when did sentiment shift, when (if visible) did the language become urgent or churn-adjacent.

**Step 3: Match against market patterns**
Were the signals this account raised also common in the broader churned cohort? Or were they account-specific? This determines whether the churn was preventable at a product level or required a different intervention.

**Step 4: Root cause HYPOTHESIS**
Based on the timeline and patterns, propose the most likely explanation for the churn. Label as HYPOTHESIS.

**Step 5: Counterfactual**
What, if anything, could have been done differently at the product level to change the outcome? Be honest: if the signals were account-specific or the issue was price/fit rather than product, say so.

End with a limitations section in both modes.
