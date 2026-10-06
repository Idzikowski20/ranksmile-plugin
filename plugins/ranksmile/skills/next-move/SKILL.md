---
name: next-move
description: "Pick the single highest-leverage next move for a Ranksmile workspace's AI visibility, with one number to hit in 4 weeks, and log the decision. Use when the user asks what to do next, what to work on this week, or where to focus."
---
<!-- Parts adapted from work by Antonio Blago (MIT): see THIRD_PARTY_NOTICES.md -->

# Pick the next move

One decision, one workflow, one measurable 4-week target. Not a dashboard, not a list of options.

## 1. Read the state
- `workspace__list`, then `workspace__get_context`. Read the `research_log` entries starting "Next move:" (earlier decisions) and "AI visibility checkup:". If a decision is under 4 weeks old, first check its metric with `visibility__overview` (`history`, the prompt or topic it named) and say whether it moved.
- Run the `checkup` workflow, but skip its research-log write: this workflow writes one entry at the end. Use its sections as the input below.
- If `actions__list` is not in your tool list, this connection was made before Actions existed: say once that reconnecting Ranksmile (Settings → Integrations → AI assistants) adds it, and continue without the Actions steps. Tier 4 then cannot fire (its only signal is the site actions), and tier 6 rests on `distinct_domains` from `visibility__sources` alone.

## 2. Find the gap
The lowest tier number is the highest priority and wins; one tier per cycle.

| Tier | Gap | Signal | Hand off to |
|---|---|---|---|
| 1 | Data | `scans_total` is 1, or under 7 days of history | Stop: wait for the next scan. Do not force a move. |
| 2 | Setup | setup health under 80%, or any P0 | the fix in the app: competitors (AI Visibility → Competitors) or prompts (Prompts) |
| 3 | Prompt mass | under 20 prompts, or a topic with under 2 | Prompt Radar in the app |
| 4 | Site | `actions__list` with `goal: "site"` and `status: "new"` at impact 4–5 | that action on the Actions page |
| 5 | Content | a losing prompt (`mention_rate` 0, a competitor named) on the weakest topic, with no article that answers it (`article__list`) | `visibility-gaps` for that topic |
| 6 | Citations | content exists but `distinct_domains` is under 5, or new `earned` actions at impact 4–5 | `citation-outreach` |
| 7 | Learning | 4+ weeks since the first decision, and no "AI visibility report:" entry in the last 4 weeks | `visibility-report` |

A tier whose signal needs a tool that is not in your tool list (Articles for tier 5, Actions for tiers 4 and 6) is not "no signal": say which category the connection left out, judge the tier on what you can see, and never read a missing `article__list` as "no article exists".

Tier 1 is an exit: report what data is missing and when the next scan is due, then stop. No checkup override, no decision, no log entry, no handoff.

If two tiers both fire, take the lower number. If the checkup's #1 improvement maps to a different tier than the ladder picked, prefer the checkup's #1 and say so.

## 3. Decide
Write the decision in this shape:

```
## Decision
<one sentence: one verb, one object, one deadline>

## Why this, now
<3–5 sentences: signal → what it means → therefore this>

## How
Run <workflow or app page> with: <the topic / prompt ids / action id>

## In 4 weeks
<one metric with a number, e.g. "topic 'solar' mention rate 12% → ≥ 25%">

## Not now
- <option>: <why it waits>
- <option>: <why it waits>
```

If the number would not move within 4 weeks, the metric is wrong: rewrite it.

## 4. Log and hand off
- `workspace__update_context` with `append_research_log`: "Next move: <site>. Verdict: <decision>; metric <metric>; check <YYYY-MM-DD, 4 weeks out>". If that tool is not in your tool list, say the connection is read-only and show the line for the user to keep.
- Then start the named workflow, unless it is an app step; for an app step, say exactly where to click.

## Never
- Offer a menu of options, or say "it depends" without saying on what.
- Work on two tiers at once.
- Say "everything looks fine": the value is the critical read.
