---
name: html-python-image-renderer
description: Generate deterministic social images locally with Python/Pillow or HTML screenshot rendering when AI image models are unavailable. Use when a task needs PNG/JPG/GIF social graphics, carousel slides, quote cards, thumbnails, contact sheets, whitespace/density QA, local installation of image-rendering requirements, or a repeatable non-AI image-generation workflow for weak/local LLMs.
---

# HTML/Python Image Renderer

## Purpose

Use this skill to generate social media images without GPT image models. Prefer the bundled Python/Pillow renderer for reliable local output. Use the optional HTML renderer only when the user needs browser-accurate CSS layout.

## Required Workflow

1. Read `references/local-rendering-sop.md` before generating or fixing images.
2. Check or install requirements:

```powershell
$PY = (Get-Command python).Source
& $PY scripts/setup_requirements.py --check
& $PY scripts/setup_requirements.py
```

3. Create or edit a JSON spec. Start from `assets/sample_spec.json`.
4. Render the package:

```powershell
$PY = (Get-Command python).Source
& $PY scripts/render_image_package.py --spec assets/sample_spec.json --out output/sample-package
```

5. QA before saying the work is done:

```powershell
$PY = (Get-Command python).Source
& $PY scripts/qa_image_package.py --root output/sample-package
```

6. Open the generated `qa/contact-sheet.png` and visually inspect it for whitespace, clipping, readability, repeated layouts, and whether every image can stand alone.

## Renderer Selection

- Use `render_image_package.py` for LinkedIn images/GIFs, Instagram carousel slides, X quote cards, Facebook cards, and dense educational graphics.
- Use `render_html_image.py` only when CSS/HTML layout is required. Install HTML dependencies with:

```powershell
$PY = (Get-Command python).Source
& $PY scripts/setup_requirements.py --with-html
```

## Non-Negotiable QA Rules

- Do not call an image package done until `qa_image_package.py` reports `failures: 0`.
- Do not rely only on file counts. Inspect the contact sheet.
- Fix large blank areas, tiny unreadable text, clipped text, repeated slide layouts, vague titles, and any post that feels like a continuation instead of a standalone post.
- If a box contains a prompt, label it `PROMPT`. If it contains a tip, label it `TIPS`. If it contains instructions, label it `INSTRUCTION`.
- LinkedIn static image and LinkedIn GIF must share the same core content.

## Stanley Accepted Carousel Rules

- For repurposed Instagram carousels, slide 1 is a cover rendered from `cover-prompt.json`, not a normal slide.
- The accepted cover style is cream grid, huge 1-3 line headline, one orange highlighted phrase, tool tag directly above the title, subtitle below the title, and profile pill directly under the subtitle.
- Cover headline should dominate about 60% of a 1080x1350 canvas.
- Preserve exact user-provided title and subtext.
- If Stanley does not provide cover subtext, write a specific summary of what the post is about. It should add context to the title, not sound like a generic slogan. Good shape: `This is how I would explain/use/build [tool/topic]: [specific angle].`
- Use `Stanley Chima` as the visible name and `chima-stanley-chuku` as the visible username unless the user overrides it.
- Store profile URLs in JSON metadata such as `profile_url`; never draw Markdown link syntax on the image.
- Use `asset-folder/Brand_Assets/Stan Avatar.png` for the profile photo.
- On slides 2-8, start the first content section close under the title/subtitle and use whitespace for useful audience-facing modules.
- Do not print internal QA instructions like `stand alone`, `single post`, `contain enough information`, or `this slide should make sense` inside public images.
- Save the exact executed renderer in the content package at `source/render_social_images.py`.

## Files

- `scripts/setup_requirements.py`: installs/checks local Python requirements.
- `scripts/render_image_package.py`: deterministic Pillow renderer for social packages.
- `scripts/render_html_image.py`: optional HTML-to-PNG screenshot renderer.
- `scripts/qa_image_package.py`: density/whitespace QA and contact sheet creator.
- `assets/sample_spec.json`: starter content spec.
- `assets/html-template.html`: starter HTML template for optional browser rendering.
- `references/local-rendering-sop.md`: full SOP for weak/local models.
