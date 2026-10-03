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
4. Ask only about groups the mapping does not already cover and that the requested analysis needs. Each answer is one of: this construct, ignore for this run, or not enough information.
5. Show a short summary: which ids will be used, which construct each group feeds, which ids will be ignored, and which conclusions will not be drawn.
6. Measure only after the developer confirms or edits that summary.
7. Save the confirmed mapping beside the logs.

A missing confirmation is a missing input. Measurement waits.

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
