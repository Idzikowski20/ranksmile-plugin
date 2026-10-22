# Ranksmile

Connects Claude to your [Ranksmile](https://tryranksmile.com) account through the Ranksmile MCP server, and adds seven SEO workflows that tell the assistant which tools to use and in what order.

Ranksmile tracks whether ChatGPT, Perplexity, Gemini and Google AI Overviews mention and cite your brand, next to Google rankings, Search Console data, a site audit and a content score for every article. This plugin brings that data into Claude and turns it into next steps.

## Requirements

A Ranksmile account. Plans start at €59 a month, with a 7-day trial: [tryranksmile.com/pricing](https://tryranksmile.com/pricing).

## Install

In Claude Code:

```text
/plugin marketplace add Idzikowski20/ranksmile-plugin
/plugin install ranksmile@ranksmile
```

The first time the assistant uses Ranksmile, your browser opens a consent screen. Sign in with your Ranksmile account and approve the connection.

## What you get

**The MCP server** (`https://app.tryranksmile.com/mcp`): your workspaces, articles and their content scores, Auto-Optimize history, AI visibility (scores per topic and engine, the trend over scans, each prompt's answers, citations and fan-out, the pages the answers cite), recommended Actions, tracked keyword positions, Search Console performance, site audit results, brand notes and research log.

**Seven skills:**

- `checkup`: a read-only health check of your AI visibility: setup problems, where you stand per topic, engine and prompt, and the five improvements worth most.
- `next-move`: the single next move, with one number to hit in four weeks, logged so the next run can check it.
- `visibility-gaps`: questions where AI answers name competitors instead of you, why, and what to publish or where to get mentioned to close the gap.
- `citation-outreach`: up to five outreach targets a week from the pages AI answers cite, with drafted pitches and forum answers for you to send.
- `visibility-report`: what moved since the last report, which work caused it, three things to do next and one to stop.
- `content-refresh`: pages close to Google's first page (positions 8 to 20 in Search Console), with a refresh plan for each.
- `diagnose-low-score`: why an article's content score is low, and the few edits that would raise it most.

## What the plugin runs, sends and stores

- **Connections:** the plugin connects only to the Ranksmile MCP server at `https://app.tryranksmile.com/mcp`, over HTTPS with OAuth. It has no hooks, no scripts and no local servers, and it installs no packages.
- **What it sends:** the tool calls the assistant makes, such as a workspace ID or an article ID. Ranksmile answers with data from your account.
- **Access you choose:** on the consent screen you pick which workspaces and tool categories the plugin can use, and **Read only** or **Read and write**. With **Read and write** and Brand context allowed, the workflows can add to your brand notes and save findings to the research log. The plugin never edits, publishes or deletes articles, and it never sends anything on your behalf: outreach is drafted for you to send.
- **Revoking access:** disconnect it any time in Ranksmile under **Settings > Integrations > AI assistants**.
- **Privacy:** Ranksmile's privacy policy covers what the server stores and for how long: [tryranksmile.com/docs/legal/privacy](https://tryranksmile.com/docs/legal/privacy). Support: support@tryranksmile.com.

Other assistants (Cursor, Codex, Claude Desktop) connect with the MCP URL from Ranksmile, under **Settings > Integrations > AI assistants**.

## Third-party notices

Parts of the skills are adapted from [OpenSEO](https://github.com/every-app/open-seo) (MIT) and from work by Antonio Blago (MIT). See [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).

## License

MIT. See [LICENSE](LICENSE).
