# Workspace domain language

The authoritative glossary for this workspace's own vocabulary. One term per concept; alternatives we do **not** use are listed under `_Avoid_`.

**This file defines what a term _is_ — never how the system behaves.** Where a term has consequences (where a skill lives, how it is named, who owns a path), the linked doc owns that. Skills and docs cite a term here instead of redefining it.

- **Adding or changing a term:** [docs/agents/context-md-format.md](docs/agents/context-md-format.md). This file carries **no `Last Verified`** — it is not verified against code; it is updated when a term changes.
- **Deep references:** [naming conventions](docs/guidelines/naming-conventions.md) · [folder structure](docs/introduction/folder-structure.md)

&nbsp;

## Workspace markers

**`x` marker**:
Marks something this workspace itself owns and provides, as opposed to a third-party or plugin skill — our skills are named `x-*`.
_Avoid_: `custom-`, `internal-`, `our-`

&nbsp;

## Roles

**Workspace Specialist**:
The person accountable for the workspace itself rather than for any one skill — its docs, its agent configuration (`AGENTS.md`, `CONTEXT.md`, skills), and its workspace-wide files such as `package.json`.
_Avoid_: Maintainer, Architect, Tech lead, Owner

**Code Owner**:
A person or team listed in `CODEOWNERS` as the expert for one path of the repo — distinct from the Workspace Specialist, who is accountable for the whole.
_Avoid_: Reviewer, Maintainer, Owner (unqualified)

&nbsp;

## Skills

**Skill kind**:
Which of seven jobs one of our own `x-*` skills does — `writer`, `helper`, `scaffolder`, `editor`, `enricher`, `reviewer`, `runner` — each an agent noun, stated twice: as the last segment of the skill's name and as `kind:` in its `metadata`. Plugin skills carry no kind.
_Avoid_: Skill type, Skill category, Skill flavour, Skill role

&nbsp;

## Flagged ambiguities

Terms **in use but not settled** — recorded so a contested one is not silently coined twice. Nothing here blocks: resolve one when the work makes the answer obvious, then move it into the body above. Format rules: [docs/agents/context-md-format.md](docs/agents/context-md-format.md).

**None currently.** The section stays so a contested term has a home the moment one appears.
