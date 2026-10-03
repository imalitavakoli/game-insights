[🔙](../../README.md#agents)

# Where content lives 🗂️

**One fact, one home.** Before writing anything an agent will read, decide which surface owns it.

`AGENTS.md` and `x-skill-build-helper` point here rather than carrying their own copies.

&nbsp;

## The table

| The fact is…                             | Home                                    | Loaded when                                      |
| ---------------------------------------- | --------------------------------------- | ------------------------------------------------ |
| what a term **means**                    | `CONTEXT.md` (repo root)                | you meet an unfamiliar term                      |
| a rule **every** request needs           | `AGENTS.md`                             | every turn                                       |
| what one **tool** needs to find `AGENTS.md` | that tool's entry stub (`CLAUDE.md`) | that tool loads it, every turn                   |
| how to edit **`AGENTS.md`**              | `docs/agents/agents-md-format.md`       | editing `AGENTS.md`                              |
| how to edit **`AGENTS.local.md`**        | `docs/agents/agents-md-format-local.md` | writing the personal overlay                     |
| how to edit **`CONTEXT.md`**             | `docs/agents/context-md-format.md`      | adding or changing a term                        |
| **how to perform** a step                | the skill that owns it                  | that skill is invoked                            |
| how a **topic** works                    | the relevant `docs/` page               | working on that topic                            |

&nbsp;

## A term's meaning vs its consequences

- **`CONTEXT.md` gets the definition** — what the thing _is_, in one or two sentences.
- **The doc or skill gets the consequences** — where it lives, how it is named, who must do what.

&nbsp;

## What qualifies for `AGENTS.md`

`AGENTS.md` is read in full on **every** request. A line earns its place only if every request needs it. How to write one: [agents-md-format.md](agents-md-format.md).

&nbsp;

## A tool entry stub points; it never teaches

Some tools read a file of their own before anything else — `CLAUDE.md`. It exists to send that tool to `AGENTS.md`. A stub holds a title and a pointer. It does not restate a rule.

&nbsp;

## Writing a pointer

1. **State when to read the target.** A trigger ("read `X` when you meet a term you cannot define from the request alone") is what makes the pointer skippable.
2. **Match the read to the target.** A glossary or index: read the one entry. A contract or procedure (`SKILL.md`, a format doc): read it **in full**, and the pointer must say so.
3. **Cite a path and a heading.** Those survive an edit. A line number or a quoted sentence does not. Check the heading exists before you commit.
4. **Do not point twice from the same file** at the same target.

&nbsp;

## When a rule already exists in more than one place

Pick the home from the table, move the rule there, and replace the other copies with a pointer — in the same change. Then grep `AGENTS.md`, `CONTEXT.md`, `docs/`, and `.agents/skills/` for a distinctive phrase from what you removed.

[🔙](../../README.md#agents)
