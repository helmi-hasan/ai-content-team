# Pipeline Runner — Master Orchestration

**Trigger:** "run the daily pipeline" or scheduled by /schedule
**Runs:** Daily at 07:00 AEST (Mon–Fri)
**Duration:** ~25–40 minutes total
**Purpose:** Run all 5 daily agents in sequence. Log results. Handle failures gracefully.

---

## Pre-Flight Check

Before running any agent:

1. Read `config/settings.md` — verify Notion database IDs are filled in
2. Check today's date — do not run if it's a weekend (Sat/Sun) unless manually triggered
3. Check `logs/YYYY-MM-DD.md` — if today's log already exists, ask:
   "Pipeline already ran today. Run again? (yes/no)"
   - If no: stop.
   - If yes: proceed (outputs will be overwritten)

---

## Pipeline Execution

Run agents in this exact order. Each agent has a PASS/FAIL/SKIP status.

---

### STAGE 1 — Trend Scout

**Instruction file:** `agents/02-trend-scout.md`

Read and follow all steps in that file.

**Result outcomes:**
- **PASS:** At least one outlier found with score >= 1.5
- **FAIL:** Error encountered (VidIQ unavailable, Notion write failed)
- **NO SIGNAL:** No outliers found above threshold

Log result: `TREND_SCOUT: [PASS/FAIL/NO SIGNAL] — [top outlier title or error message]`

**Rule:** If FAIL → continue to Stage 4 (skip Script Writer + Thumbnail Designer).
**Rule:** If NO SIGNAL → continue to Stage 4 (skip Script Writer + Thumbnail Designer).
**Rule:** If PASS → continue to Stage 2.

---

### STAGE 2 — Script Writer

**Instruction file:** `agents/03-script-writer.md`
**Prerequisite:** Trend Scout = PASS

Read and follow all steps in that file.
Pass today's top outlier data (title, channel, score, transcript, comment pain points) to the Script Writer.

**Result outcomes:**
- **PASS:** Script file created in outputs/scripts/
- **FAIL:** Error encountered or script could not be generated

Log result: `SCRIPT_WRITER: [PASS/FAIL] — [script title or error]`

**Rule:** If FAIL → continue to Stage 4 (skip Thumbnail Designer).
**Rule:** If PASS → continue to Stage 3.

---

### STAGE 3 — Thumbnail Designer

**Instruction file:** `agents/04-thumbnail-designer.md`
**Prerequisite:** Script Writer = PASS

Read and follow all steps in that file.
Pass today's script title, hook, and outlier URL to the Thumbnail Designer.

**Result outcomes:**
- **PASS:** Thumbnail brief created in outputs/thumbnails/
- **FAIL:** Error encountered

Log result: `THUMBNAIL_DESIGNER: [PASS/FAIL] — [brief file or error]`

---

### STAGE 4 — Daily Reporter

**Instruction file:** `agents/05-daily-reporter.md`
**Always runs.** Collects results from all previous stages.

Read and follow all steps in that file.
Pass today's full status (what ran, what was skipped, what failed) to the reporter.

Log result: `DAILY_REPORTER: [PASS/FAIL] — [email subject or error]`

---

### STAGE 5 — Dashboard

**Instruction file:** `agents/06-dashboard.md`
**Always runs.**

Read and follow all steps in that file.
Generate all 3 HTML files regardless of other stages' outcomes.

Log result: `DASHBOARD: [PASS] — 3 files generated`

---

## Write Today's Log

Save `logs/YYYY-MM-DD.md`:

```markdown
# Pipeline Log — YYYY-MM-DD

**Run time:** HH:MM AEST
**Triggered by:** Schedule / Manual

## Stage Results

| Stage | Status | Detail |
|-------|--------|--------|
| Trend Scout | PASS / FAIL / NO SIGNAL | [outlier title or note] |
| Script Writer | PASS / FAIL / SKIPPED | [script title or note] |
| Thumbnail Designer | PASS / FAIL / SKIPPED | [file path or note] |
| Daily Reporter | PASS / FAIL | [email subject] |
| Dashboard | PASS | 3 files generated |

## Top Outlier
Title: [title]
Channel: [channel]
Score: [X.X]x
URL: [url]

## Script Produced
Title: [title]
File: outputs/scripts/[filename]
Word count: [X]

## Thumbnail Concepts
File: outputs/thumbnails/[filename]
Recommended: Concept [X]

## Errors
[list any errors encountered]

## Velio
[Used / Skipped]

---
*Next run: [tomorrow's date] at 07:00 AEST*
```

---

## Post-Pipeline Summary

After all stages complete, print a final summary to the console:

```
═══════════════════════════════════════
   AI CONTENT TEAM — DAILY PIPELINE
   [DATE] · [TIME] AEST
═══════════════════════════════════════

TREND SCOUT    ✓  [outlier title] ([score]x)
SCRIPT WRITER  ✓  [script title] ([X] words)
THUMBNAILS     ✓  3 concepts ready
DAILY REPORTER ✓  Email draft created
DASHBOARD      ✓  3 HTML files updated

─────────────────────────────────────
YOUR NEXT ACTION:
→ Check your email digest
→ Open dashboard: outputs/dashboard/dashboard.html
→ Record your video

PIPELINE COMPLETE. See you tomorrow.
═══════════════════════════════════════
```

Or if stages were skipped:

```
TREND SCOUT    ○  No strong outliers today (best: [X.X]x)
SCRIPT WRITER  —  Skipped (no outlier)
THUMBNAILS     —  Skipped (no script)
DAILY REPORTER ✓  Email draft created
DASHBOARD      ✓  Updated (no script content)

TODAY: No video to record. Review your content calendar for a backlog item.
```

---

## Error Recovery Rules

1. **VidIQ unavailable:** Log error, continue with web search fallback in Trend Scout
2. **Notion write fails:** Log error, save data to `logs/notion-fallback-YYYY-MM-DD.md`
3. **Script Writer produces < 500 words:** Flag as warning, save anyway, note in report
4. **Mailerlite unavailable:** Save email to `logs/email-YYYY-MM-DD.md`
5. **Any unhandled error:** Log to `logs/errors-YYYY-MM-DD.md`, continue to next stage

Never stop the pipeline entirely unless a catastrophic error prevents logging.

---

## Manual Run Options

To run only specific stages, say:
- "run trend scout only"
- "run script writer only" ← will read today's existing outlier from Notion
- "run thumbnail designer only" ← will read today's existing script
- "run daily reporter only"
- "run dashboard only"
