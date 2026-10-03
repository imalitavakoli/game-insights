[🔙](../../README.md#runbooks)

# Workspace: Update AI instructions

**Important!** This task should be done by the Workspace Specialist most of the time.

AI agents rely on these files to follow the workspace rules. When a rule changes, review:

- `AGENTS.md`
- `docs/agents/` — format docs for `AGENTS.md` and `CONTEXT.md`, and [where content lives](../agents/where-content-lives.md)
- `.agents/hooks/` — hook scripts; each harness registers them (`.claude/settings.json`, `.cursor/hooks.json`)

If that change also updates `.agents/_pins/plugins/catalog.json`, update `.claude/plugins/.claude-plugin/marketplace.json` in the same change (same version and SHA). Claude Code reads the marketplace file, not the catalog. Cursor Cloud's installer reads the catalog itself, so `.cursor/cloud/install-pinned-plugins.mjs` does not get a second copy of the commit. Layout: [.agents/_pins/plugins/README.md](../../.agents/_pins/plugins/README.md).

[🔙](../../README.md#runbooks)
