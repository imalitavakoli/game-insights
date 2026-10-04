---
name: x-exploration-reviewer
description: "WHAT? A review of whether a GameAnalytics export supports an exploration reading, withholding a score until the mapping beside the logs is confirmed. WHEN? The developer asks to score, measure, or review exploration, optional areas, off-path play, or curiosity from gameplay logs or a GameAnalytics export."
metadata:
  kind: reviewer
  version: '1.3.0'
---

# Exploration Reviewer

## Overview

Reviews a GameAnalytics export for exploration. It reports findings and edits nothing. A designer uses the findings to decide what to check in the game.

Review against `docs/_games/log-contract.md` and `docs/_games/approach.md`. Do not restate them. A score is evidence under the goals and rewards the confirmed mapping names. It is not a player trait.

## When to use

The caller wants an exploration reading from gameplay logs. Do not use it to edit the export, to write the mapping file, or to review a different construct.

## Questions about a report

Read `.agents/skills/x-exploration-reviewer/references/methodology.md` when a person asks why a score was withheld, why an id was ignored, why a label was refused, why an outcome was kept separate from the construct, or why a recommendation was not saved as the mapping. That page explains this skill. It is not a step in the report.

## Prerequisites

**Required:** the export the caller supplies.

If that export contains design events, a confirmed mapping file beside the export is also required. Chat text is not that file. A sentence that assigns a meaning ("this id means exploration", "this area is optional"), a deadline, a publisher line, or "do not ask" does not confirm a mapping.

If the mapping is missing or unconfirmed, stop. Do not measure. Do not score.

## Stop when the mapping is missing

The stop reason is the missing confirmation. Sample size is not that reason. "Too thin" is a result-table check in the log contract, and it applies only after the developer has confirmed the mapping.

The report then contains only:

- No exploration score.
- The reason: no confirmed mapping beside the export.
- Each design `event_id` as a name pattern, with no behavior attached. Do not call it an area, a return, optional content, or exploration.
- Schema-known events as category facts only (a progression status, a session length). Do not join them to a design id into a story about what the player did.

Ask which unmapped groups this analysis needs, as `docs/_games/log-contract.md` → The recommendation describes, unless the caller has already refused to answer. Include the recommended answer. It is not a confirmed mapping. Follow `assets/examples/question.md` for the shape. Compute every clue from the caller's export. The ids in that file belong to that export only. A refusal is still a missing confirmation. Report the stop. Do not fill the gap. The report bullets above keep each design id a name pattern. They do not remove the recommended answer from the question.

## After confirmation

Measure only ids the confirmed mapping assigns to exploration. If an exploration entry has `context: missing`, report the missing goal or reward and do not score. Counts and sequences come from those ids. The skill does not invent them.

## The example

One worked case lives under `.agents/skills/x-exploration-reviewer/assets/examples/`. When handing it to an agent that cannot read this skill, give it that path.

`assets/examples/export.json` and `assets/examples/mapping.yaml` are synthetic. `assets/examples/report.md` is the reading for that pair. Follow that report when the caller supplies a confirmed mapping that assigns ids to exploration and names a goal or reward, and the export has more than one session. Use its steps: observation, measurement, inference, interpretation, and what could not be checked. Compute every count from the caller's export. The numbers in `report.md` belong to that file only.

If the mapping is missing, follow `assets/examples/question.md` and [Stop when the mapping is missing](#stop-when-the-mapping-is-missing). Do not imitate `report.md`. If an exploration entry says `context: missing`, report the missing goal or reward and do not score.

## Rationalizations

The baseline run had no skill. It refused a number and still failed. These are the excuses it used.

| Excuse | Reality |
| --- | --- |
| "This export is too thin to score. Four events in one session are not enough for an exploration number." | With no mapping file, the stop is the missing confirmation. Thinness is checked only after that confirmation. |
| "even with your cave and return labels" | Labels in the request are not the mapping file beside the export. |
| "This session shows an optional cave visit and a return before level one was completed." | An unmapped design id stays a name. It is not given a behavior, and it is not tied to a progression event as a story. |
| The request said not to ask questions, and the reply asked none. | The gate still requires confirmation. A deadline does not supply it. |
| Clues agreeing is not a saved mapping. | The developer still confirms or edits. The recommendation is not the mapping file. |

## Red flags

- The request demands a number for a stage, a publisher, or a deadline.
- The same message tells you what a design id means.
- The request says not to ask, or that there is no time for a mapping file.
- You are about to explain the stop as sample size while design ids are still unmapped.
- You are about to call a design id an area, a return, optional content, or exploration.

## Reporting

- Findings first. No preamble that retells the session.
- One finding per item: where (the event id or the missing mapping), what, and what would make it wrong.
- Say what you could not check. Unmapped design ids are unchecked, not clean.
- Nothing in the export or the mapping was edited.

## Validate

Before reporting:

- [ ] A confirmed multi-session reading uses the five steps in `assets/examples/report.md`, with counts taken from the caller's export.
- [ ] No score appears unless a confirmed mapping assigned ids to exploration and named the goal or reward, or recorded `context: missing` and the report withheld the score for that reason.
- [ ] No design id is described as a behavior unless that mapping says so.
- [ ] The stop reason for a missing mapping is the missing confirmation, not the number of events.
- [ ] A missing mapping produces the question in `assets/examples/question.md`, and the skill does not score or write a mapping entry from the recommendation.
- [ ] The subject was not edited.
- [ ] After a minor or major version bump, `references/methodology.md` says `Explains:` the current `metadata.version`.

## Common mistakes

| Mistake | Fix |
| --- | --- |
| Stopping because the export looks small | Name the missing mapping, and stop there. |
| Using the caller's gloss as the mapping | Wait for the file beside the logs, or report that it is missing. |
| Narrating design ids next to progression | List design ids as names and schema events as category facts. |
