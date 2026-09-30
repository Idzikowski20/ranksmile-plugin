---
name: content-refresh
description: "Find the Ranksmile site's pages that are close to Google's first page and plan a refresh for each. Use when the user asks what to update, which pages are slipping, or where the quick SEO wins are."
---
<!-- Adapted from OpenSEO (MIT) plugins/openseo/skills/seo-audit/SKILL.md -->

# Plan a content refresh

## Before you start
- `workspace__list`, then `workspace__get_context`. If `research_log` holds a refresh plan for this site under 30 days old, start from it instead of redoing the work.

## Workflow
1. `gsc__performance` with `group_by: "page"`: pages with many impressions and `position` between 8 and 20 are the candidates. If `connected` is false, say Search Console is not connected (Settings → Integrations) and continue with rankings only.
2. `gsc__performance` with `group_by: "query"`: the queries behind those pages.
3. `rank__keywords`: tracked positions and `best`. A keyword well below its best position has slipped.
4. `article__list` to match each candidate page to its Ranksmile article, then `article__score` on each. The refresh fixes the slots and terms it reports.
5. `audit__overview` when a candidate may have a technical problem (issues with `severity: "error"`).

## Report
- At most five pages, best opportunity first. One row each: page, clicks / impressions / position, the query to win, the two or three edits from `article__score`, and the effort.
- Finish with `workspace__update_context` and `append_research_log`: "Content refresh plan: <site>. Verdict: <top pages>". If that tool is not in your tool list, the connection is read-only: say so once and skip it.
