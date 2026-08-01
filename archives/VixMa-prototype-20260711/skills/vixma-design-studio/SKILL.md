---
name: vixma-design-studio
description: Create editable VixMa local browser designs from AIS-OS repurpose packages, with no login, local project memory, one design per image, and PNG export.
---

# VixMa Design Studio

Use `AIS-OS/workflows/vixma-editable-design-repurpose-sop.md`.

VixMa lives in `AIS-OS/VixMa/`. Start the prototype with:

```powershell
.\VixMa\start-vixma.ps1
```

Rules:

- Keep VixMa local-first and no-login.
- Use one editable design per final image.
- Save project memory locally.
- Export PNGs back to the repurpose package when asked.
- Use `https://github.com/penpot/penpot` as the future full-fork base if no local source tree is available.
