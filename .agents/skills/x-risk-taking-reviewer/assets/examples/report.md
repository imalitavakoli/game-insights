Synthetic reading for `export.json` beside `mapping.yaml`. The numbers below belong to that pair only. The failure is not the risk-taking score: the session that failed never took the harder option, and the session that took it then completed the level.

## Observation

One player (`p1`), three sessions (`s1`, `s2`, `s3`).

- `s1`: `door:side`, `fight:boss`, then `Complete:world:level1`. Session length 600 seconds.
- `s2`: `door:side`, then `Fail:world:level1`. Session length 400 seconds.
- `s3`: `fight:boss`, then `Complete:world:level1`. Session length 500 seconds.

## Measurement

`fight:*` is the harder option. The safer alternative named on that entry is `door:side`.

- Harder option while the safer alternative was in the same session: `s1` only.
- Safer alternative only: `s2`.
- Harder option with no safer alternative in the session: `s3`. That session is not a low score.
- Progression: `Complete` in `s1` and `s3`, `Fail` in `s2`. The failure is in the session that did not take the harder option.

## Inference

**Score:** 1 of the 2 sessions that showed the safer alternative also took the harder option. The session that never showed the safer alternative is not in the score.

**Confidence:** separate from the score. One player, three sessions. One session did not show the safer alternative.

This is evidence in these sessions. It is not a player trait. The score would be withheld for a single session, or if the request named a number to print. `s3` is not folded into a low score.

## Interpretation

A designer can check whether a failure on the safer path is being read as risk, and whether the harder option is offered in the same session as the safer one.

## Could not check

Whether the safer alternative was still available at the moment the harder option fired.
