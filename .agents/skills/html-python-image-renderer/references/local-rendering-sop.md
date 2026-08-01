# SOP: Local HTML/Python Social Image Rendering

## Purpose

Use this SOP when you need to create social images without GPT Image, Midjourney, Canva, or any cloud image model. The system generates images from deterministic templates using local Python.

This is meant for weak/local models. Do not ask the model to design every pixel from scratch. Make it edit a JSON spec, run the renderer, run QA, inspect the contact sheet, and fix the template only when needed.

## What This Skill Produces

- LinkedIn static thumbnail
- LinkedIn diagram image
- LinkedIn animated GIF
- Instagram 9-slide carousel
- X quote cards
- Facebook thumbnail and course card
- QA report
- Contact sheet for visual inspection

## Folder Contract

For each package, use this structure:

```text
output-folder/
  LinkedIn/images/
    linkedin-thumbnail.png
    linkedin-diagram.png
    linkedin-animation.gif
  Instagram/images/
    instagram-slide-01.png
    ...
    instagram-slide-09.png
  X/images/
    x-thumbnail.png
    x-quote-01.png
    ...
    x-quote-06.png
    x-quote.png
  Facebook/images/
    facebook-thumbnail.png
    facebook-course-card.png
  qa/
    contact-sheet.png
    qa-report.json
```

## One-Time Setup

From the skill folder:

```powershell
$PY = (Get-Command python).Source
& $PY scripts/setup_requirements.py --check
& $PY scripts/setup_requirements.py
```

If HTML screenshots are needed:

```powershell
$PY = (Get-Command python).Source
& $PY scripts/setup_requirements.py --with-html --install-browser
```

If installation fails, report the exact missing package or network error. Do not pretend the renderer worked.

## Basic Use

1. Copy or edit `assets/sample_spec.json`.
2. Replace the content fields:
   - `package_title`
   - `creator_name`
   - `handle`
   - `badge`
   - `title`
   - `subtitle`
   - `bottom_takeaway`
   - `steps`
   - `slides`
   - `quotes`
3. Render:

```powershell
$PY = (Get-Command python).Source
& $PY scripts/render_image_package.py --spec assets/sample_spec.json --out output/my-package
```

4. QA:

```powershell
$PY = (Get-Command python).Source
& $PY scripts/qa_image_package.py --root output/my-package
```

5. Open `output/my-package/qa/contact-sheet.png`.
6. Only say done if the QA command has zero failures and the contact sheet looks good.

## JSON Writing Rules

Keep the model away from layout code unless there is a real template bug. Most jobs should only change JSON.

Write content like this:

- `title`: clear standalone headline, not a continuation title.
- `subtitle`: explain the value of the image in one or two lines.
- `bottom_takeaway`: one memorable lesson.
- `steps`: five labeled rows for LinkedIn and GIF.
- `slides`: nine standalone carousel slides.
- `quotes`: six standalone X posts.

Avoid:

- vague phrases like "unlock your potential"
- jargon that normal people would not understand
- titles that only make sense after reading a previous slide
- repeated slide text
- fake claims, fake metrics, or fake source details

## Slide Rules

Every Instagram slide must stand alone.

Slide 1:

- Treat slide 1 as the carousel cover.
- Render it from `drafts/Instagram/images/cover-prompt.json`.
- Use a cream grid background, huge 1-3 line headline, one orange highlighted
  phrase, small tool tag directly above the title, subtitle directly below the
  title, and profile pill directly under the subtitle.
- The cover headline should fill about 60% of the canvas.
- Preserve exact user-provided title and subtext.
- If no exact cover subtext is provided, write a specific one-line summary that
  gives context for the title. It should say what the post is actually about,
  such as `This is how I would explain Claude to anyone: start with one real
  task, then let Claude ask the questions.`
- Use `chima-stanley-chukwu` as the display name, `@chima-stanley-chukwu` as the visible
  username, and `asset-folder/Brand_Assets/Stan Avatar.png` as the profile
  photo unless Stanley gives replacements.

Slides 2-9:

- Use varied modules
- Mix checklist, instruction, comparison, workflow, tips, tech stack, QA gate, output, and save-this panels
- Do not make every slide a prompt box
- Start the first content section close under the title/subtitle. Do not leave a
  large blank band.
- Fill whitespace with useful public-facing details, not filler.
- If a prompt is shown, label it `PROMPT`
- If a tip is shown, label it `TIPS`
- If instructions are shown, label them `INSTRUCTION`
- Never render internal QA instructions such as `stand alone`, `single post`,
  `contain enough information`, or `this slide should make sense`.

## LinkedIn Rules

LinkedIn static image and LinkedIn GIF must use the same core content.

The LinkedIn visual should have:

- badge
- creator row
- title
- subtitle
- five labeled steps
- bottom takeaway

If the thumbnail and GIF do not match, fix the renderer or regenerate both.

## X Rules

X cards should look like normal tweet screenshots:

- avatar area
- name
- handle
- tweet text

Do not add carousel labels, lesson labels, footers, timestamps, or fake engagement rows unless the user asks.

Each X card must make sense as a single standalone post.

## Facebook Rules

Facebook images should be beginner-friendly and practical.

Use:

- strong title
- short subtext
- compact task/context/review modules
- clear practice checklist

Avoid a blank middle band.

## QA Rules

Run:

```powershell
$PY = (Get-Command python).Source
& $PY scripts/qa_image_package.py --root output/my-package
```

Pass condition:

- `missing: 0`
- `failures: 0`
- `gif_issue: null`
- contact sheet inspected manually

The QA script catches:

- missing required images
- GIF missing or not animated
- very sparse images
- underused canvas

The QA script does not fully catch:

- bad writing
- confusing wording
- wrong source interpretation
- ugly repetition
- subtle text clipping

That is why contact-sheet inspection is mandatory.

## Fixing Failures

If one image fails:

1. Open the image.
2. Check whether text is too short, too small, clipped, or too sparse.
3. Edit the JSON if content is weak.
4. Edit the renderer only if the template leaves too much blank space.
5. Rerender.
6. Rerun QA.

If many images fail:

1. Do not manually patch PNGs.
2. Fix the template in `scripts/render_image_package.py`.
3. Add cards, chips, rows, bottom bars, or extra modules.
4. Rerender all images.
5. Rerun QA.

## Optional HTML Rendering

Use HTML rendering when CSS layout matters more than the Pillow template.

Install:

```powershell
$PY = (Get-Command python).Source
& $PY scripts/setup_requirements.py --with-html --install-browser
```

Render:

```powershell
$PY = (Get-Command python).Source
& $PY scripts/render_html_image.py --source assets/html-template.html --out output/html-card.png --width 1200 --height 1200
```

Then include that PNG in the package or inspect it manually.

## Final Handoff

Report:

- output folder
- QA report path
- contact sheet path
- number of images checked
- failures count
- anything not fixed

Never say "done" before QA and contact-sheet inspection.
