# Settings

## Channel

```
YOUTUBE_CHANNEL_HANDLE=@helmihasan
YOUTUBE_CHANNEL_URL=https://www.youtube.com/@helmihasan
```

## Notion Database IDs

Fill in after creating Notion pages (or paste existing IDs if they already exist).

```
NOTION_DAILY_OUTLIERS_DB=PASTE_ID_HERE
NOTION_CONTENT_CALENDAR_DB=PASTE_ID_HERE
NOTION_COMPETITOR_TRACKER_DB=PASTE_ID_HERE
NOTION_BRAND_VOICE_PAGE=PASTE_ID_HERE
```

To get a Notion database ID: open the database in Notion → copy URL → the ID is the
32-character string before the `?` (format: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx)

## Pipeline Schedule

```
RUN_TIME=07:00 AEST
RUN_DAYS=Monday,Tuesday,Wednesday,Thursday,Friday
```

## Output Preferences

```
SCRIPT_FORMAT=markdown
THUMBNAIL_CONCEPTS=3
SCRIPT_PREVIEW_LINES=10
```

## Email (Daily Reporter)

```
REPORT_EMAIL=helmi@helmihasan.com
MAILERLITE_GROUP=Content Team Reports
```

## VidIQ

Connected via MCP — no API key needed.
Competitor channels are pulled from `config/competitors.md`.

## Velio

Not yet connected via MCP. Manual paste step is included in the Trend Scout agent.
