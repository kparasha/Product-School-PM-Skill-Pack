---
description: Surface new patterns vs. a baseline period
argument-hint: '"time window" "category filter"'
allowed-tools: Read
---

Identify emerging, spiking, and fading feedback patterns by comparing a recent period against a baseline using data from ~~feedback tool.

Parse $ARGUMENTS:
- No args → compare last 30 days vs. prior 30 days, all categories
- One arg (e.g. `"last 14 days"`) → use that as the recent window; baseline = equivalent prior window
- Two args (e.g. `"last 30 days" "Product"`) → apply both the window and category filter

Apply the `feedback-trend-analysis` skill for period selection and statistical guardrails.

Produce four sections:

**1. New Patterns**
Themes that appear in the recent window but were absent or minimal in the baseline. Sort by account count, not mention count.

**2. Volume Spikes**
Themes that existed in the baseline but have grown significantly (≥20% increase and ≥3 distinct accounts). Include trend direction (accelerating, spike-then-stable, or spike-then-declining).

**3. Sentiment Shifts**
Areas where sentiment has meaningfully changed (≥10 points) without a corresponding volume change. A quietly worsening area can be more dangerous than a loud one.

**4. Fading Themes**
Themes that were prominent in the baseline but are declining in the recent window. Note whether the decline likely reflects a fix that worked, a change in customer behavior, or a data gap.

For each finding, include: theme name, account count in each period, direction, and one representative quote.

Apply the `customer-evidence-synthesis` skill for quote selection and problem sizing.

End with a "So What" summary paragraph identifying the one or two findings most worth acting on, and a limitations section noting any coverage gaps or seasonal factors that could affect the comparison.
