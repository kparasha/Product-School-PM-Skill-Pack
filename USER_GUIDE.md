A practical guide to running customer feedback analysis with Claude. Whether you're connected to a feedback platform like Zendesk or Enterpret, or just have a CSV export you want to make sense of, this plugin gives you 14 analysis commands organized around the moments in a PM's week that actually matter.

---

## **Getting Started**

### **Step 1: Install the plugin**

Open feedback-intelligence.plugin in Cowork. You'll see a preview of what's included — press **Install** to add it to your session.

[Detailed Installation Instructions](https://app.notion.com/p/Detailed-Installation-Instructions-38efa20bfe06806da0ddc5e5072b0d3d?pvs=21)

### **Step 2: Connect your feedback data**

You have three options, and they all work:

**Option A — MCP-connected feedback tool (best results)**  
MCP (Model Context Protocol) is the standard that connects Claude to your other tools, like your feedback platform. If you have a feedback platform connected via MCP (Zendesk, Intercom, Enterpret, Gong, etc.), the plugin uses it automatically. After installing, run the cowork-plugin-customizer skill to replace the \~\~feedback tool placeholder in commands with your tool's name:

"Use the cowork-plugin-customizer skill to set up my feedback-intelligence plugin with Zendesk"

**Option B — CSV upload**  
 Export your feedback data as a CSV, upload the file to your conversation, and then run any command. Claude will read the file and apply the full analytical framework to your data.

For best results, your CSV should include:

| Column | Why It Matters |
| ----- | ----- |
| Account / Company name | Enables distinct account counting (vs. raw row counts) |
| Feedback text | The content that gets analyzed |
| Date | Enables trend analysis and time comparisons |
| Account tier or segment | Unlocks cohort analysis and urgency weighting |

Missing columns degrade gracefully — Claude will note what it can't calculate and why.

**File size recommendations for CSV uploads**

There are two limits to keep in mind, and they bite at different points.

First, a platform upload cap: in the Claude app, individual files must be **under 30 MB** (the Claude API allows much larger, \~500 MB, if you build your own pipeline). These are product limits that can change, so check Anthropic's current [help docs](https://support.claude.com/en/articles/8241126-upload-files-to-claude) rather than treating the number as fixed.

Second — and this is the one you'll usually hit first — the practical ceiling is **how much feedback text the model has to read**, not the file's size on disk. Pure aggregation (counts, trends, sentiment splits when those columns already exist) runs in the processing sandbox and scales to very large files. But any step that reads raw text — classifying feedback, pulling quotes, synthesizing themes — is bounded by the context window, measured in tokens. A good working budget is **\~30–50K tokens of raw feedback text per pass** (roughly 120–200K characters, or \~150 support-ticket-length records). A 5 MB CSV of dense free-text uploads fine but can easily exceed that in a single read.

When your text exceeds that budget, don't push a bigger file — instead pre-classify the data once and reuse the labeled file, analyze a representative sample, or chunk it into multiple passes and combine the results.

**Option C — Paste or describe your data**  
 No file? Just paste support tickets, interview notes, or a summary of feedback directly into the conversation, then run a command. The output quality scales with the richness of what you provide.

### **Step 3: Run your first command**

```
/weekly-memo
```

This is the best starting point. It runs a Big 5 scan across your feedback and returns a Monday-morning briefing in about 60 seconds. If it produces useful output, you're set up correctly.

[Sample Output](https://app.notion.com/p/Sample-Output-38efa20bfe0680929843dc080f399091?pvs=21)

---

## **How to Read the Output**

Every command produces output with the same anatomy:

**Analysis body** — the actual findings, structured to the command's purpose (ranked lists, tables, comparisons, etc.)

**Supporting quotes** — direct customer quotes selected for diversity, each with an attribution (account tier, date, source channel)

**HYPOTHESIS labels** — any inference Claude makes — a root cause, a predicted impact, a causal explanation — is explicitly labeled HYPOTHESIS. This is intentional. The data shows patterns; Claude doesn't have certainty about causes.

**Limitations section** — every output ends with what the analysis can't tell you: recency gaps, coverage biases, what you'd need to validate the findings. This isn't a disclaimer; it's the most honest part of the output.

When you see a finding that matters, the limitations section tells you whether to act on it immediately or validate it first.

---

## **Commands by Workflow**

### **Monday Morning: Get Oriented**

**/weekly-memo**

Your weekly pulse. Runs five detection scans — emerging themes, worsening signals, enterprise blockers, self-serve friction, and a Decision of the Week — and returns them as a structured briefing.

Tailor the output by passing an audience flag:

```
/weekly-memo          → default PM view
/weekly-memo cpo      → strategic framing, fewer details
/weekly-memo eng      → bugs, regressions, reliability
/weekly-memo cx       → account health, escalation risk
```

*Tip: Schedule this to run every Monday at 8am using the /schedule command in Cowork.*

---

**/emerging-signals**

Compares a recent period against a prior baseline and surfaces what's changed — new patterns, volume spikes, sentiment shifts, and fading themes.

```
/emerging-signals                              → last 30 days vs. prior 30 days
/emerging-signals "last 14 days"               → custom window
/emerging-signals "last 30 days" "Integrations"  → scoped to a category
```

Use this when the weekly memo mentions something you want to understand better, or when you want to catch what's moving between planning cycles.

---

### **When Something Is On Fire**

**/escalation-triage**

Scans for P0, P1, and P2 issues simultaneously — sentiment crashes, volume spikes, new themes, account concentration, and direct escalation language.

```
/escalation-triage                  → full scan, last 7 days
/escalation-triage dashboards       → scoped to a feature area
/escalation-triage --hours 12       → last 12 hours only
```

Run this before a weekend, when a deployment goes out, or any time you sense something is wrong but don't know where to look.

*P0 \= interrupt now. P1 \= act today. P2 \= weekly review.*

---

**/bug-triage**

Takes customer-reported issues and produces an engineering-ready summary. Groups similar reports into clusters, estimates how many distinct accounts are affected, assigns severity, and writes a reproduction hypothesis.

```
/bug-triage                → all reported bugs
/bug-triage "search"       → scoped to a feature area
```

Hand the output directly to your engineering lead. Everything inferred (root causes, reproduction steps) is labeled HYPOTHESIS so engineers know what's confirmed vs. what needs investigation.

---

### **Planning What to Build**

**/sprint-planning**

Generates a customer-evidence-ranked backlog. Scores each theme using five factors: recency, velocity, account tier concentration, volume, and whether there's existing work planned for it.

```
/sprint-planning                → all themes, auto-categorized
/sprint-planning "Analytics"    → scoped to a feature area
```

Output includes: ranked themes with urgency scores, any P0/P1 bugs that should top the sprint regardless of score, and a "sleeper" — a lower-volume signal that's accelerating and worth watching.

*Note: urgency scores tell you what customers care about most right now. They don't account for engineering complexity or dependencies — that's your call.*

---

**/roadmap-review**

Compares your roadmap items against live customer feedback and recommends what to do with each one.

```
/roadmap-review                            → landscape scan (good for quarterly reviews)
/roadmap-review [paste your roadmap here]  → scored comparison
```

Each item gets one of six recommendations:

| Label | Meaning |
| ----- | ----- |
| **Accelerate** | Strong signal — consider pulling this forward |
| **Maintain** | On track, current timeline is supported |
| **Defer** | Weak or declining signal — consider pushing back |
| **Merge** | Multiple items address the same underlying need |
| **Stop** | No signal, or signal contradicts the item's premise |
| **NEW** | Customer signal exists for a theme with no roadmap coverage |

The **NEW** flags are often the most valuable output — they surface unaddressed needs that don't appear anywhere in your current plan.

---

### **Building Your Case**

**/prd-evidence**

Builds the customer evidence section for a PRD or product proposal. You give it a topic; it returns a structured argument: volume, trend, sentiment, segment breakdown, five curated quotes, impact assessment, and a limitations section. Also generates a slide blurb and a stakeholder email you can paste directly.

```
/prd-evidence "bulk CSV export"
/prd-evidence "mobile notifications"
/prd-evidence "role-based permissions"
```

This is the command to run when you have a feature you want to propose and need the data to back it up. Use it *after* /roadmap-review or /sprint-planning tells you what to go deep on.

---

### **Before You Ship**

**/launch-audit**

Scans 90 days of historical feedback to identify what you're walking into before a launch. Looks for four categories of risk: workflows you might be disrupting, adjacent features that could be affected, segments likely to push back, and gaps between customer expectations and what you're shipping.

```
/launch-audit "new navigation redesign"
/launch-audit "removing the legacy export format"
/launch-audit "Linear integration"
```

Output includes a risk matrix and communication recommendations — which segments to notify proactively and what to prepare for.

*Run this 1–2 weeks before shipping, not the day before.*

---

### **After You Ship**

**/post-launch**

Compares feedback before and after a launch date. Classifies what changed for each affected theme.

```
/post-launch "v3 dashboard" "2026-03-15"
/post-launch "new onboarding flow" "2026-02-01"
```

Classifications:

* **Improved** — negative signal reduced or gone after launch  
* **Regressed** — new or worsened signal introduced by the launch  
* **Mixed** — both improvement and regression  
* **No change** — no movement despite the launch touching this area  
* **Adjacent regression** — something nearby degraded even though the target improved  
* **New theme** — a feedback pattern that didn't exist before launch

Wait at least 14 days after launch before running this. The signal isn't meaningful before then.

*"Adjacent regression" and "No change" are the findings most worth paying attention to — they surface unintended consequences and fixes that didn't work.*

---

### **Understanding Your Customers**

**/account-brief**

Analyzes one account's feedback and cross-references it against market-wide patterns. The key output is a classification for each theme:

* **Scalable product gap** — appears in 10%+ of all accounts; worth roadmap consideration  
* **Segment-specific need** — common in accounts like this one; evaluate at the segment level  
* **Account-specific request** — rare across the market; needs validation before acting on

```
/account-brief "Acme Corp"
/account-brief "Nextdoor"
```

Also generates QBR talking points for each account. Bring this into any CS sync or executive escalation.

---

**/cohort-deep-dive**

Compares two or more customer segments side by side — by tier, geography, industry, or any other grouping in your data.

```
/cohort-deep-dive "Enterprise" "SMB"
/cohort-deep-dive "Financial Services" "Healthcare" "Tech"
/cohort-deep-dive "North America" "Europe"
```

Output shows three views: shared needs (affects everyone), differential needs (matters to some but not others), and unique needs (only one segment). The differential view is where the product strategy questions live.

---

**/nps-drivers**

Compares what detractors (NPS 0–6) and promoters (NPS 9–10) are saying. Ranks themes by how strongly they differentiate the two groups.

```
/nps-drivers                → all available NPS data
/nps-drivers "last 90 days"  → custom window
```

Output tells you: what to fix (themes overrepresented in detractors) and what to protect (themes overrepresented in promoters). Passives are analyzed separately to show which direction they're likely to move.

---

**/churn-analyzer**

Two modes depending on what question you're asking:

```
/churn-analyzer                → market-wide: what patterns precede churn?
/churn-analyzer "Acme Corp"    → post-mortem: what happened with this account?
```

Market-wide mode compares churned accounts against healthy accounts to find pre-churn warning signals — the patterns that reliably appeared before accounts left. Post-mortem mode walks through a specific account's feedback timeline and hypothesizes why they churned.

---

### **Competitive Positioning**

**/competitive-intel**

Three modes for three different questions:

**Gaps** — what are customers saying about competitors that reveals a product gap?

```
/competitive-intel                       → all competitors
/competitive-intel gaps "Competitor X"  → one competitor
```

Each gap is classified as Parity (they have it, you don't), Differentiation (you lead), Value (you have it but customers don't know), or Migration friction (switching cost). Each gets a Build, Message, or Ignore recommendation.

**Signals** — where and how often is a competitor being mentioned?

```
/competitive-intel signals "Competitor X"
```

Returns a source breakdown (support tickets, sales calls, NPS, reviews) with monthly volume trends.

**Research** — build a battle card from public information

```
/competitive-intel research "Competitor X"
```

Searches the web for the competitor's positioning, capabilities, G2 reviews, and recent announcements. Returns a battle card with a capability matrix and sales talking points.

---

## **Workflow Recipes**

These are the sequences that work well together for common PM situations.

### **The weekly planning routine**

```
Monday:    /weekly-memo
           → if something looks serious: /escalation-triage
Wednesday: /sprint-planning "feature area"
           → /roadmap-review [paste current roadmap]
```

### **Preparing for a feature proposal**

```
1. /emerging-signals  → confirm the problem is real and growing
2. /prd-evidence "topic"  → build the evidence section
3. /cohort-deep-dive  → understand if all segments are affected equally
```

### **A launch cycle**

```
2 weeks before: /launch-audit "launch name"
After shipping:  wait 14+ days
Then:            /post-launch "launch name" "YYYY-MM-DD"
```

### **Responding to a customer escalation**

```
1. /account-brief "Account Name"   → understand their history
2. /escalation-triage "feature area"  → is this isolated or market-wide?
3. /prd-evidence "topic"   → if it's scalable, build the case for fixing it
```

### **Quarterly review prep**

```
/roadmap-review         → landscape scan with no input
/churn-analyzer         → market-wide pre-churn patterns
/nps-drivers "last 90 days"   → what's driving the score
/competitive-intel gaps       → where are we losing on features vs. messaging
```

---

## **Tips for Better Output**

**Be specific with topics.** /prd-evidence "export" is vague. /prd-evidence "bulk CSV export for data teams" gives Claude a cleaner signal to search for.

**Scope commands when you can.** Adding a feature area (e.g., /sprint-planning "Analytics") produces a more focused, actionable backlog than scanning everything.

**Use the limitations section.** When an output says "this analysis doesn't cover X," that's telling you something real about your data coverage. Don't ignore it.

**Chain commands.** The weekly memo tells you *what* is happening. Escalation triage tells you *how bad* it is. Sprint planning tells you *what to do about it*. They're designed to be used together.

**When you get a HYPOTHESIS you care about, validate it.** Run a customer interview, check with support, or pull a sample of the raw tickets. The plugin gives you a starting point for investigation, not a final answer.

---

## **Working With CSV Data**

If you're uploading a CSV rather than using a connected feedback tool:

1. Upload the CSV file at the start of your conversation  
2. Tell Claude what the columns mean if they're not obvious: "The 'org' column is the account name, 'verbatim' is the feedback text, 'submitted\_at' is the date"  
3. Run your command normally

**What works well with CSVs:**

* /prd-evidence, /sprint-planning, /escalation-triage — work with any structured feedback data  
* /cohort-deep-dive — works if your CSV has a segment or tier column  
* /nps-drivers — works if your CSV includes NPS scores alongside feedback text

**What degrades without date data:**

* /emerging-signals and /post-launch need dates to compare periods. Without dates, Claude will note the limitation and skip time-based comparisons.

**What degrades without account data:**

* Commands that count "distinct accounts" will fall back to row counts and flag that the unit is different. The analysis still runs; just note the caveat.

---

## **Getting Help**

Ask Claude in plain language. The pm-guide skill loads automatically when you ask things like:

* "What command should I use to prepare for a QBR?"  
* "How do I compare enterprise vs. SMB feedback?"  
* "Which command is best for understanding why we lost an account?"  
* "What commands are available?"

You can also ask Claude to explain what it found in simpler terms, reformat the output for a specific audience, or turn any analysis into a Slack message, email, or slide copy.

