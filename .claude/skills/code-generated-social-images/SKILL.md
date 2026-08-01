---
name: code-generated-social-images
description: Generate final social media PNG/GIF assets from AIS-OS repurpose packages using deterministic local code instead of editable VixMa/Penpot canvases. Use for local Python/Pillow or HTML-rendered LinkedIn, Instagram, X, and Facebook images, contact sheets, image QA, and one-design-per-image specs.
---

# Code-Generated Social Images

## Purpose

Create final image files for repurpose packages with local code. This is the deterministic image-generation lane split away from VixMa's editable design lane.

## Required Workflow

Read `AIS-OS/workflows/repurpose-social-full-package-dumb-model-sop.md` before executing.

Also read:

- `AIS-OS/workflows/local-html-python-image-rendering-full-workflow.md`
- `AIS-OS/.claude/skills/html-python-image-renderer/SKILL.md`

## Operating Rules

- Preserve the original repurpose workflow.
- Render real PNG/GIF files before calling a package complete.
- Keep one design/spec per image.
- Store final images inside `drafts/<Platform>/images/`.
- Keep editable JSON/spec files near their rendered outputs when possible.
- Run image QA and write `preview/image-qa.md`.
- Inspect representative visuals or a contact sheet before handoff.

## Output

Return the content package path, generated image paths, QA path, and which platform assets are ready for approval.
