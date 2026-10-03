# game-insights

Skills that help an AI agent turn gameplay telemetry into a reading a designer can check.

Two audiences: a [studio](#studio) getting a reading, and a [contributor](#contributor) changing this repo.

## Studio

You do not install this repo's packages. The game skills are the files under `.agents/skills/`.

1. Clone the repository.
2. Open this folder as the agent's workspace.
3. Install the agent you use, if it is not installed yet. Claude Code and Cursor Cloud use the Superpowers pin in this repo. Cursor on your own machine uses Superpowers' own install, which [Setting up the repository](docs/getting-started/setting-up-the-repository.md) links to.

### Get a reading

1. Bring a GameAnalytics export: one JSON object per event. The [log contract](docs/_games/log-contract.md) is the shape.
2. Confirm the mapping once, and save that file beside the export. The agent asks only about design event ids. You say which ids are exploration, risk-taking, or experimentation, or that they should be ignored. A sentence in the chat is not the mapping file. A later run asks only about ids the file does not already cover.
3. Ask for exploration, risk-taking, and experimentation in any order. Each one reads the same export and the same mapping.
4. Ask for play style only after those three readings exist. Give it the three readings and the same export.

| Ask for | The mapping must already say | You get a score when |
| --- | --- | --- |
| Exploration | which ids are optional or off-path, and the goal or reward | that goal or reward is in the sessions. If it is absent, the report says so and does not score |
| Risk-taking | which id is the harder option, and the safer alternative | more than one session shows the safer alternative. A failure is not the score |
| Experimentation | which ids can change between attempts | there is more than one session. A later win is not the score |
| Play style | nothing further. It does not re-read design events | all three readings are in hand. It keeps them side by side with progression and resource counts, and it does not produce one style number |

If one of those three readings is missing, play style stops.

You receive the counts, the order of events, a score and a separate confidence, and a note a designer can check. A thin trace leaves the score out. The reading is not a personality score. Each example below is synthetic. A real export is read the same way.

### Game analysis

- [`x-exploration-reviewer`](.agents/skills/x-exploration-reviewer/SKILL.md) — exploration from a GameAnalytics export, once the mapping beside the logs is confirmed. [Example](.agents/skills/x-exploration-reviewer/assets/examples/report.md). [Methodology](.agents/skills/x-exploration-reviewer/references/methodology.md).
- [`x-risk-taking-reviewer`](.agents/skills/x-risk-taking-reviewer/SKILL.md) — a harder option taken while a safer one was available, kept separate from the outcome. [Example](.agents/skills/x-risk-taking-reviewer/assets/examples/report.md). [Methodology](.agents/skills/x-risk-taking-reviewer/references/methodology.md).
- [`x-experimentation-reviewer`](.agents/skills/x-experimentation-reviewer/SKILL.md) — variation across attempts from a GameAnalytics export, once the mapping beside the logs is confirmed. [Example](.agents/skills/x-experimentation-reviewer/assets/examples/report.md). [Methodology](.agents/skills/x-experimentation-reviewer/references/methodology.md).
- [`x-play-style-reviewer`](.agents/skills/x-play-style-reviewer/SKILL.md) — the three readings together with progression and resource patterns. [Example](.agents/skills/x-play-style-reviewer/assets/examples/report.md). [Methodology](.agents/skills/x-play-style-reviewer/references/methodology.md).

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
