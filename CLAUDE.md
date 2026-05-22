# MyDPA.ai — Agent Context

## What This Project Is
MyDPA.ai is a packaged product that lets anyone deploy their own AI personal assistant in Telegram, connected to Notion, email, and a cloud VPS. It is built on the nova-bridge stack developed by Walt Bayliss.

## Repository Layout
```
mydpa/
├── CLAUDE.md               ← this file
├── README.md
├── .env.example            ← all required variables with descriptions
├── docs/
│   ├── PRD.md              ← product requirements & vision
│   ├── ARCHITECTURE.md     ← system design
│   ├── DECISIONS.md        ← key decisions log
│   └── SPRINT_LOG.md       ← session-by-session build log
├── setup/
│   ├── SETUP.md            ← THE single-file setup guide (copy-paste)
│   ├── bridge.py           ← generalized Telegram↔Claude bridge daemon
│   ├── nova_classify.py    ← permission gate risk classifier
│   ├── approve_mcp.py      ← Telegram approve/deny MCP tool
│   ├── mydpa.service       ← systemd unit file template
│   └── install.sh          ← one-shot install script
└── product/
    ├── MANUAL.md           ← full end-user manual
    └── SALES.md            ← positioning, copy, funnel map
```

## Core Rules for Development
1. Everything in `setup/` must work with zero Nova-specific dependencies — it is for end-users, not Walt's personal stack.
2. All variables are `{{PLACEHOLDER}}` format in setup files — never hardcode real values.
3. `DECISIONS.md` gets an entry for every significant design choice.
4. `SPRINT_LOG.md` gets an entry at the close of every build session.
5. The `setup/SETUP.md` file is the hero deliverable — all other docs serve it.
