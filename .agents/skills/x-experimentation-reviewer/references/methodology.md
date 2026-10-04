Explains: v1.5.0

Answers for a person asking why an experimentation reading came out as it did. The shared method is `docs/_games/approach.md` and `docs/_games/log-contract.md`. This page covers only the choices this skill makes.

## Why a number the caller names is not the score

This skill does not print a score the caller names, including one presented as a ratio. Low confidence does not sit beside that number.

## Why one session does not score

This skill treats one session as too thin to score, even when the mapped option changes inside it. A single sitting cannot show whether the change is a pattern. The counts and the sequence can still be reported. A score waits until there is more than one session. This skill does not rescale those counts into a decimal.

## Why a later completion does not prove the change worked

A progression completion means that step finished. It does not mean the mapped option caused the finish. The same split applies to a failure.

## Why the score counts sessions where the mapped option changed

The score is how many sessions changed the option the mapping assigns to experimentation, out of the sessions in the export. The event counts and the order stay in the measurement. Each export supplies its own count.

## Why the report will not claim an option was available

This skill does not claim an option was available and unused, or that a chosen option lasted into the attempt. It does not interpret the optional value on a design event.

## Why a recommendation is not a mapping

The recommendation is defined in `docs/_games/log-contract.md` under The recommendation. This skill includes it in the confirmation question. The developer's answer is the mapping. This page does not restate the tests.

## Why every group is on one form

A list of recommendations is not the interview. This skill asks every unmapped group on one form. Each question has three options the developer selects. The recommended option is first. The reply waits once.

## Why one clue is enough

One clue, or two clues that name the same construct, recommends that construct. Two clues that name different constructs, or no clue, recommends not enough information. The tests and the cue list stay in the log contract.
