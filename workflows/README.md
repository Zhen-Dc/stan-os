# Workflows

This folder holds WAT workflows: Markdown SOPs the AIOS can run end to end.

Use a workflow when a process is repeatable, has clear inputs and outputs, and benefits from a stable sequence instead of improvisation.

Each workflow should include:

- Objective
- Required inputs
- Tools or scripts to use
- Steps
- Expected outputs
- Edge cases and recovery notes
- Where the final deliverable should live

Do not overwrite a workflow casually. Improve it when real use reveals better methods, constraints, timing issues, rate limits, or failure modes.

## Available Workflows

- `video-production-sop.md` - Default raw-footage-to-finished-video lane for transcript packing, filler-word removal, strategy approval, preview renders, HyperFrames motion graphics, and final delivery.
- `repurpose-social-full-package-dumb-model-sop.md` - Canonical full-package SOP for repurposed social content. Use this as the only execution checklist for package creation, image rendering, QA, preview, and manifest validation.
- `repurpose-youtube-video-v3` skill copy - Default repurpose lane for web URLs. It uses Firecrawl first, creates Instagram cover/slide JSON prompt files, then renders the same final PNG/GIF package.

## Repurpose Routing Rule

If Stanley gives a LinkedIn/social/blog/article/Substack/web URL and says
"repurpose this post", "recreate this", "turn this into content", or similar,
do not stop at source analysis, a loose draft, a single SVG, or a flat PNG
folder.

Use this sequence:

1. Run Firecrawl through
   `.claude/skills/repurpose-youtube-video-v3/scripts/firecrawl_scrape.py`.
   The script auto-detects local Firecrawl at `http://localhost:3002` for local
   models. Do not use the old `webscraper` skill for v3 web capture.
2. Read `repurpose-social-full-package-dumb-model-sop.md` as the single
   canonical execution SOP.
3. Execute `repurpose-social-full-package-dumb-model-sop.md` to create the
   full local social package under `asset-folder/content/<slug>/`.
4. Put platform text and generated media under the required
   `drafts/<Platform>/text` and `drafts/<Platform>/images` folders.
5. For Instagram, create `cover-prompt.json`, `slide-blueprint.json`, and one
   `slide-XX-prompt.json` per carousel slide before rendering.
6. Create `preview/preview.md`, `preview/image-qa.md`, and a valid
   `manifest.json` that lists the generated image and animation counts.

If Stanley explicitly asks for analysis, swipe-file research, or strategy notes
without a repurposed content package, still use
`repurpose-social-full-package-dumb-model-sop.md` and stop after its source
analysis section.

## Video Editing Routing Rule

If Stanley drops raw footage into a folder or asks to edit a video end to end,
do not jump straight into ad hoc ffmpeg commands or motion-graphics generation.

Use this sequence:

1. Read `video-production-sop.md`.
2. Verify the machine stack with `tools/check-video-studio.ps1`.
3. Use the local `video-use` skill to inventory footage, build transcripts, and
   create `edit/takes_packed.md`.
4. Propose the edit strategy in plain English and wait for approval before
   making cut decisions.
5. Render `edit/preview.mp4` first, self-check the cut boundaries, then add
   HyperFrames or motion-graphics work only when the base edit is solid.
6. Keep all outputs inside the source folder's `edit/` directory, including
   transcripts, EDL, animations, previews, and final renders.
