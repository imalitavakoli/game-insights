Explains: v1.2.0

Answers for a person asking why a risk-taking reading came out as it did. The shared method is `docs/_games/approach.md` and `docs/_games/log-contract.md`. This page covers only the choices this skill makes.

## Why a failure is not the score

This skill scores a session only when the harder option and the safer alternative both appear in it. A progression failure in a session that never took the harder option is not that score. A completion after the harder option is not that score either. The outcome stays a category fact beside the choice.

## Why one session does not score

One session can show the harder option beside the safer alternative and still be too thin to score. A single sitting cannot show whether the choice is a pattern. The counts can still be reported. A score waits until there is more than one session. This skill does not rescale those counts into a decimal.

## Why a session without the safer alternative is not low risk

The score counts sessions where the safer alternative was in the log and the harder option was taken. A session that shows the harder option and never shows the safer alternative has nothing to compare. This skill names that gap and does not fill it with a low score.

## Why the score is that session count

The score is how many sessions took the harder option, among the sessions that also showed the safer alternative. Sessions that never show the safer alternative stay outside that count. Each export supplies its own count.

## Why a recommendation is not a mapping

The recommendation is defined in `docs/_games/log-contract.md` under The recommendation. This skill includes it in the confirmation question. The developer's answer is the mapping. This page does not restate the tests.

## Why a missing mapping still asks

The safer alternative is checked after the mapping is confirmed. A missing mapping still asks the confirmation question. That check has no recommended answer.
