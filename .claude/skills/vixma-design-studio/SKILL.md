---
name: vixma-design-studio
description: Create editable multi-platform social designs inside the local VixMa Penpot fork from AIS-OS repurpose packages. Use when Stanley asks for VixMa, editable designs, brand libraries, platform projects, carousel boards, template-driven social assets, local no-login design editing, or exporting repurpose package images from editable files.
---

# VixMa Design Studio

## Purpose

Turn one AIS-OS repurpose package into editable VixMa projects that Stanley can
open, revise, version, and export in the browser.

VixMa is the full Penpot 2.16.2 fork at `AIS-OS/VixMa/`. It runs locally at
`http://localhost:9004`, injects one local owner at the backend boundary, and
has no login, registration, password, logout, or session requirement.

## Required Workflow

Read `AIS-OS/workflows/repurpose-social-full-package-dumb-model-sop.md` before execution.

When source drafts or package assets are incomplete, also read:

- `AIS-OS/references/penpot-openmontage-content-workflow.md`

## Operating Rules

- Preserve the code-generated image workflow as a separate lane.
- Start VixMa with `AIS-OS/VixMa/start-vixma.ps1`.
- Create a separate VixMa project for LinkedIn, Instagram, Facebook, X,
  Threads, and TikTok.
- Create one editable board per final image.
- Keep every carousel in one editable file with one board per slide.
- Use the locked Stanley social template exactly unless Stanley requests a
  template change.
- Keep text, shapes, images, colors, typography, logos, and components editable.
- Create a new numbered version when source-package content changes. Never
  overwrite an earlier manually edited version.
- Reuse the VixMa brand library for colors, typography, logos, image assets,
  templates, and components.
- Keep source-derived claims and copy only.
- Export approved PNGs into the matching
  `drafts/<Platform>/images/` package folder.
- Record VixMa project, file, board, version, source, and export identifiers in
  `preview/vixma-projects.json`.
- Preserve `.penpot` compatibility and upstream license notices.

## Project Naming

Use:

```text
<slug> / <Platform>
<slug> / <Platform> / vNN
```

Use one project per platform. Within a project, use one file per content version.
For carousels, name boards `Slide 01`, `Slide 02`, and so on.

## Completion Gate

Do not call a VixMa run complete until:

- VixMa opens without an authentication screen.
- Every requested platform has an editable project and file.
- Every final image maps to a separate editable board.
- The Stanley template and real brand assets are present.
- A refreshed browser still shows the saved project.
- Exported PNGs exist in the package platform folders.
- `preview/vixma-projects.json`, `preview/preview.md`,
  `preview/image-qa.md`, and `manifest.json` are truthful.

## Output

Return the VixMa URL, source package, project/version names, project record path,
and exported image paths.
