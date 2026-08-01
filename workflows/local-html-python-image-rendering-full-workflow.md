# Local HTML/Python Image Rendering Workflow

## Purpose

This document explains the full workflow for generating social media images locally without using GPT Image, Midjourney, Canva, or any cloud image model.

The goal is simple:

1. Give a weak/local model a safe workflow it can follow.
2. Make the model edit content in a JSON file instead of inventing image code.
3. Generate images locally using Python/Pillow or optional HTML rendering.
4. Run QA before saying the images are done.
5. Avoid the common problem of images having too much white space, weak titles, repeated layouts, or unreadable content.
6. Save the exact image-generation code used for each repurpose package so the
   images can be regenerated later without guessing.

This workflow was created after the image packages had quality issues, especially excessive white space in carousel and LinkedIn images.

## What This Workflow Does

This workflow creates deterministic image files from templates.

It can generate:

- LinkedIn static thumbnail
- LinkedIn diagram image
- LinkedIn animated GIF
- Instagram 8-slide carousel
- X quote cards
- Facebook thumbnail
- Facebook course card
- QA report
- Contact sheet for visual inspection

The main rendering method is Python/Pillow.

Optional HTML rendering is also included for cases where browser/CSS layout is needed.

For repurpose packages, the executed renderer must be saved at:

```text
asset-folder/content/<slug>/source/render_social_images.py
```

If the renderer was executed from `tools/` or a skill folder, copy that exact
script into the package after rendering.

## What This Workflow Does Not Do

This workflow does not use GPT Image or any AI image model.

It does not magically design images from a vague prompt.

It does not replace human QA.

It does not guarantee the writing is good. The QA script can catch missing files and sparse images, but a human or model still has to check whether the message makes sense.

## Main Skill Folder

The reusable skill was created here:

```text
C:\Users\DELL\Master Project\Stan OS\AIS-OS\.claude\skills\html-python-image-renderer
```

Important files:

```text
html-python-image-renderer/
  SKILL.md
  agents/
    openai.yaml
  assets/
    sample_spec.json
    html-template.html
  references/
    local-rendering-sop.md
  scripts/
    setup_requirements.py
    render_image_package.py
    render_html_image.py
    qa_image_package.py
```

## Simple Explanation

Think of the workflow like this:

1. `sample_spec.json` is the content.
2. `render_image_package.py` is the designer.
3. `qa_image_package.py` is the checker.
4. `contact-sheet.png` is the visual review page.
5. The final images are saved into platform folders.

The local model should usually only edit the JSON file.

It should not edit the Python renderer unless many images fail for the same layout reason.

## One-Time Setup

Open PowerShell in the skill folder:

```powershell
cd "C:\Users\DELL\Master Project\Stan OS\AIS-OS\.claude\skills\html-python-image-renderer"
```

Find Python:

```powershell
$PY = (Get-Command python).Source
```

Check requirements:

```powershell
& $PY scripts\setup_requirements.py --check
```

Install missing requirements:

```powershell
& $PY scripts\setup_requirements.py
```

If using the optional HTML renderer:

```powershell
& $PY scripts\setup_requirements.py --with-html --install-browser
```

The base requirement is:

```text
Pillow
```

The optional HTML requirement is:

```text
Playwright + Chromium
```

## If Python Is Not Found

If this fails:

```powershell
$PY = (Get-Command python).Source
```

Then Python is not available on PATH.

Use one of these fixes:

1. Install Python from python.org.
2. Install Python with winget:

```powershell
winget install Python.Python.3.12
```

3. Use the full Python path if it is already installed. Example:

```powershell
& "C:\Users\DELL\AppData\Local\Programs\Python\Python312\python.exe" scripts\setup_requirements.py --check
```

## Normal Image Generation Workflow

### Step 1: Copy Or Edit The Spec

Start with:

```text
assets\sample_spec.json
```

This file contains the content for the images.

The local model should edit these fields:

```json
{
  "package_title": "AI Workflow Example",
  "creator_name": "chima-stanley-chukwu",
  "handle": "@chima-stanley-chukwu",
  "badge": "AI WORKFLOW",
  "title": "Stop Starting Every Post From Zero",
  "subtitle": "Turn one repeated task into a reusable AI workflow with context, rules, review, and handoff.",
  "bottom_takeaway": "The prompt is not the system. The repeatable workflow is.",
  "steps": [],
  "slides": [],
  "quotes": []
}
```

### Step 2: Write Good Content

Every image should be able to stand alone.

That means:

- The title must make sense by itself.
- The subtitle must explain the point.
- The image must not depend on a previous slide.
- The image must not feel like a continuation of another platform post.
- The text must be clear and practical.
- Avoid jargon.
- Avoid vague phrases.
- Avoid fake claims.

### Step 3: Render The Images

Run:

```powershell
$PY = (Get-Command python).Source
& $PY scripts\render_image_package.py --spec assets\sample_spec.json --out output\my-package
```

This creates:

```text
output\my-package\
  LinkedIn\images\
  Instagram\images\
  X\images\
  Facebook\images\
```

### Step 4: Run QA

Run:

```powershell
$PY = (Get-Command python).Source
& $PY scripts\qa_image_package.py --root output\my-package
```

Pass result should look like:

```json
{
  "checked": 20,
  "missing": 0,
  "failures": 0,
  "gif_issue": null,
  "contact_sheet": "output\\my-package\\qa\\contact-sheet.png"
}
```

### Step 5: Inspect The Contact Sheet

Open:

```text
output\my-package\qa\contact-sheet.png
```

Check every image visually.

Do not say the package is done just because the files exist.

Do not say the package is done just because the script ran.

Only say it is done after:

- Required images exist.
- QA has zero failures.
- LinkedIn GIF exists and is animated.
- Contact sheet was inspected.
- No obvious white-space issue remains.
- No text is clipped.
- No title cuts into a subtitle.
- No body section, footer, profile row, or action panel overlaps another
  element.
- The slides do not all look the same.
- Every post can stand alone.

## Output Folder Contract

Every finished package should follow this folder structure:

```text
output-folder/
  LinkedIn/images/
    linkedin-thumbnail.png
    linkedin-diagram.png
    linkedin-animation.gif
  Instagram/images/
    instagram-slide-01.png
    instagram-slide-02.png
    instagram-slide-03.png
    instagram-slide-04.png
    instagram-slide-05.png
    instagram-slide-06.png
    instagram-slide-07.png
    instagram-slide-08.png
  X/images/
    x-thumbnail.png
    x-quote-01.png
    x-quote-02.png
    x-quote-03.png
    x-quote-04.png
    x-quote-05.png
    x-quote-06.png
    x-quote.png
  Facebook/images/
    facebook-thumbnail.png
    facebook-course-card.png
  qa/
    contact-sheet.png
    qa-report.json
```

## Platform Rules

## Stanley Carousel Quality Standard

Use this exact standard for repurposed Instagram carousel images when Stanley
asks for the accepted reference-style result.

For B2B automation posts, the carousel must be aimed at a clear buyer and
business function before visuals are written. Pick the target company type,
industry, or department first, then build the title, subtitle, modules, and CTA
around a real automation bottleneck such as marketing, UGC/ad production,
Google Ads campaign work, content repurposing, lead research, sales follow-up,
reporting, onboarding, customer support, or internal operations.

- Treat `instagram-slide-01.png` as a cover, not a normal teaching slide.
- Build the cover from `drafts/Instagram/images/cover-prompt.json`.
- Follow the Premium Editorial cover look: cream grid background, huge
  magazine-style headline, one orange highlighted phrase, small tool tag
  directly above the title, subtitle directly under the title, and compact
  profile pill directly under the subtitle.
- Keep cover titles to one, two, or three lines only. The title should be large
  enough to dominate roughly 60% of the canvas.
- Preserve exact user-provided title and subtext.
- If Stanley does not provide exact cover subtext, write a specific summary of
  what the post is about. It must add context to the title, not read like a
  generic slogan. Good pattern: `This is how I would explain/use/build
  [tool/topic]: [specific angle].`
- Use `chima-stanley-chukwu` as the display name.
- Use `@chima-stanley-chukwu` as the visible username unless Stanley gives a
  new username. Store the URL in JSON metadata as
  `https://www.linkedin.com/in/chima-stanley-chukwu/`; do not draw Markdown
  syntax into the image.
- Use the brand avatar at `asset-folder/Brand_Assets/Stan Avatar.png`.
- The profile tag on Instagram teaching slides should match the cover profile
  pill: white rounded background, soft shadow, real avatar, name line, and
  visible `@` username line.
- On slides 2-8, place the first content section close under the title/subtitle.
  Do not leave a large blank vertical gap.
- Fill whitespace with useful content modules: comparison boxes, workflow rows,
  route maps, cost maps, checklists, matrices, dashboards, prompt boxes, ratio
  charts, or save-this summaries.
- Do not print internal QA or creator instructions inside the public image,
  including `stand alone`, `single post`, `contain enough information`, or
  `this slide should make sense`.
- Do not use the same layout across every slide. Pick the layout from the
  content: comparison for wrong/right, process flow for steps, dashboard for
  metrics, prompt box only when an actual prompt is useful.
- After rendering, save the exact executed renderer into
  `asset-folder/content/<slug>/source/render_social_images.py`.
- Rebuild and inspect a contact sheet before final handoff.
- Run or write a package-specific QA report after every render. It must check
  image count, expected dimensions, GIF frames, visible avatar/profile row, and
  layout overlap risks. For covers, explicitly check that the title block does
  not collide with the subtitle or profile pill. Save the result as
  `preview/image-qa.json` when possible.

### LinkedIn

LinkedIn images must use a dense standalone lesson format.

Each LinkedIn visual should include:

- Badge
- Creator row
- Clear title
- Subtitle
- Five labeled rows
- Bottom takeaway

Important rule:

```text
LinkedIn static image and LinkedIn GIF must use the same core content.
```

The GIF should animate/highlight the same five rows used in the static image.

### Instagram

Instagram uses an 8-slide carousel.

Slide 1:

- Strong title
- Clear subtext
- Useful content modules
- No empty lower half

Slides 2 to 8:

- Each slide must stand alone.
- Layouts should vary.
- Do not use a prompt box every time.
- Use checklist, instruction, workflow, tips, tech stack, QA gate, output, or save-this modules when appropriate.
- If the block is a prompt, label it `PROMPT`.
- If the block is a tip, label it `TIPS`.
- If the block is an instruction, label it `INSTRUCTION`.

### X

X cards should look like normal tweet screenshots.

Use:

- Avatar area
- Name
- Handle
- Tweet text

Avoid:

- Lesson labels
- Carousel footers
- Fake engagement rows
- Fake timestamps
- Continuation-style wording

Each X card must be a standalone post.

### Facebook

Facebook images should feel beginner-friendly and practical.

Use:

- Strong title
- Short subtext
- Task/context/review modules
- Practice checklist

Avoid:

- Blank middle space
- Too little information
- Generic "learn more" style cards

## QA Script Rules

The QA script checks:

- Required PNG files
- LinkedIn GIF existence
- LinkedIn GIF frame count
- Basic image density
- Basic canvas usage
- Contact sheet creation

The QA script does not fully check:

- Whether the writing is good
- Whether the source was understood correctly
- Whether the title makes sense
- Whether the design is beautiful
- Whether a slide feels repetitive

That is why the contact sheet inspection is mandatory.

## What To Do When QA Fails

### If Missing Files Fail

Problem:

```text
missing > 0
```

Fix:

1. Check the output folder path.
2. Rerun the renderer.
3. Make sure the JSON spec is valid.
4. Make sure the script completed without errors.

### If GIF Fails

Problem:

```text
gif_issue is not null
```

Fix:

1. Check `LinkedIn\images\linkedin-animation.gif`.
2. Make sure the renderer created more than one frame.
3. Check that the `steps` array has at least two rows.
4. Rerun the renderer.

### If Images Are Too Sparse

Problem:

```text
failures > 0
```

Common causes:

- Title is too short.
- Subtitle is missing.
- Slide has only one small text box.
- Lower half of the image is empty.
- X card has too little text.
- Facebook card has a blank middle.
- LinkedIn thumbnail uses a sparse cover instead of the dense lesson template.

Fix:

1. Open the failed image.
2. Open the contact sheet.
3. If only one image is weak, edit the JSON content.
4. If many images are weak, edit the renderer template.
5. Rerender the whole package.
6. Rerun QA.

## When To Edit JSON Versus Python

Edit JSON when:

- The title is weak.
- The subtitle is unclear.
- A step needs better wording.
- A quote is too short.
- A slide body is too vague.

Edit Python when:

- Many images have the same layout problem.
- The template leaves too much blank space.
- A platform needs a new module.
- Text is consistently too small.
- Cards overlap.
- The contact sheet shows repeated boring layouts.

Weak/local models should edit JSON first.

Only edit Python when the template itself is the problem.

## Optional HTML Rendering Workflow

Use HTML rendering only when you need browser/CSS layout.

The optional template is:

```text
assets\html-template.html
```

Install HTML requirements:

```powershell
$PY = (Get-Command python).Source
& $PY scripts\setup_requirements.py --with-html --install-browser
```

Render HTML to PNG:

```powershell
$PY = (Get-Command python).Source
& $PY scripts\render_html_image.py --source assets\html-template.html --out output\html-card.png --width 1200 --height 1200
```

Use this only when Pillow layout is not enough.

For most social graphics, use the Pillow package renderer.

## Full Process Used To Create This Workflow

### 1. The Original Problem

The generated images had too much white space.

The user said:

- LinkedIn image and animation should have the same content.
- LinkedIn titles should make sense as standalone posts.
- X posts should stand alone.
- Instagram slides should have more subtext.
- Slides should not all look the same.
- Not every slide should use a prompt box.
- Prompt boxes, tips, and instructions should be labeled correctly.
- Every slide should be rechecked for meaning and readability.
- QA must happen before saying the images are done.

### 2. First QA Pass

A QA script was created:

```text
AIS-OS\tools\qa_repurpose_images.py
```

It checked:

- 8 packages
- Required image files
- LinkedIn GIF frame count
- Whitespace/density metrics
- Contact sheets

Initial failures:

```text
9 image failures
```

Most failures were LinkedIn thumbnails.

One failure was an Instagram cover.

### 3. Failed LinkedIn Issue

Problem:

LinkedIn thumbnails were still using an old sparse cover template.

They had:

- Title
- Short subtitle
- Large empty middle/lower area

Fix:

The renderer was patched so `linkedin-thumbnail.png` uses the same dense LinkedIn lesson renderer as:

```text
linkedin-diagram.png
linkedin-animation.gif
```

Result:

LinkedIn static image, diagram, and GIF now share the same source-specific lesson structure.

### 4. Failed Instagram Cover Issue

Problem:

Instagram cover technically passed later, but visually still had too much quiet middle space.

Fix:

The cover renderer was patched to add four labeled modules:

- SOURCE LESSON
- USE IT FOR
- QA GATE
- SAVE THIS

Result:

The cover kept the intro style but became more useful and less empty.

### 5. Facebook Visual Issue

Problem:

Facebook images passed numeric QA but visually had a quiet middle band.

Fix:

Facebook renderer was patched to add compact modules:

- TASK
- CONTEXT
- REVIEW

The practice checklist was made dynamic so the sections do not overlap.

Result:

Facebook cards became denser without obvious clipping.

### 6. Final Repurpose Image QA

After fixes, QA was rerun.

Final result:

```json
{
  "packages_checked": 8,
  "pngs_checked": 160,
  "missing_gif_issues": 0,
  "automated_image_failures": 0
}
```

Contact sheets were visually inspected for:

- LinkedIn
- Instagram
- X
- Facebook

### 7. User Asked What Generated The Images

Answer:

The images were generated with local HTML/Python rendering, not GPT Image.

Actual renderer:

```text
Python + Pillow
```

Optional renderer:

```text
HTML + Playwright screenshot
```

### 8. User Asked For A Reusable Skill

A new reusable local skill was created:

```text
AIS-OS\.claude\skills\html-python-image-renderer
```

Purpose:

Let a local model generate images without Codex or GPT Image access.

The skill contains:

- Requirement setup script
- Pillow package renderer
- Optional HTML renderer
- QA script
- Sample JSON spec
- HTML template
- SOP reference

### 9. Skill Creation Failure

Problem:

The skill initializer rejected the first `short_description`.

Error:

```text
short_description must be 25-64 characters
```

Cause:

The generated UI description was too long.

Fix:

The skill folder was kept and the final `agents\openai.yaml` was written manually with a shorter description.

Final short description:

```text
Generate local social images from templates.
```

### 10. Python PATH Failure

Problem:

Running scripts directly inside the skill folder failed:

```text
python is not recognized
```

Cause:

PowerShell did not resolve `python` in that command context.

Fix:

The SOP and skill commands were updated to resolve Python first:

```powershell
$PY = (Get-Command python).Source
& $PY scripts\setup_requirements.py --check
```

This is safer for Windows.

### 11. Sample QA Failure

Problem:

The sample package rendered successfully, but QA failed 8 X images.

Failure:

```text
X card text appears too sparse.
```

Cause:

The X QA threshold was too strict for normal tweet-style cards.

X cards are intentionally simpler than carousels and should not be filled with fake labels or footers.

Fix:

The X density rule was relaxed so normal tweet cards pass if they contain real text, while near-empty cards still fail.

Old idea:

```text
Fail X if ink < 0.055
```

New idea:

```text
Fail X if ink < 0.02 or bbox < 0.20
```

Result:

Sample QA passed.

### 12. Skill Validation

The skill was validated with:

```powershell
python "C:\Users\DELL\.codex\skills\.system\skill-creator\scripts\quick_validate.py" "C:\Users\DELL\Master Project\Stan OS\AIS-OS\.claude\skills\html-python-image-renderer"
```

Result:

```text
Skill is valid!
```

### 13. Requirement Check

Requirement check result:

```text
missing: []
```

Meaning:

Pillow was already installed.

### 14. Sample Render Test

Sample render command:

```powershell
$PY = (Get-Command python).Source
& $PY scripts\render_image_package.py --spec assets\sample_spec.json --out output\sample-package
```

Result:

```text
status: rendered
```

### 15. Sample QA Test

Sample QA command:

```powershell
$PY = (Get-Command python).Source
& $PY scripts\qa_image_package.py --root output\sample-package
```

Result:

```json
{
  "checked": 20,
  "missing": 0,
  "failures": 0,
  "gif_issue": null
}
```

### 16. Cleanup

The generated sample output was removed after validation so the skill folder stayed clean.

Only reusable files remain in the skill folder.

## Current Final Skill Files

```text
AIS-OS\.claude\skills\html-python-image-renderer\SKILL.md
AIS-OS\.claude\skills\html-python-image-renderer\agents\openai.yaml
AIS-OS\.claude\skills\html-python-image-renderer\assets\sample_spec.json
AIS-OS\.claude\skills\html-python-image-renderer\assets\html-template.html
AIS-OS\.claude\skills\html-python-image-renderer\references\local-rendering-sop.md
AIS-OS\.claude\skills\html-python-image-renderer\scripts\setup_requirements.py
AIS-OS\.claude\skills\html-python-image-renderer\scripts\render_image_package.py
AIS-OS\.claude\skills\html-python-image-renderer\scripts\render_html_image.py
AIS-OS\.claude\skills\html-python-image-renderer\scripts\qa_image_package.py
```

## Dummy-Friendly Execution Checklist

Use this checklist every time.

### First Time Only

1. Open PowerShell.
2. Go to the skill folder:

```powershell
cd "C:\Users\DELL\Master Project\Stan OS\AIS-OS\.claude\skills\html-python-image-renderer"
```

3. Find Python:

```powershell
$PY = (Get-Command python).Source
```

4. Check requirements:

```powershell
& $PY scripts\setup_requirements.py --check
```

5. Install requirements if missing:

```powershell
& $PY scripts\setup_requirements.py
```

### Every New Image Package

1. Copy `assets\sample_spec.json`.
2. Rename the copy for the new project.
3. Edit the title, subtitle, steps, slides, and quotes.
4. Render:

```powershell
$PY = (Get-Command python).Source
& $PY scripts\render_image_package.py --spec assets\sample_spec.json --out output\my-package
```

5. QA:

```powershell
$PY = (Get-Command python).Source
& $PY scripts\qa_image_package.py --root output\my-package
```

6. Open:

```text
output\my-package\qa\contact-sheet.png
```

7. Inspect every image.
8. Fix the JSON or renderer if needed.
9. Rerender.
10. Rerun QA.
11. Only call it done when QA and visual inspection pass.

## Final Rule

Never say:

```text
The images are done.
```

until:

```text
QA passes + contact sheet is inspected + no obvious visual issue remains.
```

That rule exists because file generation is not the same thing as image quality.
