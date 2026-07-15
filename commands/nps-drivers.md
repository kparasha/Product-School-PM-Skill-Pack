---
description: What's driving NPS scores up or down
argument-hint: [time window]
allowed-tools: Read
---

Analyze what's driving NPS scores by comparing feedback themes from detractors (low scores) vs. promoters (high scores) using data from ~~feedback tool.

Time window: $ARGUMENTS (default: all available NPS data)

Apply the `customer-evidence-synthesis` skill throughout.

**Important:** If NPS data is not available or the sample size is fewer than 20 respondents, return a note explaining the limitation and suggest alternative analyses (/cohort-deep-dive or /prd-evidence).

**Step 1: Define score groups**
- Promoters: NPS 9–10
- Passives: NPS 7–8 (include in analysis but note separately)
- Detractors: NPS 0–6

Report sample sizes for each group.

**Step 2: Surface top themes per group**
For each group, identify the top 8–10 feedback themes by prevalence (% of accounts in the group that mention the theme).

**Step 3: Differential analysis**
The most valuable output is the *difference* — what do detractors mention that promoters don't, and vice versa?

Calculate: (% of detractors mentioning theme) − (% of promoters mentioning theme)

Themes with a large positive difference are **detractor drivers** — fixing them would most likely improve NPS.
Themes with a large negative difference are **promoter drivers** — these are what you must protect.

**Step 4: Passive analysis**
Passives are customers who could go either way. Look at their themes: do they skew toward detractor themes or promoter themes? This reveals which direction they're likely to move and what it would take to convert them.

**Step 5: Produce the driver table**

| Theme | Promoter Prevalence | Detractor Prevalence | Difference | Implication |
|---|---|---|---|---|

Followed by two short paragraphs: "What to Protect" (promoter drivers) and "What to Fix" (detractor drivers).

Include 2 representative quotes per top detractor driver and 2 per top promoter driver. Apply quote diversity rules from `customer-evidence-synthesis`.

End with a limitations section. Note if NPS responses are skewed toward certain account tiers or recent interactions, which would affect reliability.
