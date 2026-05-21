# Agent 3 — Script Writer

**Runs:** Daily (after Trend Scout)
**Trigger:** "run the script writer" or called by pipeline
**Prerequisite:** Trend Scout must have found a usable outlier
**Duration:** ~10–15 minutes
**Purpose:** Write a full camera-ready script in Helmi's voice, remixed from today's outlier.

---

## Step 1 — Load Context

Read:
- `config/brand-voice.md` — Helmi's voice, ICA, tone
- `config/settings.md` — Notion database IDs

Load today's outlier from Notion Daily Outliers:
- Title, channel, views, transcript, viewer pain points from comments

Also load Helmi's positioning via the `positioning` skill context:
- ICA definition
- Method name
- Anti-positioning
- Channel narrative

---

## Step 2 — Generate 5 Hook Options

Based on today's outlier topic, generate 5 hook variations using Helmi's voice.

Each hook must follow the 7-Step Hook Framework:
1. Pattern interrupt (unexpected statement or visual cue)
2. Identify the viewer ("If you're a founder who...")
3. Name the problem (specific, not generic)
4. Introduce the opportunity (reframe)
5. Promise the result ("By the end of this video you'll have...")
6. Tease the evidence ("I used this exact approach with [X] clients...")
7. CTA to keep watching ("Let me show you how.")

Hook types to vary across 5 options:
- Contrarian open: challenges mainstream belief
- Story open: starts mid-scene, past tense
- Question open: poses the painful question the ICA asks themselves
- Data open: surprising stat or number
- Bold claim open: makes a specific promise upfront

Format each hook as:
```
HOOK [number] — [type]
[Full hook text, spoken naturally, 90–120 words]
```

---

## Step 3 — Select Best Hook

Evaluate each hook against:
- Does it speak directly to Helmi's ICA (service-based founders)?
- Does it feel like something Helmi would actually say?
- Does it create enough curiosity without being clickbait?
- Is it specific enough to pre-qualify viewers?

Select the strongest hook. Note why.

---

## Step 4 — Write the Full Script

Structure:
```
[HOOK] — selected hook from Step 3

[BRIDGE] — 2–3 sentences connecting hook to body
Establish Helmi's credibility on this topic briefly.

[BODY — Section 1]
Main point
Supporting story or example (from Helmi's experience or client results)
Analogy (make the concept concrete)
B-roll cue: [describe visual]
Transition line

[BODY — Section 2]
(same structure)

[BODY — Section 3]
(same structure)

[BODY — Section 4 — optional]
(same structure)

[CTA]
Subscribe line: direct, specific, not generic
Recommended next video: [suggest a related topic]
```

**Script rules:**
- Write in first person, Helmi's voice (warm, direct, no fluff)
- Each section should be 150–250 words spoken
- Total script: 1,000–1,800 words (8–14 mins at Helmi's pace)
- No filler phrases: "So today we're going to...", "Without further ado..."
- B-roll cues in brackets: [show screen recording], [cut to whiteboard], [show result screenshot]
- Paragraph breaks = natural pause points when reading on teleprompter

---

## Step 5 — Generate Title Options

Write 5 title options for this video. Titles should:
- Be 50–70 characters
- Front-load the most powerful word or concept
- Match Helmi's voice (no clickbait, no "guru" framing)
- Speak to the ICA pain or opportunity

Include at least:
- 1 "How I" title
- 1 question title
- 1 contrarian/surprising claim title
- 1 "X reasons/steps" title
- 1 benefit-forward title

---

## Step 6 — Save Outputs

**Save script as markdown:**
File: `outputs/scripts/YYYY-MM-DD-[slug].md`

```markdown
# [Selected Title]

**Date:** YYYY-MM-DD
**Outlier Source:** [channel] — [title] — [outlier score]x
**Hook Type:** [type]
**Estimated Runtime:** ~X minutes

---

## All Hooks (5 options)
[all 5 hooks]

---

## Selected Hook
[selected hook + reason]

---

## Full Script
[full script]

---

## Title Options
1. [title]
2. [title]
3. [title]
4. [title]
5. [title]
```

**Update Notion Content Calendar:**
Create a new row with:
- Date: today
- Title: selected title option #1
- Hook: first line of selected hook
- Script Status: Ready
- Thumbnail Status: Pending
- Publish Status: Not started
- Script File: link to outputs/scripts/ file path
- Source Outlier: [channel] — [video title]

---

## Step 7 — Output Summary

Print:

```
SCRIPT WRITER — [DATE]

TOPIC: [remixed topic]
SELECTED HOOK TYPE: [type]
TITLE: [recommended title]

HOOK PREVIEW:
"[first 2 sentences of selected hook]"

SCRIPT: [X] words (~[X] minutes)
SECTIONS: [X] body sections

SAVED TO: outputs/scripts/[filename]
NOTION: Content Calendar updated

TITLE OPTIONS:
1. [title]
2. [title]
3. [title]
4. [title]
5. [title]
```

---

## Output Checklist

- [ ] 5 hooks generated
- [ ] Best hook selected with rationale
- [ ] Full script written (1,000–1,800 words)
- [ ] 5 title options written
- [ ] Script saved to outputs/scripts/
- [ ] Notion content calendar updated

---

## Script Quality Rules

The script is good if:
- A founder watches the hook and thinks "that's me"
- The body delivers a specific, actionable insight (not generic tips)
- Helmi's story or client story is used as evidence, not just assertion
- The CTA recommends a next step that keeps the viewer in Helmi's world
- Someone could read the script cold and record it without any rewriting
