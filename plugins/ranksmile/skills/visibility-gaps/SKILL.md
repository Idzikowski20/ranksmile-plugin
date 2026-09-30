---
name: visibility-gaps
description: "Find the questions where AI answers (ChatGPT, Perplexity, Gemini, Google AI) name competitors instead of the user's brand, and plan content to close them. Use when the user asks about AI visibility, AI search, or why AI tools don't mention them."
---
<!-- Adapted from OpenSEO (MIT) plugins/openseo/skills/competitive-landscape/SKILL.md -->

# Close AI visibility gaps

## Before you start
- `workspace__list`, then `workspace__get_context`. `brand_knowledge` says what the brand can credibly claim. `research_log` entries under 30 days old can be reused.

## Workflow
1. `visibility__overview`: `overview` is the brand score, and `prompts` come least-mentioned first. Prompts at `mention_rate` 0 are the gaps, and `brands_named` shows who the answers name instead. If `overview` is null, no scan has finished yet: say so and stop.
2. Group the gap prompts by `topic`. For each topic, look in `article__list` for an article that should answer it, and use `article__score` to see how well it does.
3. `gsc__performance` with `group_by: "query"` shows whether Google already sends traffic for the same questions.

## Report
- Per topic: the gap prompts, the brands named instead, and one action. Either improve an existing article (with its `article__score` gaps) or write a new one that answers the question.
- Claim only what `brand_knowledge` supports.
- Finish with `workspace__update_context` and `append_research_log`: "AI visibility gaps: <site>. Verdict: <topics to cover>". If that tool is not in your tool list, the connection is read-only: say so once and skip it.
