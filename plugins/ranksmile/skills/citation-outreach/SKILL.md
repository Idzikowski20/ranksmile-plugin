---
name: citation-outreach
description: "Turn the pages AI answers cite for competitors into a short, prioritised outreach batch with ready-to-send pitches and forum answers. Use when the user wants to get mentioned on outside sites, get cited by AI, do digital PR or link outreach, or work through their earned Actions."
---
<!-- Parts adapted from work by Antonio Blago (MIT): see THIRD_PARTY_NOTICES.md -->

# Citation outreach

Most AI-visibility lift comes from being named on pages the engines already cite. This workflow picks at most five targets a week and writes a specific pitch for each.

## Before you start
- `workspace__list`, then `workspace__get_context`. Pitches use `brand_knowledge`; never claim a number or client it does not support. Before drafting for a target, check whether it was already contacted: an `earned` Action in progress or done covers its URL, or a "Outreach sent:" entry in `research_log` names it. To find those Actions, call `actions__list` with `goal: "earned"` and `status: "in_progress"`, then with `status: "done"` (paging while `has_more`), and read each one's `pages` with `actions__get` to match by URL. Only that counts as contacted. An "Outreach drafts:" entry means drafted, not sent: draft it again if it is still the best target, and say it was drafted before. `research_log` holds only the newest 20 entries, so the Action status is the record that lasts.
- If the brand has nothing to point to yet (no case study, guide or data page), say so and suggest `visibility-gaps` first: a pitch without an asset behind it is noise.
- If `actions__list` is not in your tool list, this connection was made before Actions existed: say once that reconnecting Ranksmile (Settings → Integrations → MCP) adds it, and continue without the Actions steps. Candidates then come from `visibility__sources` alone.

## 1. Candidates
- `actions__list` with `goal: "earned"` and `status: "new"`; sort them by `impact`, highest first, and read the top five with `actions__get` (their `pages`, `competitor_evidence`, `steps`).
- `visibility__sources` with `gap_only: true`: pages cited for competitors, not for the brand.

Merge by URL. Drop pages with an `http_status` of 4xx or 5xx, and pages typed `You` or `Competitor`: those are content work for `visibility-gaps`, not outreach.

## 2. Prioritise
- Impact: the action's `impact`, or the page's `times_cited`.
- Difficulty: a forum or Reddit thread is easy (answer it), an editorial list or blog is medium (email the author), a major publication or closed community is hard.
- High impact and easy first; hard and low impact is dropped. Cap at 5, or what the user asks for.

## 3. Contact and angle
For each target, read the page (fetch it) to find the author box, contact page or thread author, and the exact section the brand belongs in. Use `visibility__prompt` on a prompt that cites it to see how the answers describe the competitors listed there.

## 4. Write
Write in the page's language.
- **Editorial pitch** (subject + up to 120 words): quote the exact section, offer one concrete addition (a data point, a short expert quote, an updated entry), say what you can deliver and by when, and sign with one reference URL. No "happy to collaborate".
- **Forum or Reddit answer** (100–300 words): answer the question in the first two sentences, put one concrete method or number from practice in the middle, and link only if the link completes the answer. From a personal account, never a brand account, and say in the answer that you work for or with the brand. Follow the community's self-promotion rules: undisclosed promotion gets accounts banned and breaks consumer-protection law.
- **Reference entry**: the correction or addition, with its source.

## Report
- A table: target, type, contact, angle, status "to send". Then each pitch in full.
- The follow-up rule: one follow-up after 7–10 days, then stop.
- The success check: re-run `visibility__sources` after 4 weeks and see whether the answers citing the page now name the brand (`answer_names_brand`).
- Tell the user to mark the matching Actions "In progress" when sent and "Done" when the mention is live: that status is the tracker.
- Finish with `workspace__update_context` and `append_research_log`: "Outreach drafts: <site>. Verdict: <targets drafted, not yet sent>". When the user later says which ones they sent, append "Outreach sent: <site>. Verdict: <targets>". If that tool is not in your tool list, the connection is read-only: say so once and skip it.

## Never
- Send anything yourself. Draft; the user sends.
- Write a generic pitch: no quoted section and no concrete offer means no pitch.
- Exceed the weekly cap, or measure before 4 weeks.
