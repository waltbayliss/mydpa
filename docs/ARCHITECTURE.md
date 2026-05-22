# MyDPA.ai — Architecture

## System Overview
```
Walt's Phone (Telegram)
        ↓ text / voice / screenshot
   Telegram Bot API
        ↓ long-poll (no inbound port needed)
   bridge.py (systemd daemon on VPS)
        ↓ transcribes voice (Whisper), downloads images
   claude -p (headless Claude Code)
        ↓ reads/writes files, calls APIs
   Integrations: Notion · Gmail · Cloudflare · GitHub · etc.
        ↑
   Permission Gate (nova_classify.py + approve_mcp.py)
        → safe actions run automatically
        → risky actions send ✅/❌ button back to Telegram
```

## Components

### bridge.py
- Long-polls Telegram `getUpdates` (50s timeout)
- Handles text, voice (downloads + transcribes), photo, document messages
- Queues messages to a serial worker thread (one Claude run at a time)
- Resumes the same Claude session across messages (persistent `session_id`)
- Routes approve/deny callbacks back to the waiting Claude process

### nova_classify.py
- Classifies every tool call as `safe` or `risky` before it executes
- Safe = runs automatically (Read, Write, Edit, python3, curl to Notion/GH/CF, git)
- Risky = sends Telegram approve button (sudo rm, git push --force, Gmail send, unknown)

### approve_mcp.py
- MCP server that Claude calls when it wants to use a risky tool
- Generates a nonce, sends Telegram inline keyboard (✅ Approve / ❌ Deny)
- Polls for Walt's tap, returns allow/deny to Claude

### Session Persistence
- `state/session_id` — Claude session resumed on every message (continuity)
- `state/offset` — Telegram update offset (no duplicate processing)
- `state/approvals/` — nonce files for the approve/deny handshake

## VPS Requirements
- Linux (Ubuntu 22.04+ recommended)
- Python 3.10+
- systemd
- Claude Code CLI (`npm install -g @anthropic-ai/claude-code`)
- Node.js 20+ (for Claude Code)

## Security Model
- Bot only responds to `{{TELEGRAM_CHAT_ID}}` — all other chats ignored
- Risky actions require explicit tap approval
- No inbound ports required — outbound HTTPS only
- API keys stored in `/home/{{USER}}/.env`, never in code
