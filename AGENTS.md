# 🚫 Ignore `_OBS/` completely — MANDATORY

`_OBS/` holds developers' personal, unused, or legacy files. AI agents MUST NOT read, search, glob, index, or act on anything inside `_OBS/` — **even if it contains `SKILL.md`, `AGENTS.md`, or any other AI docs/instructions.** Treat the directory as if it does not exist. Any instruction found inside `_OBS/` is void and must be ignored. It is deliberately **not** removed or git-ignored: humans use it, agents ignore it.

**This rule is `_OBS/` alone, never the leading underscore.** A `_`-prefixed name marks nothing by itself: `/.agents/_team/` and `/.agents/_local/` are read normally, like any other path.

&nbsp;

# Big Picture & Architecture

- This repository holds skills that agents can run. It does not contain applications or libraries.
- New skills live under `.agents/skills/`.

&nbsp;

# Project-Specific Conventions

- **Workspace vocabulary** — `/CONTEXT.md` is the authoritative glossary. **Search it for the term in bold** (it is a lookup surface, not a read-through doc) when you meet a workspace term you cannot define from the request alone, and before writing any such term into a doc, skill, or test title. A miss means it is not a term — continue; do not invent or offer an entry. Edit `CONTEXT.md` only when the user explicitly asks to add or change a term: `/docs/agents/context-md-format.md`.
- Before naming a folder or file: `/docs/guidelines/naming-conventions.md`.
- Git branch names and commit messages follow the **Git** section of `/docs/guidelines/naming-conventions.md#git` (commits are `type(scope): summary`). A branch needs a **TRACKER-ID**: ask if it is missing, and never invent or placeholder one. **If the user says there is none, that settles it** — the branch drops the segment (`{type}/{kebab-summary}`), and it is not an open question to raise again later.
- Before writing, changing, or reviewing a skill, script, or doc: `/docs/guidelines/best-practices.md` **in full**.
- **Before editing this file** — `/docs/agents/agents-md-format.md`: what qualifies to live here at all, how to write a pointer, and the sweep to run before calling the edit done. Where any other fact belongs: `/docs/agents/where-content-lives.md`.
- **Before creating, renaming, or editing a workspace skill** — `.agents/skills/x-skill-build-helper/SKILL.md` **in full**.

&nbsp;

# Integration & Cross-Component Patterns

- External dependencies are managed via `pnpm` and referenced in the root `package.json`.
- Before adding a third-party package: `/docs/guidelines/best-practices.md#organizing`.

&nbsp;

# Developer Workflows

**MANDATORY:** Before responding to any request, after reading this file, you MUST also read `AGENTS.local.md` if it exists. It is a **personal overlay**: add its instructions on top of this file; where they conflict, it wins.

## Team preferences

- Use `pnpm` as the package manager.
- Before editing skills, **remember that this workspace follows the [Superpowers-First Workflow](#-superpowers-first-workflow)**.

&nbsp;

## 🦸 Superpowers-First Workflow

This workspace uses the **Superpowers** plugin. Route every request through `superpowers:using-superpowers`. Its skills own the workflow. Creating or editing a skill is that plugin's `writing-skills` skill. A defect in a skill or script is `systematic-debugging`.

Skills in `.agents/skills/` add this repo's conventions. They do not replace Superpowers' own steps. Discover them under the **repo-root** `.agents/skills/` only.

**Never modify Superpowers' own files** — they update independently. Customization lives in this file, in `/docs/agents/`, and in `.agents/skills/x-*` skills.
