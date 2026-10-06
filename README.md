# game-insights

Skills that help an AI agent turn gameplay telemetry into a reading a designer can check.

Two audiences: a [game studio](#game-studio) getting a reading, and a [contributor](#contributor) changing this repo.

## Game Studio

You do not install this repo's packages. The game skills are the files under `.agents/skills/`.

1. Install the agent you use, if it is not installed yet. Claude, Cursor, Codex, and other agents that read skills from an open folder.
2. Clone the repository.
3. Open this folder as that agent's workspace, and start a conversation.

### Get a reading

1. Bring a GameAnalytics export: Each event inside that file is its own JSON object. Our [log contract](docs/_games/log-contract.md) is the shape.
2. A mapping is a file that says what each design event means. Confirm the mapping once, and save that file beside the export. The agent asks only about design event ids. You say which ids are exploration, risk-taking, or experimentation, or that they should be ignored.
3. Ask for exploration, risk-taking, and experimentation in any order. Each one reads the same export and the same mapping.
4. Ask for play style only after those three readings exist. Give it the three readings and the same export.

| Ask for         | The mapping must already say                               | You get a score when                                                                                                                      |
| --------------- | ---------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| Exploration     | which ids are optional or off-path, and the goal or reward | that goal or reward is in the sessions. If it is absent, the report says so and does not score                                            |
| Risk-taking     | which id is the harder option, and the safer alternative   | more than one session shows the safer alternative. A failure is not the score                                                             |
| Experimentation | which ids can change between attempts                      | there is more than one session. A later win is not the score                                                                              |
| Play style      | nothing further. It does not re-read design events         | all three readings are in hand. It keeps them side by side with progression and resource counts, and it does not produce one style number |

If one of those three readings is missing, play style stops.

You receive the counts, the order of events, a separate confidence, and a note a designer can check. Exploration, risk-taking, and experimentation each report how often the mapped behavior showed up. A higher count means it showed up in more sessions. The designer compares that count to the behavior they built the game for. In the exploration example below, 2 of 3 sessions visit an optional place. A designer who built those places for players to find reads 2 of 3 as players reaching them. A designer who built them as rare detours reads the same 2 of 3 as the main path losing people. Play style has no score of its own. It sets those three counts beside progression and resource. A thin trace leaves the count out. The reading describes what these sessions did. Each example below is synthetic. A real export is read the same way.

### Game analysis

#### [Exploration](.agents/skills/x-exploration-reviewer/SKILL.md)

**Purpose.** Show a designer whether players visit optional places while a goal is available.

**Measures.** Optional-area events, and how many sessions contain them, under that goal.

**Example.** Three sessions all finish the level. Two of them also visit a cave or a grove. Score: 3 optional-area events in 2 of 3 sessions. The session that only finishes the level stays in the count.

[Full report](.agents/skills/x-exploration-reviewer/assets/examples/report.md) · [Methodology](.agents/skills/x-exploration-reviewer/references/methodology.md)

#### [Risk-taking](.agents/skills/x-risk-taking-reviewer/SKILL.md)

**Purpose.** Show a designer when players pick the harder option while a safer one is also there.

**Measures.** Sessions that contain both. The later win or failure stays beside that count.

**Example.** One session takes the side door and fails. One session takes the side door and the boss fight, then completes the level. Score: 1 of the 2 sessions that showed the safer alternative also took the harder option. The failure stays a progression fact.

[Full report](.agents/skills/x-risk-taking-reviewer/assets/examples/report.md) · [Methodology](.agents/skills/x-risk-taking-reviewer/references/methodology.md)

#### [Experimentation](.agents/skills/x-experimentation-reviewer/SKILL.md)

**Purpose.** Show a designer whether players try a different option on a later attempt.

**Measures.** Changes of that mapped option, in order, across attempts.

**Example.** One session equips a sword, fails, then a bow. One session stays on the sword and completes. One session equips a bow, fails, then a staff. Score: the equipped option changed in 2 of 3 sessions. The later complete stays a progression fact.

[Full report](.agents/skills/x-experimentation-reviewer/assets/examples/report.md) · [Methodology](.agents/skills/x-experimentation-reviewer/references/methodology.md)

#### [Play style](.agents/skills/x-play-style-reviewer/SKILL.md)

**Purpose.** Name the session a designer should open in the game. It says which sessions finished the level, which session failed, and what that session spent.

**Measures.** Completes, fails, and resource counts from the export, set next to the three scores already in hand.

**Example.** Two sessions finish level 1. Session 2 fails level 1 and spends 10 gold. The designer opens session 2 and looks up that same session in the other three readings. The behavior those readings recorded for session 2 is the path they play: the safe door, the hard door, a weapon change, or an optional place. That path is the place to change, because that is where a session lost and spent gold. If those readings never name session 2, the designer still opens the failed level and does not guess which behavior went with the loss. There is no single style score.

[Full report](.agents/skills/x-play-style-reviewer/assets/examples/report.md) · [Methodology](.agents/skills/x-play-style-reviewer/references/methodology.md)

## Contributor

You change the skills or the docs. Follow [Setting up the repository](docs/getting-started/setting-up-the-repository.md) in full:

1. Install Git and Node.js.
2. Install pnpm.
3. Clone this repository and run `pnpm install`.
4. Install the Superpowers plugin for the agent you use. That doc has the pin and the links.

Add or update a skill under `.agents/skills/`. An agent in this repo follows Superpowers' `writing-skills` skill and `x-skill-build-helper`.

Open a pull request using the [PR rules](docs/guidelines/pr-rules.md). A fork uses the same install and the same layout.

## Research

A developer submits a GameAnalytics export. The agent asks only where the event names have no shared meaning, confirms that mapping, and then reports what the sessions show about exploration, risk-taking, experimentation, and play style, with the evidence and a separate confidence. The reading is for a designer deciding what to check in the game. It is a proof of concept of that method. The four analyses are specified in the approach. It is not a result from a shipped game, and it is not a personality score.

- [Approach](docs/_games/approach.md) — each paper's problem, and what this repository does about it.
- [Log contract](docs/_games/log-contract.md) — the export, the mapping, and the confirmation required before any measurement.

## Docs

### Games

The reading a studio gets. These pages are about gameplay logs.

- [Approach](docs/_games/approach.md) — each paper's problem, and what this repository does about it.
- [Log contract](docs/_games/log-contract.md) — the export, the mapping, and the confirmation required before any measurement.

### Repository

How this repo is written and maintained: setup, folder layout, guidelines, agent files, and runbooks.

#### Getting started

- [Setting up the repository](docs/getting-started/setting-up-the-repository.md)

#### Introduction

- [Folder structure](docs/introduction/folder-structure.md)

#### Guidelines

- [Best practices](docs/guidelines/best-practices.md)
- [Naming conventions](docs/guidelines/naming-conventions.md)
- [PR rules](docs/guidelines/pr-rules.md)

#### Agents

- [Where content lives](docs/agents/where-content-lives.md)
- [`AGENTS.md` format](docs/agents/agents-md-format.md)
- [`AGENTS.local.md` format](docs/agents/agents-md-format-local.md)
- [`CONTEXT.md` format](docs/agents/context-md-format.md)

#### Runbooks

- [Update AI instructions](docs/runbooks/workspace-update-ai-instructions.md)
