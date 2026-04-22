---
name: query-dataverse-table
description: Retrieve records from a Microsoft Dataverse table in the PlayerPortal org. Use when the user asks to look up rows, list records, filter data, or answer a question that requires reading Dataverse data (e.g. "show me open cases", "list active accounts created this week", "find contacts in Texas"). Relies on the dataverse MCP server tools (retrieve_records / run_query) — do not fall back to web browsing or scraping the Dynamics UI.
---

# Query a Dataverse table

## When to trigger

Use this skill any time the user wants to READ data from Dataverse. Examples:

- "How many leads did we create last week?"
- "Show me contacts where the email domain is playerportal.app"
- "What's on account 12345?"
- Any question answered by a `SELECT`-style operation against a Dataverse table.

Do NOT use this skill for creating, updating, or deleting records — that's a write operation and should be handled carefully with explicit user confirmation.

## How to run a query

1. **Confirm the target table.** If the user names a table in business terms ("leads", "cases"), map it to the logical Dataverse name (`lead`, `incident`, `account`, `contact`, etc.). If you're unsure of the logical name, call the `list_tables` tool on the dataverse MCP first.
2. **Select columns thoughtfully.** Dataverse tables often have 100+ columns. Pick only the columns needed to answer the question; don't dump everything.
3. **Apply filters using FetchXML or the MCP's query parameters.** Prefer server-side filters over client-side filtering — don't pull 10,000 rows to find 3.
4. **Cap the result size.** Default to `$top=50` unless the user explicitly asks for more. Mention the cap in your response.
5. **Render results as a concise table** (markdown) with the most relevant columns. Link to the Dataverse record URL if the MCP returns one.

## Guardrails

- Never expose system columns (`createdon`, `modifiedon`, `ownerid`) unless the user asked about them.
- Never display full GUIDs in the output unless the user explicitly asks — they add noise. A short record name + URL is enough.
- If the query would return more than ~500 rows, offer to summarize (counts, groupings) instead of dumping them.

## Example

User: "Show me the 10 most recent contacts."

1. Call the dataverse MCP's query tool for the `contact` table.
2. Order by `createdon desc`, top 10.
3. Select `fullname`, `emailaddress1`, `createdon`.
4. Render as a markdown table.
