---
description: P0/P1/P2 scan for issues needing immediate attention
argument-hint: "feature-area --hours N"
allowed-tools: Read
---

Scan customer feedback from ~~feedback tool for issues requiring immediate attention. Classify findings as P0, P1, or P2 using the `severity-classification` skill.

Parse $ARGUMENTS:
- No args → full scan across all product areas, last 7 days
- Feature area (e.g. `dashboards`) → scope to that area only
- `--hours N` → narrow the detection window to the last N hours (e.g. `--hours 12`)

Run five detection passes:

**1. Sentiment crashes**
Identify any area where sentiment has dropped sharply (≥15 points) within the detection window. A sudden crash often indicates a broken release or a new bug being discovered by multiple customers simultaneously.

**2. Volume spikes**
Flag any theme where volume has doubled or more within the detection window compared to the equivalent prior window. Apply the minimum threshold: ≥3 distinct accounts.

**3. New themes**
Surface any feedback pattern that appears for the first time (or re-emerges after 60+ days of silence) within the detection window.

**4. Account concentration**
Identify if any single enterprise or high-tier account is responsible for an unusual share of recent negative feedback. Flag the account (anonymized if appropriate) and note any known relationship context.

**5. Direct escalation signals**
Look for explicit escalation language: "urgent," "blocking," "this is critical," "I need this fixed today," "about to churn," "going to switch." These should be surfaced regardless of volume.

For each finding, apply the `severity-classification` skill to assign P0/P1/P2 and estimate blast radius.

Format output as a triage table:

| Severity | Issue | Accounts Affected | First Seen | Recommended Action |
|---|---|---|---|---|

Follow the table with 1–2 sentences of context per P0 and P1 finding.

End with a limitations section. Note the detection window and any areas not covered by the scan.
