---
description: Single account feedback analysis vs. market patterns
argument-hint: [account name]
allowed-tools: Read
---

Analyze one account's feedback history and cross-reference it against market-wide patterns using data from ~~feedback tool.

Account: $ARGUMENTS

Apply the `customer-evidence-synthesis` and `product-prioritization` skills throughout.

**Step 1: Surface the account's feedback**
Pull all feedback from this account. Identify the top 5–8 themes by volume. Note the time range of available data.

**Step 2: Cross-reference against market patterns**
For each account theme, check how prevalent that theme is across all other accounts. Calculate: what percentage of all accounts with this theme does this one account represent?

**Step 3: Classify each theme**

| Classification | Criteria |
|---|---|
| **Scalable product gap** | This theme appears in ≥10% of accounts across the market. The account's request reflects a broadly shared need. Worth prioritizing. |
| **Segment-specific need** | This theme is common in accounts that share a characteristic with this account (size, industry, use case). Evaluate at the segment level. |
| **Account-specific request** | This theme is rare across the market (<5% of accounts). May reflect this account's unusual workflow or environment. Needs validation before roadmap consideration. |

**Step 4: NPS Trends**
If NPS data is available for this account, show the score history over the last 12 months and identify which themes correlate with score changes.

**Step 5: Feature Request History**
List the account's feature requests, noting: request date, current status (open / in progress / shipped / declined), and whether the request is scalable or account-specific.

**Step 6: QBR Talking Points**
Generate 3–5 talking points for a customer success or executive review:
- One thing that's improved for this account
- One thing that's still open and the timeline
- One scalable gap where this account's feedback aligns with a broader product investment
- One account-specific request that needs an honest conversation about prioritization

Format output as a brief with header (account name, date, data range), classification table, and QBR talking points section.

End with a limitations section. Flag clearly if this account is an outlier submitter (very high volume) that might be distorting the classification.
