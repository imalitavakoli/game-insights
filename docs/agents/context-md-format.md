[🔙](../../README.md#agents)

# `CONTEXT.md` format 📖

How to write and maintain the workspace glossary at `CONTEXT.md` (repo root).

**What belongs in it at all** is decided by [where-content-lives.md](where-content-lives.md) → _A term's meaning vs its consequences_. Read that first; this doc only covers the shape of an entry once the fact belongs here.

**When to edit.** Edit this glossary only when the user has explicitly asked to add or change a term. A miss in `CONTEXT.md` is not that ask. A miss means the phrase is not a term. Do not invent an entry or offer to add one.

&nbsp;

## Entry shape

```markdown
**{Term}**:
{One or two sentences saying what it IS.}
_Avoid_: {alternative names we do not use, comma-separated}
```

- **One term per concept.** If two names are in circulation, pick one and put the loser under `_Avoid_`.
- **Define the thing, not its behaviour.** No "so you must…". Those are consequences and live in the doc or skill.
- **Group when it helps.** Use `##` sections once a flat list is hard to scan.
- **Bold the term, colon, definition on the next line.**

**This workspace has one glossary:** `CONTEXT.md` at the repo root. Do not add a second context file.

&nbsp;

## What to leave out

Ask: **is this term specific to this workspace, or would it mean the same in any repo?** Only the first belongs here.

| Leave out                                      | Why                                              |
| ---------------------------------------------- | ------------------------------------------------ |
| General programming concepts                   | They mean the same everywhere                    |
| Plugin vocabulary (Superpowers skill names)    | The plugin's own docs own them                   |
| Anything with no competing name                | An entry that could never be misread earns nothing |
| Consequences, procedures, examples of use      | [where-content-lives.md](where-content-lives.md) routes these |

&nbsp;

## `_Avoid_` is not decoration

It is the working half of an entry. A wrong marker breaks a grep, so the rejected spellings belong here:

- `x-` skills, never `custom-` — the prefix is what a search matches.

Omit `_Avoid_` only when no alternative name is plausible.

&nbsp;

## Flagged ambiguities

A `## Flagged ambiguities` section at the end holds terms that are **in use but not settled**. Record the competing readings so the eventual resolution is a real decision. This does not block work. Resolve one when the work makes the answer obvious, and move it into the body.

&nbsp;

## Keeping it a glossary as it grows

`CONTEXT.md` is a **lookup surface**: a reader arrives with one unfamiliar term and wants one entry.

- **When it passes roughly 50 entries, prune before you add.** Re-run _What to leave out_.
- **Do not split it by topic.** A reader does not know which file holds their term.
- An entry that needs a second sentence to stay true, or that could be replaced by a link, is a consequence that crept in. Move that consequence out.

&nbsp;

## Maintenance

The glossary is **not** verified against code, so it carries **no `Last Verified` stamp**. Update it when a term changes:

1. **Coining a term** that will appear in more than one doc, skill, or test title → add its entry in the same change.
2. **Renaming a term** → update the entry and move the old name into `_Avoid_`.
3. **Sweeping** — when a rule changes, `x-skill-build-helper` lists `CONTEXT.md` among the places a copy may already live.

[🔙](../../README.md#agents)
