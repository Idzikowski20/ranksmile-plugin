---
name: visibility-report
description: "Close the loop on a Ranksmile workspace's AI visibility: what moved since the last report, which work caused it, and the three things to do next plus one to stop. Use for a weekly or monthly AI visibility report, or when the user asks what worked."
---
<!-- Parts adapted from work by Antonio Blago (MIT): see THIRD_PARTY_NOTICES.md -->

# AI visibility report

At most 400 words. A narrative with numbers, not a dashboard.

## Before you start
- `workspace__list`, then `workspace__get_context`. The last "AI visibility report:" entry in `research_log` is the baseline date; without one, use the oldest `history` point.
- `visibility__overview`: if `scans_total` is under 2, say there is too little signal yet and stop. `history` holds the last 12 scans, which at a daily cadence is under two weeks: when it starts after the window does, say how far back the trend reaches and use the logged baseline for the rest.
- If `actions__list` is not in your tool list, this connection was made before Actions existed: say once that reconnecting Ranksmile (Settings → Integrations → AI assistants) adds it, and continue without the Actions steps.

## 1. What moved
- Brand `visibility_score` and `mention_rate` over the window: the logged baseline score and mention rate against now (an older entry without a mention rate gives the score only), or the first against the last `history` point when the history covers the window.
- Per topic over the window: compare with the topic rates logged in the last report entry. A topic with no logged rate has no baseline: say so, and do not call it new or a gain.
- Latest-scan movement, labelled as such: per prompt and topic, `mention_rate` against `previous_mention_rate`. It is one scan's change, not the window's.

## 2. What was done
- `actions__list` with `status: "done"`: those with `done_at` inside the window. Page with `offset` while `has_more` is true.
- `article__list`: articles published or updated in the window, paging the same way. If it is not in your tool list, the connection left out Articles: say so and attribute without them.
- `research_log`: the "Next move:", "Outreach sent:" and "AI visibility gaps:" entries in the window (drafts that were never sent are not work done).

## 3. Attribution
- Match each piece of work to the prompts it targets: the action's prompts in `actions__get`, the article's topic, and for an outreach target the prompts whose answers cite it (the `citations` in `visibility__prompt`).
- Baseline drift is the median change of the prompts nobody worked on: over the window where a baseline exists, otherwise `mention_rate` − `previous_mention_rate` (and say it is the latest scan's). A worked prompt's lift counts only above that drift. If no untouched prompt has a `previous_mention_rate`, say the drift is unknown instead of guessing.
- Correlation is not cause. Name the mechanism ("the article is now cited in the answers to prompts 12 and 14", from the `visibility__prompt` citations), or call the change unexplained.

## Report
Use this shape:

```
# AI visibility — <site> (<window>)
## Headline
<the single most important finding>
## What moved
- Visibility: X → Y (Δ); mention rate X% → Y%
- Strongest / weakest topic: <topic> (Δ) / <topic> (Δ)
## What worked
<2–3 sentences, each with its mechanism>
## What did not
<1–2 sentences, with the most likely reason>
## Do now (exactly 3)
1. …
## Stop doing
- …
```

- Finish with `workspace__update_context` and `append_research_log`: "AI visibility report: <site>. Verdict: <headline>; baseline score <Y>, mention <M>%, topics <topic=rate, …>" with every topic, written short (`solar=12`), so the next report has a baseline for each. If they do not fit in 500 characters, keep the topics with the most prompts and say in the report which ones the next one will lack. If that tool is not in your tool list, the connection is read-only: say so once and show the line for the user to keep.

## Never
- Skip the baseline drift, or the "Stop doing" line.
- Report a lift without saying what caused it, or that the cause is unknown.
