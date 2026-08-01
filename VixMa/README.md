# VixMa

VixMa is Stanley's local AI design studio and brand asset builder. It is a
custom-branded fork of Penpot 2.16.2 that keeps the complete editable design
editor while adding a localhost-only, single-owner mode with no login screen.

## Local Use

Run:

```powershell
.\start-vixma.ps1
```

VixMa opens at `http://localhost:9004`. The first launch builds the custom
frontend and backend images, mirrors the existing `penpot-stan` designs, and
stores the independent VixMa database and assets under `data/`.

Useful commands:

```powershell
.\build-vixma.ps1
.\mirror-penpot-data.ps1
.\stop-vixma.ps1
```

`data/` and `.env.vixma` are intentionally excluded from Git. Copy the source,
templates, and skills when moving VixMa; create a fresh local data directory on
the destination computer.

## Repurpose Integration

The VixMa workflow creates a separate project for each social platform. A
carousel is one editable file with one board per slide. Repurpose source changes
create a new version so previous manual edits remain available.

## Upstream And License

VixMa is derived from [Penpot](https://github.com/penpot/penpot) and remains
licensed under Mozilla Public License 2.0. Upstream copyright and license notices
must remain in source files and distributions. VixMa branding does not imply
endorsement by the Penpot project or Kaleidos.
