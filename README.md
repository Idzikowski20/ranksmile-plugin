# Ranksmile for Claude Code

Connects Claude Code to your [Ranksmile](https://ranksmile.pl) account through the Ranksmile MCP server, and adds three SEO workflows that tell the assistant which tools to use and in what order.

## Install

In Claude Code:

```text
/plugin marketplace add Idzikowski20/ranksmile-plugin
/plugin install ranksmile@ranksmile
```

The first time the assistant uses Ranksmile, your browser opens a consent screen. Sign in with your Ranksmile account and approve the connection.

## What you get

**The MCP server** (`https://app.ranksmile.pl/mcp`): your workspaces, articles and their content scores, Auto-Optimize history, AI visibility, tracked keyword positions, Search Console performance, site audit results, brand notes and research log.

**Three skills:**

- `diagnose-low-score`: why an article's content score is low, and the few edits that would raise it most.
- `content-refresh`: pages close to Google's first page (positions 8 to 20 in Search Console), with a refresh plan for each.
- `visibility-gaps`: questions where AI answers name competitors instead of you, and what to publish to close the gap.

On the consent screen you choose which workspaces and tool categories the plugin can use. With **Read and write** (the default when the plugin asks for it) and Brand context allowed, the workflows can also add to your brand notes and save what they found to the research log; **Read only** keeps them to reading. The plugin never edits, publishes or deletes articles.

Other assistants (Cursor, Codex, Claude Desktop) connect with the MCP URL from Ranksmile, under **Settings > Integrations > MCP**.

## Third-party notices

Parts of the skills are adapted from [OpenSEO](https://github.com/every-app/open-seo) (MIT). See [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).
