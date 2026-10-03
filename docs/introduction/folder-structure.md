[🔙](../../README.md#introduction)

# Folder structure 📁

This repository holds skills and the docs and agent configuration around them. New skills go in `.agents/skills/`.

```
game-insights/
├── _OBS/                         // Personal or legacy files. AI agents ignore this directory.
├── .agents/
│   ├── _pins/                    // Source of truth for pinned plugins (`plugins/catalog.json`).
│   ├── hooks/                    // Hook scripts. Each agent's settings file registers them.
│   └── skills/                   // Our skills. This is the canonical copy.
├── .claude/
│   ├── plugins/                  // Claude adapter for the pin (`marketplace.json` matches the catalog).
│   └── skills/                   // Pointer stubs so Claude Code can find the canonical skills.
├── .cursor/
│   └── cloud/                    // Cursor Cloud pin install and VM notes.
├── docs/                         // Workspace documentation. The README indexes it.
│   ├── _games/                   // Player-behavior research: the log contract and the academic argument. Agents read this folder.
│   ├── agents/                   // How to edit AGENTS.md, CONTEXT.md, and where a fact lives.
│   ├── getting-started/
│   ├── guidelines/
│   ├── introduction/
│   └── runbooks/
├── AGENTS.md                     // Instructions every agent reads.
├── AGENTS.local.md               // Personal overlay on AGENTS.md. Gitignored.
├── CLAUDE.md                     // Claude Code's entry point. It points at AGENTS.md.
├── CODEOWNERS                    // Who is the expert for a path.
├── CONTEXT.md                    // This workspace's vocabulary. Look a term up; do not read it through.
├── package.json
└── README.md
```

&nbsp;

[🔙](../../README.md#introduction)
