---
name: visibility-gaps
description: "Find the questions where AI answers (ChatGPT, Perplexity, Gemini, Google AI) name competitors instead of the user's brand, see why, and plan what to publish or where to get mentioned to close each gap. Use when the user asks about AI visibility, AI search, why AI tools don't mention them, or for a content brief for an AI prompt."
---
<!-- Adapted from OpenSEO (MIT) plugins/openseo/skills/competitive-landscape/SKILL.md. Parts adapted from work by Antonio Blago (MIT): see THIRD_PARTY_NOTICES.md -->

# Close AI visibility gaps

## Before you start
- `workspace__list`, then `workspace__get_context`. `brand_knowledge` says what the brand can credibly claim. `research_log` entries under 30 days old can be reused.
- If `actions__list` is not in your tool list, this connection was made before Actions existed: say once that reconnecting Ranksmile (Settings → Integrations → MCP) adds it, and continue without the Actions steps.

## Workflow
1. `visibility__overview`: `overview` is the brand score, `topics` come weakest first, and `prompts` least-mentioned first. Prompts at `mention_rate` 0 with `brands_named` are the gaps. If `overview` is null, no scan has finished yet: say so and stop. If the user named a prompt or topic, work on that; otherwise take the weakest topic.
2. For the top three gap prompts, `visibility__prompt`:
   - `brands` and their `quotes`: what the answers say about the winners. That is the claim to beat.
   - `citations`: the pages the answer leans on.
   - `fan_out_queries`: what the engine actually searched. These are the sub-questions the content must answer.
   - `advice`, when present: Ranksmile's stored "how to get cited". Build on it rather than contradict it.
   - The wording of the answers and the fan-out is how buyers phrase it: use it verbatim in headings.
3. `visibility__sources` with `gap_only: true`. Decide by the page `type`:
   - **Competitor**, or an article or how-to on any site → own content: write or improve a page that answers the same question better.
   - **Editorial** (lists, rankings, reviews) → get included: hand to `citation-outreach`.
   - **UGC** (Reddit, forums, YouTube) → take part in the thread, from a personal account that says you work for or with the brand, within the community's self-promotion rules.
   - **Reference** / **Institutional** → a correct, sourced entry is the target, not a pitch.
4. For own content: `article__list` to find an article that should answer it, and `article__score` to see how well it does. `gsc__performance` with `group_by: "query"` shows whether Google already sends traffic for the same question.
5. `actions__list` with `goal: "owned"`: if an action for this topic exists, use its brief (`actions__get`) instead of writing a new one.

## Report
Per topic (at most three):
- The gap prompts, the brands named instead, and what the answers say about them.
- One action: improve an existing article (with its `article__score` gaps and the fan-out questions it misses), write a new one, or get onto the listed pages (hand to `citation-outreach`).
- For a new article, a brief: the target question, the page type (comparison, how-to, list, service page: match the type of the pages that win), a working title (≤ 60 chars), an H2 outline from the fan-out questions, the buyer phrasing to use, and the 4-week metric ("prompt <id>: 0% → mentioned by at least one engine").
- Claim only what `brand_knowledge` supports.
- Finish with `workspace__update_context` and `append_research_log`: "AI visibility gaps: <site>. Verdict: <topics to cover>". If that tool is not in your tool list, the connection is read-only: say so once and skip it.

## Never
- Mix intents in one brief: an informational question and a buying question need different pages.
- Judge a page by its domain alone: read what it says (`visibility__prompt` quotes and citations) before calling it unbeatable.
