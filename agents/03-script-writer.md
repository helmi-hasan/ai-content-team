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

Also load Helmi's positioning:
- ICA: service-based founders (coaches, consultants, agency owners)
- Outcome they want: inbound clients from YouTube, without going viral
- Anti-positioning: not for creators chasing views or subscribers

---

## Step 2 — Define the Contrarian One-Liner

Before writing a single word of script, write one sentence that captures the video's entire argument.

Format: "You don't need to [mainstream advice] — you just need to [Helmi's contrarian take]."

This one sentence is the spine of the whole video. Everything else flows back to it.
If you can't write it clearly, the video idea isn't sharp enough yet. Sharpen it.

---

## Step 3 — Define the Specific Outcome

Complete this sentence: "After watching this video, my ideal client will be able to [specific outcome] — so they can attract clients."

**Bad:** "understand YouTube strategy"
**Good:** "know exactly which video format gets founders inbound DMs without going viral"

This outcome governs every word in the script. If a section doesn't serve this outcome, cut it.

---

## Step 4 — Hook 1: Thumbnail & Title (Packaging First)

Generate 5 title options. Each must:
- Be 50–70 characters
- Speak directly to Helmi's ICA (founders, not general creators)
- Be specific enough to pre-qualify viewers
- Follow one of these formats:
  - Contrarian: "Stop [mainstream thing] — do this instead"
  - Story: "I [did X] — here's what I learned"
  - Specific outcome: "How to [achieve result] without [common sacrifice]"
  - Direct address: "If you're a founder doing [X], watch this"
  - Curiosity gap: "[Common belief] is wrong — here's what actually works"

Mark one as the recommended A/B/C test set.

---

## Step 5 — Hook 2: First 30 Seconds

Write the first 30 seconds using this exact structure:

### Problem *(their exact words, not yours)*
State the specific frustration your ICA has — in the language they'd use at 11pm when nobody's watching. Hyper specific. Embarrassingly accurate. Makes them think: "this is literally me."

Bad: "Many founders struggle with their YouTube presence."
Good: "You've been posting for 6 months. Your videos get 200 views. And none of those 200 people have ever asked to work with you."

### Stakes *(cost of inaction)*
What does it cost them to stay stuck? Make it concrete — time, money, missed clients, lost confidence. Emotional but not melodramatic. Show the cost of inaction, not the pain of the past.

### 15s Backstory
One of these formats (use whichever fits the video topic):
*"Before I [my mission], I was [inner conflict]. Then [trigger point] happened, and I realised [insight]. Now I help [ICA] by [transformation]."*

Or use Helmi's default backstory if the topic fits:
*"Hi, I'm Helmi. I burned $15K on YouTube gurus who only taught me to go viral. But when I asked my existing clients, they all found me from my low-view videos where I told a story about my business journey. So I reverse-engineered why that worked — and now on this channel, I help founders, coaches and consultants attract clients from YouTube, without becoming a full-time YouTuber."*

### What They're Going to Get
Connect the insight to the offer. Tell them clearly what transformation this video delivers. Frame it as the shortcut they didn't know existed.

Bad: "So today I created this framework to help people like you."
Good: "I'm going to show you the exact 3-video sequence that got me 8 inbound inquiries in 14 days — and how to build yours this week."

---

## Step 6 — Body: 3–5 Core Points

Each point uses this structure: **Mirror → Stakes → Aha Moment → Bridge → Teaching → Re-hook**

### MIRROR
Make the audience feel understood. Name their inner state — not just the external situation. What are they thinking? What are they feeling? What have they already tried that hasn't worked?

Aim for: "this person is in my head."

### STAKES
What does it cost them to stay in this pattern? Be specific. Connect it to their dream outcome (inbound clients, trust, credibility).

### AHA MOMENT
The insight that reframes the problem. This is the belief-breaker — the moment where they see the situation differently. Not a tip. A shift.

### THE BRIDGE
Connect Helmi's personal experience or a client story to the insight. Give it a time, place, and specific detail. "A client said one sentence that changed how I think about this" beats "I realised eventually."

### TEACHING
The practical takeaway. One specific thing they can do differently after watching this point. Frame it as: "Before your next video, do this one thing..."

### RE-HOOK
End each body point with either:
1. A 2-way conversation prompt: "So which type are you? [Option A] or [Option B]? Comment below."
2. A tease for the next point: "Here's the part nobody tells you about [next step]."

---

## Step 7 — CTA

Three parts:

1. **Callback** — Summarise the core teaching in 2–3 sentences. Not a recap — a restatement of the insight in a new way.

2. **Lead magnet bridge** — Connect to Helmi's offer or free resource. Frame it as the logical next step for someone who found this video useful.
   "If you want to go further with this, [resource] in the description gives you [specific thing]. It takes [time] and it's the difference between [before] and [after]."

3. **Next video** — Recommend a specific related video topic (or actual video if known).
   "And if you're trying to figure out [related problem], watch this next. I'll put it right here."

---

## Step 8 — Create Notion Script Page

Create a new page inside the AI Content Team hub (parent: `3676a1eb-2418-8107-bb8e-e336526ca08b`) with:

Title: `📝 [Recommended Title A] — [YYYY-MM-DD]`

Content structure in Notion:

```
**Source outlier:** [channel] — [outlier title] — [score]x
**Contrarian one-liner:** [the one sentence]
**Specific outcome:** [what they'll be able to do]
**Estimated runtime:** ~X minutes

---

# TITLE OPTIONS
A: [title]
B: [title]
C: [title]

---

# HOOK 2 — FIRST 30 SECONDS

**Problem:** [written out]
**Stakes:** [written out]
**Backstory:** [written out]
**What they get:** [written out]

---

# BODY

## Point 1: [heading]
**MIRROR** — [text]
**STAKES** — [text]
**AHA MOMENT** — [text]
**THE BRIDGE** — [text]
**TEACHINGS** — [text]
*Re-hook: [text]*

## Point 2: [heading]
[same structure]

## Point 3: [heading]
[same structure]

---

# CTA
[callback + lead magnet bridge + next video]

---

# THUMBNAIL BRIEF
[added by Thumbnail Designer agent]
```

Format for reading aloud — short paragraphs, clear breaks. This page IS the teleprompter.

After creating, note the Notion URL.

---

## Step 9 — Update Notion Content Calendar

Create a new row with:
- Date: today
- Title: selected title option A
- Hook: first sentence of the Problem section
- Script Status: Ready
- Thumbnail Status: Pending
- Publish Status: Not Started
- Script File: [Notion script page URL]
- Source Outlier: [channel] — [video title]

---

## Step 10 — Output Summary

Print:

```
SCRIPT WRITER — [DATE]

CONTRARIAN ONE-LINER: [one sentence]
RECOMMENDED TITLE: [title A]
ESTIMATED RUNTIME: ~X minutes

HOOK PREVIEW:
"[first 2 sentences of Problem section]"

BODY: [X] points
SAVED TO: [Notion URL]
NOTION CALENDAR: Updated
```

---

## Script Quality Rules

The script passes if:
- The contrarian one-liner is so clear you could put it on a billboard
- A founder reads the Problem section and thinks "this is literally me"
- Each body point has a real story or specific example — not just advice
- The Mirror section names a feeling, not just a situation
- The CTA connects the video's insight to Helmi's offer naturally
- Someone could read this cold and record it without rewriting

## Voice Rules

- First person ("I", "my clients", "here's what happened to me")
- Warm and direct — like a smart friend, not a course instructor
- Specific numbers and details wherever possible ("6 months", "200 views", "$15K")
- No filler openers: "So today we're going to...", "In this video I'll show you..."
- No guru framing: "viral", "passive income", "hustle", "leverage"
- "Founders" not "entrepreneurs" or "business owners"
- "Inbound clients" not "leads"
