# Agent 1 — Channel Analyst

**Runs:** Once on setup, then weekly (Sundays)
**Trigger:** "run the channel analyst"
**Duration:** ~10–15 minutes
**Purpose:** Study Helmi's channel + competitors. Refresh brand voice. Update competitor tracker in Notion.

---

## Step 1 — Load Config

Read:
- `config/settings.md` — channel handle, Notion IDs
- `config/competitors.md` — competitor channel list
- `config/brand-voice.md` — current brand voice (will be updated)

---

## Step 2 — Analyse Helmi's Channel

Use VidIQ MCP to pull Helmi's channel data:

```
vidiq_channel_stats(channel: "@helmihasan")
vidiq_channel_analytics(channel: "@helmihasan")
vidiq_channel_videos(channel: "@helmihasan", limit: 20)
```

Extract and record:
- Total subscribers, total views, avg views per video
- Top 5 performing videos (views, outlier score vs channel avg)
- Bottom 5 performing videos
- Most common title patterns in top performers
- Thumbnail styles in top performers (text-heavy, face-forward, object-only)
- Hook patterns from top video titles

Calculate channel average views:
```
channel_avg = total_views / total_videos
```

For each of the last 20 videos, calculate:
```
outlier_score = video_views / channel_avg
```

Flag any video with outlier_score > 2.0 as a strong performer.

---

## Step 3 — Analyse Competitor Channels

For each channel in `config/competitors.md` (Tier 1 and Tier 2):

Use VidIQ MCP:
```
vidiq_channel_stats(channel: handle)
vidiq_channel_videos(channel: handle, limit: 10)
vidiq_outliers(channel: handle)
```

For each competitor, record:
- Avg views
- Best performing video in last 30 days (title, views, outlier score)
- Common title formulas
- Thumbnail patterns

---

## Step 4 — Detect Cross-Channel Patterns

Look for patterns that appear across 3+ competitor channels:
- Title formulas (e.g., "How I [verb] [result] in [timeframe]")
- Topic clusters (e.g., multiple channels doing "YouTube SEO" videos)
- Hook structures
- Thumbnail layouts

These patterns indicate high-demand topics worth targeting.

---

## Step 5 — Update Brand Voice

Based on Helmi's top performers, update `config/brand-voice.md`:

- Add any new "hooks that work" observed from top videos
- Update "words Helmi uses" if new catchphrases appear in top performers
- Add any new content pillars that emerged from data

Do NOT remove existing brand voice entries — only add or refine.

Write the updated file with a new timestamp at the bottom.

---

## Step 6 — Update Notion Competitor Tracker

For each Tier 1 competitor, update or create a row in the Notion Competitor Tracker database:

Fields to fill:
- Channel name
- Handle
- Subscribers (from VidIQ)
- Avg views (calculated)
- Best recent video title
- Best recent video views
- Best recent video outlier score
- Thumbnail style
- Notes (1-line summary of their positioning)
- Last updated (today's date)

Use Notion MCP to upsert rows.

---

## Step 7 — Write Analysis Report

Save a report to `logs/channel-analyst-YYYY-MM-DD.md`:

```
# Channel Analyst Report — YYYY-MM-DD

## Helmi's Channel
- Subscribers: X
- Avg views: X
- Top performer: [title] (Xk views, X.Xx outlier score)
- Weakest performer: [title]
- Pattern in top 5: [observation]

## Competitor Summary
For each Tier 1 competitor:
- [Channel]: [best video title] — [views] — [outlier score]

## Cross-Channel Patterns
1. [Pattern 1]
2. [Pattern 2]
3. [Pattern 3]

## Recommended Topics (based on gap analysis)
1. [Topic that competitors are winning on that Helmi hasn't covered]
2. [Topic]
3. [Topic]

## Brand Voice Updates
[What changed, if anything]
```

---

## Output Checklist

- [ ] Channel stats pulled from VidIQ
- [ ] Competitor data pulled for all Tier 1 channels
- [ ] Brand voice file updated
- [ ] Notion competitor tracker updated
- [ ] Analysis report saved to logs/

---

## Notes

- If VidIQ rate-limits, pause and retry for the next competitor
- If a competitor channel handle returns no data, skip and note it in the report
- Focus analysis on videos from the last 30 days for competitor data
- For Helmi's channel, look at all-time top performers as well
