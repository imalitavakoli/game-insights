Synthetic reading for `export.json` beside `mapping.yaml`. The numbers below belong to that pair only.

## Observation

One player (`p1`), three sessions (`s1`, `s2`, `s3`).

- `s1`: `area:cave`, `area:grove`, `ui:pause`, then `Complete:world:level1`. Session length 800 seconds.
- `s2`: `Complete:world:level1` only. Session length 400 seconds.
- `s3`: `area:cave`, then `Complete:world:level1`. Session length 600 seconds.

`ui:pause` matches `ui:*` and is ignored.

## Measurement

`area:*` is an optional area for exploration. The named goal `Complete:world:level1` is present in every session.

- `area:cave`: 2 events (`s1`, `s3`).
- `area:grove`: 1 event (`s1`).
- Optional-area events: 3, in 2 of 3 sessions.
- `s2` has the goal and no `area:*` event.

## Inference

**Score:** 3 optional-area events in 2 of 3 sessions, under the goal `Complete:world:level1`.

**Confidence:** separate from the score. One player, three sessions, two mapped area ids.

This is evidence in these sessions. It is not a player trait. The score would be withheld if the mapping said `context: missing`, or if the trace were too thin to carry it.

## Interpretation

A designer can check whether `area:grove` is harder to reach than `area:cave`, and whether a session that only completes `world:level1` (`s2`) is the intended on-path while those optional areas stay available.

## Could not check

The mapping names a goal and does not name a reward. Dwell and coverage are not in the export. `data.value` is 1 on every area row.
