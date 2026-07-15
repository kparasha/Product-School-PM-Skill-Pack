# Command Reference

Full argument documentation and output descriptions for all 14 commands.

---

## Signal Detection & Monitoring

### /weekly-memo
**Arguments:** Optional audience flag — `pm` (default), `cpo`, `eng`, `cx`
**Output:** A structured briefing covering the Big 5: emerging themes, worsening signals, enterprise blockers, self-serve friction, and a Decision of the Week backed by the data.
**Best for:** Monday mornings. Schedule for 8am weekly.

### /emerging-signals
**Arguments:**
- No args → last 30 days vs. prior 30 days, all categories
- `"last 14 days"` → custom window (baseline = equivalent prior window)
- `"last 30 days" "Product"` → window + category filter
**Output:** Ranked list of changing patterns with trend direction, account counts, and representative quotes.
**Best for:** Spotting what you're missing between planning cycles.

### /escalation-triage
**Arguments:**
- No args → full scan across all product areas
- `dashboards` → scope to a specific feature area
- `--hours 12` → narrow detection window (default: 7 days)
**Output:** P0/P1/P2 classified issues with blast radius estimates and direct quotes.
**Best for:** Daily or on-demand fire checks.

### /bug-triage
**Arguments:**
- No args → all reported bugs
- `"search"` → scope to a feature area
**Output:** Clustered bug report with severity levels, affected account counts, and HYPOTHESIS-labeled reproduction steps.
**Best for:** Engineering handoff.

---

## Prioritization & Planning

### /roadmap-review
**Arguments:**
- No args → landscape scan (useful for quarterly reviews)
- Paste roadmap items → scored comparison
**Recommendation labels:** Accelerate, Maintain, Defer, Merge, Stop, NEW
**Output:** Scored roadmap table with composite urgency formula and recommendation per item.
**Best for:** Weekly planning meetings, quarterly roadmap reviews.

### /sprint-planning
**Arguments:**
- No args → all themes, auto-categorized
- `"Analytics"` → scoped to feature area
**Scoring factors:** Recency, velocity, account tier, volume, coverage gap
**Output:** Prioritized backlog with urgency scores, trend direction, quotes, and severity-classified bugs.
**Best for:** Sprint kickoffs.

### /prd-evidence
**Arguments:** Topic or feature name as a string
**Output:** Volume + trend, sentiment, segment breakdown, 5 curated quotes with citations, impact assessment, limitations. Plus artifacts: roadmap slide copy and stakeholder email.
**Best for:** Strengthening any product proposal with data.

---

## Launch Lifecycle

### /launch-audit
**Arguments:** Launch name or description
**Output:** Pre-launch risk assessment: collision risks, adjacent workflow disruption, likely rejector segments, expectation mismatches.
**Best for:** Before shipping — identifies who will react and what might break.

### /post-launch
**Arguments:** Launch name + launch date (ISO format, e.g. `"new onboarding flow" "2026-03-01"`)
**Classification types:** Improved, Regressed, Mixed, No change, Adjacent regression, New theme
**Output:** Before/after comparison with NPS movement, weekly trend table, work item linkage, remaining gaps.
**Best for:** Measuring whether a launch actually helped customers.

---

## Account Intelligence

### /account-brief
**Arguments:** Account name (e.g. `"Nextdoor"`)
**Theme classification:** Scalable product gap | Segment-specific need | Account-specific request
**Output:** Account dossier with NPS trends, feature request history, and QBR talking points.
**Best for:** CS syncs, QBR prep, enterprise escalation response.

### /churn-analyzer
**Arguments:**
- No args → market-wide pattern analysis
- `"AccountName"` → post-mortem on a specific churned account
**Output (pattern mode):** Pre-churn signals ranked by predictive correlation.
**Output (post-mortem mode):** Feedback timeline with root cause hypothesis and limitations.
**Best for:** Building early warning systems and retention strategies.

### /cohort-deep-dive
**Arguments:** Two or more segment names (e.g. `"Enterprise" "SMB"` or `"NA" "Europe" "APAC"`)
**Output:** Side-by-side comparison of top themes, sentiment, and quotes per segment. Summary of differential needs and strategic implications.
**Best for:** Understanding whether segments need different product strategies.

### /nps-drivers
**Arguments:**
- No args → all time
- `"last 90 days"` → custom time window
**Output:** Themes ranked by how strongly they differentiate promoters from detractors. Sentiment scores per group.
**Best for:** NPS improvement planning.

---

## Competitive Intelligence

### /competitive-intel
**Modes:**
- `gaps` (default) — classifies competitive mentions as Parity, Differentiation, Value, Migration friction. Recommends Build, Message, or Ignore.
- `signals "CompetitorName"` — source breakdown of competitor mentions with monthly trends.
- `research "CompetitorName"` — web-based battle card and capability matrix.

**Output:** Varies by mode. Gaps gives prioritized action list. Signals gives sourced trend report. Research gives battle card document.
**Best for:** Competitive positioning, win/loss analysis, sales enablement.
