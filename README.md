# game-insights

Skills that help an AI agent turn gameplay telemetry into a reading a designer can check.

## Research

A developer submits a GameAnalytics export. The agent asks only where the event names have no shared meaning, confirms that mapping, and then reports what the sessions show about exploration, risk-taking, experimentation, and play style, with the evidence and a separate confidence. The reading is for a designer deciding what to check in the game. It is a proof of concept of that method. The four analyses are specified in the approach. It is not a result from a shipped game, and it is not a personality score.

- [Approach](docs/_games/approach.md) — each paper's problem, and what this repository does about it.
- [Log contract](docs/_games/log-contract.md) — the export, the mapping, and the confirmation required before any measurement.

### Game analysis

- [`x-exploration-reviewer`](.agents/skills/x-exploration-reviewer/SKILL.md) — exploration from a GameAnalytics export, once the mapping beside the logs is confirmed. [Example](.agents/skills/x-exploration-reviewer/assets/examples/report.md). [Methodology](.agents/skills/x-exploration-reviewer/references/methodology.md).
- [`x-experimentation-reviewer`](.agents/skills/x-experimentation-reviewer/SKILL.md) — variation across attempts from a GameAnalytics export, once the mapping beside the logs is confirmed. [Example](.agents/skills/x-experimentation-reviewer/assets/examples/report.md). [Methodology](.agents/skills/x-experimentation-reviewer/references/methodology.md).

## Start here

Follow [Setting up the repository](docs/getting-started/setting-up-the-repository.md) in order. It is the setup for a new machine. Do these before you start a session:

1. Install Git and Node.js.
2. Install pnpm.
3. Clone this repository and install its dependencies.
4. Install the Superpowers plugin for the agent you use. Claude Code and Cursor Cloud use the pin in this repo. Cursor on your own machine uses Superpowers' own install, which that doc links to.

Then open this folder as the agent's workspace and start a session. Ask for what you want. Skills live in `.agents/skills/`, and the agent reads the one that matches.

## Contributing

Complete [Start here](#start-here) first. The same setup is what a contributor or a fork needs.

Add or update a skill under `.agents/skills/`. In this repo, an agent follows Superpowers' `writing-skills` skill and `x-skill-build-helper`.

Open a pull request using the [PR rules](docs/guidelines/pr-rules.md). A fork uses the same layout: change the skills in your copy the same way.

## Docs

Reference for this workspace.

### Games

- [Approach](docs/_games/approach.md)
- [Log contract](docs/_games/log-contract.md)

### Getting started

- [Setting up the repository](docs/getting-started/setting-up-the-repository.md)

### Introduction

- [Folder structure](docs/introduction/folder-structure.md)

### Guidelines

- [Best practices](docs/guidelines/best-practices.md)
- [Naming conventions](docs/guidelines/naming-conventions.md)
- [PR rules](docs/guidelines/pr-rules.md)

### Agents

- [Where content lives](docs/agents/where-content-lives.md)
- [`AGENTS.md` format](docs/agents/agents-md-format.md)
- [`AGENTS.local.md` format](docs/agents/agents-md-format-local.md)
- [`CONTEXT.md` format](docs/agents/context-md-format.md)

### Runbooks

- [Update AI instructions](docs/runbooks/workspace-update-ai-instructions.md)
