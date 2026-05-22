# MyDPA.ai — User Manual

## Welcome
You now have an AI personal assistant that lives in your Telegram and runs on your own server. This manual covers everything you can do with it and how to get the most out of it.

---

## Talking to your assistant

### Text messages
Just type normally. Your assistant understands natural language.

Examples:
- "What's on my Notion today?"
- "Add a task called 'Call John' to my Tasks database"
- "Send an email to sarah@example.com saying I'll be 10 mins late"

### Voice messages
Hold the microphone button in Telegram and speak. Your message is automatically transcribed and sent to your assistant. Speak as you naturally would.

### Screenshots
Take a screenshot on your phone and send it to the bot. Your assistant will read what's in the image and can act on it.

Examples:
- Screenshot a Notion page and say "add these tasks to my database"
- Screenshot an email and say "draft a reply to this"
- Screenshot a website and say "summarise this"

---

## What your assistant can do

### Notion
- Read any database you've connected
- Create new pages and database entries
- Update existing records
- Search across your workspace

### Gmail
- Send emails on your behalf
- Draft emails for you to review first
- (Your assistant will always confirm before sending)

### Research
- Search the web for information
- Summarise articles and pages
- Answer questions using up-to-date information

### Files (on your VPS)
- Read and write files on your server
- Run scripts
- Deploy static websites

---

## The approval system

When your assistant wants to do something that could have consequences — like sending an email or running a system command — it will send you a Telegram message with two buttons:

**✅ Approve** — go ahead  
**❌ Deny** — cancel

Safe actions (reading Notion, creating pages, writing files) happen automatically. Only actions that are hard to undo or affect external systems require your approval.

---

## Tips for getting the best results

**Be specific about where:** "Add to my Tasks database" works better than "add a task"

**Give context:** "I have a meeting at 3pm — remind me to prepare by adding a Notion page for it"

**Chain requests:** "Check my Notion inbox, summarise anything urgent, and draft replies for the two oldest items"

**Use voice for quick commands:** It's faster than typing and your assistant handles it perfectly

---

## Privacy & security

- Your messages go: Telegram → your VPS → Claude AI → back to you
- Nothing is stored by MyDPA.ai — your server, your data
- Your API keys never leave your server
- The approval system ensures your assistant can't take irreversible actions without your tap
