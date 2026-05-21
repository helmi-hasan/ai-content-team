# AI Content Team — Helmi Hasan

An 8-agent content system that researches, scripts, designs, and reports every day.
Powered by Claude Code + MCP tools. Zero Python required.

## Project Structure

```
AI-Content-Team/
├── CLAUDE.md                  ← you are here
├── config/
│   ├── settings.md            ← channel URL, Notion IDs, run preferences
│   ├── brand-voice.md         ← Helmi's voice, ICA, tone (auto-updated by Channel Analyst)
│   └── competitors.md         ← competitor channel list
├── agents/
│   ├── 01-channel-analyst.md  ← runs once + weekly: builds brand voice + competitor tracker
│   ├── 02-trend-scout.md      ← daily: finds outliers via VidIQ + Velio input
│   ├── 03-script-writer.md    ← daily: writes full script in Helmi's voice
│   ├── 04-thumbnail-designer.md ← daily: 3 thumbnail concepts via Canva
│   ├── 05-daily-reporter.md   ← daily: email digest via Mailerlite
│   ├── 06-dashboard.md        ← daily: generates HTML tools
│   └── pipeline.md            ← master orchestration — runs agents 2-6 in sequence
├── outputs/
│   ├── scripts/               ← generated scripts (markdown)
│   ├── thumbnails/            ← thumbnail briefs + Canva links
│   └── dashboard/             ← dashboard.html, teleprompter.html, recording.html
└── logs/                      ← daily run logs (YYYY-MM-DD.md)
```

## Connected Tools (MCP)

| Tool | Used by |
|------|---------|
| VidIQ | Trend Scout, Channel Analyst |
| Notion | All agents (memory layer) |
| Canva | Thumbnail Designer |
| Mailerlite | Daily Reporter |
| Web Search | Trend Scout (backup) |

## How to Run

**Full daily pipeline:**
Open this project in Claude Code and say: `run the daily pipeline`

**Individual agent:**
Say: `run the trend scout` or `run the script writer`

**First-time setup:**
Say: `run the channel analyst` — this runs once to build brand voice + competitor data

**Automated daily run:**
Configured via `/schedule` — runs every morning at 07:00 AEST

## Notion Databases

See `config/settings.md` for Notion page/database IDs.

Required Notion pages:
- Daily Outliers database
- Content Calendar database  
- Brand Voice document
- Competitor Tracker database

## Velio Data (Manual Input)

Velio is not yet connected via MCP. When running the Trend Scout, you will be
prompted to paste Velio data. Format: paste the outlier list from Velio's dashboard.

## Key Rules

1. Trend Scout runs first — if no outliers found, skip Script Writer and Thumbnail Designer
2. Script Writer only runs if Trend Scout found a usable outlier
3. Thumbnail Designer only runs if Script Writer produced a script
4. Daily Reporter and Dashboard always run regardless
5. All outputs are logged to `logs/YYYY-MM-DD.md`
