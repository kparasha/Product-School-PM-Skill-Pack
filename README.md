# Feedback Intelligence

A PM plugin for customer feedback analysis. Provides 14 commands covering signal detection, prioritization, launch lifecycle, account intelligence, and competitive positioning.

Works with any customer feedback platform — Zendesk, Intercom, Enterpret, Gong, Productboard, or even a CSV export. See `CONNECTORS.md` for setup details.

---

## Getting Started

### Step 1: Install the plugin

Open `feedback-intelligence.plugin` in Cowork. You'll see a preview of what's included — press **Install** to add it to your session.

### Step 2: Connect your feedback data

You have three options, and they all work:

**Option A — MCP-connected feedback tool (best results)**
If you have a feedback platform connected via MCP (Zendesk, Intercom, Enterpret, Gong, etc.), the plugin uses it automatically. After installing, run the `cowork-plugin-customizer` skill to swap the `~~feedback tool` placeholder in commands with your tool's name:

> "Use the cowork-plugin-customizer skill to set up my feedback-intelligence plugin with Zendesk"

**Option B — CSV upload**
Export your feedback data as a CSV, upload the file to your conversation, and then run any command. Claude will read the file and apply the full analytical framework to your data.

For best results, your CSV should include:

| Column | Why It Matters |
|---|---|
| Account / Company name | Enables distinct account counting vs. raw row counts |
| Feedback text | The content being analyzed |
| Date | Enables trend analysis and time-window comparisons |
| Account tier or segment | Unlocks cohort analysis and urgency score weighting |

Missing columns degrade gracefully — Claude will note what it can't calculate and why.

**Option C — Paste or describe your data**
No file? Paste support tickets, interview notes, or a summary of feedback directly into the conversation, then run a command. Output quality scales with the richness of what you provide.

### Step 3: Run your first command

```
/weekly-memo
```

This is the best starting point. It scans your feedback and returns a Monday-morning briefing covering the five most important signal categories. If it produces useful output, you're set up correctly.

---

## How to Read the Output

Every command produces output with the same anatomy:

**Analysis body** — the findings, structured to the command's purpose: ranked lists, comparison tables, classification outputs.

**Supporting quotes** — customer quotes selected for diversity, each with an attribution (account tier, date, source channel).

**HYPOTHESIS labels** — any inference Claude makes — a root cause, a predicted impact, a causal explanation — is explicitly labeled `HYPOTHESIS`. The data shows patterns; Claude doesn't have certainty about causes.

**Limitations section** — every output ends with what the analysis can't tell you: recency gaps, coverage biases, what you'd need to validate the findings. This isn't a disclaimer — it's the most honest part of the output and tells you whether to act immediately or investigate further.

---

## Commands

### Signal Detection & Monitoring

**`/weekly-memo`** — Monday morning Big 5 briefing: emerging themes, worsening signals, enterprise blockers, self-serve friction, and a Decision of the Week. Tailor framing by passing an audience flag:

```
/weekly-memo          → default PM view
/weekly-memo cpo      → strategic framing, fewer details
/weekly-memo eng      → bugs, regressions, reliability signals
/weekly-memo cx       → account health, escalation risk
```

*Tip: Schedule this to run every Monday at 8am using the `/schedule` command in Cowork.*

---

**`/emerging-signals`** — Compares a recent period against a prior baseline to surface new patterns, volume spikes, sentiment shifts, and fading themes.

```
/emerging-signals                                → last 30 days vs. prior 30 days
/emerging-signals "last 14 days"                 → custom window
/emerging-signals "last 30 days" "Integrations"  → window + category filter
```

Use this when something in the weekly memo catches your attention, or when you want to catch what's moving between planning cycles.

---

**`/escalation-triage`** — P0/P1/P2 scan for issues needing immediate attention. Runs five detection passes simultaneously: sentiment crashes, volume spikes, new themes, account concentration, and explicit escalation language.

```
/escalation-triage                  → full scan, last 7 days
/escalation-triage dashboards       → scoped to a feature area
/escalation-triage --hours 12       → last 12 hours only
```

P0 = interrupt now. P1 = act today. P2 = weekly review.

---

**`/bug-triage`** — Clusters customer-reported issues by likely root cause, estimates blast radius (distinct accounts, not ticket count), assigns severity, and writes a reproduction hypothesis for each cluster. All inferences are labeled `HYPOTHESIS`.

```
/bug-triage             → all reported bugs
/bug-triage "search"    → scoped to a feature area
```

The output is formatted for engineering handoff.

---

### Prioritization & Planning

**`/sprint-planning`** — Generates a customer-evidence-ranked sprint backlog. Scores each theme across five factors: recency, velocity, account tier concentration, volume, and whether existing work covers it. Also flags P0/P1 bugs that should top the sprint regardless of score, and a "sleeper" signal worth watching.

```
/sprint-planning                 → all themes, auto-categorized
/sprint-planning "Analytics"     → scoped to a feature area
```

---

**`/roadmap-review`** — Compares roadmap items against live customer feedback and produces a scored recommendation for each. Run with no input for a landscape scan, or paste your roadmap items directly.

```
/roadmap-review                             → landscape scan
/roadmap-review [paste your roadmap items]  → scored comparison
```

Recommendation labels: **Accelerate**, **Maintain**, **Defer**, **Merge**, **Stop**, **NEW**. The NEW flags — signals with no roadmap coverage — are often the most valuable output.

---

**`/prd-evidence`** — Builds a paste-ready customer evidence section for a PRD or product proposal: volume, trend, sentiment, segment breakdown, five curated quotes, impact assessment, and a limitations section. Also generates a slide blurb and stakeholder email.

```
/prd-evidence "bulk CSV export"
/prd-evidence "role-based permissions"
```

Use this after `/roadmap-review` or `/sprint-planning` identifies what to go deep on.

---

### Launch Lifecycle

**`/launch-audit`** — Pre-launch risk scan against 90 days of historical feedback. Identifies four risk categories: workflows you might be disrupting, adjacent features that could be affected, segments likely to push back, and gaps between customer expectations and what you're shipping.

```
/launch-audit "new navigation redesign"
/launch-audit "removing the legacy export format"
```

Run this 1–2 weeks before shipping, not the day before. Output includes a risk matrix and communication recommendations — which segments to notify proactively and what to prepare for.

---

**`/post-launch`** — Compares feedback before and after a launch date. Classifies what changed for each affected theme.

```
/post-launch "v3 dashboard" "2026-03-15"
/post-launch "new onboarding flow" "2026-02-01"
```

Classifications: **Improved**, **Regressed**, **Mixed**, **No change**, **Adjacent regression**, **New theme**. Wait at least 14 days after launch before running — the signal isn't meaningful before then.

---

### Account Intelligence

**`/account-brief`** — Analyzes one account's feedback and cross-references it against market-wide patterns. Classifies each theme as a scalable product gap, segment-specific need, or account-specific request — preventing a single vocal customer from distorting your roadmap. Also generates QBR talking points.

```
/account-brief "Acme Corp"
```

---

**`/cohort-deep-dive`** — Compares feedback themes and sentiment side by side across two or more customer segments. Shows what's shared across all segments, what's differential (matters to some but not others), and what's unique to one segment.

```
/cohort-deep-dive "Enterprise" "SMB"
/cohort-deep-dive "Financial Services" "Healthcare" "Tech"
```

---

**`/nps-drivers`** — Compares what detractors (NPS 0–6) and promoters (NPS 9–10) are saying. Ranks themes by how strongly they differentiate the two groups to show what to fix and what to protect.

```
/nps-drivers                  → all available NPS data
/nps-drivers "last 90 days"   → custom window
```

---

**`/churn-analyzer`** — Two modes depending on what you're asking:

```
/churn-analyzer               → market-wide: what patterns precede churn?
/churn-analyzer "Acme Corp"   → post-mortem on a specific churned account
```

Market-wide mode finds the feedback patterns that reliably appeared before accounts left. Post-mortem mode walks through a specific account's feedback timeline and hypothesizes a root cause.

---

### Competitive Intelligence

**`/competitive-intel`** — Three modes for three different questions:

```
/competitive-intel                        → gaps analysis across all competitors (default)
/competitive-intel gaps "Competitor X"    → gaps for one competitor
/competitive-intel signals "Competitor X" → source breakdown with monthly trends
/competitive-intel research "Competitor X"→ web-based battle card
```

Gaps mode classifies each mention as Parity, Differentiation, Value, or Migration friction, and recommends Build, Message, or Ignore for each. Research mode produces a capability matrix and sales talking points from public web sources.

---

## Workflow Recipes

Common sequences that work well together:

**Weekly planning**
```
/weekly-memo  →  if something looks serious: /escalation-triage  →  /sprint-planning
```

**Feature proposal**
```
/emerging-signals  →  /prd-evidence "topic"  →  /cohort-deep-dive
```

**Launch cycle**
```
/launch-audit  →  [ship it]  →  wait 14+ days  →  /post-launch
```

**Customer escalation**
```
/account-brief "Account"  →  /escalation-triage "feature area"  →  /prd-evidence "topic"
```

**Quarterly review**
```
/roadmap-review  →  /churn-analyzer  →  /nps-drivers "last 90 days"  →  /competitive-intel gaps
```

---

## Skills

These load automatically when relevant commands run. You don't need to invoke them directly.

| Skill | What It Does |
|---|---|
| `pm-guide` | Plugin overview and command navigation. Ask "what command should I use for X?" to trigger it. |
| `customer-evidence-synthesis` | Quote selection, problem sizing, narrative structure |
| `product-prioritization` | Urgency scoring formula and Accelerate/Defer/Stop labels |
| `severity-classification` | P0/P1/P2 framework and blast radius calculation |
| `feedback-trend-analysis` | Pre/post comparison methodology and period selection |

---

## Core Guarantees

Every output follows these rules:

1. **Distinct accounts, not ticket counts.** Impact is always measured in unique companies or users — never raw submission volume.
2. **HYPOTHESIS labels on inferences.** Causal claims and root cause explanations are always labeled as HYPOTHESIS.
3. **Mandatory limitations section.** Every output ends with what the data doesn't tell you.

---

## Tips

- **Be specific with topics.** `/prd-evidence "bulk CSV export for data teams"` produces better output than `/prd-evidence "export"`.
- **Scope commands when you can.** Adding a feature area (e.g., `/sprint-planning "Analytics"`) produces a more focused backlog than scanning everything.
- **Chain commands.** The weekly memo tells you *what* is happening. Escalation triage tells you *how bad*. Sprint planning tells you *what to do*. They're designed to work together.
- **When you get a HYPOTHESIS you care about, validate it.** Run a customer interview, check with support, or pull the raw tickets. This plugin gives you a starting point for investigation, not a final answer.
- **Ask in plain language.** "What command should I use to prepare for a QBR?" or "How do I compare enterprise vs. SMB feedback?" will trigger the pm-guide skill and route you to the right command.
