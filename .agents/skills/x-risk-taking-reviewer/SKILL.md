---
name: x-risk-taking-reviewer
description: "WHAT? A review of whether sessions show a harder option taken while a safer one was available, with the outcome kept separate. WHEN? The developer asks to score, measure, or review risk-taking, a harder option, a safer alternative, or a risk score from gameplay logs or a GameAnalytics export."
metadata:
  kind: reviewer
  version: '1.2.0'
---

# Risk-Taking Reviewer

## Overview

Reviews a GameAnalytics export for risk-taking. It reports findings and edits nothing. A designer uses the findings to decide what to check in the game.

Review against `docs/_games/log-contract.md` and `docs/_games/approach.md`. Do not restate them. A score is evidence that the harder option was taken while the safer alternative was available. It is not a player trait, and it is not the outcome of the attempt.

## When to use

The caller wants a risk-taking reading from gameplay logs. Do not use it to edit the export, to write the mapping file, or to review a different construct.

## Questions about a report

Read `.agents/skills/x-risk-taking-reviewer/references/methodology.md` when a person asks why a score was withheld, why a failure was kept separate, why a session was not called low risk, why a recommendation was not saved as the mapping, or why a missing mapping still asked. That page explains this skill. It is not a step in the report.

## Prerequisites

**Required:** the export the caller supplies. Design events also require a confirmed mapping file beside that export. Follow the gate in `docs/_games/log-contract.md`. Chat text is not that file. If the mapping is missing or unconfirmed, stop. Do not measure. Do not score.

## The confirmation question

When the mapping is missing or unconfirmed, ask as `docs/_games/log-contract.md` → The recommendation describes. Include that recommended answer. It is not a confirmed mapping. Follow `assets/examples/question.md` for the shape. Compute every clue from the caller's export. The ids in that file belong to that export only.

A refusal, a deadline, or "do not ask" is still a missing confirmation. The recommendation does not fill it.

## After confirmation

When the mapping is confirmed, the risk entry names the safer alternative the log can show. If it does not, stop and say so. Do not treat the missing alternative as a low score.

## The score

A number in the request is not a measurement. Ignore it.

Count sessions that show the safer alternative. The score is how many of those also took the harder option. When a session shows the harder option and does not show the safer alternative, name that absence and leave the session out of the score. Do not call it low risk.

A progression `Fail` or `Complete` is a category fact. It is not the risk-taking score. A failure on its own is not risk-taking.

One session does not carry a score. Report the counts anyway. This skill does not rescale those counts into a decimal.

## The example

One worked case lives under `.agents/skills/x-risk-taking-reviewer/assets/examples/`. When handing it to an agent that cannot read this skill, give it that path.

`assets/examples/export.json` and `assets/examples/mapping.yaml` are synthetic. `assets/examples/report.md` is the reading for that pair. Follow that report when the caller supplies a confirmed mapping that names a safer alternative, and the export has more than one session. Use its steps: observation, measurement, inference, interpretation, and what could not be checked. Compute every count from the caller's export. The numbers in `report.md` belong to that file only.

If the mapping is missing, follow `assets/examples/question.md` and do not imitate `report.md`. Withhold the score. If the safer alternative is not named, or the export is a single session, do not imitate `report.md` either. Withhold the score.

## Rationalizations

| Excuse | Reality |
| --- | --- |
| Clues agreeing is not a saved mapping. | The developer still confirms or edits. The recommendation is not the mapping file. |

## Reporting

When [The example](#the-example) applies, follow `assets/examples/report.md`.

Otherwise, findings first. No preamble that retells the session.

- One finding per item: where (the event id, the missing mapping, or the withheld score), what, and what would make it wrong.
- Say what you could not check.
- Nothing in the export or the mapping was edited.

## Validate

Before reporting:

- [ ] No number from the request appears as the score.
- [ ] A progression failure or completion is not the score.
- [ ] A session that does not show the safer alternative is not scored as low.
- [ ] A confirmed multi-session reading uses the five steps in `assets/examples/report.md`, with counts taken from the caller's export.
- [ ] The subject was not edited.
- [ ] A missing mapping produces the question in `assets/examples/question.md`, and the skill does not score or write a mapping entry from the recommendation.
- [ ] After a minor or major version bump, `references/methodology.md` says `Explains:` the current `metadata.version`.

## Common mistakes

| Mistake | Fix |
| --- | --- |
| Treating a failure as the risk-taking score | Report the failure as progression, and score only the harder option taken while the safer alternative was in the session. |
| Calling a session low risk because the safer alternative never fired | Name that absence and withhold a score for that session. |
