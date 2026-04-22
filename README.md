# PlayerPortal Dataverse Marketplace

A single-plugin Cowork marketplace hosting the `playerportal-dataverse` plugin, which connects Cowork to the PlayerPortal Microsoft Dataverse org.

## Install in Cowork

1. Push this repo to GitHub (public, or private if Cowork supports it — public is safer while we verify).
2. In Cowork, open **Settings → Plugins → Add marketplace**.
3. Paste the GitHub URL, e.g.:
   ```
   https://github.com/<your-username>/playerportal-dataverse-marketplace
   ```
4. Cowork fetches the repo, reads `.claude-plugin/marketplace.json`, and shows `playerportal-dataverse` as an installable plugin.
5. Click **Install** next to it.

## What's inside

```
playerportal-dataverse-marketplace/
├── .claude-plugin/
│   └── marketplace.json          ← Cowork reads this first
├── playerportal-dataverse/       ← the actual plugin
│   ├── .claude-plugin/
│   │   └── plugin.json           ← plugin manifest
│   ├── .mcp.json                 ← declares the Dataverse MCP server
│   ├── README.md                 ← user docs for the plugin
│   └── skills/
│       ├── describe-dataverse-schema/SKILL.md
│       └── query-dataverse-table/SKILL.md
└── README.md                     ← this file
```

## Push to GitHub

From this folder (`playerportal-dataverse-marketplace`):

```bash
cd "C:\Users\User\Documents\Claude\Cody\Power Pages Site\playerportal-dataverse-marketplace"
git init
git add .
git commit -m "Initial marketplace with playerportal-dataverse plugin"
git branch -M main
# Create the empty repo on GitHub first (no README, no .gitignore — we already have them)
git remote add origin https://github.com/<your-username>/playerportal-dataverse-marketplace.git
git push -u origin main
```

Then go paste `https://github.com/<your-username>/playerportal-dataverse-marketplace` into Cowork Settings → Plugins → Add marketplace.

## Updating

1. Edit files in the plugin folder.
2. Bump `version` in both `marketplace.json` and `playerportal-dataverse/.claude-plugin/plugin.json` (keep them in sync).
3. `git commit && git push`.
4. In Cowork, the marketplace refetches; you'll see an update prompt for the plugin.
