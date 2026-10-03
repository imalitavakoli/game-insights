# game-insights

Skills that help an AI agent turn game analytics into insights.

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
