# Mapping recommendation

When a construct skill asks the developer to confirm a design-id group, the question includes a recommended answer. The developer still confirms or edits that answer. The recommendation is not a mapping.

The method lives in the log contract. Exploration, experimentation, and risk-taking point at it. Play style does not ask these questions.

## Where it lives

Add `## The recommendation` to `docs/_games/log-contract.md`, after `## The gate`, in that page's existing heading and link style. The section holds the agreement rule, the structural tests, the attempt window, and the cue list.

Gate step 4 keeps the three answers: this construct, ignore for this run, or not enough information. It points at `## The recommendation` for what the question shows and how the recommended answer is chosen. Steps 5 through 7 are unchanged: the summary uses the developer's answers, measurement waits for that confirmation, and the confirmed mapping is saved beside the logs.

The three skills do not copy the tests or the cue list.

Unchanged: `docs/_games/approach.md`, the mapping-file shape, play style, and the later questions for a goal, a reward, or a safer alternative. Those context questions carry no recommended answer.

## The confirmation question

For each design-id group this analysis needs and the mapping does not already cover, the question shows:

- The id pattern.
- One structural observation, and the one construct it points at, or that it points at none.
- The word clue: each matched cue, one id that contained it, and that cue's construct, or that no cue matched.
- The recommended answer.
- The three choices: this construct, ignore for this run, or not enough information.

The developer's answer is what gets saved.

- A recommended construct is written only after the developer confirms it.
- Ignore is written when the developer confirms ignore.
- Not enough information writes nothing for that group. A later run may ask again.

A refusal, a deadline, or "do not ask" is still a missing confirmation. The recommendation does not fill it. Chat text is still not the mapping file.

## Agreement rule

- Both clues point at this skill's construct. Recommend this construct.
- Both clues point at one other construct. Recommend ignore for this run, and name the construct they agreed on.
- Any other case, including one clue, no clue, or a disagreement. Recommend not enough information, and show whichever clues exist.

A structural result that points at none is not a clue for any construct. A risk-taking word cue cannot agree with the structure, because no structural test names risk-taking. That case recommends not enough information.

## Groups and the attempt window

A group is the first colon-separated segment of a design `data.event_id`, written as `segment:*`. An id with no colon is its own group, and the pattern is that full id. Only events whose `data.category` is `design` form groups.

A progression step is the progression `data.event_id` with the status segment removed. `Start:world:level1`, `Fail:world:level1`, and `Complete:world:level1` are the step `world:level1`. Status is `Start`, `Fail`, or `Complete`.

An attempt owns the design events after the previous `Fail` or `Complete` for that user and session, up through this outcome. When there is no previous outcome, it owns the events from the start of the session through this outcome. A `Start` inside that window belongs to the attempt. The window does not depend on `Start` being present. Design events after the last outcome in the session belong to no attempt.

`attempt_num`, when present, distinguishes attempts. When it is absent, the order of outcomes in the session distinguishes them.

Events outside any attempt, and an export with no progression events, give every group no structural clue.

## Structural tests

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

## Cue list

Split each design `event_id` on `:`, `_`, and `-`. Compare each whole token to the list with case ignored. A group has a word clue only when every matched cue belongs to one construct. The question quotes every matched cue and one id that contained it. Cues from two constructs leave no word clue.

| Cue | Construct |
| --- | --- |
| `area`, `explore`, `exploration`, `optional` | exploration |
| `loadout`, `equip`, `experiment` | experimentation |
| `fight`, `risk`, `danger` | risk-taking |

`door`, `ui`, `cave`, `grove`, `room`, `return`, `sword`, `bow`, `staff`, and `boss` are not cues. `door` names a safer alternative. The others are instance words.

## Skill changes

Each construct skill bumps a minor version. The confirmation question points at `docs/_games/log-contract.md` → `## The recommendation`. The skill text does not restate the tests or the cue list.

| Skill | Version |
| --- | --- |
| `x-exploration-reviewer` | 1.2.0 → 1.3.0 |
| `x-experimentation-reviewer` | 1.2.0 → 1.3.0 |
| `x-risk-taking-reviewer` | 1.0.0 → 1.1.0 |

Each `references/methodology.md` updates its `Explains:` line to that version and gains a short section: the recommendation is defined in the log contract, this skill includes it in the question, and the developer's answer is the mapping. The section does not restate the tests.

Each skill gains this rationalization: clues agreeing is not a saved mapping. The developer still confirms or edits. Exploration and experimentation already have a rationalizations table. Risk-taking gains a rationalizations table with this one row.

Each skill's Validate list gains one item: a missing mapping produces the question in `assets/examples/question.md`, and the skill does not score or write a mapping entry from the recommendation.

`x-play-style-reviewer` stays at 1.1.0.

## Worked checks

`assets/examples/report.md` stays the reading after a mapping is confirmed. Each construct skill gains `assets/examples/question.md`: the question for that skill's `export.json` when no mapping is supplied. When the mapping is missing, the skill asks in that shape and takes the clues from the caller's export. The ids in `question.md` belong to that export only.

| Export | Group | Structure | Word clue | Recommended answer |
| --- | --- | --- | --- | --- |
| Exploration | `area:*` | Present in s1 and s3, absent in s2. Points at exploration. | `area` in `area:cave` | exploration |
| Exploration | `ui:*` | Present in s1 only. Points at exploration. | none | not enough information |
| Experimentation | `loadout:*` | In s1, `loadout:sword` on attempt 1 and `loadout:bow` on attempt 2. Points at experimentation. | `loadout` | experimentation |
| Risk-taking | `fight:*` | `door` in s2 and `fight` in s3 swap across attempts of `world:level1`. Points at experimentation. | `fight` in `fight:boss`, risk-taking | not enough information |
| Risk-taking | `door:*` | Same swap. Points at experimentation. | none | not enough information |

The ignore-for-another-construct case has no fixture. The agreement rule is the check.

## Review correction

The safer-alternative check runs only after the mapping is confirmed. A missing mapping still produces the group question. That check carries no recommended answer. The same timing applies to a goal or a reward.

`x-risk-taking-reviewer` is `1.2.0` for this correction. `references/methodology.md` says `Explains: v1.2.0`. The `1.1.0` row above is the recommendation change. This correction follows it.

## Files

- `docs/_games/log-contract.md`
- `.agents/skills/x-exploration-reviewer/SKILL.md`
- `.agents/skills/x-exploration-reviewer/references/methodology.md`
- `.agents/skills/x-exploration-reviewer/assets/examples/question.md`
- `.agents/skills/x-experimentation-reviewer/SKILL.md`
- `.agents/skills/x-experimentation-reviewer/references/methodology.md`
- `.agents/skills/x-experimentation-reviewer/assets/examples/question.md`
- `.agents/skills/x-risk-taking-reviewer/SKILL.md`
- `.agents/skills/x-risk-taking-reviewer/references/methodology.md`
- `.agents/skills/x-risk-taking-reviewer/assets/examples/question.md`
- `CODEOWNERS` — an owner line for `/docs/superpowers/`. The handle matched from `git config user.name` is `@Vida`.
