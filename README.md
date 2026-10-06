# Ranksmile for Claude Code

Connects Claude Code to your [Ranksmile](https://ranksmile.pl) account through the Ranksmile MCP server, and adds seven SEO workflows that tell the assistant which tools to use and in what order.

## Install

In Claude Code:

```text
/plugin marketplace add Idzikowski20/ranksmile-plugin
/plugin install ranksmile@ranksmile
```

The first time the assistant uses Ranksmile, your browser opens a consent screen. Sign in with your Ranksmile account and approve the connection.

## What you get

**The MCP server** (`https://app.ranksmile.pl/mcp`): your workspaces, articles and their content scores, Auto-Optimize history, AI visibility (scores per topic and engine, the trend over scans, each prompt's answers, citations and fan-out, the pages the answers cite), recommended Actions, tracked keyword positions, Search Console performance, site audit results, brand notes and research log.

**Seven skills:**

- `checkup`: a read-only health check of your AI visibility: setup problems, where you stand per topic, engine and prompt, and the five improvements worth most.
- `next-move`: the single next move, with one number to hit in four weeks, logged so the next run can check it.
- `visibility-gaps`: questions where AI answers name competitors instead of you, why, and what to publish or where to get mentioned to close the gap.
- `citation-outreach`: up to five outreach targets a week from the pages AI answers cite, with drafted pitches and forum answers for you to send.
- `visibility-report`: what moved since the last report, which work caused it, three things to do next and one to stop.
- `content-refresh`: pages close to Google's first page (positions 8 to 20 in Search Console), with a refresh plan for each.
- `diagnose-low-score`: why an article's content score is low, and the few edits that would raise it most.

On the consent screen you choose which workspaces and tool categories the plugin can use. With **Read and write** (the default when the plugin asks for it) and Brand context allowed, the workflows can also add to your brand notes and save what they found to the research log; **Read only** keeps them to reading. The plugin never edits, publishes or deletes articles, and it never sends anything on your behalf: outreach is drafted for you to send. A connection made before the Actions category existed doesn't include it; reconnect to add it.

Other assistants (Cursor, Codex, Claude Desktop) connect with the MCP URL from Ranksmile, under **Settings > Integrations > AI assistants**.

## Third-party notices

Parts of the skills are adapted from [OpenSEO](https://github.com/every-app/open-seo) (MIT) and from work by Antonio Blago (MIT). See [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).

## License

MIT. See [LICENSE](LICENSE).
