---
description: Competitive gaps, signals, or battle card research
argument-hint: "gaps|signals|research [competitor name]"
allowed-tools: Read, WebSearch, WebFetch
---

Generate competitive intelligence using feedback from ~~feedback tool and, for research mode, public web sources.

Parse $ARGUMENTS:
- `gaps` or no args → gaps analysis (default)
- `gaps "CompetitorName"` → gaps for a specific competitor
- `signals "CompetitorName"` → signal/source breakdown for a specific competitor
- `research "CompetitorName"` → web-based battle card

---

## Mode: gaps (default)

Surface competitive mentions in customer feedback and classify each by type.

**Step 1:** Find all feedback where a competitor is mentioned by name, or where customers describe switching, comparing, or considering alternatives.

**Step 2:** Classify each competitive mention:

| Gap Type | Definition |
|---|---|
| **Parity** | Competitor does something you don't; customers notice the difference |
| **Differentiation** | Area where you lead; customers call it out positively |
| **Value** | You have the capability but customers don't know about it (messaging gap) |
| **Migration friction** | Switching cost keeping customers with you despite considering alternatives |

**Step 3:** Assign a response recommendation:

- **Build** — Close the parity gap; it's costing you
- **Message** — You have it; customers need to know
- **Ignore** — Not worth closing; likely a niche edge case

Format as a table: Competitor | Gap Type | Description | Affected Accounts | Recommendation

---

## Mode: signals [competitor name]

Show where and how a competitor is being mentioned across feedback channels.

For each available source channel (support tickets, sales calls, NPS responses, reviews, etc.):
- Count of competitor mentions per month (last 6 months)
- Sentiment context (positive comparison, negative comparison, neutral mention)
- Most common associated themes

Format as a source breakdown table with monthly trends.

---

## Mode: research [competitor name]

Research the competitor using public web sources and produce a battle card.

Search for: competitor website, recent press releases, G2/Capterra reviews, LinkedIn presence, pricing page, and any recent product announcements.

Produce:
1. **One-paragraph overview**: what they do, who they serve, their primary positioning
2. **Capability matrix**: feature-by-feature comparison table (use only verified public information)
3. **Where they win**: scenarios where customers choose them over you
4. **Where you win**: scenarios where you have the advantage
5. **Sales talking points**: 3–5 specific responses to "Why you over [competitor]?"
6. **Watch list**: any recent announcements or product directions worth monitoring

Label all capability comparisons as based on public information with a date stamp. Do not make claims about competitor capabilities without a public source.

---

End all modes with a limitations section.
