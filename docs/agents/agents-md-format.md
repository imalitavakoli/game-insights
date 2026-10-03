[🔙](../../README.md#agents)

# `AGENTS.md` format ⚙️

How to edit `AGENTS.md` — the only file an agent reads **in full on every request**.

**What belongs in it at all** is decided by [where-content-lives.md](where-content-lives.md). Read that first.

&nbsp;

## The one test

> A line earns its place in `AGENTS.md` only if **every** request needs it.

Everything else goes behind a pointer. Name the destination and the condition, and stop. How to write that pointer: [where-content-lives.md](where-content-lives.md) → _Writing a pointer_.

&nbsp;

## What the file is

`AGENTS.md` is a **router**, not a manual. It holds workspace facts every request needs (what this repo is, the package manager, off-limits directories) and the pointers that decide where to look next.

The gitignored companion is `AGENTS.local.md`. It has no required shape: [agents-md-format-local.md](agents-md-format-local.md).

&nbsp;

## Adding a rule

1. **Does every request need it?** → `AGENTS.md`.
2. **Is it how to perform a step?** → the skill that owns the step. `AGENTS.md` says _when_ and _which_; the skill says _how_.
3. **Otherwise** → the `docs/` page for that topic.

A rule that lands in two of these will drift. Pick one and point from the others.

&nbsp;

## Editing conventions

- **`&nbsp;` between top-level sections.**
- **`#` for top-level sections.**
- **Absolute repo paths** (`/docs/…`, `/CONTEXT.md`) when pointing out of the file.
- **State the trigger, not the topic**, in every pointer.

&nbsp;

## Before calling an edit done

Run the sweep in [where-content-lives.md](where-content-lives.md) → _When a rule already exists in more than one place_.

[🔙](../../README.md#agents)
