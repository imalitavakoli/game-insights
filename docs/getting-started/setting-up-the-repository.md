[🔙](../../README.md#getting-started)

# Setting up the repository on a new machine 💻

Before proceeding, ensure you have the following installed on your machine:

- [Node.js](https://nodejs.org/) (version 22.19.0), which includes npm.
- [Git](https://git-scm.com/).

&nbsp;

[🔝](#setting-up-the-repository-on-a-new-machine-💻)

## Installing pnpm

- Run `npm install -g pnpm@10.33.0` to install [pnpm](https://pnpm.io/) globally.
- Run `pnpm setup` to set up pnpm's global bin directory.

&nbsp;

[🔝](#setting-up-the-repository-on-a-new-machine-💻)

## Installing local dependencies

- Clone the repository.
- From the repository root, run `pnpm install --frozen-lockfile`.

&nbsp;

[🔝](#setting-up-the-repository-on-a-new-machine-💻)

## Installing AI tools

### Claude CLI

To use Claude Code:

- Windows: Open PowerShell and run `irm https://claude.ai/install.ps1 | iex`.
- MacOS: Open Terminal and run `curl -fsSL https://claude.ai/install.sh | bash`.

On Windows, add `C:\Users\{user}\.local\bin` to the user PATH, then from the repository root run `claude` to log in.

&nbsp;

### Superpowers plugin

[Superpowers](https://github.com/obra/superpowers) is the workflow this repo routes through, including its `writing-skills` skill for creating and editing skills. The pin lives in `.agents/_pins/plugins/catalog.json`. Claude Code installs it from `.claude/plugins/.claude-plugin/marketplace.json`, which must match that catalog. Do not install Superpowers from the upstream marketplace in this repo: project settings turn that copy off here.

After cloning, from the repo root:

```bash
claude plugin marketplace add ./.claude/plugins
```

```bash
claude plugin install superpowers@x-local-marketplace --scope user
```

Then restart Claude Code, or run `/reload-plugins`.

**Why `--scope user`?** A project-scoped install is recorded against the exact path string of your clone. On Windows the CLI and the VS Code extension can disagree on drive-letter case (`C:\…` vs `c:\…`), so an install made by one can read as "enabled but not installed" in the other. A user-scoped install records no path. Enablement still comes from the repo, which is what pins the version.

Confirm with `claude plugin list`: `superpowers@x-local-marketplace` is enabled.

Cursor Cloud Agents do not use the Claude marketplace. On VM boot, `.cursor/environment.json` runs `node .cursor/cloud/install-pinned-plugins.mjs`, which installs every `catalog.json` entry whose `harnesses` includes `cursor-cloud` into `~/.cursor/skills/`. Notes for that VM live in `.cursor/cloud/CLOUD.md`. Desktop Cursor is not covered by this pin — use Superpowers' own Cursor install if you need it there.

Another agent harness can follow Superpowers' [installation instructions](https://github.com/obra/superpowers#installation). A pin change starts in `.agents/_pins/plugins/catalog.json`, then both adapters in the same change.

&nbsp;

[🔝](#setting-up-the-repository-on-a-new-machine-💻)

## FAQ

### How to fix `Permission denied (publickey)` when Claude fetches the plugin

Claude CLI uses Git over SSH to fetch the pinned Superpowers commit. If `/doctor` reports `Permission denied (publickey)`, GitHub SSH is not set up on this machine.

1. Create `C:\Users\YOU\.ssh` if it does not exist.
2. Add GitHub's host key: `ssh-keyscan -t ed25519 github.com >> C:\Users\YOU\.ssh\known_hosts`
3. Generate a key: `ssh-keygen -t ed25519 -C "your@email.com"`
4. Copy `C:\Users\YOU\.ssh\id_ed25519.pub` into GitHub → Settings → SSH and GPG keys → New SSH key (Authentication key).
5. Test with `ssh -T git@github.com`, then run `/doctor` again.

&nbsp;

[🔝](#setting-up-the-repository-on-a-new-machine-💻)

## Opening the workspace in VS Code

Open `x.code-workspace` at the repository root. The first open suggests the recommended extensions.

[🔙](../../README.md#getting-started)
