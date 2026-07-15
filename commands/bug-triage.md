---
description: Cluster customer-reported bugs with blast radius and severity
argument-hint: [feature-area]
allowed-tools: Read
---

Analyze customer feedback from ~~feedback tool to identify, cluster, and triage reported bugs.

Parse $ARGUMENTS:
- No args → all reported bugs across all areas
- Feature area (e.g. `"search"`) → scope to that feature

Apply the `severity-classification` skill throughout.

**Step 1: Surface bug signals**
Look for feedback that describes broken behavior: error messages, unexpected outcomes, missing data, crashes, timeouts, data loss, or any language indicating the product is not working as expected. Exclude feature requests framed as bugs ("it should do X instead of Y" is a feature request if the current behavior is intentional).

**Step 2: Cluster by likely root cause**
Group similar reports together. Clusters should share: affected feature area, type of failure (data, performance, UI, auth, etc.), and symptom description. Label each cluster with a short title.

**Step 3: Estimate blast radius for each cluster**
Count distinct affected accounts (not ticket count). Note account tier distribution. Flag any cluster where >50% of mentions come from a single account (concentrated signal — lower reliability as a systemic issue).

**Step 4: Assign severity**
Apply the P0/P1/P2 framework from the `severity-classification` skill. Data loss and auth failures are always P0 regardless of account count.

**Step 5: Construct reproduction hypotheses**
For each cluster, write a HYPOTHESIS about the likely root cause based on the pattern of customer language. Label every inference as HYPOTHESIS. Do not state causes as facts.

Format each cluster as:

```
**[CLUSTER TITLE]** — P0/P1/P2
Blast radius: N distinct accounts ([tier breakdown])
Description: What customers report happening
Reproduction HYPOTHESIS: [your inference]
Recommended next step: [specific action]
Representative quote: "[quote]" — [tier], [date]
```

End with a summary table and a limitations section noting any categories not scanned and the recency window of the data used.
