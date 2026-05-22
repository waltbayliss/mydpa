# MyDPA.ai — Product Requirements Document

## Vision
Anyone with a VPS and an Anthropic API key can have a real AI personal assistant — one that takes action, not just answers questions. MyDPA.ai packages the complete setup into a single markdown file you copy, fill in your variables, and run.

## Problem
AI assistants (ChatGPT, Claude.ai, etc.) are great at answering questions but can't act on your behalf. They can't write to your Notion, send your emails, manage your calendar, or deploy your code. Building an assistant that CAN do these things requires significant technical setup most people can't or won't do.

## Solution
MyDPA.ai provides:
1. A battle-tested bridge codebase (Telegram ↔ Claude Code on VPS)
2. A single-file setup guide with copy-paste commands and `{{PLACEHOLDER}}` variables
3. A permission gate so the AI asks before doing anything risky
4. Pre-built integrations for the tools most people actually use

## Core Integrations (v1)
- **Telegram** — primary interface (text, voice, screenshots)
- **Notion** — read/write databases and pages
- **Gmail** — send emails on command
- **Cloudflare Pages** — deploy static sites
- **Voice messages** — transcribed via OpenAI Whisper
- **Screenshots** — read and act on images sent from phone

## Funnel / Pricing
| Tier | Product | Price |
|------|---------|-------|
| Entry | Setup guide + bridge code (self-hosted) | Free / $5 |
| OTO 1 | Extra integration templates (Calendar, Slack, etc.) | $35 |
| OTO 2 | Step-by-step video course + done-with-you setup | $297 |
| Continuity | Unlimited agents + weekly calls with Walt | $20/mo |

## Target Customer
- Entrepreneurs, coaches, and creators who are not developers
- Already paying for Notion, Gmail, or similar tools
- Want leverage — one assistant that knows their business and acts on it
- Comfortable following technical instructions but not writing code from scratch

## Beta Plan
- Launch to Walt's existing list/database first
- 3-sales or 50-capture validation threshold (same as AI Agent Funnel)
- Roll out fast and large once validated

## Deferred Decisions
- Brand positioning (Walt wants real time spent on this — not rushed)
- Course platform: Skool (probable) vs alternatives
- Support: CloseBot vs Notion KB
