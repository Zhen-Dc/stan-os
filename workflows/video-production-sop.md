# Video Production SOP

## Objective

Turn raw footage into a clean, reviewable, and optionally motion-graphics-enhanced final video without improvising the pipeline every time.

This workflow is the default lane when Stanley provides raw video files and wants help with:

- removing filler words, false starts, and dead space
- selecting the best takes
- creating preview-first edits
- adding captions or subtitles
- adding branded motion graphics, overlays, title cards, or transitions
- rendering a final delivery file

## Required Inputs

- A folder containing the source media files
- The target outcome:
  - content type such as talking head, tutorial, interview, montage, ad, or explainer
  - target platform or aspect ratio if known
  - target runtime if known
  - brand direction, palette, typography, or reference style if motion graphics are needed
- An ElevenLabs API key available only in the local `video-use` skill repo `.env`

## Skills and Tools

- `.agents/skills/video-use/SKILL.md`
  - transcript-driven editing
  - transcript packing
  - EDL creation
  - preview and final renders
- `.agents/skills/hyperframes/SKILL.md`
  - HTML-based overlays, captions, composition structure, transitions
- `.agents/skills/hyperframes-cli/SKILL.md`
  - `npx hyperframes init|lint|inspect|preview|render|doctor`
- `.agents/skills/motion-graphics/SKILL.md`
  - branded motion-graphics structure after the base edit is approved
- `tools/check-video-studio.ps1`
  - quick readiness check for the local stack

## Output Contract

All generated outputs live inside the source folder's `edit/` directory, never inside the skill directories.

Expected structure:

```text
<videos_dir>/
├── <original media files>
└── edit/
    ├── project.md
    ├── takes_packed.md
    ├── edl.json
    ├── transcripts/
    ├── animations/
    ├── clips_graded/
    ├── verify/
    ├── preview.mp4
    ├── final.mp4
    └── final_with_graphics.mp4
```

Use `final_with_graphics.mp4` only when a motion-graphics pass actually happened.

## Stage 0 - Readiness Check

1. Run `tools/check-video-studio.ps1`.
2. Confirm these are available before promising the full pipeline:
   - `python`
   - `node`
   - `ffmpeg`
   - `ffprobe`
   - `npx hyperframes`
3. Confirm the `video-use` repo-local skill contains `helpers/`, `SKILL.md`, and `install.md`.
4. Confirm the local `video-use` `.env` has a real ElevenLabs API key before transcribing.
5. If a dependency is missing, fix that first or clearly tell Stanley what is still blocked.

## Stage 1 - Intake and Inventory

1. Identify the actual working footage folder.
2. List the source files and inspect them with `ffprobe`.
3. Ask only the minimum questions needed to shape the edit:
   - what kind of video this is
   - where it will be published
   - desired runtime or delivery format
   - whether motion graphics are needed now or after the base cut
4. Do not make cut decisions yet.

## Stage 2 - Transcript Build

1. Use `video-use` helpers to transcribe the footage.
2. Cache transcripts under `edit/transcripts/`.
3. Build `edit/takes_packed.md`.
4. Use `takes_packed.md` as the primary reading view for the edit plan.
5. Note obvious filler words, false starts, broken lines, repeated phrases, and good punchline beats.

## Stage 3 - Strategy Approval

Before editing, propose the plan in plain English. Cover:

- the structure of the cut
- which takes or sections to keep
- what will be removed
- whether captions are needed
- whether the first pass is clean edit only or clean edit plus graphics
- the expected output files

Do not touch the cut until the strategy is approved.

## Stage 4 - Base Edit

1. Build `edit/edl.json` using transcript word boundaries.
2. Never cut inside a word.
3. Pad cut edges slightly to absorb transcript timestamp drift.
4. Prefer silence gaps and natural phrase boundaries.
5. Render a base preview to `edit/preview.mp4`.
6. Self-check the preview at cut boundaries before showing it as ready.

Base-edit rule:

- The clean edit must stand on its own before motion graphics are added.

## Stage 5 - Motion Graphics Layer

Only start this stage after the base edit is solid or explicitly approved.

Use cases:

- title cards
- lower thirds
- animated UI callouts
- diagram or explainer overlays
- branded intros and outros
- scene transitions

Flow:

1. If the user wants graphics, collect palette, accent color, background tone, brand name, typography direction, and any logo source.
2. Use `motion-graphics` when the request is a structured branded explainer or polished visual layer.
3. Use `hyperframes` for the actual HTML composition and scene timing.
4. Use `hyperframes-cli` for `lint`, `inspect`, `preview`, and `render`.
5. Keep motion-graphics source files in `edit/animations/slot_<id>/` or a clearly named local composition folder under `edit/`.
6. Preview the graphics pass before final render whenever practical.

## Stage 6 - Render and QA

1. Render the clean final edit to `edit/final.mp4`.
2. If graphics were added, render the polished version to `edit/final_with_graphics.mp4`.
3. Re-check:
   - visible cut flashes
   - audio pops at segment joins
   - subtitle placement
   - overlay timing
   - final duration
   - aspect ratio and framing
4. If HyperFrames is used:
   - run `npx hyperframes lint`
   - run `npx hyperframes inspect`
   - use `npx hyperframes preview` for the review loop
   - render only after lint and inspect are clean enough to trust

## Stage 7 - Session Memory

Append a short session note to `edit/project.md` with:

- strategy used
- important decisions
- unresolved issues
- what to preserve for the next edit round

## Edge Cases and Recovery Notes

- If `ffmpeg` or `ffprobe` is missing, the workflow is not render-ready. Fix the machine dependency before promising final output.
- If the ElevenLabs key is missing, do not fake readiness. Ask for the key or stop at install/readiness work.
- If a render fails, read the full error, fix the workflow or command, and retry with the corrected process.
- If subtitles and overlays conflict, remember that subtitles must be applied last in the final composition chain.
- If Stanley wants a timeline-style preview first, prioritize previewability before a long final render.
- If the footage folder already has an `edit/` directory, reuse it and preserve prior session memory unless the user explicitly wants a fresh pass.

## Definition of Done

This workflow is done only when:

- the local video stack is honestly verified or its remaining blocker is clearly stated
- the repo has a stable routing path for video-editing work
- the source footage has a clean `edit/` workspace
- the user can ask for a raw video edit and the agent knows the lane to follow from transcript through graphics and render
