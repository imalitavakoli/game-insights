[🔙](../../README.md#guidelines)

# Best Practices 👌

&nbsp;

[🔝](#best-practices-👌)

## Mindset

- **This repository holds skills.** A change belongs in `.agents/skills/` or in the docs and configuration that support those skills.
- **Read the skill helper first.** Before creating, renaming, or editing a workspace skill, read `.agents/skills/x-skill-build-helper/SKILL.md`.
- **Keep ownership current.** When you add or hand off a path, update the root `CODEOWNERS` file by following `.agents/skills/x-codeowners-editor/SKILL.md`.
- **One subject per skill.** Prefer a skill that does several verbs for one subject over a skill that covers unrelated subjects.
- **Prefer many small files.** A skill's `scripts/` tree should be several short TypeScript, JavaScript, or Node files rather than one long file.

&nbsp;

[🔝](#best-practices-👌)

## Documenting

These apply to skill prose and to the TypeScript, JavaScript, and Node scripts a skill ships under `scripts/`.

- **Say why.** Comments explain why a function or variable exists, not only what the next line does.
- **Use names that say what the thing is.**
- **Use JSDoc on exported functions**, and on any function whose purpose is not obvious from its name.
- **Explain an internal script at the top.** A helper file that is not the skill's main script (it can be `.ts`, `.js`, or `.mjs`) gets a JSDoc at the top: why the file exists, and what it does.

&nbsp;

[🔝](#best-practices-👌)

## Organizing

- **Ask the Workspace Specialist before adding a third-party package**, then add it to the root `package.json` with pnpm.
- Prefer a package that is widely used and still maintained.

[🔙](../../README.md#guidelines)
