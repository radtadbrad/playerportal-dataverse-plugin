# PlayerPortal Dataverse plugin

Connects Cowork to the PlayerPortal Microsoft Dataverse org (`orgd852a96e.crm.dynamics.com`) via Microsoft's official `@microsoft/dataverse` MCP proxy.

## What it does

- Discovers tables, columns, relationships, and option sets
- Retrieves records with filters, ordering, and server-side paging
- Writes records (create / update) — with guardrails in the skills

## Requirements

- **Node.js 18 or newer** must be on `PATH` (the MCP server runs via `npx`).
- **Microsoft account** with access to the Dataverse org. On first launch the MCP will open a browser window for interactive sign-in.

## Configuration

The org URL is hard-coded in `.mcp.json`:

```json
"args": ["-y", "@microsoft/dataverse", "mcp", "https://orgd852a96e.crm.dynamics.com"]
```

To point at a different org, edit that URL and re-install the plugin.

## Skills included

- `describe-dataverse-schema` — triggers on "what tables do we have", "what's the schema of X"
- `query-dataverse-table` — triggers on "show me contacts", "list leads", "find accounts in Texas"

## Troubleshooting

- **"Command not found: npx"** → Install Node.js 18+ from nodejs.org and restart Cowork.
- **Auth loop / 401 from Dataverse** → Sign out of the MS account, re-run, interactive login should appear again.
- **"No tables returned"** → Confirm your account has at least Read access to the org's default solution.
