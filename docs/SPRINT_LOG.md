# MyDPA.ai — Sprint Log

## Session 1 — 2026-05-22 (Brisbane)

### What was built
- GitHub repo created: `waltbayliss/mydpa`
- Notion product entry created in 🛒 Products For Sale database
- Full file architecture scaffolded: CLAUDE.md, PRD, ARCHITECTURE, DECISIONS, SPRINT_LOG, .env.example, setup/SETUP.md, setup/bridge.py (generalized), product/MANUAL.md, product/SALES.md
- Source material: nova-bridge stack (bridge.py, nova_classify.py, approve_mcp.py) — battle-tested on Walt's own VPS

### Key decisions made
See DECISIONS.md — D1 through D7.

### What's next
1. Generalize bridge.py, nova_classify.py, approve_mcp.py for public release (strip Walt-specific paths/tokens, add {{PLACEHOLDER}} pattern)
2. Write setup/SETUP.md — the hero single-file setup guide
3. Write product/MANUAL.md — full end-user walkthrough
4. Write product/SALES.md — funnel copy and positioning
5. Brand positioning session (Walt wants dedicated time on this)
6. Beta launch to Walt's list

### Open questions
- Brand positioning: what's the big promise? "Your AI PA" vs "AI that acts, not just answers"
- Course platform: Skool vs alternatives
- Support: CloseBot vs Notion KB
