# Agent 2 — Trend Scout

**Runs:** Daily (as part of pipeline)
**Trigger:** "run the trend scout" or called by pipeline
**Duration:** ~5–10 minutes
**Purpose:** Find today's best content opportunity — the outlier video Helmi should remix.

---

## Step 1 — Load Config

Read:
- `config/settings.md` — Notion database IDs
- `config/competitors.md` — competitor channel list

---

## Step 2 — VidIQ Outlier Research

For each Tier 1 and Tier 2 competitor in `config/competitors.md`:

```
vidiq_channel_videos(channel: handle, days: 5)
vidiq_outliers(channel: handle)
```

For each video returned, calculate:
```
outlier_score = video_views / channel_avg_views
```

Filter: keep only videos where outlier_score >= 1.5

Build a raw outlier list with:
- Title
- Channel
- Channel subscriber count (smaller = stronger signal)
- Views
- Outlier score
- URL
- Days since published

**Scoring boost for smaller channels:**
If channel has < 50K subscribers: multiply outlier_score by 1.5
If channel has < 20K subscribers: multiply by 2.0

This surfaces genuine signals from creators punching above weight.

---

## Step 3 — Trending Videos Scan

```
vidiq_trending_videos(category: "business")
vidiq_trend_categories()
```

From the trending list, flag any video that:
- Is from the last 3 days
- Has a topic relevant to Helmi's pillars (YouTube, founders, content strategy, business growth)
- Has not already appeared in the Notion Daily Outliers database

---

## Step 4 — Velio Manual Input (if available)

Ask: "Do you have Velio data to add today? Paste it now, or press Enter to skip."

If data is pasted:
- Parse the Velio outlier list
- Add each entry to the raw outlier list with source: "Velio"
- Apply the same outlier score threshold (>= 1.5)

If skipped: note "Velio: skipped" in today's log.

---

## Step 5 — Rank and Select Top Outlier

Sort raw outlier list by: adjusted_outlier_score (descending)

Select the #1 outlier as TODAY'S OPPORTUNITY.

Criteria for disqualifying an outlier:
- Already covered by Helmi in the last 90 days (check Notion content calendar)
- Off-topic for Helmi's ICA (founders wanting inbound clients)
- Title is a pure listicle with no hook potential

If top outlier is disqualified, move to #2, then #3.

---

## Step 6 — Fetch Transcript (if available)

For the selected top outlier:

```
vidiq_video_transcript(url: outlier_url)
vidiq_video_stats(url: outlier_url)
vidiq_video_comments(url: outlier_url, limit: 20)
```

Extract from transcript:
- The hook (first 60 seconds)
- Key structural sections
- Any quotes or data points worth referencing

Extract from comments:
- Pain points viewers expressed
- Questions they asked
- "I had no idea..." or "This changed how I think about..." moments

---

## Step 7 — Write to Notion Daily Outliers

Add a row to the Notion Daily Outliers database:

| Field | Value |
|-------|-------|
| Date | Today |
| Platform | YouTube |
| Channel | Competitor name |
| Title | Video title |
| Views | View count |
| Outlier Score | Adjusted score |
| URL | Video URL |
| Hook Transcript | First 60 seconds |
| Status | Selected / Backup |
| Passed to Script Writer | No (will be updated by pipeline) |

Add top 3 outliers total (1 selected, 2 backups).

---

## Step 8 — Output Summary

Print a summary:

```
TREND SCOUT — [DATE]

TODAY'S OPPORTUNITY
Title: [title]
Channel: [channel] ([X]K subs)
Views: [X]K | Outlier Score: [X.X]x
URL: [url]
Why this works: [1-sentence reason]

Hook:
"[first line of the video]"

Viewer pain from comments:
- [pain 1]
- [pain 2]
- [pain 3]

BACKUP OPTIONS
1. [title] — [channel] — [score]x
2. [title] — [channel] — [score]x

VELIO: [used / skipped]
SOURCES SCANNED: [X] channels, [X] videos
```

---

## Output Checklist

- [ ] VidIQ scanned for all Tier 1 + Tier 2 competitors
- [ ] Trending videos checked
- [ ] Velio input prompted
- [ ] Top outlier selected and disqualification check passed
- [ ] Transcript + comments fetched
- [ ] Notion Daily Outliers updated
- [ ] Summary printed

---

## Failure Handling

- If VidIQ returns no results for a channel: skip, note in log
- If no outliers found (score >= 1.5 for any video): lower threshold to 1.2 and retry
- If still nothing: flag "no outliers found today" and pass that signal to pipeline (pipeline will skip Script Writer)
- Always write something to Notion, even if it's "no outliers found"
