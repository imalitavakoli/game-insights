---
name: x-play-style-reviewer
description: "WHAT? A summary of the exploration, risk-taking, and experimentation readings together with progression and resource patterns. WHEN? The developer asks to score, measure, or review play style from those readings and a GameAnalytics export."
metadata:
  kind: reviewer
  version: '1.1.0'
---

# Play Style Reviewer

## Overview

Summarizes three readings the caller supplies, plus progression and resource patterns in the export. It reports findings and edits nothing. A designer uses the summary to decide what to check in the game.

Review against `docs/_games/log-contract.md` and `docs/_games/approach.md`. Do not restate them. The summary keeps the three readings distinct. It does not collapse them into one number or a personality label.

## When to use

The caller wants a play-style summary from an exploration reading, a risk-taking reading, an experimentation reading, and a GameAnalytics export. Do not use it to edit the export, to re-measure those three constructs from design events, or to write a mapping file.

## Questions about a report

Read `.agents/skills/x-play-style-reviewer/references/methodology.md` when a person asks why there is no single score, why a missing reading stopped the summary, or why design events were not measured again. That page explains this skill. It is not a step in the report.

## Prerequisites

**Required:** the exploration reading, the risk-taking reading, the experimentation reading, and the export.

If any reading is missing, stop. Do not summarize the readings that did arrive. Do not invent the missing one. Do not score.

The readings are the caller's artifacts. This skill does not re-open design events to produce them.

## The summary

A number in the request is not a measurement. Ignore it. A label for the player is not a measurement either.

State each reading's score and confidence as given. From the export, count progression statuses and resource flows. Those are category facts. Place them beside the three readings. Do not blend the five counts into one score.

A designer note may tie a progression or resource event to a reading only when that reading names the session. Do not reuse the example's note on another export.

## The example

One worked case lives under `.agents/skills/x-play-style-reviewer/assets/examples/`. When handing it to an agent that cannot read this skill, give it that path.

The three reading files and `assets/examples/export.json` are synthetic. `assets/examples/report.md` is the summary for that set. Follow that report when all three readings and the export are present. Use its steps: observation, measurement, inference, interpretation, and what could not be checked. Take the reading scores from the files the caller supplied. Count progression and resource from the caller's export. The numbers in `report.md` belong to that set only.

If any reading is missing, do not imitate the example.

## Reporting

When [The example](#the-example) applies, follow `assets/examples/report.md`.

Otherwise, findings first.

- One finding per item: where (the missing reading, or a progression or resource count), what, and what would make it wrong.
- Say what you could not check.
- Nothing in the export or the readings was edited.

## Validate

Before reporting:

- [ ] A missing reading stops the summary. The other readings are not scored together.
- [ ] Design events are not measured again.
- [ ] No single number and no personality label appear as the play-style score.
- [ ] A complete summary uses the five steps in `assets/examples/report.md`, with progression and resource counts taken from the caller's export.
- [ ] The subject was not edited.
- [ ] After a minor or major version bump, `references/methodology.md` says `Explains:` the current `metadata.version`.

## Common mistakes

| Mistake | Fix |
| --- | --- |
| Producing a play-style number from two readings | Stop and name the missing reading. |
| Re-counting design events | Use the scores in the readings the caller supplied. |
| Reusing the example's designer note | Tie a schema event to a reading only when that reading names the session. |
