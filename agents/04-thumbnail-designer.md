# Agent 4 — Thumbnail Designer

**Runs:** Daily (after Script Writer)
**Trigger:** "run the thumbnail designer" or called by pipeline
**Prerequisite:** Script Writer must have produced a script
**Duration:** ~5–8 minutes
**Purpose:** Generate 3 thumbnail concepts for today's video and produce Canva design prompts.

---

## Step 1 — Load Context

Read today's script from `outputs/scripts/YYYY-MM-DD-[slug].md`:
- Selected title
- Hook (to understand the emotional angle)
- Body (to understand the main promise)

Read `config/brand-voice.md`:
- ICA definition
- Tone
- What founders respond to

---

## Step 2 — Analyse Today's Outlier Thumbnail

From the Trend Scout's selected outlier URL, fetch the thumbnail:
```
vidiq_video_watch(url: outlier_url)
```

Analyse the reference thumbnail for:
- **Layout:** text-heavy / face-forward / split / object-only / minimal
- **Emotion:** surprised / confident / concerned / excited / neutral
- **Text:** headline on thumbnail (if any) — size, position, colour contrast
- **Background:** busy / clean / gradient / solid
- **Face placement:** left / right / centre / not present
- **Number/badge:** does it show a number? (e.g., "3 mistakes", "$10K")

Note: "What makes this thumbnail stop the scroll?"

---

## Step 3 — Generate 3 Thumbnail Concepts

Create 3 distinct concepts — each taking a different approach to the same topic.

For each concept, write:

```
CONCEPT [A/B/C]
Approach: [e.g., "contrarian face + bold text"]
Layout: [describe composition]
Helmi's expression: [surprised / pointing / direct eye contact / arms crossed]
Background: [colour, texture, or scene]
Text on thumbnail: "[exact words to overlay]"
Text style: [large/small, colour, placement]
Emotion conveyed: [what the viewer should feel in 0.5 seconds]
Click trigger: [why someone stops scrolling for this]
```

**Concept variety rules:**
- Concept A: Face-forward, high emotion, short text (3–5 words max)
- Concept B: Text-dominant, graphic/bold, face optional or secondary
- Concept C: Curiosity-gap approach — shows something partially obscured, question implied

**Brand constraints:**
- Helmi's face should be present in at least 2 of 3 concepts
- Colours should feel premium but not corporate (avoid pure corporate blue/grey)
- No "guru" red-arrow-pointing-at-face clichés
- Text must be legible at mobile size (thumbnail at 120px wide)

---

## Step 4 — Generate Canva Prompts

For each concept, write a ready-to-paste Canva prompt:

```
CANVA PROMPT — Concept [A/B/C]

Create a YouTube thumbnail with the following:
- Dimensions: 1280 x 720 px
- Background: [description]
- Main image: Photo of [Helmi's expression] — [placement in frame]
- Overlay text: "[text]" — font: bold sans-serif, size: large, colour: [colour], position: [left/right/centre]
- Accent element: [badge / arrow / highlight box / none]
- Overall feel: [energetic / clean / serious / surprising]
```

---

## Step 5 — Evaluate Concepts

Score each concept against Helmi's audience:

For each concept, answer:
1. Would a founder with 3 minutes to scroll stop for this? (Y/N + why)
2. Does the thumbnail deliver on the video's promise? (Y/N)
3. Does it look like something Helmi would actually post? (Y/N)

Recommend: "Start with Concept [X] for A/B testing."

---

## Step 6 — Save Outputs

**Save thumbnail brief:**
File: `outputs/thumbnails/YYYY-MM-DD-[slug].md`

```markdown
# Thumbnail Brief — [Video Title]

**Date:** YYYY-MM-DD
**Reference Outlier:** [channel] — [video title]

---

## Reference Thumbnail Analysis
[layout, emotion, text, background, face placement observations]

---

## Concept A
[full concept description]

### Canva Prompt A
[prompt]

---

## Concept B
[full concept description]

### Canva Prompt B
[prompt]

---

## Concept C
[full concept description]

### Canva Prompt C
[prompt]

---

## Recommendation
Start with Concept [X] because [reason].
```

**Append Thumbnail Brief to the Notion Script Page:**

Find today's script page in Notion (created by Script Writer — search for today's date in the hub).
Append this section to the bottom of that page:

```
---

# THUMBNAIL BRIEF

**Reference outlier:** [channel] — [video title]
**Reference thumbnail:** [layout / emotion / text observed]

---

## Concept A — [one-line description]
[full concept description]

**Canva prompt:**
[full Canva prompt, ready to paste]

---

## Concept B — [one-line description]
[full concept description]

**Canva prompt:**
[full Canva prompt, ready to paste]

---

## Concept C — [one-line description]
[full concept description]

**Canva prompt:**
[full Canva prompt, ready to paste]

---

**Recommendation:** Start with Concept [X] — [reason in one sentence]
```

**Update Notion Content Calendar:**
Find today's row and update:
- Thumbnail Status: Concepts Ready

---

## Step 7 — Output Summary

Print:

```
THUMBNAIL DESIGNER — [DATE]

VIDEO: [title]

CONCEPT A: [one-line description]
CONCEPT B: [one-line description]
CONCEPT C: [one-line description]

RECOMMENDATION: Start with Concept [X]

SAVED TO: outputs/thumbnails/[filename]
NOTION: Updated
```

---

## Output Checklist

- [ ] Reference thumbnail analysed
- [ ] 3 concepts generated (A = face, B = text, C = curiosity)
- [ ] 3 Canva prompts written
- [ ] Concepts evaluated + recommendation made
- [ ] Brief saved to outputs/thumbnails/
- [ ] Notion content calendar updated

---

## Notes

- If Helmi doesn't have a matching headshot expression, note which expression to capture
- Canva prompts should be usable as-is — no editing required before pasting
- All 3 concepts should feel like different answers to the same question, not variations of one idea
