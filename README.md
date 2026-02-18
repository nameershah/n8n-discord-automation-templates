# n8n Discord Automation Templates

> Three plug-and-play n8n workflows that deliver AI-powered content to your Discord server — no coding required.

![n8n](https://img.shields.io/badge/n8n-Automation-FF6D5A?style=flat-square&logo=n8n)
![Groq](https://img.shields.io/badge/Groq-LLaMA_3.3_70B-F55036?style=flat-square)
![Discord](https://img.shields.io/badge/Discord-Bot-5865F2?style=flat-square&logo=discord)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)

Built and demonstrated live at **HEC Generative AI Cohort 2 — Module 5**, organized by iCode Guru in collaboration with NCEAC, HEC, PakAngels, ULEF, and Aspire Pakistan.

---

## Workflows

### 1. 🎯 Hackathon Finder
`workflows/1-hackathon-finder.json`

Runs every Monday at 9:30 AM, searches the web for upcoming **online/virtual hackathons** from 60+ US universities across Tier 1, 2, and 3, and posts them to Discord with urgency color-coding. Deduplication ensures the same hackathon is never posted twice.

**Urgency indicators:** 🔴 ≤3 days · 🟠 ≤7 days · 🟡 ≤14 days · 🟢 Plenty of time

**Requires:** Groq API · Tavily Search API · Discord Bot

---

### 2. 💼 LinkedIn Post Maker
`workflows/2-linkedin-post-maker.json`

Picks a random professional topic, uses Groq's LLaMA model to generate a 200–300 word LinkedIn post with a strong hook, data-backed insights, three takeaways, and trending hashtags — then delivers it to Discord ready to copy-paste.

**Topics covered:** AI & Automation · Remote Work · Digital Transformation · Professional Development · Innovation & Leadership

**Requires:** Groq API · Discord Bot

---

### 3. ✨ Daily Inspiration
`workflows/3-daily-inspiration.json`

Fetches a random motivational quote from ZenQuotes and a safe programming joke from JokeAPI, then posts a formatted message to Discord. No API keys needed — both sources are free and public.

**Requires:** Discord Bot only

---

## Setup

### Step 1 — Import a workflow
1. Open your n8n instance
2. Click **New Workflow → ··· → Import from file**
3. Select a `.json` file from the `workflows/` folder

### Step 2 — Connect your credentials

| Placeholder | How to get it |
|-------------|--------------|
| `YOUR_GROQ_CREDENTIAL_ID` | [console.groq.com](https://console.groq.com) → API Keys, then add in n8n Credentials |
| `YOUR_TAVILY_API_KEY` | [tavily.com](https://tavily.com) → Dashboard → API Keys |
| `YOUR_DISCORD_SERVER_ID` | Discord → Enable Developer Mode → Right-click your server → Copy ID |
| `YOUR_DISCORD_CHANNEL_ID` | Discord → Right-click channel → Copy Channel ID |
| `YOUR_DISCORD_BOT_CREDENTIAL_ID` | [discord.com/developers](https://discord.com/developers/applications) → create a bot, then add in n8n Credentials |

### Step 3 — Activate
Save the workflow and toggle it **Active**. For manual workflows, click **Execute Workflow** to test.

---

## Requirements

- n8n v1.0+ (cloud or self-hosted)
- Groq account — free tier available
- Tavily account — free tier available (Workflow 1 only)
- Discord Bot with `Send Messages` permission

---

## Repository Structure

```
n8n-discord-automation-templates/
├── README.md
└── workflows/
    ├── 1-hackathon-finder.json
    ├── 2-linkedin-post-maker.json
    └── 3-daily-inspiration.json
```

---

## License

MIT — free to use, modify, and share. Attribution appreciated.

---

> ⭐ Found this useful? Star the repo and share it with your network!
