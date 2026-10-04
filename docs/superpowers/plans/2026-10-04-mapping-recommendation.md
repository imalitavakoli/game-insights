# Mapping Recommendation Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** When a construct skill asks a developer to confirm a design-id group, the question includes a recommended answer that is not itself a mapping.

**Architecture:** `docs/_games/log-contract.md` gains `## The recommendation` after `## The gate`. That section holds the agreement rule, the structural tests, the attempt window, and the cue list. Exploration, experimentation, and risk-taking point at that heading when the mapping is missing. Each gains `assets/examples/question.md` for its synthetic export. Play style does not ask these questions.

**Tech Stack:** Markdown skills and the log contract. No new packages. Owner lines go through `.agents/skills/x-codeowners-editor/scripts/upsert-owner.mjs`.

## Global Constraints

- The recommendation is not a mapping. The developer confirms or edits it before anything is saved.
- The three skills do not copy the tests or the cue list.
- `docs/_games/approach.md` stays unchanged. The mapping-file shape stays unchanged. Context questions for a goal, a reward, or a safer alternative carry no recommended answer.
- `x-play-style-reviewer` stays at version 1.1.0. Do not edit it.
- Versions: `x-exploration-reviewer` 1.2.0 → 1.3.0, `x-experimentation-reviewer` 1.2.0 → 1.3.0, `x-risk-taking-reviewer` 1.0.0 → 1.1.0. Each `references/methodology.md` `Explains:` line matches that version.
- A group is the first colon-separated segment of a design `data.event_id`, written as `segment:*`. An id with no colon is its own group.
- Only events whose `data.category` is `design` form groups.
- An attempt owns the design events after the previous `Fail` or `Complete` for that user and session, up through this outcome. When there is no previous outcome, it owns the events from the start of the session through this outcome. A `Start` inside that window belongs to the attempt. The window does not depend on `Start` being present.
- No structural test names risk-taking.
- Cue list, whole token, case ignored, split on `:`, `_`, and `-`: exploration `area`, `explore`, `exploration`, `optional`; experimentation `loadout`, `equip`, `experiment`; risk-taking `fight`, `risk`, `danger`. `door`, `ui`, `cave`, `grove`, `room`, `return`, `sword`, `bow`, `staff`, and `boss` are not cues.
- Both clues on this skill's construct → recommend this construct. Both clues on one other construct → recommend ignore for this run and name that construct. Otherwise → not enough information.
- Not enough information writes nothing for that group.
- A refusal, a deadline, or "do not ask" is still a missing confirmation. The recommendation does not fill it.
- `assets/examples/report.md` stays the reading after a mapping is confirmed. Do not edit those reports.
- Commits use `type(scope): summary` (imperative, lowercase, no trailing period). Do not create a branch. Do not invent a TRACKER-ID.
- `/docs/superpowers/` is owned by `@Vida`.
- Do not edit the `.claude/skills/` pointer stubs. Their `description` fields do not change.

---

### Task 1: Owner line for the new docs path

**Files:**
- Modify: `CODEOWNERS`
- Already on disk, do not rewrite: `docs/superpowers/specs/2026-10-04-mapping-recommendation-design.md`
- Already on disk, do not rewrite: `docs/superpowers/plans/2026-10-04-mapping-recommendation.md`

**Interfaces:**
- Consumes: confirmed owner `@Vida` for `/docs/superpowers/`
- Produces: a `CODEOWNERS` line `/docs/superpowers/ @Vida` in the docs section

- [ ] **Step 1: Check the line is absent**

Run: `rg -n "docs/superpowers" CODEOWNERS`

Expected: no matches, exit code 1.

- [ ] **Step 2: Insert the owner line**

Run from the repo root:

```
node .agents/skills/x-codeowners-editor/scripts/upsert-owner.mjs --path /docs/superpowers/ --owner @Vida
```

Expected stdout: `added`

Do not hand-edit `CODEOWNERS`. If the script reports a handoff error, stop.

- [ ] **Step 3: Check the line**

Run: `rg -n "docs/superpowers" CODEOWNERS`

Expected: a line `/docs/superpowers/ @Vida` under the docs section.

- [ ] **Step 4: Commit the new path and its owner**

The spec and this plan are already written. Do not edit them in this step.

```
git add CODEOWNERS docs/superpowers/specs/2026-10-04-mapping-recommendation-design.md docs/superpowers/plans/2026-10-04-mapping-recommendation.md
git commit -m "docs: specify mapping recommendation"
```

Expected: one commit, those three paths only.

---

### Task 2: Log contract recommendation section

**Files:**
- Modify: `docs/_games/log-contract.md` (gate step 4 around line 89; insert the new section after the gate's `[🔝](#log-contract-📋)` and before `## What a result contains`)

**Interfaces:**
- Consumes: nothing from Task 1
- Produces: heading `## The recommendation` and anchor `#the-recommendation`, which Tasks 3–5 cite. Subheadings: `### The agreement rule`, `### Groups and the attempt window`, `### Structural tests`, `### The cue list`.

- [ ] **Step 1: Check the heading is absent**

Run: `rg -n "^## The recommendation" docs/_games/log-contract.md`

Expected: no matches, exit code 1.

- [ ] **Step 2: Point gate step 4 at the new section**

Replace this sentence:

```
4. Ask only about groups the mapping does not already cover and that the requested analysis needs. Each answer is one of: this construct, ignore for this run, or not enough information.
```

with:

```
4. Ask only about groups the mapping does not already cover and that the requested analysis needs. Each answer is one of: this construct, ignore for this run, or not enough information. What the question shows, and how the recommended answer is chosen, is [The recommendation](#the-recommendation).
```

Leave steps 1–3 and 5–7 as they are.

- [ ] **Step 3: Insert the section**

Insert this block after the gate's closing `[🔝](#log-contract-📋)` and before `## What a result contains`. Keep the page's blank-line and `&nbsp;` pattern.

```markdown
## The recommendation

Gate step 4 asks the developer about each design-id group this analysis needs and the mapping does not already cover. The question shows:

- The id pattern.
- One structural observation, and the one construct it points at, or that it points at none.
- The word clue: each matched cue, one id that contained it, and that cue's construct, or that no cue matched.
- The recommended answer.
- The three choices: this construct, ignore for this run, or not enough information.

The developer's answer is what gets saved. A recommended construct is written only after the developer confirms it. Ignore is written when the developer confirms ignore. Not enough information writes nothing for that group, so a later run may ask again.

A refusal, a deadline, or "do not ask" is still a missing confirmation. The recommendation does not fill it. Chat text is still not the mapping file.

### The agreement rule

- Both clues point at this skill's construct. Recommend this construct.
- Both clues point at one other construct. Recommend ignore for this run, and name the construct they agreed on.
- Any other case, including one clue, no clue, or a disagreement. Recommend not enough information, and show whichever clues exist.

A structural result that points at none is not a clue for any construct. No structural test names risk-taking, so a risk-taking word cue cannot agree with the structure. That case recommends not enough information.

### Groups and the attempt window

The prefix in gate step 3 is this group. A group is the first colon-separated segment of a design `data.event_id`, written as `segment:*`. An id with no colon is its own group, and the pattern is that full id. Only events whose `data.category` is `design` form groups.

A progression step is the progression `data.event_id` with the status segment removed. `Start:world:level1`, `Fail:world:level1`, and `Complete:world:level1` are the step `world:level1`. Status is `Start`, `Fail`, or `Complete`.

An attempt owns the design events after the previous `Fail` or `Complete` for that user and session, up through this outcome. When there is no previous outcome, it owns the events from the start of the session through this outcome. A `Start` inside that window belongs to the attempt. The window does not depend on `Start` being present. Design events after the last outcome in the session belong to no attempt.

`attempt_num`, when present, distinguishes attempts. When it is absent, the order of outcomes in the session distinguishes them.

Events outside any attempt, and an export with no progression events, give every group no structural clue.

### Structural tests

The tests do not read the cue list. Evaluate each progression step for the group, then combine the steps.

On one step, use the first case that matches. If both experimentation cases match, the step still points at experimentation once.

1. **Experimentation, cross-group.** The group appears in one attempt and is absent in another, and a different group does the reverse: that other group is present where this one is absent, and absent where this one is present. Attempts may sit in different sessions. Both groups point at experimentation for this step.
2. **Experimentation, within one session.** Inside one session, the full design event ids of this group change across attempts of this step, and the group is present on each of those attempts. The group points at experimentation for this step.
3. **Exploration.** The group appears in some sessions that contain this step and is absent in others, and neither experimentation case matched on this step. This needs more than one session. The group points at exploration for this step.

Combine the steps:

- Every step that names a construct names the same one. The structural result points at that construct.
- Two steps name different constructs. The result points at none. The observation says the steps disagree.
- No step names a construct, and the group shares an attempt with another design-id group. The observation states that co-occurrence. The result points at none.
- Otherwise there is no structural clue.

Co-occurrence is not added when a step already named a construct, or when steps disagree.

### The cue list

Split each design `event_id` on `:`, `_`, and `-`. Compare each whole token to the list with case ignored. A group has a word clue only when every matched cue belongs to one construct. The question quotes every matched cue and one id that contained it. Cues from two constructs leave no word clue.

| Cue | Construct |
| --- | --- |
| `area`, `explore`, `exploration`, `optional` | exploration |
| `loadout`, `equip`, `experiment` | experimentation |
| `fight`, `risk`, `danger` | risk-taking |

`door`, `ui`, `cave`, `grove`, `room`, `return`, `sword`, `bow`, `staff`, and `boss` are not cues. `door` names a safer alternative. The others are instance words.

&nbsp;

[🔝](#log-contract-📋)
```

- [ ] **Step 4: Check the section**

Run:

```
rg -n "^## The recommendation|^### The agreement rule|^### Structural tests|^### The cue list" docs/_games/log-contract.md
```

Expected: four matches, in that order.

Run: `rg -n "loadout" docs/_games/log-contract.md`

Expected: the cue table row for `loadout`.

Run: `rg -n "approach.md" docs/_games/log-contract.md`

Expected: only the existing intro link to `approach.md`. No second copy of that page.

- [ ] **Step 5: Commit**

```
git add docs/_games/log-contract.md
git commit -m "docs: add mapping recommendation to the log contract"
```

---

### Task 3: Exploration skill asks with the recommendation

**Files:**
- Modify: `.agents/skills/x-exploration-reviewer/SKILL.md` (version line 6; Questions about a report line 23; Stop when the mapping is missing lines 33–44; The example line 56; Rationalizations table lines 62–67; Validate lines 84–93)
- Modify: `.agents/skills/x-exploration-reviewer/references/methodology.md` (line 1)
- Create: `.agents/skills/x-exploration-reviewer/assets/examples/question.md`
- Do not modify: `.agents/skills/x-exploration-reviewer/assets/examples/report.md`

**Interfaces:**
- Consumes: `docs/_games/log-contract.md` heading `## The recommendation`
- Produces: skill version `1.3.0`, methodology `Explains: v1.3.0`, and `assets/examples/question.md` for the exploration export

- [ ] **Step 1: Check question.md is absent**

Run: `rg -n "area:\*" .agents/skills/x-exploration-reviewer/assets/examples/question.md`

Expected: file not found, or no matches.

- [ ] **Step 2: Write question.md**

Create `.agents/skills/x-exploration-reviewer/assets/examples/question.md` with:

```markdown
# Question when the mapping is missing

This is the question for `export.json` in this folder when no mapping file is supplied. Take the clues from the caller's export. The ids below belong to this export only.

## area:*

- Structure: present in s1 and s3, absent in s2. Points at exploration.
- Word clue: `area` in `area:cave`. Construct: exploration.
- Recommended answer: exploration.
- Choices: this construct, ignore for this run, or not enough information.

## ui:*

- Structure: present in s1 only. Points at exploration.
- Word clue: none.
- Recommended answer: not enough information.
- Choices: this construct, ignore for this run, or not enough information.
```

- [ ] **Step 3: Update the skill**

In `.agents/skills/x-exploration-reviewer/SKILL.md`:

Set `version: '1.3.0'`.

In `## Questions about a report`, add `why a recommendation was not saved as the mapping` to the list of questions that send the reader to `references/methodology.md`.

Replace the Ask paragraph at the end of `## Stop when the mapping is missing` with:

```markdown
Ask which unmapped groups this analysis needs, as `docs/_games/log-contract.md` → The recommendation describes, unless the caller has already refused to answer. Include the recommended answer. It is not a confirmed mapping. Follow `assets/examples/question.md` for the shape. Compute every clue from the caller's export. The ids in that file belong to that export only. A refusal is still a missing confirmation. Report the stop. Do not fill the gap. The report bullets above keep each design id a name pattern. They do not remove the recommended answer from the question.
```

Replace the mapping-missing sentence in `## The example` with:

```markdown
If the mapping is missing, follow `assets/examples/question.md` and [Stop when the mapping is missing](#stop-when-the-mapping-is-missing). Do not imitate `report.md`. If an exploration entry says `context: missing`, report the missing goal or reward and do not score.
```

Add this row to the rationalizations table:

```markdown
| Clues agreeing is not a saved mapping. | The developer still confirms or edits. The recommendation is not the mapping file. |
```

Add this Validate item after the existing missing-mapping item:

```markdown
- [ ] A missing mapping produces the question in `assets/examples/question.md`, and the skill does not score or write a mapping entry from the recommendation.
```

Do not copy the tests or the cue list into this file.

- [ ] **Step 4: Update the methodology**

Set the first line of `references/methodology.md` to `Explains: v1.3.0`.

Append:

```markdown
## Why a recommendation is not a mapping

The recommendation is defined in `docs/_games/log-contract.md` under The recommendation. This skill includes it in the confirmation question. The developer's answer is the mapping. This page does not restate the tests.
```

- [ ] **Step 5: Check**

Run:

```
rg -n "version: '1.3.0'" .agents/skills/x-exploration-reviewer/SKILL.md
rg -n "^Explains: v1.3.0" .agents/skills/x-exploration-reviewer/references/methodology.md
rg -n "Recommended answer: exploration" .agents/skills/x-exploration-reviewer/assets/examples/question.md
rg -n "Recommended answer: not enough information" .agents/skills/x-exploration-reviewer/assets/examples/question.md
rg -n "The cue list|area`, `explore" .agents/skills/x-exploration-reviewer/SKILL.md
```

Expected: version match, Explains match, both recommended-answer lines, and no cue-list copy in `SKILL.md` (last command exit code 1).

- [ ] **Step 6: Commit**

```
git add .agents/skills/x-exploration-reviewer/SKILL.md .agents/skills/x-exploration-reviewer/references/methodology.md .agents/skills/x-exploration-reviewer/assets/examples/question.md
git commit -m "feat(x-exploration-reviewer): recommend a mapping answer"
```

---

### Task 4: Experimentation skill asks with the recommendation

**Files:**
- Modify: `.agents/skills/x-experimentation-reviewer/SKILL.md` (version line 6; Questions about a report line 23; after Prerequisites line 27; The example line 45; Rationalizations table lines 49–53; Validate lines 72–80)
- Modify: `.agents/skills/x-experimentation-reviewer/references/methodology.md` (line 1)
- Create: `.agents/skills/x-experimentation-reviewer/assets/examples/question.md`
- Do not modify: `.agents/skills/x-experimentation-reviewer/assets/examples/report.md`

**Interfaces:**
- Consumes: `docs/_games/log-contract.md` heading `## The recommendation`
- Produces: skill version `1.3.0`, methodology `Explains: v1.3.0`, and `assets/examples/question.md` for the experimentation export

- [ ] **Step 1: Check question.md is absent**

Run: `rg -n "loadout:\*" .agents/skills/x-experimentation-reviewer/assets/examples/question.md`

Expected: file not found, or no matches.

- [ ] **Step 2: Write question.md**

Create `.agents/skills/x-experimentation-reviewer/assets/examples/question.md` with:

```markdown
# Question when the mapping is missing

This is the question for `export.json` in this folder when no mapping file is supplied. Take the clues from the caller's export. The ids below belong to this export only.

## loadout:*

- Structure: in s1, `loadout:sword` on attempt 1 and `loadout:bow` on attempt 2. Points at experimentation.
- Word clue: `loadout` in `loadout:sword`. Construct: experimentation.
- Recommended answer: experimentation.
- Choices: this construct, ignore for this run, or not enough information.
```

- [ ] **Step 3: Update the skill**

In `.agents/skills/x-experimentation-reviewer/SKILL.md`:

Set `version: '1.3.0'`.

In `## Questions about a report`, add `why a recommendation was not saved as the mapping` to the list of questions that send the reader to `references/methodology.md`.

Insert this section after `## Prerequisites` and before `## The score`:

```markdown
## The confirmation question

When the mapping is missing or unconfirmed, ask as `docs/_games/log-contract.md` → The recommendation describes. Include that recommended answer. It is not a confirmed mapping. Follow `assets/examples/question.md` for the shape. Compute every clue from the caller's export. The ids in that file belong to that export only.

A refusal, a deadline, or "do not ask" is still a missing confirmation. The recommendation does not fill it.
```

Replace the mapping-missing sentence in `## The example` with:

```markdown
If the mapping is missing, follow `assets/examples/question.md` and do not imitate `report.md`. Withhold the score. If the export is a single session, do not imitate `report.md` either. Withhold the score.
```

Add this row to the rationalizations table:

```markdown
| Clues agreeing is not a saved mapping. | The developer still confirms or edits. The recommendation is not the mapping file. |
```

Add this Validate item:

```markdown
- [ ] A missing mapping produces the question in `assets/examples/question.md`, and the skill does not score or write a mapping entry from the recommendation.
```

Do not copy the tests or the cue list into this file.

- [ ] **Step 4: Update the methodology**

Set the first line of `references/methodology.md` to `Explains: v1.3.0`.

Append:

```markdown
## Why a recommendation is not a mapping

The recommendation is defined in `docs/_games/log-contract.md` under The recommendation. This skill includes it in the confirmation question. The developer's answer is the mapping. This page does not restate the tests.
```

- [ ] **Step 5: Check**

Run:

```
rg -n "version: '1.3.0'" .agents/skills/x-experimentation-reviewer/SKILL.md
rg -n "^Explains: v1.3.0" .agents/skills/x-experimentation-reviewer/references/methodology.md
rg -n "Recommended answer: experimentation" .agents/skills/x-experimentation-reviewer/assets/examples/question.md
rg -n "The cue list|fight`, `risk" .agents/skills/x-experimentation-reviewer/SKILL.md
```

Expected: version match, Explains match, the recommended-answer line, and no cue-list copy in `SKILL.md` (last command exit code 1).

- [ ] **Step 6: Commit**

```
git add .agents/skills/x-experimentation-reviewer/SKILL.md .agents/skills/x-experimentation-reviewer/references/methodology.md .agents/skills/x-experimentation-reviewer/assets/examples/question.md
git commit -m "feat(x-experimentation-reviewer): recommend a mapping answer"
```

---

### Task 5: Risk-taking skill asks with the recommendation

**Files:**
- Modify: `.agents/skills/x-risk-taking-reviewer/SKILL.md` (version line 6; Questions about a report line 23; after Prerequisites line 29; The example line 47; insert a rationalizations table before `## Reporting`; Validate lines 59–68)
- Modify: `.agents/skills/x-risk-taking-reviewer/references/methodology.md` (line 1)
- Create: `.agents/skills/x-risk-taking-reviewer/assets/examples/question.md`
- Do not modify: `.agents/skills/x-risk-taking-reviewer/assets/examples/report.md`
- Do not modify: `.agents/skills/x-play-style-reviewer/**` or `docs/_games/approach.md`

**Interfaces:**
- Consumes: `docs/_games/log-contract.md` heading `## The recommendation`
- Produces: skill version `1.1.0`, methodology `Explains: v1.1.0`, and `assets/examples/question.md` whose recommended answers are both not enough information

- [ ] **Step 1: Check question.md is absent**

Run: `rg -n "fight:\*" .agents/skills/x-risk-taking-reviewer/assets/examples/question.md`

Expected: file not found, or no matches.

- [ ] **Step 2: Write question.md**

Create `.agents/skills/x-risk-taking-reviewer/assets/examples/question.md` with:

```markdown
# Question when the mapping is missing

This is the question for `export.json` in this folder when no mapping file is supplied. Take the clues from the caller's export. The ids below belong to this export only.

## fight:*

- Structure: `door` in s2 and `fight` in s3 swap across attempts of `world:level1`. Points at experimentation.
- Word clue: `fight` in `fight:boss`. Construct: risk-taking.
- Recommended answer: not enough information.
- Choices: this construct, ignore for this run, or not enough information.

## door:*

- Structure: `door` in s2 and `fight` in s3 swap across attempts of `world:level1`. Points at experimentation.
- Word clue: none.
- Recommended answer: not enough information.
- Choices: this construct, ignore for this run, or not enough information.
```

- [ ] **Step 3: Update the skill**

In `.agents/skills/x-risk-taking-reviewer/SKILL.md`:

Set `version: '1.1.0'`.

In `## Questions about a report`, add `why a recommendation was not saved as the mapping` to the list of questions that send the reader to `references/methodology.md`.

Insert this section after `## Prerequisites` and before `## The score`:

```markdown
## The confirmation question

When the mapping is missing or unconfirmed, ask as `docs/_games/log-contract.md` → The recommendation describes. Include that recommended answer. It is not a confirmed mapping. Follow `assets/examples/question.md` for the shape. Compute every clue from the caller's export. The ids in that file belong to that export only.

A refusal, a deadline, or "do not ask" is still a missing confirmation. The recommendation does not fill it.
```

Replace the mapping-missing sentence in `## The example` with:

```markdown
If the mapping is missing, follow `assets/examples/question.md` and do not imitate `report.md`. Withhold the score. If the safer alternative is not named, or the export is a single session, do not imitate `report.md` either. Withhold the score.
```

Insert this section after `## The example` and before `## Reporting`:

```markdown
## Rationalizations

| Excuse | Reality |
| --- | --- |
| Clues agreeing is not a saved mapping. | The developer still confirms or edits. The recommendation is not the mapping file. |
```

Add this Validate item:

```markdown
- [ ] A missing mapping produces the question in `assets/examples/question.md`, and the skill does not score or write a mapping entry from the recommendation.
```

Do not copy the tests or the cue list into this file. Do not add a structural test that names risk-taking.

- [ ] **Step 4: Update the methodology**

Set the first line of `references/methodology.md` to `Explains: v1.1.0`.

Append:

```markdown
## Why a recommendation is not a mapping

The recommendation is defined in `docs/_games/log-contract.md` under The recommendation. This skill includes it in the confirmation question. The developer's answer is the mapping. This page does not restate the tests.
```

- [ ] **Step 5: Check**

Run:

```
rg -n "version: '1.1.0'" .agents/skills/x-risk-taking-reviewer/SKILL.md
rg -n "^Explains: v1.1.0" .agents/skills/x-risk-taking-reviewer/references/methodology.md
rg -n "Recommended answer: not enough information" .agents/skills/x-risk-taking-reviewer/assets/examples/question.md
rg -n "version: '1.1.0'" .agents/skills/x-play-style-reviewer/SKILL.md
```

Expected: risk-taking version `1.1.0`, Explains `v1.1.0`, two "not enough information" lines in `question.md`, and play style still `1.1.0`.

Run: `git diff -- docs/_games/approach.md .agents/skills/x-play-style-reviewer .agents/skills/x-exploration-reviewer/assets/examples/report.md .agents/skills/x-experimentation-reviewer/assets/examples/report.md .agents/skills/x-risk-taking-reviewer/assets/examples/report.md`

Expected: empty diff.

- [ ] **Step 6: Commit**

```
git add .agents/skills/x-risk-taking-reviewer/SKILL.md .agents/skills/x-risk-taking-reviewer/references/methodology.md .agents/skills/x-risk-taking-reviewer/assets/examples/question.md
git commit -m "feat(x-risk-taking-reviewer): recommend a mapping answer"
```

---

### Review correction

Task 5 inserted `## The confirmation question` after the whole Prerequisites block. That block still said to stop when the risk entry does not name the safer alternative. A missing mapping has no risk entry, so that stop can skip the group question.

The spec’s Review correction governs. The safer-alternative check runs only after the mapping is confirmed. A missing mapping still produces the question in `assets/examples/question.md`. That check has no recommended answer.

`x-risk-taking-reviewer` is `1.2.0`. `references/methodology.md` says `Explains: v1.2.0`.
