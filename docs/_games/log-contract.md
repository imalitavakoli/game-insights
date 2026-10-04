[🔙](../../README.md#research)

# Log contract 📋

What a developer provides, which fields already have a meaning, and the confirmation required before any measurement. The [approach](approach.md) says which problems this contract is for. A score describes play under the goals and rewards the log shows.

&nbsp;

[🔝](#log-contract-📋)

## What the developer provides

A GameAnalytics data export: one JSON object per event. The export schema is [GameAnalytics JSON schemas](https://docs.gameanalytics.com/products-and-features/pipeline-iq/data-export/json-schemas/). Event categories are listed in [Event types](https://docs.gameanalytics.com/events-metrics-and-filtering/event-types/event-types-introduction/).

Once any design event has been confirmed, a mapping file sits beside that export. Later runs ask only about event ids the mapping does not already cover.

&nbsp;

[🔝](#log-contract-📋)

## Fields on every event

These fields are present regardless of category. They identify who acted, when, and in which build.

| Field | Use |
| --- | --- |
| `data.user_id` | The player. |
| `data.session_id` | The session. |
| `data.session_num` | How many sessions this player has started. |
| `data.client_ts` | When the device recorded the event. |
| `data.build` | The game version. |
| `data.category` | Which schema the rest of the event uses. |

&nbsp;

[🔝](#log-contract-📋)

## Fields the schema already explains

These categories have a fixed meaning in the GameAnalytics schema. An analysis uses that meaning. It does not ask the developer what the category means.

| Category | Fields that matter | A reading may say |
| --- | --- | --- |
| `session_end` | `data.length`, the session duration in seconds | How long the session ran. |
| `progression` | `data.event_id` shaped as status, then up to three progression steps. Status is `Start`, `Fail`, or `Complete`. Optional `data.attempt_num` and `data.score` on fail or complete. | Where players start, fail, retry, and finish. |
| `resource` | `data.event_id` shaped as flow, currency, item type, and item. Flow is source (gained) or sink (spent). `data.amount` is negative when the flow is a sink. | Where a currency or item is gained or spent. |
| `business` | `data.event_id`, `data.amount`, `data.currency` | That a real-money purchase occurred. This is a business fact, not a play-style. |
| `error` | `data.severity`, `data.message` | That the client logged an error. This is a technical fact, not a behavior. |

`ad`, `impression`, and `health` are part of the same export. These analyses do not use them.

&nbsp;

[🔝](#log-contract-📋)

## Fields that stay unmapped until the studio says so

A design event is a custom `data.event_id` of up to five colon-separated parts, plus an optional `data.value`. `data.custom_01`, `data.custom_02`, and `data.custom_03` are the same kind of field: the studio chose the words.

An unmapped design id is reported as a name pattern. It is not given a behavior. `return_to_room` is not exploration until the mapping says which ids are areas, optional content, tools, or risks.

&nbsp;

[🔝](#log-contract-📋)

## The mapping file

One entry per id group. The pattern is a prefix the export actually contains. The meaning is the one the studio assigned, or an explicit ignore.

```yaml
- pattern: "area:*"
  meaning: optional area
  construct: exploration
- pattern: "ui:*"
  meaning: ignore
```

`construct` is one of `exploration`, `risk-taking`, `experimentation`, or omitted when `meaning` is `ignore`. A risk entry also names the safer alternative the log can show, when there is one. An exploration entry names the goal or reward that was available in the same session, when the log has one. If that goal, reward, or safer alternative is absent, the entry says `context: missing` and the analysis reports the missing context instead of a low score.

&nbsp;

[🔝](#log-contract-📋)

## The gate

1. Parse the export.
2. Separate events the schema already explains from design events.
3. Group design ids by prefix.
4. Ask only about groups the mapping does not already cover and that the requested analysis needs. Each answer is one of: this construct, ignore for this run, or not enough information. What the question shows, and how the recommended answer is chosen, is [The recommendation](#the-recommendation).
5. Show a short summary: which ids will be used, which construct each group feeds, which ids will be ignored, and which conclusions will not be drawn.
6. Measure only after the developer confirms or edits that summary.
7. Save the confirmed mapping beside the logs.

A missing confirmation is a missing input. Measurement waits.

&nbsp;

[🔝](#log-contract-📋)

## The recommendation

Gate step 4 is an interview. Ask one design-id group per reply, a group this analysis needs that the mapping does not already cover. The reply ends on that question. Wait for the developer. Do not list the other groups' recommendations and stop.

The question shows:

- The id pattern.
- One structural observation, and the one construct it points at, or that it points at none.
- The word clue: each matched cue, one id that contained it, and that cue's construct, or that no cue matched.
- The recommended answer.
- The three choices, asked of the developer: this construct, ignore for this run, or not enough information?

After the developer answers, ask the next uncovered group the same way. The developer's answer is what gets saved. A recommended construct is written only after the developer confirms it. Ignore is written when the developer confirms ignore. Not enough information writes nothing for that group, so a later run may ask again.

A refusal, a deadline, or "do not ask" is still a missing confirmation. The recommendation does not fill it. Chat text is still not the mapping file.

### The agreement rule

- Both clues point at this skill's construct. Recommend this construct.
- Both clues point at one other construct. Recommend ignore for this run, and name the construct they agreed on.
- Any other case, including one clue, no clue, or a disagreement. Recommend not enough information, and show whichever clues exist.

A structural result that points at none is not a clue for any construct. No structural test names risk-taking, so a risk-taking word cue cannot agree with the structure. That case recommends not enough information.

### Groups and the attempt window

The prefix in gate step 3 is this group. A group is the first colon-separated segment of a design `data.event_id`, written as `segment:*`. An id with no colon is its own group, and the pattern is that full id. Only events whose `data.category` is `design` form groups.

A progression step is the progression `data.event_id` with the status segment removed. `Start:world:level1`, `Fail:world:level1`, and `Complete:world:level1` are the step `world:level1`. Status is `Start`, `Fail`, or `Complete`.

An attempt owns the design events after the previous `Fail` or `Complete` for that user and session, up through this outcome. When there is no previous outcome, it owns the events from the start of the session through this outcome. A `Start` inside that window belongs to the attempt. The window does not depend on `Start` being present. Design events after the last outcome in the session belong to no attempt.

`attempt_num`, when present, distinguishes attempts. When it is absent, the order of outcomes in the session distinguishes them.

Events outside any attempt, and an export with no progression events, give every group no structural clue.

### Structural tests

The tests do not read the cue list. Evaluate each progression step for the group, then combine the steps.

On one step, use the first case that matches. If both experimentation cases match, the step still points at experimentation once.

1. **Experimentation, cross-group.** The group appears in one attempt and is absent in another, and a different group does the reverse: that other group is present where this one is absent, and absent where this one is present. Attempts may sit in different sessions. Both groups point at experimentation for this step.
2. **Experimentation, within one session.** Inside one session, the full design event ids of this group change across attempts of this step, and the group is present on each of those attempts. The group points at experimentation for this step.
3. **Exploration.** The group appears in some sessions that contain this step and is absent in others, and neither experimentation case matched on this step. This needs more than one session. The group points at exploration for this step.

Combine the steps:

- Every step that names a construct names the same one. The structural result points at that construct.
- Two steps name different constructs. The result points at none. The observation says the steps disagree.
- No step names a construct, and the group shares an attempt with another design-id group. The observation states that co-occurrence. The result points at none.
- Otherwise there is no structural clue.

Co-occurrence is not added when a step already named a construct, or when steps disagree.

### The cue list

Split each design `event_id` on `:`, `_`, and `-`. Compare each whole token to the list with case ignored. A group has a word clue only when every matched cue belongs to one construct. The question quotes every matched cue and one id that contained it. Cues from two constructs leave no word clue.

| Cue | Construct |
| --- | --- |
| `area`, `explore`, `exploration`, `optional` | exploration |
| `loadout`, `equip`, `experiment` | experimentation |
| `fight`, `risk`, `danger` | risk-taking |

`door`, `ui`, `cave`, `grove`, `room`, `return`, `sword`, `bow`, `staff`, and `boss` are not cues. `door` names a safer alternative. The others are instance words.

&nbsp;

[🔝](#log-contract-📋)

## What a result contains

A result keeps these steps separate.

| Step | What it is |
| --- | --- |
| Observation | The events that fired. |
| Measurement | Counts, ratios, and sequences from those events. |
| Inference | The construct those measurements support, with a separate confidence. |
| Interpretation | What a designer might check in the game. |

A score means the sessions contain evidence of that behavior under the goals, rewards, and alternatives the log shows. It does not mean the player has a trait. If the trace is too thin, or the required context is missing, the result says so and does not score.

&nbsp;

[🔙](../../README.md#research)
