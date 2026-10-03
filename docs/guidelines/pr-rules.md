[🔙](../../README.md#guidelines)

# PR (Pull Request) Rules 📏

&nbsp;

[🔝](#pr-pull-request-rules-📏)

## Making a change

1. **Branch from `main`.** Branch names: [naming-conventions.md](./naming-conventions.md#git).
2. **Commit each semantic change** on that branch. Commit messages: the same Git section. If you change `package.json` or `pnpm-lock.yaml`, tell the Workspace Specialist — dependency changes affect everyone who installs the repo.
3. **Update the doc or skill you changed** in the same change, so the written rule matches the files.
4. **Open a PR to `main`** and add the Code Owners of the paths you touched as reviewers. In the description, summarize the change and link the task.
5. **Keep the PR small.** A PR that touches more than about 20 files is hard to review. If the work is larger, stop at a stable point, open the PR, and continue in a follow-up.
6. **Merge when reviewers approve**, then delete the source branch.

You can skip the pre-PR conversation when you are the only Code Owner of every path in the PR and the change is small (a handful of files).

Code Owners review to understand the change and to suggest improvements. They are the people listed for those paths in `CODEOWNERS`.

[🔙](../../README.md#guidelines)
