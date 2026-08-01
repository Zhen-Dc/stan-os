# SOP: VixMa Editable Design Repurpose Workflow

## Purpose

Use this duplicated workflow when a repurpose package should become editable
designs inside VixMa instead of being rendered only by code.

VixMa is the full custom-branded Penpot 2.16.2 fork in `AIS-OS/VixMa/`. It
keeps Penpot's complete editor, boards, pages, layers, components, libraries,
version history, collaboration internals, and exporters while running as a
localhost-only, single-owner application with no authentication UI.

The deterministic code-rendering lane remains separate in
`workflows/code-generated-images-repurpose-sop.md`.

## Runtime

- App root: `AIS-OS/VixMa/`
- Start command: `AIS-OS/VixMa/start-vixma.ps1`
- Browser URL: `http://localhost:9004`
- Local data: `AIS-OS/VixMa/data/`
- Owner: imported `Stan Local` profile
- Authentication: disabled through VixMa local-owner mode
- Upstream base: `https://github.com/penpot/penpot`
- Compatible release: `2.16.2`

Do not rename the `.penpot` interchange format or remove upstream MPL notices.

## Required References

Read:

- `AIS-OS/.claude/skills/vixma-design-studio/SKILL.md`
- `AIS-OS/workflows/repurpose-youtube-video-execution-sop.md`
- `AIS-OS/workflows/repurpose-social-full-package-dumb-model-sop.md`
- `AIS-OS/references/penpot-openmontage-content-workflow.md`

## Source Package Contract

Use the established package root:

```text
AIS-OS/asset-folder/content/<slug>/
  source/
  drafts/
    LinkedIn/{images,text}/
    Instagram/{images,text}/
    Facebook/{images,text}/
    X/{images,text}/
    Threads/{images,text}/
    TikTok/{images,text}/
  preview/
    preview.md
    image-qa.md
    vixma-projects.json
  approved/
  published/
  manifest.json
```

Create missing Threads and TikTok folders only when those platform assets are
requested. Do not weaken the original LinkedIn, Instagram, Facebook, and X
package requirements.

## VixMa Project Model

Create one VixMa project per platform:

```text
<slug> / LinkedIn
<slug> / Instagram
<slug> / Facebook
<slug> / X
<slug> / Threads
<slug> / TikTok
```

Inside each platform project:

- Create one editable file for each content version.
- Name versions `v01`, `v02`, and so on.
- Create one board per final image.
- Put all carousel slides in one file as separate ordered boards.
- Keep text, shapes, colors, images, logos, badges, creator rows, and accents as
  independent editable layers.
- Link reusable elements to the Stanley brand library.

When package content changes, create the next version. Do not overwrite an
earlier version, even when its export is no longer current.

## Stanley Brand Library

Maintain one reusable VixMa library containing:

- Locked Stanley social-template components.
- Stanley avatar from
  `AIS-OS/asset-folder/Brand_Assets/Stan Avatar.png`.
- Brand colors and typography.
- Logos and creator-row components.
- Platform board presets and export sizes.
- Cover, content, quote, process, CTA, and carousel-navigation components.

Template changes require Stanley's explicit instruction.

## Generation Sequence

1. Validate the repurpose package and source confidence.
2. Start VixMa and verify the local-owner profile opens directly.
3. Load or create the Stanley brand library.
4. Create or resolve the platform project.
5. Determine the next content version.
6. Create one file for that version.
7. Create one board per required image.
8. Populate editable layers from source-derived platform drafts.
9. Apply the locked Stanley template and real brand assets.
10. Save the project and verify it survives refresh.
11. Export each board to the matching platform image folder.
12. Inspect representative exports and update image QA.
13. Write `preview/vixma-projects.json` with project, file, board, version,
    source, and export mappings.
14. Update `preview/preview.md` and `manifest.json` truthfully.

## Project Record Schema

Use:

```json
{
  "source_slug": "<slug>",
  "vixma_url": "http://localhost:9004",
  "template": "Stanley Social Template",
  "projects": [
    {
      "platform": "LinkedIn",
      "project_name": "<slug> / LinkedIn",
      "project_id": "<uuid>",
      "file_name": "<slug> / LinkedIn / v01",
      "file_id": "<uuid>",
      "version": 1,
      "boards": [
        {
          "name": "Slide 01",
          "board_id": "<uuid>",
          "export_path": "drafts/LinkedIn/images/slide-01.png"
        }
      ]
    }
  ]
}
```

## Completion Gate

A VixMa package is complete only when:

- No login, registration, password, or logout action appears.
- Every requested platform has its own VixMa project.
- Every final image has a corresponding editable board.
- Carousel order is correct in one editable file.
- The locked Stanley template and real avatar are used.
- Earlier content versions remain available.
- Browser refresh preserves the designs.
- Actual PNG exports exist under platform image folders.
- `preview/vixma-projects.json`, preview, QA, and manifest are valid.

## First Automation Milestone

Generate one LinkedIn carousel from an existing repurpose package as one VixMa
project, one versioned editable file, and multiple ordered boards. Export every
board to `drafts/LinkedIn/images/`, then repeat the same model for the other
platforms.
