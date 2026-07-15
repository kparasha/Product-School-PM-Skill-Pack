# Connectors

## How tool references work

Plugin files use `~~feedback tool` as a placeholder for whatever customer feedback platform you have connected. Commands describe analytical workflows in terms of categories rather than specific products — so the same command works whether you're connected to Zendesk, Intercom, Enterpret, or any other platform with an MCP integration.

## Connectors for this plugin

| Category | Placeholder | Suggested Options |
|---|---|---|
| Customer feedback platform | `~~feedback tool` | Enterpret, Zendesk, Intercom, Freshdesk, Gong, UserVoice, Productboard, Pendo |

## Setting Up Your Connector

When you install this plugin, replace `~~feedback tool` in command files with the name of your connected feedback tool. For example:

- `~~feedback tool` → `Zendesk` (if you have Zendesk MCP connected)
- `~~feedback tool` → `Intercom` (if you have Intercom MCP connected)
- `~~feedback tool` → `Enterpret` (if you use Enterpret's Wisdom Knowledge Graph)

If your feedback tool doesn't have an MCP integration, commands will still work — Claude will ask you to paste or describe the relevant feedback, and will apply the same analytical frameworks to whatever data you provide.

## Don't have a feedback tool connected?

These commands also work with:
- Feedback exported to a spreadsheet or CSV (share the file with Claude)
- Support tickets pasted directly into the conversation
- Qualitative research notes or interview transcripts
- Any structured feedback data in a format Claude can read

The analytical methodology in the skills is tool-agnostic. The quality of the output depends on the quality and coverage of the data you provide.
