---
name: pm-guide
description: >
  This skill should be used when a user asks "what commands are available",
  "how do I use this plugin", "what can I do with customer feedback", "what should
  I run for sprint planning", "how do these commands work together", or any
  question about navigating the feedback-intelligence plugin's capabilities.
  Also triggers when someone asks for help choosing the right command for their
  situation.
---

# PM Feedback Intelligence — Command Guide

This plugin provides 14 commands organized around the moments in a PM's week where customer feedback analysis matters. Each command applies a structured analytical methodology and returns output you can act on or paste into a doc.

## Core Guarantees Across All Outputs

Every analysis follows these rules:

- **Distinct accounts, not ticket counts.** Reported volumes always reflect how many unique companies are affected. This prevents a single noisy account from distorting priorities.
- **HYPOTHESIS labels on inferences.** Anything concluded through reasoning — a root cause, a reproduction hypothesis, a predicted impact — is explicitly labeled as a HYPOTHESIS.
- **Mandatory limitations section.** Every output ends with what the data *doesn't* tell you: recency gaps, coverage biases, what you'd need to validate the findings.

## Choosing the Right Command

Use the workflow sections below to match your current situation to the right command.

### Monday Morning Pulse
- `/weekly-memo` — Big 5 briefing: emerging themes, worsening signals, enterprise blockers, self-serve friction, decision of the week. Pass `pm`, `cpo`, `eng`, or `cx` to adjust framing.
- `/emerging-signals` — Compare a recent window against a baseline to spot new patterns and volume spikes.

### When Something Is On Fire
- `/escalation-triage` — P0/P1/P2 classification of active issues. Pass `--hours 12` to narrow the window. Scope to a feature area with an argument.
- `/bug-triage` — Cluster customer-reported bugs by root cause, estimate blast radius, assign severity.

### Planning What to Build
- `/sprint-planning` — Customer-evidence-ranked backlog, scored by recency, velocity, account tier, volume, and coverage gap.
- `/roadmap-review` — Score roadmap items against customer feedback. Recommends Accelerate, Maintain, Defer, Merge, Stop, or flags NEW unmatched signals.

### Building Your Case
- `/prd-evidence` — Paste-ready customer evidence block for a PRD: volume, trend, sentiment, segment breakdown, quotes, impact, limitations.

### Launch Lifecycle
- `/launch-audit` — Pre-launch risk scan: collision risks, rejector segments, expectation mismatches.
- `/post-launch` — Before/after comparison: Improved, Regressed, Mixed, No change, Adjacent regression, New theme.

### Understanding Customers
- `/account-brief` — Single account analysis cross-referenced against market patterns. Classifies each theme as scalable gap, segment need, or account-specific request.
- `/cohort-deep-dive` — Side-by-side comparison of two or more segments.
- `/nps-drivers` — What's driving NPS up or down. Compares detractor vs. promoter theme prevalence.
- `/churn-analyzer` — Pre-churn warning signals. Pass an account name for a post-mortem, or run with no args for market-wide patterns.

### Competitive Positioning
- `/competitive-intel` — Three modes: `gaps` (default), `signals`, `research`.

## How Commands Compose

All commands draw from shared analytical skills:

- `customer-evidence-synthesis` — quote selection, problem sizing, narrative structure
- `product-prioritization` — urgency scoring, recommendation labels
- `severity-classification` — P0/P1/P2 framework, blast radius
- `feedback-trend-analysis` — pre/post comparison methodology

See `references/command-reference.md` for full argument documentation and example output descriptions.
