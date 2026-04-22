---
name: describe-dataverse-schema
description: Discover tables, columns, relationships, and option sets in the PlayerPortal Dataverse org. Use when the user asks "what tables do we have", "what columns are on the account table", "what's the schema of X", or when you need to map a user's business term to the correct Dataverse logical name before running a query. Relies on the dataverse MCP server's schema tools — do not guess column names.
---

# Describe Dataverse schema

## When to trigger

Use this skill whenever the answer depends on knowing what exists in the Dataverse environment, not what's inside the rows. Typical triggers:

- "What tables are in our org?"
- "What fields are on the Lead table?"
- "Is there a custom table for tournaments?"
- Any time you're about to write a query but aren't sure of the exact logical names.

## How to explore

1. **Start broad, then narrow.** Begin with `list_tables` to see what's available. Filter to custom tables (prefix `new_`, `pp_`, `tp_`, or whatever the org uses) when the user is asking about their own data model.
2. **For a specific table, fetch metadata.** Use the MCP's metadata tool to pull columns, data types, and whether each column is required/custom/lookup.
3. **For relationships, explicitly ask.** Lookup columns point at related tables — surface the target table name so the user understands the relationship.
4. **Summarize; don't dump.** A Dataverse table may have 150+ columns. Group by category (identifiers, display fields, system audit, custom fields) and highlight the ones most likely relevant to the user's question.

## Output format

When describing a table, render:

- **Logical name** (e.g. `account`) — what to use in queries
- **Display name** (e.g. "Account") — what users see in Dynamics
- **Primary fields** — name column, ID column
- **Key columns** — the 5-10 columns most likely to be useful (with data type)
- **Custom columns** — anything with a non-default prefix
- **Relationships** — lookups to other tables, with target table names

## Guardrails

- Don't invent column names. If you're unsure, call the metadata tool rather than guessing.
- Don't display every single column by default — that's noisy. Offer "show all columns" as a follow-up.
- Flag deprecated columns (often named with `_old`, `_legacy`, or `statecode=Inactive`) so the user doesn't build on them.
