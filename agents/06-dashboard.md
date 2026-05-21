# Agent 6 — Dashboard

**Runs:** Daily (always runs)
**Trigger:** "run the dashboard" or called by pipeline
**Duration:** ~3–5 minutes
**Purpose:** Generate 3 local HTML tools — dashboard, teleprompter, recording cheat sheet.

---

## Step 1 — Load Today's Data

Read:
- `outputs/scripts/YYYY-MM-DD-[slug].md` — script (if exists)
- `outputs/thumbnails/YYYY-MM-DD-[slug].md` — thumbnail concepts (if exists)
- `logs/YYYY-MM-DD.md` — pipeline status

---

## Step 2 — Generate dashboard.html

Save to `outputs/dashboard/dashboard.html`

Content:
```html
<!DOCTYPE html>
<html>
<head>
  <title>Content Dashboard — [DATE]</title>
  <style>
    /* Clean, dark-mode friendly, mobile-first */
    body { font-family: -apple-system, sans-serif; max-width: 800px; margin: 0 auto; padding: 20px; background: #0f0f0f; color: #f0f0f0; }
    h1 { font-size: 1.4rem; border-bottom: 1px solid #333; padding-bottom: 10px; }
    .card { background: #1a1a1a; border-radius: 8px; padding: 16px; margin: 12px 0; }
    .status-ok { color: #4ade80; }
    .status-skip { color: #94a3b8; }
    .status-error { color: #f87171; }
    .hook { font-size: 1.1rem; line-height: 1.6; font-style: italic; border-left: 3px solid #6366f1; padding-left: 12px; }
    a { color: #818cf8; }
  </style>
</head>
<body>
  <h1>Content Dashboard — [DATE]</h1>

  <div class="card">
    <h2>Today's Video</h2>
    <p><strong>[VIDEO TITLE or "No video today"]</strong></p>
    <div class="hook">[HOOK PREVIEW — first 2 sentences]</div>
    <p>Script: [X words, ~X mins] | Thumbnails: [X concepts]</p>
  </div>

  <div class="card">
    <h2>Top Outlier</h2>
    <p><strong>[OUTLIER TITLE]</strong></p>
    <p>[CHANNEL] · [VIEWS] views · [SCORE]x outlier</p>
    <p><a href="[URL]" target="_blank">Watch →</a></p>
  </div>

  <div class="card">
    <h2>Tools</h2>
    <p><a href="teleprompter.html">📺 Open Teleprompter</a></p>
    <p><a href="recording.html">🎬 Recording Cheat Sheet</a></p>
  </div>

  <div class="card">
    <h2>Pipeline Status</h2>
    <p class="[status-class]">Trend Scout: [status]</p>
    <p class="[status-class]">Script Writer: [status]</p>
    <p class="[status-class]">Thumbnail Designer: [status]</p>
    <p class="[status-class]">Daily Reporter: [status]</p>
  </div>
</body>
</html>
```

Replace all `[PLACEHOLDERS]` with actual data from today's outputs.

---

## Step 3 — Generate teleprompter.html

Save to `outputs/dashboard/teleprompter.html`

This is a fullscreen scrolling script reader.

Content:
```html
<!DOCTYPE html>
<html>
<head>
  <title>Teleprompter — [VIDEO TITLE]</title>
  <style>
    body { background: #000; color: #fff; font-family: 'Georgia', serif; font-size: 2rem; line-height: 1.8; padding: 60px 15%; }
    .controls { position: fixed; bottom: 20px; right: 20px; display: flex; gap: 10px; }
    button { background: #333; color: #fff; border: none; padding: 10px 20px; border-radius: 6px; cursor: pointer; font-size: 1rem; }
    .section-break { color: #555; font-size: 1rem; margin: 40px 0 20px; text-transform: uppercase; letter-spacing: 0.1em; }
    p { margin-bottom: 1.5rem; }
  </style>
</head>
<body>
  [SCRIPT CONTENT — formatted as paragraphs]
  [B-roll cues displayed as: <span class="section-break">[B-ROLL: description]</span>]

  <div class="controls">
    <button onclick="document.body.style.fontSize = (parseFloat(getComputedStyle(document.body).fontSize) - 2) + 'px'">A-</button>
    <button onclick="document.body.style.fontSize = (parseFloat(getComputedStyle(document.body).fontSize) + 2) + 'px'">A+</button>
  </div>
</body>
</html>
```

If no script was produced today: show "No script generated today." in the centre.

---

## Step 4 — Generate recording.html

Save to `outputs/dashboard/recording.html`

A one-page cheat sheet Helmi can glance at while recording.

Content:
```html
<!DOCTYPE html>
<html>
<head>
  <title>Recording Cheat Sheet — [DATE]</title>
  <style>
    body { font-family: -apple-system, sans-serif; max-width: 600px; margin: 0 auto; padding: 20px; }
    h2 { color: #6366f1; border-bottom: 1px solid #eee; }
    .hook { font-size: 1.2rem; font-weight: bold; background: #f8f8ff; padding: 12px; border-radius: 6px; }
    .section { margin: 16px 0; }
    .key-point { background: #f0f4ff; padding: 8px 12px; border-radius: 4px; margin: 6px 0; }
  </style>
</head>
<body>
  <h1>[VIDEO TITLE]</h1>
  <p><em>[DATE] · ~[X] mins</em></p>

  <h2>Hook (say this first)</h2>
  <div class="hook">[SELECTED HOOK — first 2–3 sentences only]</div>

  <h2>Body — Key Points</h2>
  <div class="section">
    <strong>Section 1:</strong>
    <div class="key-point">[main point]</div>
    <div class="key-point">[key analogy or story]</div>
  </div>
  [repeat for each body section]

  <h2>CTA</h2>
  <div class="key-point">[CTA line]</div>
  <div class="key-point">Next video recommendation: [topic]</div>

  <h2>Thumbnail Reminder</h2>
  <p>Concept A expression: [expression needed]</p>
  <p>Text to show: "[thumbnail text]"</p>
</body>
</html>
```

---

## Step 5 — Output Summary

Print:

```
DASHBOARD — [DATE]

Files generated:
- outputs/dashboard/dashboard.html
- outputs/dashboard/teleprompter.html
- outputs/dashboard/recording.html

Open dashboard: file:///Users/helmihasan/Documents/Claude/Projects/AI-Content-Team/outputs/dashboard/dashboard.html
```

---

## Output Checklist

- [ ] dashboard.html generated with today's data
- [ ] teleprompter.html generated with full script
- [ ] recording.html generated with cheat sheet
- [ ] All files saved to outputs/dashboard/

---

## Notes

- If no script exists, teleprompter.html should display "No script today" gracefully
- HTML must be valid and render correctly when opened locally (file:// URL)
- No external dependencies (no CDN links) — all styles inline
- Files are overwritten each day — they always show today's content
