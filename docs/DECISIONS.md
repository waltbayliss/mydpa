# MyDPA.ai — Decisions Log

## 2026-05-22 — Session 1: Project Kickoff

### D1: Working title confirmed as MyDPA.ai
**Decision:** Use MyDPA.ai as the working title and domain.
**Reason:** Walt confirmed domain + title in session 99. Brand positioning still open — not rushed.

### D2: Bridge-first architecture (not an app)
**Decision:** The product ships as a self-hosted bridge (code + guide), not a SaaS app.
**Reason:** No ongoing infrastructure cost for Walt; buyers own their own Claude API key and VPS; privacy story is stronger (your data never leaves your server).

### D3: Telegram as the primary interface
**Decision:** Telegram only for v1 (no web UI, no other chat platform).
**Reason:** Telegram has inline keyboards (approve/deny buttons), supports voice messages, photos, and has a generous bot API. WhatsApp Business API is expensive and restrictive. Discord is developer-skewed.

### D4: Claude Code (headless) as the AI engine
**Decision:** Use `claude -p` (headless Claude Code) not raw Anthropic API.
**Reason:** Claude Code already has tool use (file read/write, bash, web fetch) built in. Building equivalent capability on raw API would take months. The permission gate hooks into Claude Code's `--permission-prompt-tool` flag.

### D5: Permission gate is opt-out-able per action type
**Decision:** Ship with a classifier that auto-approves safe actions; risky actions require a tap.
**Reason:** The gate is the safety story that makes buyers comfortable deploying this. Without it, buyers are handing an AI unrestricted VPS access.

### D6: Voice via OpenAI Whisper API (not local)
**Decision:** Transcribe voice messages via OpenAI Whisper API, not local whisper.
**Reason:** Local whisper needs GPU or is slow on cheap VPS. Whisper API is $0.006/min — negligible for personal use. Requires `OPENAI_API_KEY` but that's already common.

### D7: Notion as the primary "memory + workspace" integration
**Decision:** Notion is the first and primary integration, ahead of Calendar or Drive.
**Reason:** Most target customers already use Notion. Read/write to Notion databases is the #1 "wow moment" — the assistant can actually update your task list, not just talk about it.
