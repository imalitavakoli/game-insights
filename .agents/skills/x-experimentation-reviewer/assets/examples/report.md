Synthetic reading for `export.json` beside `mapping.yaml`. The numbers below belong to that pair only.

## Observation

One player (`p1`), three sessions (`s1`, `s2`, `s3`).

- `s1`: `loadout:sword`, `Fail:world:level1` (attempt 1), `loadout:bow`, `Complete:world:level1` (attempt 2). Session length 500 seconds.
- `s2`: `loadout:sword`, then `Complete:world:level1` (attempt 1). Session length 300 seconds.
- `s3`: `loadout:bow`, `Fail:world:level1` (attempt 1), `loadout:staff`, `Complete:world:level1` (attempt 2). Session length 700 seconds.

## Measurement

`loadout:*` is an equipped option for experimentation.

- `loadout:sword`: 2 events (`s1`, `s2`).
- `loadout:bow`: 2 events (`s1`, `s3`).
- `loadout:staff`: 1 event (`s3`).
- Equipped-option events: 5. Order: `loadout:sword`, `loadout:bow`, `loadout:sword`, `loadout:bow`, `loadout:staff`.
- The equipped option changed inside `s1` and `s3`. `s2` kept one option.

Progression stays a category fact. `Fail:world:level1` twice. `Complete:world:level1` three times. A later `Complete` does not show that a loadout change worked.

## Inference

**Score:** the equipped option changed in 2 of 3 sessions.

**Confidence:** separate from the score. One player, three sessions, three mapped loadout ids.

This is evidence in these sessions. It is not a player trait. The score would be withheld for a single session, or if the request named a number to print.

## Interpretation

A designer can check whether a second equipped option after a fail (`s1`, `s3`) is the intended retry, whether keeping one option when the first attempt completes (`s2`) is intended, and whether `loadout:staff` appearing once and last matches how that option is offered.

## Could not check

Whether every option was available in every session. Whether an equip persisted into the attempt. What `data.value` of 1 means.
