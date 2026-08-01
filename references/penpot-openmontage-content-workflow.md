# Penpot + OpenMontage Content Workflow

Stan OS has its own local Penpot stack and OpenMontage checkout for internet-inspired content recreation, social graphics, and video planning.

## Local services

- Penpot: http://localhost:9002
- Penpot mail catcher: http://localhost:1081
- Penpot compose file: `C:\Users\DELL\Master Project\Stan OS\external\penpot-local\docker-compose.yml`
- Penpot local access note: `C:\Users\DELL\Master Project\Stan OS\external\penpot-local\local-login.md`
- OpenMontage: `C:\Users\DELL\Master Project\Stan OS\external\OpenMontage`

Penpot does not have a supported persistent no-auth mode. This local stack uses a permanent local profile with public registration and onboarding disabled. Login once in the normal browser profile, then keep using the saved session.
- FFmpeg binary: `C:\Users\DELL\AppData\Local\Microsoft\WinGet\Packages\Gyan.FFmpeg_Microsoft.Winget.Source_8wekyb3d8bbwe\ffmpeg-8.1.2-full_build\bin\ffmpeg.exe`

## What Penpot is for

Use Penpot as the editable design platform for Stan's reusable social media image assets: carousels, quote cards, platform covers, thumbnails, comparison images, promo layouts, and recreated reference styles.

Recommended Penpot organization:

- Create one Penpot project for each brand, content pillar, or campaign.
- Keep each internet reference or recreated concept as a separate Penpot file.
- Create pages named by platform, for example `Instagram Feed`, `Instagram Story`, `TikTok Cover`, `LinkedIn`, `YouTube Thumbnail`.
- Export production-ready files into `C:\Users\DELL\Master Project\Stan OS\AIS-OS\asset-folder\penpot-exports\`.

Useful frame sizes:

- Instagram portrait feed: 1080 x 1350
- Instagram square: 1080 x 1080
- Reels, Shorts, TikTok cover/story: 1080 x 1920
- YouTube thumbnail: 1280 x 720
- LinkedIn image post: 1200 x 627
- X image post: 1600 x 900

## What OpenMontage is for

Use OpenMontage as the structured video production planner. It can help convert a reference, content idea, or Penpot image system into a pipeline: script, scenes, asset list, tool choices, review gates, and rendering handoff.

Stan OS already has scraping, HyperFrames, and video-use. In this system:

- Existing scraper collects allowed references and source facts.
- Penpot stores editable image designs and platform variants.
- OpenMontage coordinates the production plan and asset/review steps.
- HyperFrames and video-use remain the preferred tools for hands-on video editing and final social video assembly when they fit better.

## Working process

1. Save the internet reference and rights notes in Stan OS.
2. Create a content brief: audience, promise, platform, hook, source inspiration, and what must be original.
3. Recreate/adapt the design in Penpot so Stan can manually edit it later.
4. Export platform-specific image assets to `AIS-OS\asset-folder\penpot-exports\`.
5. Use OpenMontage to turn the brief/assets into a video plan, scene plan, or production checklist.
6. Use HyperFrames/video-use for animated edits, captions, render previews, and final video output.
7. Save approved assets and videos in the relevant Stan OS content package.

## Commands

Start Penpot:

```powershell
.\AIS-OS\tools\start_penpot_stan.ps1
```

Check OpenMontage:

```powershell
.\AIS-OS\tools\check_openmontage_stan.ps1
```

