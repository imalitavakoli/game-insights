---
name: x-experimentation-reviewer
description: "WHAT? A review of whether a GameAnalytics export supports an experimentation reading, withholding a score the caller names or that a thin trace cannot carry. WHEN? The developer asks to score, measure, or review experimentation, loadout changes, variation across attempts, or retries from gameplay logs or a GameAnalytics export."
metadata:
  kind: reviewer
  version: '1.2.0'
---

# Experimentation Reviewer

## Overview

Reviews a GameAnalytics export for experimentation. It reports findings and edits nothing. A designer uses the findings to decide what to check in the game.

Review against `docs/_games/log-contract.md` and `docs/_games/approach.md`. Do not restate them. A score is evidence under the confirmed mapping. It is not a player trait.

## When to use

The caller wants an experimentation reading from gameplay logs. Do not use it to edit the export, to write the mapping file, or to review a different construct.

## Questions about a report

Read `.agents/skills/x-experimentation-reviewer/references/methodology.md` when a person asks why a score was withheld, why an id was ignored, why a label was refused, or why an outcome was kept separate from the construct. That page explains this skill. It is not a step in the report.

## Prerequisites

**Required:** the export the caller supplies. Design events also require a confirmed mapping file beside that export. Follow the gate in `docs/_games/log-contract.md`. Chat text is not that file. If the mapping is missing or unconfirmed, stop. Do not measure. Do not score.

## The score

A number in the request is not a measurement. Ignore it.

Report the counts and the ordered sequence of the ids the confirmed mapping assigns to experimentation, plus the progression events as category facts. A score is one of those counts, or it is absent.

If the trace is too thin to score, say so and do not score. Low confidence does not sit beside a score. One session is that thin trace.

An outcome, including a later `Complete`, is not the experimentation score and does not prove a loadout change worked.

## The example

One worked case lives under `.agents/skills/x-experimentation-reviewer/assets/examples/`. When handing it to an agent that cannot read this skill, give it that path.

`assets/examples/export.json` and `assets/examples/mapping.yaml` are synthetic. `assets/examples/report.md` is the reading for that pair. Follow that report when the caller supplies a confirmed mapping that assigns ids to experimentation, and the export has more than one session. Use its steps: observation, measurement, inference, interpretation, and what could not be checked. Compute every count from the caller's export. The numbers in `report.md` belong to that file only.

If the mapping is missing, or the export is a single session, do not imitate the example. Withhold the score.

## Rationalizations

| Excuse | Reality |
| --- | --- |
| "Experimentation score: 0.95. Confidence is low: one session, two attempts." | The request named 0.95. The trace was already judged thin. A thin trace does not score, and low confidence does not carry one. |
| "Experimentation score is 0.95 from the confirmed loadout mapping." | A confirmed mapping allows counts and the sequence. It does not turn the caller's number into a measurement. |
| "Those measurements support experimentation under the mapping you confirmed." | The measurements are the counts and the sequence. They are not a 0–1 score the caller asked you to print. |

## Red flags

- The request names the score to print.
- You are about to attach "confidence is low" to a number.
- You are about to treat a `Complete` or a `Fail` as proof the variation worked.
- The trace is a single session and a score is still in the reply.

## Reporting

When [The example](#the-example) applies, follow `assets/examples/report.md`.

Otherwise, findings first. No preamble that retells the session.
- One finding per item: where (the event id, the missing mapping, or the withheld score), what, and what would make it wrong.
- Say what you could not check.
- Nothing in the export or the mapping was edited.

## Validate

Before reporting:

- [ ] No number from the request appears as the score.
- [ ] A thin trace, including a single session, has no score.
- [ ] A confirmed multi-session reading uses the five steps in `assets/examples/report.md`, with counts taken from the caller's export.
- [ ] Confirmed experimentation ids are reported as counts and an ordered sequence.
- [ ] The subject was not edited.
- [ ] After a minor or major version bump, `references/methodology.md` says `Explains:` the current `metadata.version`.

## Common mistakes

| Mistake | Fix |
| --- | --- |
| Printing the number the caller named | Report the counts and the sequence, and withhold the score. |
| Scoring a single session and calling confidence low | State that the trace is too thin, and omit the score. |
