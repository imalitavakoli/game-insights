# Mapping Interview Form Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** A missing mapping asks every uncovered design-id group on one question form, each with a selectable recommended choice, and one clue is enough to recommend a construct.

**Architecture:** `docs/_games/log-contract.md` → `## The recommendation` changes the interview from one group per reply to one form, and changes the agreement rule so one clue recommends that construct. Exploration, experimentation, and risk-taking point at that heading. Each `assets/examples/question.md` shows every group from that skill's export on one form. Play style does not ask these questions.

**Tech Stack:** Markdown skills and the log contract. No new packages. The shell is PowerShell. `rg` may be absent; checks use `Select-String`.

## Global Constraints

- The recommendation is not a mapping. The confirmed summary is what gets saved. An edit on that summary replaces the form selection.
- The reply is one question form. Every design-id group the mapping does not already cover is a question on that form. The reply waits once. It does not ask one group and then another group on a later turn. It does not list recommendations and stop.
- A construct review needs every design-id group the mapping does not already cover. Ignore is one of the answers, so a group is not left off the form because its clues point elsewhere or because it has no clue.
- The developer selects one option. The recommended option is first and labeled recommended. The other two follow in this order, skipping the one already placed first: this construct, ignore for this run, not enough information.
- Writing those three choices as a sentence is not the form. When the session has no question form, the same reply still lists every uncovered group, each with those three options, and waits once.
- One clue, or two clues that name the same construct, recommends that construct. Two clues that name different constructs recommend not enough information. No clue recommends not enough information.
- A structural result that points at none is not a clue. No matched cue is not a clue. No structural test names risk-taking. A risk-taking word cue is still a clue.
- Not enough information writes nothing for that group.
- A refusal, a deadline, or "do not ask" is still a missing confirmation. The recommendation does not fill it. Chat text is still not the mapping file.
- The three skills do not copy the tests or the cue list. Do not invent an example file for a word cue with no structural clue.
- Goal, reward, and safer alternative stay a later question, after a group is assigned. Those questions have no recommended answer. Do not move the risk-taking safer-alternative check back into Prerequisites.
- `docs/_games/approach.md` stays unchanged. The mapping-file shape stays unchanged. `assets/examples/report.md` stays unchanged. `x-play-style-reviewer` stays at 1.1.0. Do not edit it.
- Versions: `x-exploration-reviewer` 1.4.0 → 1.5.0, `x-experimentation-reviewer` 1.4.0 → 1.5.0, `x-risk-taking-reviewer` 1.3.0 → 1.4.0. Each `references/methodology.md` `Explains:` line matches that version.
- Commits use `type(scope): summary` (imperative, lowercase, no trailing period). Do not create a branch. Do not invent a TRACKER-ID. Do not stage `fixtures/`.
- Do not edit the `.claude/skills/` pointer stubs. Their `description` fields do not change.
- Before editing a skill, read `.agents/skills/x-skill-build-helper/SKILL.md`.

---

### Task 1: Record the spec and this plan

**Files:**
- Already on disk, do not rewrite: `docs/superpowers/specs/2026-10-04-mapping-interview-form-design.md`
- Already on disk, do not rewrite: `docs/superpowers/specs/2026-10-04-mapping-recommendation-design.md`
- Already on disk, do not rewrite: `docs/superpowers/plans/2026-10-04-mapping-interview-form.md`

**Interfaces:**
- Consumes: the approved spec
- Produces: a commit those three docs can be cited from. Later tasks edit the log contract and the skills, not these three files.

- [ ] **Step 1: Confirm the spec is the form spec**

Run:

```
Select-String -Path docs/superpowers/specs/2026-10-04-mapping-interview-form-design.md -Pattern "one question form"
```

Expected: at least one match.

- [ ] **Step 2: Commit the spec, the supersession note, and this plan**

Do not edit the three files in this step. Do not stage `fixtures/`.

```
git add docs/superpowers/specs/2026-10-04-mapping-interview-form-design.md docs/superpowers/specs/2026-10-04-mapping-recommendation-design.md docs/superpowers/plans/2026-10-04-mapping-interview-form.md
git commit -m "docs: specify the mapping interview form"
```

Expected: one commit, those three paths only.

---

### Task 2: One form and one clue in the log contract

**Files:**
- Modify: `docs/_games/log-contract.md` (gate step 4, and `## The recommendation` through the end of `### The agreement rule`)
- Do not modify: `### Groups and the attempt window`, `### Structural tests`, `### The cue list`

**Interfaces:**
- Consumes: the agreement rule and the form from the spec
- Produces: heading `## The recommendation` whose interview is one form, and `### The agreement rule` whose one-clue rule the three skills point at

- [ ] **Step 1: Confirm the current interview is one group per reply**

Run:

```
Select-String -Path docs/_games/log-contract.md -Pattern "one design-id group per reply"
```

Expected: one match. If it is already absent, stop and report that. Do not apply the replacement twice.

- [ ] **Step 2: Replace gate step 4**

Replace this line:

```
4. Ask only about groups the mapping does not already cover and that the requested analysis needs. Each answer is one of: this construct, ignore for this run, or not enough information. What the question shows, and how the recommended answer is chosen, is [The recommendation](#the-recommendation).
```

with:

```
4. Ask about every design-id group the mapping does not already cover. A construct review needs all of them. Each answer is one of: this construct, ignore for this run, or not enough information. What the question shows, and how the recommended answer is chosen, is [The recommendation](#the-recommendation).
```

- [ ] **Step 3: Replace the interview and the agreement rule**

Replace the block from `## The recommendation` through the paragraph that ends `That case recommends not enough information.` (stop before `### Groups and the attempt window`) with:

```markdown
## The recommendation

Gate step 4 is one question form. Every design-id group the mapping does not already cover is a question on that form. A construct review needs all of them. Ignore is one of the answers, so a group stays on the form when its clues point elsewhere or when it has no clue. The reply waits once. It does not ask one group and then another group on a later turn. It does not list recommendations and stop.

Each question shows:

- The id pattern.
- One structural observation, and the one construct it points at, or that it points at none.
- The word clue: each matched cue, one id that contained it, and that cue's construct, or that no cue matched.
- The recommended choice, listed first and labeled recommended.

The developer selects one option. The recommended option is first. The other two follow in this order, skipping the one already placed first: this construct, ignore for this run, not enough information.

- This construct. The skill names it.
- Ignore for this run. When the clues point at a different construct, the option names that construct.
- Not enough information.

Writing those three choices as a sentence is not the form. When the session has no question form, the same reply still lists every uncovered group, each with those three options, and waits once.

After the developer answers the form, show the short summary in gate step 5 and wait. The confirmed summary is what gets saved. An edit on that summary replaces the form selection. A construct in the confirmed summary is written. Ignore in the confirmed summary is written. Not enough information writes nothing for that group, so a later run may ask again.

A refusal, a deadline, or "do not ask" is still a missing confirmation. The recommendation does not fill it. Chat text is still not the mapping file.

### The agreement rule

A clue is a structural result that points at one construct, or a word clue that names one construct. A structural result that points at none is not a clue. No matched cue is not a clue.

- One clue, or two clues that name the same construct, recommends that construct. When it is this skill's construct, the recommended option is this construct. When it is another construct, the recommended option is ignore for this run, and the option names that construct.
- Two clues that name different constructs recommend not enough information. The question shows both clues.
- No clue recommends not enough information.

No structural test names risk-taking. A risk-taking word cue is still a clue. On its own, it recommends risk-taking for the risk-taking skill. It recommends ignore, naming risk-taking, for another skill. When the structure points at a different construct, the two clues disagree, and the recommendation is not enough information.
```

Leave a blank line, then the existing `### Groups and the attempt window`.

- [ ] **Step 4: Check the contract**

Run:

```
Select-String -Path docs/_games/log-contract.md -Pattern "one design-id group per reply"
Select-String -Path docs/_games/log-contract.md -Pattern "One clue, or two clues"
Select-String -Path docs/_games/log-contract.md -Pattern "one question form"
Select-String -Path docs/_games/log-contract.md -Pattern "\| ``area``"
```

Expected: no match for `one design-id group per reply`. One match for `One clue, or two clues`. One match for `one question form` in `## The recommendation`. The cue table still contains `` `area` ``. `### Structural tests` is still present.

- [ ] **Step 5: Commit**

```
git add docs/_games/log-contract.md
git commit -m "docs: ask every mapping group on one form"
```

Expected: one commit, `docs/_games/log-contract.md` only.

---

### Task 3: Exploration skill asks on one form

**Files:**
- Modify: `.agents/skills/x-exploration-reviewer/SKILL.md`
- Modify: `.agents/skills/x-exploration-reviewer/references/methodology.md`
- Modify: `.agents/skills/x-exploration-reviewer/assets/examples/question.md`

**Interfaces:**
- Consumes: `docs/_games/log-contract.md` → `## The recommendation`
- Produces: version `1.5.0`, `Explains: v1.5.0`, and a question file whose `ui:*` recommended option is exploration

- [ ] **Step 1: Read the skill helper**

Read `.agents/skills/x-skill-build-helper/SKILL.md` before editing. The version change is a minor bump from the committed `1.4.0` to `1.5.0`. Do not change `description`.

- [ ] **Step 2: Set the version**

In `.agents/skills/x-exploration-reviewer/SKILL.md` frontmatter, replace `version: '1.4.0'` with `version: '1.5.0'`.

- [ ] **Step 3: Replace the stop-section interview**

Replace:

```
The reply is one interview question for one unmapped group. It ends by asking the developer to choose. Include the recommended answer. Wait. A list of recommendations is not the interview.
```

with:

```
The reply is one question form for every unmapped group. The developer selects one option on each question. The recommended option is first. Wait once. A list of recommendations is not the form.
```

Replace:

```
Ask one unmapped group, as `docs/_games/log-contract.md` → The recommendation describes, unless the caller has already refused to answer. The reply ends on that question. Include the recommended answer. It is not a confirmed mapping. Follow the "Ask this first" block in `assets/examples/question.md`. Compute every clue from the caller's export. The ids in that file belong to that export only. After the developer answers, ask the next group. A refusal is still a missing confirmation. Do not fill the gap. The report bullets above keep each design id a name pattern. They do not remove the question.
```

with:

```
Ask as `docs/_games/log-contract.md` → The recommendation describes, unless the caller has already refused to answer. Every uncovered group is on that one form. The recommended option is first. It is not a confirmed mapping. Follow `assets/examples/question.md`. Compute every clue from the caller's export. The ids in that file belong to that export only. A refusal is still a missing confirmation. Do not fill the gap. The report bullets above keep each design id a name pattern. They do not remove the form.
```

Replace:

```
If the mapping is missing, follow the "Ask this first" block in `assets/examples/question.md` and [Stop when the mapping is missing](#stop-when-the-mapping-is-missing). Do not imitate `report.md`. The reply ends on that one question. If an exploration entry says `context: missing`, report the missing goal or reward and do not score.
```

with:

```
If the mapping is missing, follow `assets/examples/question.md` and [Stop when the mapping is missing](#stop-when-the-mapping-is-missing). Do not imitate `report.md`. Every uncovered group is on that one form. If an exploration entry says `context: missing`, report the missing goal or reward and do not score.
```

Replace the rationalization row:

```
| The recommendations were shown, so the turn can end. | The reply ends on one unanswered question. Wait for the developer. |
```

with:

```
| The recommendations were shown, so the turn can end. | Every uncovered group is on the one form. A list of recommendations is not that form. |
```

Replace the red flag:

```
- You are about to end the turn after listing recommendations, without asking the developer to choose for one group.
```

with:

```
- You are about to end the turn after listing recommendations, without a question form the developer can answer for every uncovered group.
```

Replace the validate item:

```
- [ ] A missing mapping ends the reply on one unanswered question for one group, including the recommended answer. The other groups wait until the developer answers.
```

with:

```
- [ ] A missing mapping asks every uncovered group on one form, with the recommended choice first. It does not leave the other groups for a later turn.
```

- [ ] **Step 4: Replace the question example**

Write `.agents/skills/x-exploration-reviewer/assets/examples/question.md` as:

```markdown
# Question form when the mapping is missing

One form. Every group below is a question on it. The developer selects one option per group. The first option is recommended. Take the clues from the caller's export. The ids below belong to `export.json` in this folder.

## area:*

- Structure: present in s1 and s3, absent in s2. Points at exploration.
- Word clue: `area` in `area:cave`. Construct: exploration.
- Options:
  1. exploration (recommended)
  2. ignore for this run
  3. not enough information

## ui:*

- Structure: present in s1 only. Points at exploration.
- Word clue: none.
- Options:
  1. exploration (recommended)
  2. ignore for this run
  3. not enough information
```

- [ ] **Step 5: Update the methodology**

In `.agents/skills/x-exploration-reviewer/references/methodology.md`, replace `Explains: v1.4.0` with `Explains: v1.5.0`.

Replace the section `## Why the reply ends on one question` and its two sentences with:

```markdown
## Why every group is on one form

A list of recommendations is not the interview. This skill asks every unmapped group on one form. Each question has three options the developer selects. The recommended option is first. The reply waits once.

## Why one clue is enough

One clue, or two clues that name the same construct, recommends that construct. Two clues that name different constructs, or no clue, recommends not enough information. The tests and the cue list stay in the log contract.
```

- [ ] **Step 6: Check the skill**

Run:

```
Select-String -Path .agents/skills/x-exploration-reviewer/SKILL.md -Pattern "version: '1.5.0'"
Select-String -Path .agents/skills/x-exploration-reviewer/references/methodology.md -Pattern "Explains: v1.5.0"
Select-String -Path .agents/skills/x-exploration-reviewer/assets/examples/question.md -Pattern "Ask this first"
Select-String -Path .agents/skills/x-exploration-reviewer/assets/examples/question.md -Pattern "exploration \(recommended\)"
Select-String -Path .agents/skills/x-exploration-reviewer/SKILL.md -Pattern "one unanswered question"
```

Expected: version and Explains match. `Ask this first` is absent. `exploration (recommended)` matches twice (`area:*` and `ui:*`). `one unanswered question` is absent from the skill.

- [ ] **Step 7: Commit**

```
git add .agents/skills/x-exploration-reviewer/SKILL.md .agents/skills/x-exploration-reviewer/references/methodology.md .agents/skills/x-exploration-reviewer/assets/examples/question.md
git commit -m "feat(x-exploration-reviewer): ask mapping groups on one form"
```

Expected: one commit, those three paths only.

---

### Task 4: Experimentation skill asks on one form

**Files:**
- Modify: `.agents/skills/x-experimentation-reviewer/SKILL.md`
- Modify: `.agents/skills/x-experimentation-reviewer/references/methodology.md`
- Modify: `.agents/skills/x-experimentation-reviewer/assets/examples/question.md`

**Interfaces:**
- Consumes: `docs/_games/log-contract.md` → `## The recommendation`
- Produces: version `1.5.0`, `Explains: v1.5.0`, and a question file whose only group is `loadout:*` with experimentation recommended first

- [ ] **Step 1: Read the skill helper**

Read `.agents/skills/x-skill-build-helper/SKILL.md` before editing. The version change is a minor bump from the committed `1.4.0` to `1.5.0`. Do not change `description`.

- [ ] **Step 2: Set the version**

In `.agents/skills/x-experimentation-reviewer/SKILL.md` frontmatter, replace `version: '1.4.0'` with `version: '1.5.0'`.

- [ ] **Step 3: Replace the confirmation question**

Replace:

```
The reply is one interview question for one unmapped group. It ends by asking the developer to choose. Include the recommended answer. It is not a confirmed mapping. Wait. A list of recommendations is not the interview.
```

with:

```
The reply is one question form for every unmapped group. The developer selects one option on each question. The recommended option is first. It is not a confirmed mapping. Wait once. A list of recommendations is not the form.
```

Replace:

```
Ask as `docs/_games/log-contract.md` → The recommendation describes, unless the caller has already refused to answer. Follow the "Ask this first" block in `assets/examples/question.md`. Compute every clue from the caller's export. The ids in that file belong to that export only. After the developer answers, ask the next group.
```

with:

```
Ask as `docs/_games/log-contract.md` → The recommendation describes, unless the caller has already refused to answer. Every uncovered group is on that one form. The recommended option is first. Follow `assets/examples/question.md`. Compute every clue from the caller's export. The ids in that file belong to that export only.
```

Replace:

```
If the mapping is missing, follow the "Ask this first" block in `assets/examples/question.md` and do not imitate `report.md`. Withhold the score. The reply ends on that one question. If the export is a single session, do not imitate `report.md` either. Withhold the score.
```

with:

```
If the mapping is missing, follow `assets/examples/question.md` and do not imitate `report.md`. Withhold the score. Every uncovered group is on that one form. If the export is a single session, do not imitate `report.md` either. Withhold the score.
```

Replace the rationalization row:

```
| The recommendations were shown, so the turn can end. | The reply ends on one unanswered question. Wait for the developer. |
```

with:

```
| The recommendations were shown, so the turn can end. | Every uncovered group is on the one form. A list of recommendations is not that form. |
```

Replace the red flag:

```
- You are about to end the turn after listing recommendations, without asking the developer to choose for one group.
```

with:

```
- You are about to end the turn after listing recommendations, without a question form the developer can answer for every uncovered group.
```

Replace the validate item:

```
- [ ] A missing mapping ends the reply on one unanswered question for one group, including the recommended answer. The other groups wait until the developer answers.
```

with:

```
- [ ] A missing mapping asks every uncovered group on one form, with the recommended choice first. It does not leave the other groups for a later turn.
```

- [ ] **Step 4: Replace the question example**

Write `.agents/skills/x-experimentation-reviewer/assets/examples/question.md` as:

```markdown
# Question form when the mapping is missing

One form. Every group below is a question on it. The developer selects one option per group. The first option is recommended. Take the clues from the caller's export. The ids below belong to `export.json` in this folder.

## loadout:*

- Structure: in s1, `loadout:sword` on attempt 1 and `loadout:bow` on attempt 2. Points at experimentation.
- Word clue: `loadout` in `loadout:sword`. Construct: experimentation.
- Options:
  1. experimentation (recommended)
  2. ignore for this run
  3. not enough information
```

- [ ] **Step 5: Update the methodology**

In `.agents/skills/x-experimentation-reviewer/references/methodology.md`, replace `Explains: v1.4.0` with `Explains: v1.5.0`.

Replace the section `## Why the reply ends on one question` and its two sentences with:

```markdown
## Why every group is on one form

A list of recommendations is not the interview. This skill asks every unmapped group on one form. Each question has three options the developer selects. The recommended option is first. The reply waits once.

## Why one clue is enough

One clue, or two clues that name the same construct, recommends that construct. Two clues that name different constructs, or no clue, recommends not enough information. The tests and the cue list stay in the log contract.
```

- [ ] **Step 6: Check the skill**

Run:

```
Select-String -Path .agents/skills/x-experimentation-reviewer/SKILL.md -Pattern "version: '1.5.0'"
Select-String -Path .agents/skills/x-experimentation-reviewer/references/methodology.md -Pattern "Explains: v1.5.0"
Select-String -Path .agents/skills/x-experimentation-reviewer/assets/examples/question.md -Pattern "Ask this first"
Select-String -Path .agents/skills/x-experimentation-reviewer/assets/examples/question.md -Pattern "experimentation \(recommended\)"
Select-String -Path .agents/skills/x-experimentation-reviewer/SKILL.md -Pattern "one unanswered question"
```

Expected: version and Explains match. `Ask this first` is absent. `experimentation (recommended)` matches once. `one unanswered question` is absent from the skill.

- [ ] **Step 7: Commit**

```
git add .agents/skills/x-experimentation-reviewer/SKILL.md .agents/skills/x-experimentation-reviewer/references/methodology.md .agents/skills/x-experimentation-reviewer/assets/examples/question.md
git commit -m "feat(x-experimentation-reviewer): ask mapping groups on one form"
```

Expected: one commit, those three paths only.

---

### Task 5: Risk-taking skill asks on one form

**Files:**
- Modify: `.agents/skills/x-risk-taking-reviewer/SKILL.md`
- Modify: `.agents/skills/x-risk-taking-reviewer/references/methodology.md`
- Modify: `.agents/skills/x-risk-taking-reviewer/assets/examples/question.md`

**Interfaces:**
- Consumes: `docs/_games/log-contract.md` → `## The recommendation`
- Produces: version `1.4.0`, `Explains: v1.4.0`, `fight:*` recommending not enough information, and `door:*` recommending ignore for this run — experimentation

- [ ] **Step 1: Read the skill helper**

Read `.agents/skills/x-skill-build-helper/SKILL.md` before editing. The version change is a minor bump from the committed `1.3.0` to `1.4.0`. Do not change `description`. Leave `## After confirmation` where it is. The safer-alternative check stays after a confirmed mapping.

- [ ] **Step 2: Set the version**

In `.agents/skills/x-risk-taking-reviewer/SKILL.md` frontmatter, replace `version: '1.3.0'` with `version: '1.4.0'`.

- [ ] **Step 3: Replace the confirmation question**

Replace:

```
The reply is one interview question for one unmapped group. It ends by asking the developer to choose. Include the recommended answer. It is not a confirmed mapping. Wait. A list of recommendations is not the interview.
```

with:

```
The reply is one question form for every unmapped group. The developer selects one option on each question. The recommended option is first. It is not a confirmed mapping. Wait once. A list of recommendations is not the form.
```

Replace:

```
Ask as `docs/_games/log-contract.md` → The recommendation describes, unless the caller has already refused to answer. Follow the "Ask this first" block in `assets/examples/question.md`. Compute every clue from the caller's export. The ids in that file belong to that export only. After the developer answers, ask the next group.
```

with:

```
Ask as `docs/_games/log-contract.md` → The recommendation describes, unless the caller has already refused to answer. Every uncovered group is on that one form. The recommended option is first. Follow `assets/examples/question.md`. Compute every clue from the caller's export. The ids in that file belong to that export only.
```

Replace:

```
If the mapping is missing, follow the "Ask this first" block in `assets/examples/question.md` and do not imitate `report.md`. Withhold the score. The reply ends on that one question. If the safer alternative is not named, or the export is a single session, do not imitate `report.md` either. Withhold the score.
```

with:

```
If the mapping is missing, follow `assets/examples/question.md` and do not imitate `report.md`. Withhold the score. Every uncovered group is on that one form. If the safer alternative is not named, or the export is a single session, do not imitate `report.md` either. Withhold the score.
```

Replace the rationalization row:

```
| The recommendations were shown, so the turn can end. | The reply ends on one unanswered question. Wait for the developer. |
```

with:

```
| The recommendations were shown, so the turn can end. | Every uncovered group is on the one form. A list of recommendations is not that form. |
```

Replace the validate item:

```
- [ ] A missing mapping ends the reply on one unanswered question for one group, including the recommended answer. The other groups wait until the developer answers.
```

with:

```
- [ ] A missing mapping asks every uncovered group on one form, with the recommended choice first. It does not leave the other groups for a later turn.
```

This skill has no Red flags section. Do not add one.

- [ ] **Step 4: Replace the question example**

Write `.agents/skills/x-risk-taking-reviewer/assets/examples/question.md` as:

```markdown
# Question form when the mapping is missing

One form. Every group below is a question on it. The developer selects one option per group. The first option is recommended. Take the clues from the caller's export. The ids below belong to `export.json` in this folder.

## fight:*

- Structure: `door` in s2 and `fight` in s3 swap across attempts of `world:level1`. Points at experimentation.
- Word clue: `fight` in `fight:boss`. Construct: risk-taking.
- Options:
  1. not enough information (recommended)
  2. risk-taking
  3. ignore for this run — experimentation

## door:*

- Structure: `door` in s2 and `fight` in s3 swap across attempts of `world:level1`. Points at experimentation.
- Word clue: none.
- Options:
  1. ignore for this run — experimentation (recommended)
  2. risk-taking
  3. not enough information
```

- [ ] **Step 5: Update the methodology**

In `.agents/skills/x-risk-taking-reviewer/references/methodology.md`, replace `Explains: v1.3.0` with `Explains: v1.4.0`.

Leave `## Why a missing mapping still asks` in place.

Replace the section `## Why the reply ends on one question` and its two sentences with:

```markdown
## Why every group is on one form

A list of recommendations is not the interview. This skill asks every unmapped group on one form. Each question has three options the developer selects. The recommended option is first. The reply waits once.

## Why one clue is enough

One clue, or two clues that name the same construct, recommends that construct. Two clues that name different constructs, or no clue, recommends not enough information. The tests and the cue list stay in the log contract.
```

- [ ] **Step 6: Check the skill**

Run:

```
Select-String -Path .agents/skills/x-risk-taking-reviewer/SKILL.md -Pattern "version: '1.4.0'"
Select-String -Path .agents/skills/x-risk-taking-reviewer/references/methodology.md -Pattern "Explains: v1.4.0"
Select-String -Path .agents/skills/x-risk-taking-reviewer/assets/examples/question.md -Pattern "Ask this first"
Select-String -Path .agents/skills/x-risk-taking-reviewer/assets/examples/question.md -Pattern "not enough information \(recommended\)"
Select-String -Path .agents/skills/x-risk-taking-reviewer/assets/examples/question.md -Pattern "ignore for this run — experimentation \(recommended\)"
Select-String -Path .agents/skills/x-risk-taking-reviewer/SKILL.md -Pattern "one unanswered question"
Select-String -Path .agents/skills/x-risk-taking-reviewer/SKILL.md -Pattern "## After confirmation"
```

Expected: version and Explains match. `Ask this first` is absent. `fight:*` recommends not enough information. `door:*` recommends ignore for this run — experimentation. `one unanswered question` is absent. `## After confirmation` is still present, and it still sits after the confirmation question.

- [ ] **Step 7: Commit**

```
git add .agents/skills/x-risk-taking-reviewer/SKILL.md .agents/skills/x-risk-taking-reviewer/references/methodology.md .agents/skills/x-risk-taking-reviewer/assets/examples/question.md
git commit -m "feat(x-risk-taking-reviewer): ask mapping groups on one form"
```

Expected: one commit, those three paths only.
