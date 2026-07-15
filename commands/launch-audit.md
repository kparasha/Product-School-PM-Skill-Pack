---
description: Pre-launch risk scan from historical feedback
argument-hint: [launch name or description]
allowed-tools: Read
---

Run a pre-launch risk scan against 90 days of historical customer feedback from ~~feedback tool to identify what you're walking into before shipping.

Launch: $ARGUMENTS

Apply the `feedback-trend-analysis` skill for period selection and the `customer-evidence-synthesis` skill for evidence structuring.

Scan for four categories of risk:

**1. Collision Risks**
Existing customer workflows or expectations that directly overlap with what you're changing. Search for feedback about the current behavior in the area you're launching into. High volume of positive feedback about the current state = collision risk (you may be removing something customers rely on).

For each collision risk: describe the workflow, cite the account count that relies on it, and include one representative quote.

**2. Adjacent Workflow Disruption**
Features or flows that don't seem directly related to the launch but are likely affected. Think one level of adjacency: if you're changing A, what does A connect to? Look for feedback about those adjacent areas.

**3. Likely Rejector Segments**
Cohorts with above-average attachment to the current behavior. Look for: heavy users of the current feature, enterprise accounts with customizations in the affected area, and any accounts that previously requested the opposite of what you're shipping.

**4. Expectation Mismatches**
Feedback where customers have explicitly described what they expect this type of change to do. Compare that against what you're actually shipping. Note where the gap is largest.

Format output as a risk matrix:

| Risk Category | Severity | Affected Accounts | Description | Mitigation Suggestion |
|---|---|---|---|---|

Follow with a "Communication Recommendations" section: which segments to notify proactively, what to say, and what questions to prepare for.

End with a limitations section: what this scan can't predict, and what user research would be needed to reduce remaining uncertainty.
