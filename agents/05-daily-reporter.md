# Agent 5 — Daily Reporter

**Runs:** Daily (always runs, regardless of other agents' outcomes)
**Trigger:** "run the daily reporter" or called by pipeline
**Duration:** ~3–5 minutes
**Purpose:** Send Helmi a phone-scannable morning digest with today's opportunity and system status.

---

## Step 1 — Gather Today's Data

Read from `logs/YYYY-MM-DD.md` (written by pipeline runner):
- Trend Scout result (top outlier or "no outliers found")
- Script Writer result (script ready or skipped)
- Thumbnail Designer result (concepts ready or skipped)
- Any errors encountered

Read from today's output files:
- `outputs/scripts/YYYY-MM-DD-[slug].md` — if it exists
- `outputs/thumbnails/YYYY-MM-DD-[slug].md` — if it exists

Read from Notion Content Calendar:
- Today's row (title, hook, script status, thumbnail status)

---

## Step 2 — Compose the Email

**Subject line format:**
`[DATE] — Your content brief is ready` (if script exists)
`[DATE] — No strong outlier today` (if no script)

**Email body structure:**

---

**TODAY'S VIDEO** *(only if script was produced)*

**[VIDEO TITLE]**

Hook:
> [first 2–3 sentences of the selected hook]

Script: [X] words (~[X] minutes) — ready to record
Thumbnails: [X] concepts ready

[Read full script →] [path to file or Notion link]

---

**TOP OUTLIERS FOUND**

1. **[title]** — [channel] — [score]x outlier
   [URL]

2. **[title]** — [channel] — [score]x outlier
   [URL]

3. **[title]** — [channel] — [score]x outlier
   [URL]

*(or: "No strong outliers found today (best score: X.Xx). Pipeline paused script generation.")*

---

**SYSTEM STATUS**

| Agent | Status |
|-------|--------|
| Trend Scout | ✓ Complete / ✗ No outliers / ✗ Error |
| Script Writer | ✓ Complete / — Skipped / ✗ Error |
| Thumbnail Designer | ✓ Complete / — Skipped / ✗ Error |
| Dashboard | ✓ Updated |

---

**QUICK LINKS**
- [Open dashboard →]
- [Open teleprompter →]
- [View content calendar in Notion →]

---

*AI Content Team · helmi@helmihasan.com*

---

## Step 3 — Send via Mailerlite

Use the Mailerlite MCP to create a campaign draft:

```
create_campaign(
  subject: "[DATE] — Your content brief is ready",
  from_name: "Helmi AI Team",
  from_email: "helmi@helmihasan.com",
  to_email: "helmi@helmihasan.com",
  body: [email body]
)
```

Do NOT send automatically — create as a draft so Helmi can review it if needed.

If Mailerlite is not available: write the email to `logs/email-YYYY-MM-DD.md` and print it to the console.

---

## Step 4 — Output Summary

Print:

```
DAILY REPORTER — [DATE]

Email draft created: [subject line]
Sent to: helmi@helmihasan.com
Status: Draft (review in Mailerlite before sending)

— OR —

Email draft saved to: logs/email-YYYY-MM-DD.md
(Mailerlite unavailable)
```

---

## Output Checklist

- [ ] Data gathered from logs and output files
- [ ] Email body composed
- [ ] Mailerlite draft created (or fallback file saved)

---

## Email Design Rules

- Maximum 250 words in the email body
- No paragraphs longer than 3 lines
- Most important content in the first 100 words (above the fold on mobile)
- No marketing language — this is a briefing, not a campaign
- Tone: like a smart assistant leaving a note on the desk
