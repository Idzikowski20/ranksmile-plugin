---
name: checkup
description: "Read-only health check of a Ranksmile workspace's AI visibility: is the prompt set and competitor list sound, where does the brand stand per topic, engine and prompt, and the five improvements worth most. Use when the user asks where they stand, how their AI visibility is doing, what is wrong with their setup, or what the biggest opportunities are."
---
<!-- Parts adapted from work by Antonio Blago (MIT): see THIRD_PARTY_NOTICES.md -->

# AI visibility checkup

Read-only. Diagnose and rank; never change anything except one research-log entry at the end.

## Before you start
- `workspace__list`, then `workspace__get_context`. If `research_log` holds a checkup for this site under 7 days old and nothing big changed since, show it and ask before redoing it.
- If `actions__list` is not in your tool list, this connection was made before Actions existed: say once that reconnecting Ranksmile (Settings → Integrations → AI assistants) adds it, and continue without the Actions steps.

## 1. Inventory
`visibility__overview` (page with `offset` while `has_more`). Count: prompts, prompts per `intent` (informational / commercial / transactional / none), topics, tags, tracked competitors (`tracked: true`), engines in `overview.per_model`, `scans_total`, and the days between the first and last `history` point.
- If `overview` is null: no scan has finished. Say so and stop.
- If `scans_total` is 1 or the history spans under 7 days: report counts and setup health only, and mark performance as "insufficient data". Never draw trends from one scan.

## 2. Setup health
Score each check, with the evidence. P0 blocks valid measurement, P1 skews it, P2 is nice to have.
- **Competitors are buyer alternatives** (P0): tracked competitors or the most-named brands include software tools (Semrush, Ahrefs, Sistrix, Senuto, Surfer, Yoast, Screaming Frog) for a business that does not sell software. They distort the share of voice.
- **Invisible competitors** (P1): brands in `competitors` with a high `mention_rate` that are not `tracked`. Name them.
- **Intent balance** (P1): among prompts that have an intent, any of informational / commercial / transactional under 20% or over 50%. Prompts with no intent are their own finding.
- **Prompt mass** (P1): under 20 prompts, or a topic with fewer than 2.
- **Topics slice the business** (P2): topics that are pure themes ("SEO", "AI") with one prompt each give nothing to compare.
- **Tags** (P2): no tags at all means no way to slice by offer or persona.
- **Buyer language** (P2): prompts that read like marketing copy rather than how a buyer asks.

Setup health = share of checks passed.

## 3. Performance now
From `visibility__overview` and `visibility__sources`:
- Brand `visibility_score` and `mention_rate`, and the change from the previous `history` point when there is one (none with a single scan: say so, no delta).
- Weakest and strongest `topics`; weakest engine in `overview.per_model`.
- Winning prompts: `mention_rate` over 50 (top 5). Losing prompts: `mention_rate` 0 where a competitor is named (top 5, with `brands_named`).
- Source base: `distinct_domains` (under 5 is narrow, over 15 healthy) and `type_shares`.

## 4. Top improvements
Candidates: `actions__list` with `status: "new"` (all goals), the P0/P1 findings above, and `visibility__sources` with `gap_only: true`.

Rank by impact × effort × fit:
- impact: the action's `impact`, or for a gap page its `times_cited`.
- effort: a site fix or an edit to an existing page beats one pitch, which beats a new article, which beats a project.
- fit: it fixes the weakest topic or engine from §3.

Keep five. If setup health is under 80%, or any P0 check failed, at least one of the five is a setup fix: a broken setup makes every other number wrong.

For each: one-sentence action, the signal that caused it, the workflow to run next (`visibility-gaps`, `citation-outreach`, `content-refresh`, or the Actions page), effort S/M/L, and the number it should move in 4 weeks.

## Report
- TL;DR (5 lines): visibility now and its change, setup health, weakest topic and who wins it, recommended next step.
- Then sections 1–4 as above. Say which numbers come from the tools and which are your judgement.
- End with one line: "Next: <workflow> for <scope>".
- Finish with `workspace__update_context` and `append_research_log`: "AI visibility checkup: <site>. Verdict: <score>, setup <health>%, next <step>". If that tool is not in your tool list, the connection is read-only: say so once and skip it.

## Never
- Change prompts, competitors or actions. Suggest; the user decides in the app.
- List more than five improvements.
- Bury a P0 setup issue under content ideas.
