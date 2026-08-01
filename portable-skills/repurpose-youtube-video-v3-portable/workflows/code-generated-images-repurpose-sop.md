# SOP: Code-Generated Social Images From Repurpose Packages

## Purpose

Use this duplicated workflow when a repurpose package needs final PNG/GIF assets generated with code instead of an editable design studio. This keeps the original `repurpose-youtube-video-execution-sop.md` untouched and gives deterministic image rendering its own lane.

This workflow is for:

- One source package under `AIS-OS/asset-folder/content/<slug>/`.
- One design per output image.
- Local code-rendered images using Python/Pillow or HTML screenshots.
- LinkedIn, Instagram, X, and Facebook assets in the existing package format.
- Preview, QA, approval folders, and a truthful `manifest.json`.

## Skill Name

Use `code-generated-social-images`.

The skill is a duplicate of the repurpose skill, narrowed to local image generation and QA.

## Required References

Read these before execution:

- `AIS-OS/workflows/repurpose-social-full-package-dumb-model-sop.md`
- `AIS-OS/workflows/local-html-python-image-rendering-full-workflow.md`
- `AIS-OS/.claude/skills/code-generated-social-images/SKILL.md`
- `AIS-OS/.claude/skills/html-python-image-renderer/SKILL.md`

## Folder Contract

Use the existing repurpose package root:

```text
AIS-OS/asset-folder/content/<slug>/
  source/
  drafts/
    LinkedIn/images/
    LinkedIn/text/
    Instagram/images/
    Instagram/text/
    X/images/
    X/text/
    Facebook/images/
    Facebook/text/
  preview/
  approved/
  published/
  manifest.json
```

Do not create a separate `visuals/png` folder as the primary deliverable.

## Rendering Rules

1. Generate real images with code before calling a package complete.
2. Keep one design spec per image so every image can be edited or regenerated independently.
3. Use Stanley's locked social template unless he explicitly asks for a new template.
4. Put generated PNGs directly in the platform `drafts/<Platform>/images/` folder.
5. Keep prompt/spec/source files next to the output images when useful.
6. Keep LinkedIn GIF/static content aligned when the source is a process, framework, or workflow.
7. Confirm Stanley's real avatar from `AIS-OS/asset-folder/Brand_Assets/Stan Avatar.png` appears where the template requires it.
8. Always save the exact code used to generate the images inside the package as
   `source/render_social_images.py`. If the renderer was run from `tools/` or a
   skill folder, copy that executed script into the package after rendering.

## QA Gate

Before approval:

- Run the deterministic renderer QA.
- Create or update `preview/image-qa.md`.
- Inspect representative output images or a contact sheet.
- Confirm there is no clipped text, fake avatar, repeated weak layouts, unreadable type, or excessive whitespace.
- Confirm `manifest.json` tells the truth about image status.

## Handoff

After successful rendering, send Stanley:

- The content package path.
- The image folder paths.
- The preview and QA files.
- Which platform(s) are ready for approval.
