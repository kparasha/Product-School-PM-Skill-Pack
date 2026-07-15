---
description: Side-by-side segment comparison
argument-hint: '"Segment A" "Segment B" ...'
allowed-tools: Read
---

Compare feedback themes and sentiment across two or more customer segments using data from ~~feedback tool.

Segments: $ARGUMENTS (e.g. `"Enterprise" "SMB"` or `"North America" "Europe" "APAC"` or `"Financial Services" "Healthcare"`)

Apply the `customer-evidence-synthesis` and `product-prioritization` skills throughout.

**Step 1: Define segment boundaries**
Confirm how each segment is defined in the data. Note sample sizes (distinct accounts per segment). Flag if any segment has fewer than 5 accounts — the analysis will have low reliability.

**Step 2: Surface top themes per segment**
For each segment, identify the top 8–10 themes by distinct account count within that segment.

**Step 3: Build the comparison**
Three comparison views:

*Shared needs (themes prominent in ALL segments):*
These are universal — high confidence they're a broad product gap worth addressing regardless of segment strategy.

*Differential needs (themes prominent in SOME segments but not others):*
These reveal where segments diverge. For each: note which segment(s) rate it highly, what share of accounts in that segment mention it, and why it may not matter to other segments.

*Unique needs (themes prominent in ONLY ONE segment):*
These are segment-specific. Flag whether they are worth a dedicated investment or whether they represent edge cases.

**Step 4: Sentiment comparison**
For themes that appear in multiple segments, compare sentiment across segments. The same feature can generate satisfaction in one segment and frustration in another.

**Step 5: Strategic implications**
Based on the comparison, answer:
- Do these segments need the same product or different products?
- Which themes are safe to optimize for everyone, and which require tradeoffs?
- Are there any segment-specific investments that would have outsized impact?

Format output as a side-by-side table (shared / differential / unique), followed by the strategic implications section.

Apply quote diversity rules from the `customer-evidence-synthesis` skill. Include at least one representative quote per segment for each differential theme.

End with a limitations section noting sample sizes and any coverage gaps by segment.
