# Cursor Cloud

Durable notes for **Cursor Cloud Agent** VMs only — not desktop Cursor, not Claude Code.

SessionStart injects a pointer at this file when `CURSOR_AGENT` is set. Do not copy this body into `AGENTS.md` (that file is paid for by every harness on every turn).

Template headings for reuse: [`CLOUD.skeleton.md`](./CLOUD.skeleton.md).

## This repository

### Runtime & install

- Node / pnpm versions and laptop setup: `docs/getting-started/setting-up-the-repository.md` — do not restate version numbers here.
- **Boot already ran** (via `.cursor/environment.json`): `node .cursor/cloud/install-pinned-plugins.mjs`, which installs SHA-pinned plugins from `.agents/_pins/plugins/catalog.json` into `~/.cursor/skills/` for harness `cursor-cloud`. Do not re-run that installer unless pins look missing.
- **Deps install / recovery:** `pnpm install --frozen-lockfile` (same as getting-started). Use when `node_modules` is missing or broken — not as a substitute for the pin installer.
- `CURSOR_AGENT=1` marks this harness; desktop Cursor does not use this install path.

### Auth & external services

- None recorded for this repo.

### Host limits

- This is a Linux Cloud VM. Do not assume a macOS-only toolchain is installed.

### Known baseline failures

- None recorded.
