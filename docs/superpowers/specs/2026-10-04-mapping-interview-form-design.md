# Mapping interview form

A missing mapping is one question form. Every design-id group the mapping does not already cover is a question on that form. Each question offers three choices the developer selects. One of them is marked recommended. The developer confirms every group. The recommendation is not a mapping.

This replaces the confirmation question, the agreement rule, the one-group-per-reply paragraph, and the recommended answers for `ui:*` and `door:*` in `2026-10-04-mapping-recommendation-design.md`. The structural tests, the attempt window, and the cue list in that spec still hold. The log contract remains the method. The three construct skills point at it and do not copy the tests or the cue list.

## The form

The reply is one question form. It waits once. It does not ask one group and then another group on a later turn. It does not list recommendations and stop.

A construct review needs every design-id group the mapping does not already cover. Ignore is one of the answers, so a group is not left off the form because its clues point elsewhere or because it has no clue.

Each question shows:

- The id pattern.
- One structural observation, and the one construct it points at, or that it points at none.
- The word clue: each matched cue, one id that contained it, and that cue's construct, or that no cue matched.
- The recommended choice, listed first and labeled recommended.

The developer selects one option. The recommended option is first. The other two follow in this order, skipping the one already placed first: this construct, ignore for this run, not enough information.

- This construct. The skill names it: `exploration`, `experimentation`, or `risk-taking`.
- Ignore for this run. When the clues point at a different construct, the option names that construct.
- Not enough information.

Writing those three choices as a sentence is not the form. When the session has no question form, the same reply still lists every uncovered group, each with those three options, and waits once.

After the developer answers the form, the agent shows the short summary from gate step 5 and waits. Measurement and saving wait for the developer to confirm or edit that summary.

The confirmed summary is what gets saved. An edit on that summary replaces the form selection.

- A construct in the confirmed summary is written.
- Ignore in the confirmed summary is written.
- Not enough information writes nothing for that group. A later run may ask again.

A refusal, a deadline, or "do not ask" is still a missing confirmation. The recommendation does not fill it. Chat text is still not the mapping file.

Goal, reward, and safer alternative stay a later question, after a group is assigned to a construct that needs them. Those questions have no recommended answer.

## One clue is enough

A clue is a structural result that points at one construct, or a word clue that names one construct. A structural result that points at none is not a clue. No matched cue is not a clue.

- One clue, or two clues that name the same construct, recommends that construct. When it is this skill's construct, the recommended option is this construct. When it is another construct, the recommended option is ignore for this run, and the option names that construct.
- Two clues that name different constructs recommend not enough information. The question shows both clues.
- No clue recommends not enough information.

No structural test names risk-taking. A risk-taking word cue is still a clue. On its own, it recommends risk-taking for the risk-taking skill. It recommends ignore, naming risk-taking, for another skill. When the structure points at a different construct, the two clues disagree, and the recommendation is not enough information. A word cue with no structural clue has no example file. The rule in this section is the check.

## Skill changes

Each construct skill bumps a minor version. The confirmation question points at `docs/_games/log-contract.md` → `## The recommendation`. The skill text does not restate the tests or the cue list.

| Skill | Version |
| --- | --- |
| `x-exploration-reviewer` | 1.4.0 → 1.5.0 |
| `x-experimentation-reviewer` | 1.4.0 → 1.5.0 |
| `x-risk-taking-reviewer` | 1.3.0 → 1.4.0 |

Each `references/methodology.md` updates its `Explains:` line to that version. It explains why every uncovered group is on one form, and why one clue is enough to recommend a construct. It does not restate the tests or the cue list.

Each skill replaces the rationalization that ends the turn on one unanswered question. The replacement: every uncovered group is on the one form, and a list of recommendations is not that form.

Each skill's Validate list requires a missing mapping to ask every uncovered group on that one form, with the recommended choice first, and forbids scoring or writing a mapping entry from the recommendation.

`x-play-style-reviewer` stays at 1.1.0. `docs/_games/approach.md` and the mapping-file shape stay as they are.

## Worked checks

`assets/examples/question.md` is the form for that skill's `export.json` when no mapping is supplied. Every group in the file is on that one form. The ids belong to that export only. The caller's export supplies the clues on a real run.

| Export | Group | Structure | Word clue | Recommended option |
| --- | --- | --- | --- | --- |
| Exploration | `area:*` | Present in s1 and s3, absent in s2. Points at exploration. | `area` in `area:cave` | exploration |
| Exploration | `ui:*` | Present in s1 only. Points at exploration. | none | exploration |
| Experimentation | `loadout:*` | In s1, `loadout:sword` on attempt 1 and `loadout:bow` on attempt 2. Points at experimentation. | `loadout` | experimentation |
| Risk-taking | `fight:*` | `door` in s2 and `fight` in s3 swap across attempts of `world:level1`. Points at experimentation. | `fight` in `fight:boss`, risk-taking | not enough information |
| Risk-taking | `door:*` | Same swap. Points at experimentation. | none | ignore for this run — experimentation |

`ui:*` changed because one structural clue is enough. `door:*` changed for the same reason: the clue names experimentation, so a risk-taking question recommends ignore and names experimentation. `fight:*` stays not enough information because the two clues name different constructs.

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
