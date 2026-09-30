---
name: diagnose-low-score
description: "Explain why a Ranksmile article's content score is low and list the few edits that would raise it most. Use when the user asks why an article scores low or what to fix in a draft."
---
<!-- Adapted from OpenSEO (MIT) plugins/openseo/skills/seo-audit/SKILL.md -->

# Diagnose a low content score

## Before you start
- `workspace__list` to find the workspace, then `workspace__get_context`. Never contradict its `brand_knowledge`.
- `article__list` with the `workspace_id` to find the article id. Page with `offset` while `has_more` is true.

## Workflow
1. `article__score`: read `score.computed`, then sort `breakdown` by `max` minus `earned`. The top three slots are where the points are.
2. List the `terms` whose `status` is `missing` or `low`, and any `overuse` to trim. Targets come from the pages already ranking.
3. Call `article__get` only when you need to quote or place a fix. Page a long body with `content_offset` while `content_truncated` is true.
4. If Auto-Optimize "did nothing", `article__optimize_log` shows each run's before and after score and why a run was rejected. If generated text looks wrong, `article__jobs` shows what the generator was asked for.

## Report
- Lead with the score and the three slots costing the most points, each with one concrete edit: which heading, which term, how many uses.
- Say which numbers come from the tools and which are your judgement.
- The Ranksmile MCP server cannot edit articles. Hand the edits to the user, or suggest asking Smily in the editor.
- If you learned a durable fact about the business, confirm it with the user, then add it with `workspace__update_context` and `append_brand_knowledge`, which keeps the existing notes. Never send `brand_knowledge` for an addition: that replaces everything the user wrote.
- If `workspace__update_context` is not in your tool list, the connection is read-only or Brand context was not allowed. Skip the write-back and tell the user they can reconnect Ranksmile and choose "Read and write" with Brand context.
