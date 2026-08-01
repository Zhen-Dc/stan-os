---
name: horrorscope
description: Create and QA Facebook image-only horror/dark-psychology batches for the Horrorscope page. Use when generating, organizing, captioning, prompting, validating, or uploading Horrorscope assets: unsettling phone-photo style images, creepy captions, 5-post daily batches, 3 variations per post, monetization-safe horror, folder tracking, QA contact sheets, and Google Drive handoff.
---

# Horrorscope

Use this skill to produce Facebook-ready image posts for the `Horrorscope` page.

## Non-Negotiables

- Work in the user's correct project unless they specify another path: `C:\Users\DELL\Master Project\Stan OS\AIS-OS\Facebook Post Automation`.
- Save all post assets under `assets/Horrorscope/YYYY-MM-DD/Topic Title/`.
- Produce 5 topics per batch unless the user requests a different count.
- Produce exactly 3 image variations and 3 caption files per topic.
- Use 3:4 portrait as the default final image ratio.
- Put no text inside images: no words, letters, numbers, logo, watermark, or social UI.
- Keep horror monetization-safe: no blood, gore, dead bodies, weapons, explicit violence, injury, torture, self-harm imagery, sexual content, or real children in danger.
- Do not use real public figures or real victim imagery.
- Always run QA before final delivery.

## Required Style

Horrorscope images must look like believable imperfect evidence, not polished posters. Choose the camera style based on the subject instead of forcing the same angle on every image.

Prefer:
- frightened handheld phone photos
- accidental angles
- tilted framing
- motion blur from shaking hands
- low-light phone noise
- situational partial views: cracked door or cracked window for house/interior scenes, curtain/furniture gaps for hidden-room scenes, accidental reflections for mirror scenes, distant zoom or blocked foreground for outdoor folklore scenes
- off-center subjects
- underexposed rooms
- scenes that feel snapped quickly before the person ran away

Avoid:
- perfect centered poster composition
- clean studio lighting
- symmetrical horror key art
- glossy marketing-poster polish
- overly cinematic perfection
- obvious AI fantasy style

## Daily Workflow

1. Select 5 topics from the content pillars.
2. Check `assets/Horrorscope/created-topics.json` to avoid repeating a topic too soon.
3. Create the folder structure:
   - `assets/Horrorscope/YYYY-MM-DD/Topic Title/`
4. For each topic, create 3 captions:
   - `variation-1-caption.txt`
   - `variation-2-caption.txt`
   - `variation-3-caption.txt`
5. For each topic, generate 3 images:
   - `variation-1.png`
   - `variation-2.png`
   - `variation-3.png`
6. Normalize final images to true 3:4 if the generator returns another portrait ratio.
7. Back up raw generated images to `_raw-generated/` before normalization.
8. Create `_qa-contact-sheet.jpg` at the date-folder level.
9. Write `QA-report.md` at the date-folder level.
10. Update tracking files:
   - `assets/Horrorscope/created-topics.json`
   - `assets/Horrorscope/daily-log.jsonl`
11. Final response must include the date folder path, prompt JSON path, QA report path, and any Drive folder/upload link.

## Content Pillars

Rotate between these pillars:

- Dark psychology: sleep paralysis, memory distortion, intrusive thoughts, uncanny valley, fear conditioning, dreams.
- Paranormal: ghosts, shadow people, haunted places, mirrors, rooms that feel watched.
- Urban legends: warnings, village rules, cursed rooms, threshold myths, folklore from many countries.
- Reality-bending: impossible reflections, images that feel wrong, liminal spaces, what changed after staring.
- True-crime-adjacent mystery: only non-graphic psychological unease, never crime-scene visuals or killer worship.

## Image Prompt Template

Use this exact structure and adapt only the bracketed parts:

```text
Use case: photorealistic-natural
Asset type: Facebook Horrorscope post, 3:4 portrait, no text
Primary request: [Topic title], variation [1-3].
Scene/backdrop: [Specific creepy place or object tied to the caption].
Subject: [Unsettling but safe subject, symbolic not graphic].
Camera and framing: Imperfect found-phone-photo realism; choose the angle that matches the scene: house/interior shots may be through a cracked window, barely opened door, curtain gap, hallway corner, or furniture obstruction; mirror shots may use accidental reflection or flash glare; outdoor folklore scenes may use distant zoom, dusk underexposure, or partial obstruction; evidence-style posts may use degraded phone/CCTV/archive-photo realism; not a planned poster.
Style/medium: realistic phone photography, dark psychological horror, subtle supernatural dread, original and non-generic.
Lighting/mood: low light, weak practical light, underexposed shadows, quiet dread.
Color palette: [Topic-specific palette].
Constraints: no text, no letters, no numbers, no watermark, no social UI, no blood, no gore, no dead bodies, no weapons, no explicit violence, no injury, no children, no public figures. Avoid perfect centered poster composition. Make it feel like a believable imperfect image captured in the moment; use cracked-window or door-crack angles only when they fit the scene.
```

## Caption Template

Captions should feel creepy, short, and comment-friendly.

Use this structure:

```text
[Disturbing hook or psychological observation.]
[One or two lines that make the fear feel possible without claiming fake facts as verified.]
[Connect the image to the fear or story.]
[Engagement question.]
```

Good endings:
- What did you notice first?
- Would you sleep here?
- Do you believe this?
- Have you ever experienced this?
- Look again. What changed?
- Would you enter this room?

Do not use hashtags.

## Folder Contract

For a date batch:

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
  _qa-contact-sheet.jpg
  QA-report.md
```

Global tracking:

```text
assets/Horrorscope/created-topics.json
assets/Horrorscope/daily-log.jsonl
prompts/horrorscope-production-prompt.json
```

## QA Rules

Before final delivery, verify:

- Every topic folder has exactly 3 PNGs and 3 caption TXT files.
- Every final PNG is 3:4.
- The contact sheet exists.
- The image has no text or watermark.
- The image has no blood, gore, dead bodies, weapons, explicit harm, children, or public figures.
- The image looks imperfect and phone-captured enough for the current style.
- Captions are clean TXT only, creepy, safe, and end with an engagement question.

Use `scripts/qa_horrorscope_batch.py` when available.

## Google Drive Handoff

When the user asks to push to Drive:

1. Find or create a Drive folder named `Master`.
2. Create or reuse `Horrorscope Workflow` inside `Master`.
3. Zip the local workflow/package if uploading a folder tree.
4. Upload the ZIP and key standalone files:
   - prompt JSON
   - SOP
   - skill folder ZIP
   - latest batch ZIP when relevant
5. Verify the Drive upload using metadata or folder listing before reporting success.

