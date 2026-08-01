# Workflow: Repurpose YouTube Video Skill SOP

## Objective

Turn one YouTube URL, transcript, pasted script, or Firecrawl-captured web
source into review-ready social media content for LinkedIn, X, Instagram, and
Facebook.

The workflow must create editable text drafts, visual prompt files, generated PNG visuals, preview notes, QA notes, approval-ready folders, and publishing handoff records.

## What This Skill Does

The AI social media manager is the operator. The `repurpose-youtube-video` skill is the repeatable workflow the manager uses to turn a source video into organized platform content.

For LinkedIn/social/blog/article/Substack/web URLs, use
`repurpose-youtube-video-v3` instead. V3 runs Firecrawl first, creates
Instagram cover/slide JSON prompt files, and still renders the final PNG/GIF
package.

It repurposes one source into four platform lanes:

- LinkedIn: service authority, client trust, AI automation education.
- X: sharp short insight and quote-card visuals.
- Instagram: structured tweet-style educational carousel.
- Facebook: course-interest content for people learning AI skills.

The skill should make Stanley look useful, process-driven, and trustworthy. It must not make the content feel like Stanley only wants money from clients.

Every visible text idea must come from the video source: transcript/script first, then verified title, description, chapters, and source brief if the transcript is blocked. Use lessons, facts, frameworks, or takeaways from what the video actually discusses. Do not write random motivational text or unrelated AI advice.

## Inputs Needed

Minimum input:

- YouTube URL, pasted script, or transcript.

Helpful input:

- Content angle.
- Intended audience.
- Proof/result that can be mentioned.
- CTA preference.
- Platforms to include or skip.
- Brand/profile image.

Default brand profile image:

```text
AIS-OS/asset-folder/Brand_Assets/1762160371078.jpg
```

## Files To Read First

Before doing the task, read:

```text
AIS-OS/.claude/skills/repurpose-youtube-video/SKILL.md
AIS-OS/.claude/skills/repurpose-youtube-video-v3/SKILL.md
AIS-OS/.claude/skills/repurpose-youtube-video/references/platform-rules.md
AIS-OS/.claude/skills/repurpose-youtube-video/references/visual-recipes.md
AIS-OS/workflows/repurpose-youtube-video-sop.md
```

For web URLs, first run:

```powershell
python .claude/skills/repurpose-youtube-video-v3/scripts/firecrawl_scrape.py `
  --url "<source-url>" `
  --out-dir "asset-folder/content/<slug>/source"
```

Read `publish-schema.md` only when approving, publishing, logging, or preparing Notion/Drive handoff.

## Folder Rules

Always create the main package here:

```text
AIS-OS/asset-folder/content/<youtube-title-slug>/
```

Always mirror the final draft package here:

```text
AIS-OS/asset-folder/repurpose-youtube-video/<youtube-title-slug>/
```

Never use timestamped `run-*` folders for new work.

Use this structure:

```text
source/
drafts/
  Instagram/images/
  Instagram/text/
  X/images/
  X/text/
  LinkedIn/images/
  LinkedIn/text/
  Facebook/images/
  Facebook/text/
approved/
  Instagram/images/
  Instagram/text/
  X/images/
  X/text/
  LinkedIn/images/
  LinkedIn/text/
  Facebook/images/
  Facebook/text/
preview/
published/
  Instagram/images/
  Instagram/text/
  X/images/
  X/text/
  LinkedIn/images/
  LinkedIn/text/
  Facebook/images/
  Facebook/text/
manifest.json
```

Text drafts must be `.txt`.

Generated visuals must be `.png`.

Do not use `.md` for platform post drafts.

Do not use `.svg` for final visual assets.

## Step 1: Get Source Data

Try to get:

- Video title.
- Creator/channel.
- Video length.
- View count if available.
- Thumbnail URL.
- Description.
- Chapter/timestamp structure.
- Transcript if available.

If the browser/search tool gives no useful metadata, try YouTube oEmbed:

```powershell
Invoke-RestMethod -Uri 'https://www.youtube.com/oembed?url=<YOUTUBE_URL>&format=json'
```

If transcript/captions are blocked, do not fake it.

Write this clearly in `source/source.md`:

```text
Transcript Status:
Caption text fetching was blocked. This run is metadata-derived.
Do not treat these drafts as transcript-accurate quotes until a transcript/script is provided.
```

## Step 2: Create Source Brief

Create:

```text
source/source.md
```

Include:

- Source URL.
- Video title.
- Creator.
- Length.
- View count if available.
- Thumbnail URL.
- Transcript status.
- Verified description notes.
- Verified chapters.
- Repurposing angle.

The source brief is the truth file. If a detail is not in the source brief, do not pretend it is confirmed.

## Step 3: Create Manifest

Create:

```text
manifest.json
```

Required fields:

- `project_slug`
- `project_title`
- `created_at`
- `source_type`
- `source_url`
- `video_id`
- `video_author`
- `platforms`
- `brand_profile_image`
- `source_confidence`
- `status`
- `visual_format`
- `text_format`
- `notes`

Use `source_confidence: "metadata-derived"` when transcript fetching fails.

## Step 4: Extract The Content Angle

Extract these before writing:

- Core idea.
- Why it matters.
- Process lesson.
- Audience benefit.
- What should remain human.
- CTA.

For AI automation content, prefer this trust angle:

```text
The tool is not the whole value.
The value is knowing how to design the workflow, set rules, verify output, and keep human judgment in the right places.
```

## Step 5: Write Platform Drafts

Create these files:

```text
drafts/LinkedIn/text/post.txt
drafts/X/text/post.txt
drafts/Instagram/text/post.txt
drafts/Facebook/text/post.txt
```

LinkedIn:

- Business/process lesson.
- Explain why the workflow matters.
- Connect to Stanley's service authority.
- Avoid hype.
- End with a useful CTA.

X:

- Short insight.
- Optional thread.
- Make the first line strong.
- Keep it useful even without clicking the video.
- Pull the insight from the video's lesson, fact, framework, or chapter structure.

Instagram:

- Carousel caption.
- 5-8 slides.
- Each slide should teach one clear idea.
- Include a "Paste this" or action takeaway when useful.

Facebook:

- Course-interest lane.
- Beginner-friendly.
- Make the audience want to learn.
- No unrealistic income claims.

## Step 6: Write Visual Prompt Files

Create:

```text
drafts/LinkedIn/images/visual-prompt.txt
drafts/X/images/visual-prompt.txt
drafts/Instagram/images/visual-prompt.txt
drafts/Facebook/images/visual-prompt.txt
```

The prompt files must describe exactly what the generated images should show.

If the PNGs are generated locally instead of with GPT Image, still keep the prompt files. They document the intended final image.

## Step 7: Generate Visuals

Generate PNGs under each platform's `images/` folder.

LinkedIn:

```text
drafts/LinkedIn/images/linkedin-diagram.png
```

Make it a clean educational diagram with numbered boxes, arrows, and concise text.

X:

From now on, always create six different X images:

```text
drafts/X/images/x-quote-01.png
drafts/X/images/x-quote-02.png
drafts/X/images/x-quote-03.png
drafts/X/images/x-quote-04.png
drafts/X/images/x-quote-05.png
drafts/X/images/x-quote-06.png
```

Also create this compatibility copy:

```text
drafts/X/images/x-quote.png
```

`x-quote.png` should be a copy of `x-quote-01.png` so old preview links do not break.

X image style:

- 1:1 square, preferably 1080x1080.
- White background.
- Black outer frame.
- Bold uppercase centered text.
- No avatar.
- No logos.
- No clutter.
- Text must be a source-derived lesson or fact from the video.

Instagram:

```text
drafts/Instagram/images/instagram-slide-01.png
...
drafts/Instagram/images/instagram-slide-06.png
```

Use the structured tweet-style layout:

- 1080x1350.
- Warm cream grid background.
- Top-right creator pill.
- Stanley's real profile photo.
- Verified badge beside name.
- Numbered title pill.
- Short body copy.
- Simple visual block.
- Bottom "PASTE THIS" card.
- Swipe footer.

Facebook:

```text
drafts/Facebook/images/facebook-course-card.png
```

Use:

- 1080x1350.
- Course-interest headline.
- Beginner-friendly language.
- Roomy learning cards.
- Bottom CTA.
- Generous padding.

## Step 8: Visual QA

Open the PNGs before final response.

Minimum checks:

- LinkedIn diagram.
- X: at least `x-quote-01.png`, one middle option, and `x-quote-06.png`.
- Instagram: at least two representative slides, including the final slide.
- Facebook graphic.

Check:

- Text is readable.
- Nothing is clipped.
- Badge is beside name, not on top of it.
- Real Stanley profile image is visible wherever an avatar appears.
- No generated lookalike avatar.
- Facebook has enough padding.
- Instagram labels do not overlap containers.

Write the result in:

```text
preview/qa-check.txt
```

## Step 9: Preview Files

Create:

```text
preview/preview.md
preview/qa-check.txt
```

`preview.md` must link:

- All platform text drafts.
- LinkedIn image.
- All six X images plus compatibility copy.
- All Instagram slides.
- Facebook image.
- All visual prompt files.

If transcript is blocked, repeat the warning in preview:

```text
Source confidence: metadata-derived.
Do not publish as transcript-quoted content unless a transcript/script is provided.
```

## Step 10: Mirror The Package

After content package is ready, copy it to:

```text
AIS-OS/asset-folder/repurpose-youtube-video/<youtube-title-slug>/
```

Before deleting or replacing the mirrored folder, verify paths are inside:

```text
AIS-OS/asset-folder/repurpose-youtube-video/
```

Do not run destructive deletes against unverified computed paths.

## Step 11: Final Validation

Check:

- Four `post.txt` files exist.
- Four `visual-prompt.txt` files exist.
- LinkedIn PNG exists.
- Six X PNGs exist.
- `x-quote.png` compatibility copy exists.
- Instagram slides exist.
- Facebook PNG exists.
- No `.md` platform drafts inside `drafts/`.
- No `.svg` final images inside `drafts/`.

Recommended dimension checks:

- LinkedIn: 1200x1200 or 1200x627.
- X: 1:1 square, preferably 1080x1080.
- Instagram: 1080x1350.
- Facebook: 1080x1350.

## What Worked

- YouTube oEmbed worked for title and author when normal search/browser metadata was weak.
- YouTube watch-page metadata worked for title, creator, length, view count, description, and chapters.
- Caption tracks may appear on the page but still fail when fetching timed text.
- Metadata-derived content is acceptable for drafts only when clearly labeled.
- Deterministic local PNG rendering worked well for exact text placement, padding, and badge alignment.
- Keeping `x-quote.png` as a compatibility copy prevents old preview links from breaking.
- Square 1:1 X quote cards match the user's current preference better than landscape X cards.
- Treating the skill as a workflow used by the AI social media manager avoids confusing roles in future runs.

## What Failed And How To Fix It

Failure:

```text
X images were generated as landscape instead of square.
```

Fix:

- Regenerate all six X options as 1:1 PNGs.
- Prefer 1080x1080.
- Update `visual-prompt.txt`, `preview.md`, and QA notes to say square 1:1.
- Keep the same filenames so previews do not break.

Failure:

```text
The repurpose skill was described as the AI social media manager.
```

Fix:

- Describe the AI social media manager as the operator.
- Describe `repurpose-youtube-video` as the workflow/process/tool used by the manager.
- Keep this wording in `SKILL.md`, reference docs, and SOP.

Failure:

```text
Tweet/card text was too generic or not clearly from the video.
```

Fix:

- Re-read `source/source.md` before writing.
- Use the video transcript/script when available.
- If transcript is blocked, use only verified title, description, chapters, and source brief.
- Write lessons, facts, or takeaways from the video, not unrelated copy.

Failure:

```text
Transcript/caption fetch blocked by Google automated-query protection.
```

Fix:

- Mark source as `metadata-derived`.
- Use verified description and chapters.
- Do not use direct quotes from the video.
- Ask for transcript before final transcript-accurate publishing.

Failure:

```text
PowerShell helper function named P conflicted with the P alias for Remove-ItemProperty.
```

Fix:

- Do not name helper functions `P`.
- Use explicit names such as `NewPen`, `NewBrush`, and `NewFont`.
- Set `$ErrorActionPreference='Stop'` before generation scripts.

Failure:

```text
Image text can clip inside containers.
```

Fix:

- Shorten the copy.
- Reduce font size.
- Increase box height or padding.
- Reopen the PNG after regenerating.

Failure:

```text
Verified badge overlaps the creator name.
```

Fix:

- Measure or reserve the creator-name width.
- Place the badge to the right of the name with visible spacing.
- Inspect the final PNG.

Failure:

```text
Only one X image was generated.
```

Fix:

- Generate six X variants every time.
- Name them `x-quote-01.png` through `x-quote-06.png`.
- Copy `x-quote-01.png` to `x-quote.png`.
- List all six in `preview/preview.md`.

## DOs

- Do read the skill, visual rules, and this SOP first.
- Do create title-slug folders.
- Do use `.txt` for editable post drafts.
- Do generate PNGs.
- Do create six X image options.
- Do make every X image 1:1 square.
- Do source all slide, post, and quote-card text from the video.
- Do preserve edited draft text.
- Do inspect images before saying they are ready.
- Do record transcript limitations.
- Do use the real brand profile picture.
- Do keep humans in the loop when discussing automation.
- Do sync the final package to `asset-folder/repurpose-youtube-video/`.

## DON'Ts

- Do not invent transcript details.
- Do not write unrelated motivational text just because it sounds engaging.
- Do not describe the repurpose skill as the AI social media manager.
- Do not call metadata-derived content transcript-derived.
- Do not use timestamped `run-*` folders for new packages.
- Do not publish from memory if the user edited a draft file.
- Do not accept fake/generated creator avatars.
- Do not let the badge overlap the name.
- Do not use `.md` as platform post drafts.
- Do not use `.svg` as final visual assets.
- Do not fake Google Drive or Notion publishing.
- Do not delete folders unless the resolved path is verified inside the intended workspace.

## Approval And Publishing

The user approves platforms one by one.

Approved examples:

- "Approve all"
- "Approve LinkedIn and X"
- "Skip Instagram"
- "Revise Facebook"

The draft files are the source of truth. Publishing must reread:

```text
drafts/<Platform>/text/post.txt
```

Use `collect_approved.py` when packaging approvals.

Use Drive and Notion connectors only if available. If unavailable, leave upload-ready files and clearly say what connection is missing.

After live publishing, update:

```text
AIS-OS/asset-folder/repurpose-youtube-video/published-posts.csv
AIS-OS/asset-folder/repurpose-youtube-video/published-posts.jsonl
```

## Final Response Format

Keep the final response short.

Include:

- Project folder path.
- What was created.
- Any source-confidence warning.
- Ask which platform the user wants to review or approve first.

Do not paste the full drafts into chat unless the user asks.
