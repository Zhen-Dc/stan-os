---
name: frame-of-fame
description: Create and QA Facebook image-only celebrity tribute batches for the Frame of Fame page. Use when the user asks for Frame of Fame, celebrity collage posts, actor or actress birthday/memorial/legacy content, Facebook celebrity image batches, verified captions, dated asset folders, or reusable SOP-driven celebrity post production.
---

# Frame of Fame

## Core Output

Create Facebook-ready image posts for the `Frame of Fame` celebrity niche:

- `5` celebrities per daily batch unless the user asks otherwise.
- `3` image variations and `3` matching caption files per celebrity.
- Folder contract: `assets/Frame of Fame/YYYY-MM-DD/Celebrity Name/`.
- Required files per celebrity: `variation-1.png`, `variation-1-caption.txt`, `variation-2.png`, `variation-2-caption.txt`, `variation-3.png`, `variation-3-caption.txt`.
- Tracking files: `assets/Frame of Fame/created-celebrities.json` and `assets/Frame of Fame/daily-log.jsonl`.
- QA evidence: `_qa-contact-sheet.jpg` and `QA-report.md` in the dated batch folder.

Always read `references/SOP.md` completely before producing or QAing a batch. It is written as the full operator manual for a weaker model and contains the exact folder arrangement, naming format, image-generation templates, caption templates, tracking templates, QA checklist, and failure-repair rules.

## Non-Negotiables

- Verify public facts online before writing captions.
- Use only globally recognizable celebrities from the allowed countries in the SOP.
- Avoid political celebrities, active scandals, controversy-led framing, criminal-case posts, rumors, fake quotes, and unverified claims.
- Use symbolic career imagery; never pretend AI images are exact real photos from a specific event.
- Keep images 3:4 portrait by default.
- Put only the celebrity name in the image unless the user explicitly approves memorial/birthday text.
- Every smaller grid/photo panel must include the featured celebrity recognizably. Props, cameras, stages, microphones, records, red carpets, or curtains may appear only as context.
- Do not add hashtags, watermarks, page branding, social media UI, or fake caption blocks inside the image.

## Image House Structures

Use `variation-1` as the primary house structure:

- **Actresses:** use the Elegant Actress Mosaic With Name Band structure.
- **Actors, comedians, directors, voice actors, martial artists, male singers who act, male TV presenters:** use the Bold Actor Center Portrait With Side Grids structure.

Use `variation-2` and `variation-3` as related alternatives only:

- `variation-2`: related archive-card or gallery-wall version.
- `variation-3`: related monochrome, hall-of-fame, documentary, or timeline version.

Do not drift into unrelated templates.

## Batch Workflow

Use the detailed process in `references/SOP.md`. In short:

1. Select celebrities using today-relevant reasons: birthday, memorial date, anniversary, career milestone, or evergreen legacy.
2. Check `created-celebrities.json` to avoid repeats.
3. Verify facts online and keep facts out of the clean caption files.
4. Create the dated folder and per-celebrity folders.
5. Write three short warm fan-page captions per celebrity using the SOP caption templates.
6. Generate three image prompts per celebrity using the SOP image templates.
7. Save/copy generated images into the matching folder names.
8. Run the QA script:

```powershell
python skills\frame-of-fame\scripts\qa_frame_of_fame_batch.py "assets\Frame of Fame\YYYY-MM-DD"
```

9. Visually inspect `_qa-contact-sheet.jpg` yourself. The script cannot prove celebrity identity or text accuracy.
10. Fix every QA failure before telling the user the batch is ready.

## QA Gate

Never call a batch complete until:

- The QA script reports no mechanical failures.
- The contact sheet confirms the house structures are followed.
- Every smaller panel shows the featured celebrity.
- Names are spelled correctly and readable.
- No prop-only grid panels remain.
- Captions are paired with the correct images.
