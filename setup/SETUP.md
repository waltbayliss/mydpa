# MyDPA.ai — Setup Guide

> One file. Copy, fill in your variables, run the commands. You'll have your own AI personal assistant in Telegram in under 30 minutes.

---

## What you'll have when you're done
- A Telegram bot that talks directly to Claude AI
- Claude can read and write your Notion pages and databases
- Claude can send emails from your Gmail
- Claude understands voice messages (just hold and talk)
- Claude can see screenshots you send from your phone
- Everything runs on your own server — your data never leaves your control

---

## What you need before you start

| Requirement | Where to get it | Cost |
|-------------|----------------|------|
| A Linux VPS | DigitalOcean, Vultr, Hetzner | ~$6/mo |
| Anthropic API key | console.anthropic.com | Pay per use (~$5–20/mo typical) |
| Telegram account | Already have it | Free |
| Notion account | notion.so | Free |
| OpenAI API key | platform.openai.com | ~$0 for voice (Whisper is cheap) |

---

## Step 1 — Create your Telegram bot (5 min)

1. Open Telegram and search for **@BotFather**
2. Send `/newbot`
3. Choose a name (e.g. "My Assistant") and a username (e.g. `myassistant_bot`)
4. BotFather will give you a token that looks like `123456:ABC-DEF1234...`
5. Save it as `{{TELEGRAM_BOT_TOKEN}}`

**Get your Chat ID:**
1. Search for **@userinfobot** on Telegram
2. Send `/start` — it replies with your user ID (a number)
3. Save it as `{{TELEGRAM_CHAT_ID}}`

---

## Step 2 — Set up your VPS

SSH into your VPS and run:

```bash
# Install Node.js 20+
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt-get install -y nodejs

# Install Claude Code CLI
npm install -g @anthropic-ai/claude-code

# Create your .env file
mkdir -p ~/.mydpa
cat > ~/.env << 'EOF'
ANTHROPIC_API_KEY={{ANTHROPIC_API_KEY}}
TELEGRAM_BOT_TOKEN={{TELEGRAM_BOT_TOKEN}}
TELEGRAM_CHAT_ID={{TELEGRAM_CHAT_ID}}
NOTION_TOKEN={{NOTION_TOKEN}}
OPENAI_API_KEY={{OPENAI_API_KEY}}
EOF
chmod 600 ~/.env
```

---

## Step 3 — Set up Notion (5 min)

1. Go to [notion.so/my-integrations](https://notion.so/my-integrations)
2. Click **New integration** → give it a name (e.g. "MyDPA")
3. Copy the **Internal Integration Token** — this is your `{{NOTION_TOKEN}}`
4. In Notion, open each database you want your assistant to access
5. Click the `...` menu → **Connections** → add your integration

---

## Step 4 — Install the bridge

```bash
# Create the project directory
mkdir -p ~/mydpa && cd ~/mydpa

# Download the bridge files (or copy from this repo)
curl -O https://raw.githubusercontent.com/waltbayliss/mydpa/main/setup/bridge.py
curl -O https://raw.githubusercontent.com/waltbayliss/mydpa/main/setup/nova_classify.py
curl -O https://raw.githubusercontent.com/waltbayliss/mydpa/main/setup/approve_mcp.py

# Create state directories
mkdir -p state/approvals

# Install systemd service
sudo tee /etc/systemd/system/mydpa.service << 'EOF'
[Unit]
Description=MyDPA — AI assistant bridge
After=network.target

[Service]
Type=simple
User={{YOUR_USERNAME}}
WorkingDirectory=/home/{{YOUR_USERNAME}}/mydpa
EnvironmentFile=/home/{{YOUR_USERNAME}}/.env
ExecStart=/usr/bin/python3 /home/{{YOUR_USERNAME}}/mydpa/bridge.py
Restart=always
RestartSec=10

[Install]
WantedBy=multi-user.target
EOF

sudo systemctl daemon-reload
sudo systemctl enable mydpa
sudo systemctl start mydpa
```

**Check it's running:**
```bash
systemctl status mydpa
```

You should see a Telegram message from your bot: "✅ MyDPA is live."

---

## Step 5 — Set up Gmail send (optional, 10 min)

> Skip this if you don't need your assistant to send email.

1. Go to [console.cloud.google.com](https://console.cloud.google.com)
2. Create a new project → Enable **Gmail API**
3. Create **OAuth 2.0 credentials** (Desktop app type)
4. Download the credentials JSON
5. Run the auth flow:

```bash
python3 -c "
from google_auth_oauthlib.flow import InstalledAppFlow
flow = InstalledAppFlow.from_client_secrets_file('credentials.json',
    scopes=['https://www.googleapis.com/auth/gmail.compose',
            'https://www.googleapis.com/auth/gmail.modify'])
creds = flow.run_local_server(port=0)
print('GOOGLE_CLIENT_ID=' + creds.client_id)
print('GOOGLE_CLIENT_SECRET=' + creds.client_secret)
print('GOOGLE_REFRESH_TOKEN=' + creds.refresh_token)
"
```

Add the three values to your `~/.env` file.

---

## Step 6 — Test it

Send your bot a message on Telegram:

- **Text:** "What can you do?" — Nova will reply
- **Voice:** Hold and record anything — it gets transcribed and answered
- **Screenshot:** Send any image — Nova will read and describe it
- **Action:** "Create a Notion page called Test with today's date" — watch it happen

---

## Troubleshooting

**Bot doesn't respond:**
```bash
journalctl -u mydpa -f   # watch live logs
```

**"Permission denied" on a tool:**
- You'll see a Telegram message with ✅/❌ buttons — tap ✅ to approve once

**Voice not working:**
- Check `OPENAI_API_KEY` is set in `~/.env`
- Restart: `sudo systemctl restart mydpa`

---

## Variables reference

| Placeholder | Where to find it |
|------------|-----------------|
| `{{ANTHROPIC_API_KEY}}` | console.anthropic.com → API Keys |
| `{{TELEGRAM_BOT_TOKEN}}` | @BotFather on Telegram |
| `{{TELEGRAM_CHAT_ID}}` | @userinfobot on Telegram |
| `{{NOTION_TOKEN}}` | notion.so/my-integrations |
| `{{OPENAI_API_KEY}}` | platform.openai.com → API Keys |
| `{{YOUR_USERNAME}}` | Your VPS Linux username (run `whoami`) |
