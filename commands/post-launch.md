---
description: Before/after feedback comparison for a launch
argument-hint: '"launch name" YYYY-MM-DD'
allowed-tools: Read
---

Compare customer feedback before and after a launch to measure its real-world impact using data from ~~feedback tool.

Parse $ARGUMENTS: first argument = launch name, second argument = launch date in YYYY-MM-DD format.

Apply the `feedback-trend-analysis` skill throughout.

**Important:** Do not proceed if fewer than 14 days have passed since the launch date. Return a note asking the user to wait.

**Period setup:**
- Pre-period: 30 days before the launch date
- Post-period: full elapsed period since launch (up to 30 days)

**Step 1: Identify in-scope themes**
List all feedback themes that plausibly relate to the launch. Include adjacent areas (one level of adjacency beyond the primary scope).

**Step 2: Classify each theme**

Apply these classifications from the `feedback-trend-analysis` skill:
- **Improved** — negative signal reduced or absent post-launch
- **Regressed** — new or worsened negative signal post-launch
- **Mixed** — both improvement and regression in the same theme
- **No change** — no measurable movement despite the launch touching this area
- **Adjacent regression** — a related area degraded even though the target improved
- **New theme** — a pattern that didn't exist pre-launch

**Step 3: NPS Movement**
If NPS data is available, report the score before and after, and identify which themes are most correlated with any movement.

**Step 4: Weekly trend table**
Show feedback volume and sentiment week by week from 4 weeks pre-launch through the current post-launch period. Highlight the launch week.

**Step 5: Remaining gaps**
List themes that were prominent pre-launch and were expected to improve, but show No change or continued regression. These are the items still open.

Format the main output as a classification table:

| Theme | Classification | Pre-Launch Accounts | Post-Launch Accounts | Direction | Notes |
|---|---|---|---|---|---|

End with a "Verdict" paragraph (1–3 sentences: did the launch help, hurt, or produce mixed results?), and a limitations section.
