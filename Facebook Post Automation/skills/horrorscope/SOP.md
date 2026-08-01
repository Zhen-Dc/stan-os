# Horrorscope SOP

## Purpose

Use this SOP to create Facebook-ready image posts for the faceless page `Horrorscope`. The page is about dark psychology, paranormal fear, urban legends, folklore, uncanny rooms, and reality-bending images that feel like they might be real.

The final result must be image plus caption only. No video. No hashtags. No text on the image.

## Output Target

Local root:

```text
C:\Users\DELL\Master Project\Stan OS\AIS-OS\Facebook Post Automation
```

Asset root:

```text
assets/Horrorscope
```

Prompt JSON:

```text
prompts/horrorscope-production-prompt.json
```

Skill folder:

```text
skills/horrorscope
```

Installed Codex skill:

```text
C:\Users\DELL\.codex\skills\horrorscope
```

## Daily Batch Size

Create 5 posts per day.

Each post must have 3 variations.

Each variation must have:

```text
variation-N.png
variation-N-caption.txt
```

## Folder Structure

Use this exact structure:

```text
assets/Horrorscope/YYYY-MM-DD/
  Topic Title/
    variation-1.png
    variation-1-caption.txt
    variation-2.png
    variation-2-caption.txt
    variation-3.png
    variation-3-caption.txt
  _raw-generated/
    Topic Title/
      variation-1.png
      variation-2.png
      variation-3.png
  _qa-contact-sheet.jpg
  QA-report.md
```

Use title case for topic folders.

Examples:

```text
The Face in the Static
The Thing Beside the Bed
The Mirror That Arrived Late
The Room That Watches Back
The Village That Locks Its Doors at Dusk
```

## Tracking Files

Maintain these files:

```text
assets/Horrorscope/created-topics.json
assets/Horrorscope/daily-log.jsonl
```

`created-topics.json` tracks topics already generated.

`daily-log.jsonl` tracks each batch date, topic, pillar, files created, QA result, and Drive upload if any.

## Content Pillars

Use a balanced mix of:

1. Dark psychology
2. Paranormal fear
3. Urban legends
4. Folklore from different countries
5. Reality-bending images
6. Liminal spaces
7. Haunted rooms and objects
8. Creepy brain or perception facts
9. True-crime-adjacent mystery without graphic content

## Topic Selection Rules

A good topic should:

- Be understandable in one line.
- Suggest a strong image.
- Suggest a strong comment question.
- Feel scary because it might be possible.
- Avoid needing gore, weapons, or visible harm.

Do not repeat topics too soon.

Do not use real public figures.

Do not use real victim imagery.

## Image Style Rule

The image must not look perfect.

It should look like a scared person took a quick phone photo.

Use when appropriate:

- crooked angle
- imperfect framing
- motion blur
- low-light sensor noise
- partial obstruction
- door crack viewpoint for house/interior fear scenes
- window crack viewpoint for house/interior fear scenes
- curtain edge in foreground for hidden-room scenes
- mirror reflection caught by accident for mirror/reflection scenes
- hallway corner viewpoint for corridor scenes
- distant zoom or blocked foreground for outdoor folklore scenes
- degraded CCTV/archive-photo look for evidence-style posts
- off-center subject
- underexposed shadows
- too much empty space in a natural way

Avoid:

- perfect cinematic poster
- centered subject every time
- polished horror movie marketing image
- clean studio lighting
- glossy AI fantasy look
- staged symmetrical room
- fake text or signs

## Image Generation Template

Use this template for every image:

```text
Use case: photorealistic-natural
Asset type: Facebook Horrorscope post, 3:4 portrait, no text
Primary request: [Topic title], variation [1-3].
Scene/backdrop: [Specific place/object].
Subject: [Safe unsettling subject].
Camera and framing: Unprofessional frightened handheld phone snapshot; imperfect composition; [specific accidental angle]; off-center framing; slight motion blur or low-light noise; not a planned poster.
Style/medium: realistic phone photography, dark psychological horror, subtle supernatural dread, original and non-generic.
Lighting/mood: low light, weak practical light, underexposed shadows, quiet dread.
Color palette: [topic-specific colors].
Constraints: no text, no letters, no numbers, no watermark, no social UI, no blood, no gore, no dead bodies, no weapons, no explicit violence, no injury, no children, no public figures. Avoid perfect centered poster composition. Make it feel like a believable imperfect image captured in the moment; use cracked-window or door-crack angles only when they fit the scene.
```

## Variation Rules

Variation 1 should be the clearest version of the concept.

Variation 2 should change the camera position.

Variation 3 should change the psychological angle or reveal.

Example for a haunted room:

- Variation 1: taken through a door crack.
- Variation 2: taken from behind a curtain.
- Variation 3: taken from a mirror reflection with slight motion blur.

## Caption Rules

Captions should be creepy, short, and easy to comment on.

They can sound like:

- a narrator telling a scary story
- a dark psychology explainer
- a mysterious warning
- a creepy observation

They should feel factual, but never invent verified facts.

If a post is fictional or folklore-based, do not claim it is proven real.

Use this structure:

```text
[Hook: one disturbing idea or observation.]
[Build: why it feels possible or why the brain reacts to it.]
[Image tie-in: connect the fear to what the viewer is seeing.]
[Engagement question.]
```

Engagement endings:

```text
What did you notice first?
Would you sleep here?
Do you believe this?
Have you ever experienced this?
Look again. What changed?
Would you enter this room?
```

No hashtags.

## Monetization Safety Rules

Allowed:

- fear
- suspense
- supernatural dread
- paranormal topics
- folklore
- dark psychology
- creepy rooms
- implied presence
- symbolic occult or ritual mood when non-graphic
- true-crime-adjacent unease when non-graphic

Not allowed in images:

- blood
- gore
- dead bodies
- weapons
- explicit violence
- injury
- torture
- self-harm imagery
- children in danger
- sexual content
- real public figures
- real victims
- crime scene photos
- hate symbols

Not allowed in captions:

- graphic violence
- instructions for harm
- killer worship
- unverified accusations
- fake verified claims
- medical diagnosis presented as fact
- sensational real-crime claims

## QA Process

Run QA every time.

Step 1: File count

Confirm each topic has:

```text
3 PNG files
3 TXT caption files
```

Step 2: Ratio

Confirm every final image is 3:4.

If the generator returns 2:3 or another portrait ratio, do not crop important content. Expand the canvas to 3:4 using blurred edge extension. Save originals under `_raw-generated`.

Step 3: Contact sheet

Create:

```text
_qa-contact-sheet.jpg
```

The contact sheet must show all 15 images in one file.

Step 4: Manual visual review

Inspect the contact sheet for:

- text in image
- watermark
- logo
- social UI
- gore
- weapons
- dead bodies
- explicit violence
- children
- public figures
- too-perfect poster look

Step 5: Captions

Open or sample captions and confirm:

- TXT only
- no hashtags
- creepy but safe
- matches the image topic
- ends with an engagement question or comment prompt

Step 6: Report

Write:

```text
QA-report.md
```

The report must include:

- mechanical checks
- aspect ratio checks
- visual safety checks
- caption checks
- notes about any regeneration or normalization

## Google Drive Push

When pushing the workflow to Google Drive:

1. Search for `Master` folder in Google Drive.
2. If it does not exist, create it at Drive root.
3. Create `Horrorscope Workflow` inside `Master`.
4. Create local ZIP packages:
   - `horrorscope-workflow-package.zip`
   - optional latest date batch ZIP
5. Upload the ZIP package to the Drive folder.
6. Upload key standalone files when useful:
   - `prompts/horrorscope-production-prompt.json`
   - `skills/horrorscope/SKILL.md`
   - `skills/horrorscope/SOP.md`
7. Verify by listing the Drive folder.
8. Return the Drive folder link.

## Final Response Checklist

Before final response, include:

- local prompt JSON path
- local skill path
- local SOP path
- QA status if images were generated
- Google Drive folder link if uploaded
- ZIP path if created

