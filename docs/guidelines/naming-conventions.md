[🔙](../../README.md#guidelines)

# Naming conventions 👪

&nbsp;

[🔝](#naming-conventions-👪)

## Folders and skills

Workspace skills live at `.agents/skills/{name}/`. How to name one — the `x-` prefix, an optional technology segment, and the skill-kind suffix — is `.agents/skills/x-skill-build-helper/SKILL.md` → _Name the skill_. Do not restate that scheme here.

A leading `_` on a folder means agents still read it. `_OBS/` is the one exception, and that exception is stated in `AGENTS.md`.

Inside a skill, a helper file or folder that is not the skill's entry script starts with `_`. For example, `_util` or `_format.ts`.

&nbsp;

[🔝](#naming-conventions-👪)

## Scripts

Suggestions for TypeScript, JavaScript, and Node code under a skill's `scripts/`. They are conventions, not a linter rule.

- **Private variables or functions**: start with `_`. For example, `const _label = 'insight';`.
- **Booleans**: start with `is`, `has`, or `shall`. For example, `const isReady = false;`.
- **Arrays**: end with `s` or `Arr`. For example, `const errors = [];`, `const forbiddenNamesArr = ['a', 'b'];`.
- **Objects**: end with `Obj`. For example, `const userObj = { name: 'Ada' };`.
- **Observables**: end with `$`. For example, `count$: Observable<number>;`.
- **Subscriptions**: end with `Sub`. For example, `intervalSub: Subscription;`.
- **Services**: end with `Service`. For example, `usersService: UsersService;`.
- **Handlers**: start with `on`. For example, `function onClickedViewDetails() {}`.

&nbsp;

[🔝](#naming-conventions-👪)

## Git

Branch and commit naming. These are conventions, not tooling-enforced.

&nbsp;

### Branch

`{type}/{TRACKER-ID}-{kebab-summary}` — **type** ∈ `feature` | `bugfix` | `hotfix` | `release`; **TRACKER-ID** = the task id (e.g. `ABC-123`); **kebab-summary** = short, lowercase, hyphenated.

If a **TRACKER-ID** is not already in the request, the current branch, or an obvious ticket reference, ask for it. Do not invent, omit, or placeholder one. If the user says there is no ID, drop that segment: `{type}/{kebab-summary}`.

e.g. `feature/ABC-123-add-insight-skill` · `bugfix/ABC-124-fix-owner-insert` · `feature/add-insight-skill` (the user said there is no ID).

&nbsp;

### Commit

```
type(scope): summary   ← required
body                   ← optional: the why / context
footer                 ← optional: Refs: ABC-123, and trailers (e.g. Co-Authored-By:)
```

- **type** (required): `feat` | `fix` | `refactor` | `docs` | `test` | `chore` | `build`.
- **scope** (optional): one skill name (`x-skill-build-helper`) or another coarse area. Omit it for a cross-cutting, root, or config change. Never a file path.
- **summary** (required): imperative, lowercase, no trailing period, brief (≤ ~50 chars).

Describe the intent. Git already records the files. One semantic change per commit.

e.g. `docs(x-skill-build-helper): clarify skill names` · `feat(x-codeowners-editor): group owners in a section` · `chore: update prettier` (no scope).

[🔙](../../README.md#guidelines)
