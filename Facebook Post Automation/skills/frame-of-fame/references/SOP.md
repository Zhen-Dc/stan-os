# Frame of Fame SOP

This SOP is the full operating manual for producing `Frame of Fame` Facebook image posts.

Follow it exactly. Do not improvise the folder structure, filenames, image layouts, caption format, or QA process unless the user explicitly changes the rules.

## 1. What This Workflow Creates

`Frame of Fame` is a faceless Facebook page for celebrity nostalgia and legacy posts.

The content type is image-only. No videos.

The default daily output is:

- 5 different celebrities.
- 3 image variations per celebrity.
- 3 matching caption files per celebrity.
- 15 total images.
- 15 total caption `.txt` files.
- 1 daily QA contact sheet.
- 1 daily QA report.
- 1 tracking file that prevents repeated celebrities.
- 1 daily log that records why each celebrity was selected.

## 2. The Required Folder Arrangement

Always save content under this structure:

```text
assets/
  Frame of Fame/
    created-celebrities.json
    daily-log.jsonl
    YYYY-MM-DD/
      Celebrity Name/
        variation-1.png
        variation-1-caption.txt
        variation-2.png
        variation-2-caption.txt
        variation-3.png
        variation-3-caption.txt
      _qa-contact-sheet.jpg
      QA-report.md
```

Example:

```text
assets/
  Frame of Fame/
    created-celebrities.json
    daily-log.jsonl
    2026-07-16/
      Meryl Streep/
        variation-1.png
        variation-1-caption.txt
        variation-2.png
        variation-2-caption.txt
        variation-3.png
        variation-3-caption.txt
      Jackie Chan/
        variation-1.png
        variation-1-caption.txt
        variation-2.png
        variation-2-caption.txt
        variation-3.png
        variation-3-caption.txt
      _qa-contact-sheet.jpg
      QA-report.md
```

Folder rules:

- Use the page folder name exactly: `Frame of Fame`.
- Use the date folder format exactly: `YYYY-MM-DD`.
- Use the public celebrity name as the folder name.
- Do not add numbering to celebrity folders.
- Do not save images outside the celebrity folder.
- Do not place source notes inside caption files.
- Do not overwrite previous dated batches.

## 3. File Naming Format

Each celebrity folder must contain exactly these six files:

```text
variation-1.png
variation-1-caption.txt
variation-2.png
variation-2-caption.txt
variation-3.png
variation-3-caption.txt
```

Meaning:

- `variation-1.png` uses the main house structure.
- `variation-1-caption.txt` is the caption for `variation-1.png`.
- `variation-2.png` is a related secondary layout.
- `variation-2-caption.txt` is the caption for `variation-2.png`.
- `variation-3.png` is another related secondary layout.
- `variation-3-caption.txt` is the caption for `variation-3.png`.

Never use:

- `final.png`
- `image1.png`
- `caption.txt`
- `post.txt`
- `Celebrity Name.png`
- `variation one.png`

## 4. Allowed Celebrity Pool

Use only globally recognizable celebrities from these countries:

- USA
- UK
- Canada
- China
- Japan
- South Korea
- India
- France
- Italy
- Australia
- Mexico
- Spain
- Nigeria
- Hong Kong
- Taiwan
- Turkey
- Brazil

Allowed celebrity types:

- Actors
- Actresses
- Directors
- Comedians
- Voice actors
- TV presenters
- Martial artists
- Singers who also act

Do not use:

- Political celebrities.
- People mainly famous for politics.
- People currently known mostly for active scandals.
- Criminal-case-centered personalities.
- Rumor-driven celebrities.
- People whose key facts cannot be verified.

## 5. Celebrity Selection Process

For a daily batch, choose 5 celebrities using a mix of:

- Birthday today.
- Memorial date.
- Death anniversary.
- Career anniversary.
- Movie or TV milestone.
- Award anniversary.
- Evergreen legacy post.

Selection steps:

1. Search online for celebrity birthdays, memorials, and entertainment anniversaries for today.
2. Make a candidate list of at least 8 names.
3. Remove names outside the allowed countries.
4. Remove names with active major scandal or controversy-led relevance.
5. Remove names that are not globally recognizable enough.
6. Open `assets/Frame of Fame/created-celebrities.json`.
7. Remove names already created unless the user asks for a repeat.
8. Pick the best 5.
9. Record each selection in `created-celebrities.json`.
10. Record the reason and facts in `daily-log.jsonl`.

If there are not enough strong today-relevant names, fill the remaining slots with evergreen globally recognized legends.

## 6. Fact Verification Process

Always verify facts online before writing captions.

Verify:

- Full public name.
- Country or public nationality.
- Date of birth.
- Current age for birthday posts.
- Death date for memorial posts.
- Known films, shows, songs, or career milestones.
- Major awards or honors.

Use at least one reliable public source per celebrity. Prefer:

- Official website.
- Britannica.
- Academy/award body pages.
- Rock Hall/Kennedy Center/major institution pages.
- Reputable news or biography pages.
- Wikipedia only as a quick cross-check, not the only source when better sources are available.

Never write:

- Rumors.
- Speculation.
- Fake quotes.
- Unverified relationship claims.
- Political opinions.
- Criminal accusations.
- Claims like `most loved ever` unless verified and meaningful.

## 7. Tracking File Template

File:

```text
assets/Frame of Fame/created-celebrities.json
```

If the file does not exist, create it:

```json
{
  "page": "Frame of Fame",
  "created": []
}
```

For each completed celebrity, append:

```json
{
  "name": "Celebrity Name",
  "country": "USA",
  "date_created": "YYYY-MM-DD",
  "post_type": "Birthday / career legacy",
  "reason_selected": "Born Month Day, Year; turns AGE on Month Day, YYYY."
}
```

Rules:

- Do not duplicate names.
- Keep names consistent.
- Use the same celebrity name spelling in folder, image prompt, caption, and tracking file.

## 8. Daily Log Template

File:

```text
assets/Frame of Fame/daily-log.jsonl
```

Append one line per celebrity:

```json
{"date":"YYYY-MM-DD","page":"Frame of Fame","celebrity":"Celebrity Name","country":"USA","post_type":"Birthday / career legacy","reason_selected":"Born Month Day, Year; turns AGE on Month Day, YYYY.","folder":"assets/Frame of Fame/YYYY-MM-DD/Celebrity Name","facts_used":["Verified fact 1.","Verified fact 2.","Verified fact 3."]}
```

Rules:

- JSONL means one complete JSON object per line.
- Do not wrap all rows in an array.
- Keep facts short.
- Facts in the log are for internal tracking; the caption file stays clean.

## 9. Caption Generation Rules

Caption files must be clean, ready to paste into Facebook.

Default caption length:

- 35 to 70 words.
- Short, direct, emotional, and comment-friendly.

Tone:

- Warm fan-page voice.
- Respectful.
- Nostalgic.
- Celebratory.
- Human.
- Simple enough for casual Facebook readers.

Do not use:

- Hashtags.
- Source links.
- Rumors.
- Clickbait.
- Fake quotes.
- Long paragraphs.
- Overly formal biography language.

### Caption Formula

Use this structure:

```text
[Warm opening tied to the occasion]. [Verified career fact or milestone]. [Emotional legacy sentence]. [Engagement question or call to comment.]
```

### Birthday Caption Template

```text
Happy [AGE]th birthday to [Name], a [short identity phrase]. From [known work] to [known work], [he/she/they] built a career filled with [emotion/quality]. [Milestone or verified fact]. Which [movie/role/performance/song] made you a fan?
```

Example:

```text
Happy 65th birthday to Forest Whitaker, one of cinema's quiet powerhouses. From Bird to The Butler, Black Panther, and Rogue One, he built a career around depth and unforgettable presence. His Oscar-winning role in The Last King of Scotland remains a defining moment. Which Forest Whitaker role stayed with you the longest?
```

### Memorial Caption Template

```text
In Memoriam: [Name]
([Birth Month Day, Year] - [Death Month Day, Year])

[Name] gave audiences [emotion/quality] through [known works]. [Verified career milestone]. [Legacy sentence]. Gone but never forgotten.
```

### Evergreen Legacy Caption Template

```text
Some stars become part of cinema history because their work still feels alive years later. [Name] brought [quality] to [known work or genre], earning a place in the memories of fans around the world. Which performance would you recommend first to someone discovering [him/her/them] today?
```

### Engagement Ending Options

Rotate these naturally:

- `Which movie made you a fan?`
- `Which role was unforgettable?`
- `What's your favorite movie from this legend?`
- `Rate this legend from 1-10.`
- `Comment your favorite memory.`
- `Tag someone who loved their movies.`
- `Which performance stayed with you the longest?`
- `Gone but never forgotten.`
- `Happy Birthday!`

## 10. Image Generation Rules

Every image must be:

- 3:4 portrait by default.
- Premium tribute style.
- Photorealistic editorial collage.
- Focused on the featured celebrity.
- Clear enough for Facebook mobile feed.
- Built around nostalgia, transformation, legacy, and career moments.

Every image must include:

- The celebrity name.
- Multiple panels showing the same celebrity.
- Different ages, career moods, or symbolic life/career stages.
- A premium bottom name band or title block.

Every image must avoid:

- Empty prop-only panels.
- Empty cameras, microphones, records, chairs, stages, streets, curtains, or spotlights as standalone panels.
- Distant silhouettes that cannot be recognized as the celebrity.
- Watermarks.
- Page branding.
- Social media UI.
- Fake quotes.
- Long text blocks.
- Hashtags.
- Political framing.
- Scandal framing.
- Copyright logos.
- Exact movie-scene recreations.

Important:

The AI may generate symbolic portraits. Do not claim these images are real archival photos. They are tribute collage visuals.

## 11. House Structure A: Actress Structure

Name:

```text
Elegant Actress Mosaic With Name Band
```

Use for:

- Actresses.
- Female singers who also act.
- Female TV presenters.
- Female directors when the post is about their personal legacy.

This is the main structure for `variation-1` when the celebrity is an actress.

### Actress Structure Layout

The image must look like this:

- 3:4 vertical portrait.
- One large center portrait of the actress.
- Smaller panels around the center portrait.
- Top-left panel: younger version or early-career mood.
- Top-right panel: mature or behind-the-scenes mood.
- Middle-left panel: elegant close-up or career-era portrait.
- Middle-right panel: role-inspired portrait.
- Bottom-left panel: stage or screen performance with actress visible.
- Bottom-right panel: film-set or behind-the-scenes portrait with actress visible.
- Bottom name band: wide textured band with the celebrity name.

All panels must show the same actress.

The actress should feel:

- Elegant.
- Warm.
- Graceful.
- Timeless.
- Cinematic.
- Premium.

### Actress Structure Prompt Template

Copy and fill this:

```text
Use case: photorealistic-natural
Asset type: Facebook image post for Frame of Fame, 3:4 portrait

Primary request:
Create a premium celebrity tribute collage for [CELEBRITY NAME] using the Elegant Actress Mosaic With Name Band structure.

Subject:
[CELEBRITY NAME], respectful recognizable likeness across life stages: younger early-career actress, peak-career performer, mature screen legend. Every panel must show [CELEBRITY NAME] recognizably. Stage curtains, film lights, cameras, dressing rooms, microphones, records, or theater props may appear only as background/context while [CELEBRITY NAME] is present.

Style/medium:
Photorealistic elegant cinema mosaic, premium tribute poster, warm editorial photography, refined but not ornate.

Composition/framing:
Vertical 3:4 portrait. One large elegant center portrait. Surrounding smaller life-stage and career-scene panels on the left, right, top, and lower area. Wide textured bottom name band. Thin clean dividers. No empty object-only panels. No prop-only panels. No distant silhouette-only panels.

Panel requirements:
Top-left: [CELEBRITY NAME] as a younger early-career actress.
Top-right: [CELEBRITY NAME] in mature or behind-the-scenes screen setting.
Middle-left: [CELEBRITY NAME] in an elegant close-up.
Middle-right: [CELEBRITY NAME] in a symbolic role-inspired portrait.
Bottom-left: [CELEBRITY NAME] visible in stage or screen performance mood.
Bottom-right: [CELEBRITY NAME] visible near film-set or behind-the-scenes context.

Lighting/mood:
Warm cinematic lighting, nostalgic, graceful, celebratory, premium, timeless.

Color palette:
[Choose one: deep navy and ivory / burgundy and gold / black and warm amber / emerald and cream / monochrome with warm highlights].

Text (verbatim):
"[CELEBRITY NAME IN ALL CAPS]" only, large clean readable serif in the bottom name band.

Constraints:
Every grid panel must include [CELEBRITY NAME] recognizably. No standalone prop panels. No fake quotes. No hashtags. No watermark. No Facebook UI. No page branding. No extra text. No political references. No scandal references. Name must be correctly spelled and readable.
```

## 12. House Structure B: Actor Structure

Name:

```text
Bold Actor Center Portrait With Side Grids
```

Use for:

- Actors.
- Directors.
- Comedians.
- Voice actors.
- Martial artists.
- Male singers who also act.
- Male TV presenters.

This is the main structure for `variation-1` when the celebrity is an actor or male performer.

### Actor Structure Layout

The image must look like this:

- 3:4 vertical portrait.
- Large central portrait of the celebrity.
- Left column with 2 or 3 smaller panels.
- Right column with 2 or 3 smaller panels.
- One panel should show performance/career context.
- One panel may show voiceover/stage/film-set context if relevant.
- Bottom title block with the celebrity name.

All panels must show the same celebrity.

The actor should feel:

- Bold.
- Recognizable.
- Strong.
- Warm or dramatic depending on their brand.
- Premium.
- High-engagement for Facebook.

### Actor Structure Prompt Template

Copy and fill this:

```text
Use case: photorealistic-natural
Asset type: Facebook image post for Frame of Fame, 3:4 portrait

Primary request:
Create a premium celebrity tribute collage for [CELEBRITY NAME] using the Bold Actor Center Portrait With Side Grids structure.

Subject:
[CELEBRITY NAME], respectful recognizable likeness across life stages: younger early-career performer, peak-career star, mature legacy figure. Every panel must show [CELEBRITY NAME] recognizably. Microphones, cameras, stages, red carpets, records, city lights, film sets, martial arts settings, or studio props may appear only as background/context while [CELEBRITY NAME] is present.

Style/medium:
Photorealistic modern documentary poster, premium Facebook tribute collage, emotionally accessible, cinematic, high contrast.

Composition/framing:
Vertical 3:4 portrait. Large expressive central portrait. Narrow side-column panels showing the same celebrity in career/life-stage moments. One larger performance or role panel. Strong lower title block. No empty object-only panels. No prop-only panels. No distant silhouette-only panels.

Panel requirements:
Center: large expressive portrait of [CELEBRITY NAME].
Left-top: [CELEBRITY NAME] as younger or early-career performer.
Left-middle: [CELEBRITY NAME] in another age/career mood.
Left-bottom: [CELEBRITY NAME] in energetic or expressive portrait.
Right-top: [CELEBRITY NAME] in performance, stage, film, or role-inspired setting.
Right-bottom: [CELEBRITY NAME] in career-context setting such as recording booth, film set, red carpet, action scene mood, or dramatic close-up.

Lighting/mood:
Warm stage or cinema lighting, nostalgic, celebratory, legacy-focused, premium.

Color palette:
[Choose one: black and amber / dark teal and cream / charcoal and gold / navy and warm bronze / monochrome with selective warm highlights].

Text (verbatim):
"[CELEBRITY NAME IN ALL CAPS]" only, large clean readable serif in the lower title block.

Constraints:
Every grid panel must include [CELEBRITY NAME] recognizably. No standalone prop panels. No fake quotes. No hashtags. No watermark. No Facebook UI. No page branding. No extra text. No political references. No scandal references. Name must be correctly spelled and readable.
```

## 13. Variation 2 Template

Variation 2 must be related to the house structure, not a random new design.

Use this template:

```text
Use case: photorealistic-natural
Asset type: Facebook image post for Frame of Fame, 3:4 portrait

Primary request:
Create variation 2 for [CELEBRITY NAME]. Use a related archive-card / gallery-wall version of the [ACTRESS OR ACTOR HOUSE STRUCTURE NAME].

Subject:
[CELEBRITY NAME], respectful recognizable likeness across life stages. Every photo card must show [CELEBRITY NAME] recognizably. Props/settings may appear only as background/context.

Style/medium:
Premium archive-card collage, layered photo prints, cinematic gallery wall, refined editorial tribute.

Composition/framing:
Vertical 3:4 portrait. Five or six photo cards arranged around one larger central card. Each card contains [CELEBRITY NAME]. Bottom nameplate or title band with the name. No empty prop cards.

Text (verbatim):
"[CELEBRITY NAME IN ALL CAPS]" only.

Constraints:
No object-only panels. No fake quotes. No hashtags. No watermark. No Facebook UI. No page branding. Name must be spelled correctly and readable.
```

## 14. Variation 3 Template

Variation 3 must be related to the house structure.

Use this template:

```text
Use case: photorealistic-natural
Asset type: Facebook image post for Frame of Fame, 3:4 portrait

Primary request:
Create variation 3 for [CELEBRITY NAME]. Use a related monochrome hall-of-fame or documentary timeline version of the [ACTRESS OR ACTOR HOUSE STRUCTURE NAME].

Subject:
[CELEBRITY NAME], respectful recognizable likeness across life stages. Every panel must show [CELEBRITY NAME] recognizably.

Style/medium:
Black-and-white or mostly monochrome premium documentary collage with selective warm highlights.

Composition/framing:
Vertical 3:4 portrait. Three age-journey portraits plus three smaller career-context portraits, all showing [CELEBRITY NAME]. Strong readable name at top or bottom. No empty prop panels.

Text (verbatim):
"[CELEBRITY NAME IN ALL CAPS]" only.

Constraints:
Every panel must include [CELEBRITY NAME]. No standalone microphones, cameras, records, empty stages, city streets, chairs, curtains, spotlights, or silhouettes. No fake quotes. No watermark. No Facebook UI. Name must be spelled correctly and readable.
```

## 15. Prompt Filling Instructions

Before generating each image prompt, fill these fields:

```text
CELEBRITY NAME:
COUNTRY:
POST TYPE:
AGE OR MEMORIAL YEARS:
KNOWN WORKS:
CAREER MOOD:
COLOR PALETTE:
HOUSE STRUCTURE:
```

Example filled fields:

```text
CELEBRITY NAME: Gabriel Iglesias
COUNTRY: USA
POST TYPE: Birthday / comedy and voice acting
AGE OR MEMORIAL YEARS: Turns 50
KNOWN WORKS: stand-up comedy, Mr. Iglesias, voice acting
CAREER MOOD: warm, funny, stage performer, recording booth
COLOR PALETTE: dark teal, black, warm amber, cream
HOUSE STRUCTURE: Bold Actor Center Portrait With Side Grids
```

Then fill the image prompt template.

## 16. Full Per-Celebrity Production Checklist

For each celebrity:

1. Confirm the name spelling.
2. Confirm country is allowed.
3. Confirm the celebrity type.
4. Confirm the post reason.
5. Verify at least 3 public facts.
6. Create the celebrity folder.
7. Write `variation-1-caption.txt`.
8. Write `variation-2-caption.txt`.
9. Write `variation-3-caption.txt`.
10. Create image prompt for variation 1 using the correct house structure.
11. Generate `variation-1.png`.
12. Create image prompt for variation 2 using archive-card/gallery-wall related structure.
13. Generate `variation-2.png`.
14. Create image prompt for variation 3 using monochrome/documentary related structure.
15. Generate `variation-3.png`.
16. Check each image manually before moving on.
17. If a panel does not show the celebrity, regenerate immediately.
18. If the name is misspelled or unreadable, regenerate immediately.
19. If the image has unwanted text or watermark, regenerate immediately.
20. Update tracking and daily log.

## 17. QA Script

Run after all files are created:

```powershell
python skills\frame-of-fame\scripts\qa_frame_of_fame_batch.py "assets\Frame of Fame\YYYY-MM-DD"
```

If `python` is not available, use the machine's known Python path or launcher.

The script checks:

- Dated folder exists.
- Celebrity folders exist.
- Each celebrity folder has 3 PNG files.
- Each celebrity folder has 3 TXT caption files.
- Each variation has a matching caption.
- Every image is 3:4.
- A contact sheet is created.
- A QA report is created.

The script cannot check:

- Whether the celebrity likeness is correct.
- Whether a small panel actually shows the celebrity.
- Whether the name text is spelled correctly inside the image.
- Whether the image feels premium.

Those require manual visual QA.

## 18. Manual Visual QA Checklist

Open:

```text
assets/Frame of Fame/YYYY-MM-DD/_qa-contact-sheet.jpg
```

Check every image.

For each image, answer:

1. Is it 3:4 portrait?
2. Is the celebrity name visible?
3. Is the name spelled correctly?
4. Is the name readable on mobile?
5. Does every smaller grid/photo panel show the featured celebrity?
6. Are there any empty prop-only panels?
7. Are there any camera-only, microphone-only, record-only, stage-only, street-only, chair-only, or curtain-only panels?
8. Are there any distant silhouettes that do not clearly show the celebrity?
9. Does the image match the correct house structure?
10. Does it feel premium?
11. Is there any watermark?
12. Is there any Facebook UI?
13. Is there any fake quote?
14. Is there any extra text besides the celebrity name?
15. Is there any political/scandal framing?

Pass only if all answers are correct.

## 19. QA Failure Rules

If an image has an empty prop-only panel:

- Regenerate the image.
- Add this line to the prompt:

```text
Every single grid panel must show [CELEBRITY NAME] recognizably. Do not create any object-only panels.
```

If the name is misspelled:

- Regenerate the image.
- Put the name in the prompt as:

```text
Text (verbatim): "[EXACT NAME]" only.
Spell the name exactly as: [EXACT NAME].
```

If the aspect ratio is wrong:

- Regenerate as 3:4 portrait.
- If the image is otherwise excellent, pad it to 3:4 without cropping.

If the layout is wrong:

- Regenerate using the correct house structure.
- Do not accept random layouts.

If the caption has unverifiable facts:

- Rewrite the caption.
- Use only verified public facts.

## 20. QA Report Requirements

`QA-report.md` must include:

- Batch date.
- Number of celebrities.
- Number of PNGs.
- Number of captions.
- Mechanical QA result.
- Manual visual QA result.
- Notes about regenerated images.
- Final pass/fail decision.

Minimum report structure:

```markdown
# Frame of Fame QA Report - YYYY-MM-DD

## Batch Summary

- Page: Frame of Fame
- Date: YYYY-MM-DD
- Celebrities: 5
- PNG files: 15
- Caption files: 15
- Contact sheet: _qa-contact-sheet.jpg

## Mechanical QA

- Folder completeness: Pass
- Caption pairing: Pass
- 3:4 aspect ratio: Pass

## Manual Visual QA

- Correct house structure: Pass
- Celebrity appears in every smaller panel: Pass
- Name readable and correctly spelled: Pass
- No prop-only panels: Pass
- No watermark or Facebook UI: Pass
- No extra text or fake quotes: Pass

## Fixes Made

- List regenerated images here, or write: None.

## Final Decision

Pass. Ready for manual Facebook posting.
```

## 21. Final Handoff Template

When finished, reply with:

```text
Done. I created the Frame of Fame batch for YYYY-MM-DD.

Batch folder:
[absolute path]

Output:
- 5 celebrities
- 15 PNG images
- 15 caption files
- QA contact sheet
- QA report

QA:
- Mechanical QA passed.
- Manual visual QA passed.
- Every smaller panel shows the featured celebrity.
- Names are readable and correctly spelled.
```

If anything failed, do not say the batch is ready. Say what failed and what still needs fixing.

## 22. Absolute Quality Rules

The batch is not complete until all of these are true:

- The folder structure is correct.
- Every celebrity has exactly 3 PNG files.
- Every celebrity has exactly 3 caption files.
- Captions are clean and Facebook-ready.
- Facts were verified online.
- The image structure follows the approved house layouts.
- `variation-1` uses the correct main house structure.
- `variation-2` and `variation-3` are related variations.
- Every smaller panel contains the featured celebrity.
- No prop-only panels exist.
- Names are correctly spelled.
- The contact sheet was manually inspected.
- The QA report says pass.

If even one item fails, fix it before handoff.
