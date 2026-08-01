# SOP: Repurpose YouTube/Video Social Content Execution

## Purpose

Use this SOP when repurposing a YouTube video, LinkedIn video, LinkedIn/social
post, transcript, source brief, or video script into social content for Stanley.

This SOP is written for a weak or dumb model. Follow it literally. Do not skip
steps. Do not say the package is done until the verification checklist passes.

Locked visual template:

Before generating or repairing any visuals, also read:

```text
AIS-OS/workflows/repurpose-social-full-package-dumb-model-sop.md
```

That file is the current Stanley-approved template SOP. Do not replace that
template with a new style unless the user explicitly asks. It contains the
corrected LinkedIn image/GIF pattern, the dense carousel rules, the standalone X
rules, the failure log, and the fixes learned from the July 2026 restart.

The goal is to create a complete local social media package with:

- Source notes.
- Platform-specific text drafts.
- Platform-specific visual prompts.
- Actual generated image files.
- A LinkedIn animated GIF when LinkedIn explains a process, framework, sequence,
  or educational walkthrough.
- Instagram carousel images with a clean intro cover and dense, varied teaching
  slides.
- Preview and QA notes.
- A manifest that tells the truth about the package state.

This SOP exists because the workflow can fail in subtle ways:

- Stopping at text drafts or prompt files.
- Making every Instagram slide a sparse prompt box.
- Leaving too much unused white space.
- Using a fake or fallback avatar instead of Stanley's real avatar.
- Forgetting the LinkedIn animated GIF.
- Publishing or asking for approval before images and QA are complete.

## Skill Name

`repurpose-youtube-video`

For any web source, use the v3 skill copy:

```text
AIS-OS/.claude/skills/repurpose-youtube-video-v3/
AIS-OS/.agents/skills/repurpose-youtube-video-v3/
```

V3 is the default for LinkedIn/social/blog/article/Substack/web URLs because it
captures the source with Firecrawl first and creates Instagram JSON prompt
files before rendering.

## What The Skill Does

The skill turns one source video into a social media content package for:

- LinkedIn.
- Instagram.
- X.
- Facebook.

It creates editable text files and image files in a stable folder contract. The
user can review, edit, approve, revise, skip, or later publish each platform.

The skill has four jobs:

1. Capture the source honestly.
2. Write source-derived platform drafts.
3. Generate real visuals, not just prompts.
4. Prepare a local approval-ready package.

## Default Platform Purpose

LinkedIn:
Use for B2B trust, AI automation services, operator education, and strategic
authority. For process/framework posts, create an animated GIF as the primary
visual and keep a PNG poster/fallback.

Instagram:
Use for educational carousel content. Slide 1 is a clean intro cover. Slides 2+
are dense, structured teaching slides with varied modules.

X:
Use for concise insight, quote cards, or short threads. Keep X images clean and
content-tight.

Facebook:
Use for beginner-friendly course interest and AI skill learning. Do not use
luxury, desperation, or unrealistic income claims.

## Required Inputs

Accept one of these:

- YouTube URL.
- LinkedIn video URL.
- LinkedIn/social post URL.
- Transcript.
- Source brief from the client-trust LinkedIn scrape/recreate SOP.
- Pasted video script.
- Handoff script from another AIS-OS workflow.

Optional but useful:

- Target audience.
- Platform subset.
- Preferred angle.
- Any claims the user approves.
- Brand assets or profile image.
- Reference images or style examples.

If the user provides reference images, inspect their layout rules and apply the
style to the visual recipes and local renderer. Do not copy the images exactly.
Replicate the structure in Stanley's brand style.

If the user provides a LinkedIn/social post URL and asks to "repurpose",
"recreate", or "turn this into content", first run
`client-trust-linkedin-scrape-and-recreate-sop.md` to capture the source
mechanics and Stanley angle, then complete this full package SOP. Do not stop at
the LinkedIn analysis output.

For any public web URL, including LinkedIn, Substack, blog posts, articles, and
social posts, capture with Firecrawl before drafting:

```powershell
python .claude/skills/repurpose-youtube-video-v3/scripts/firecrawl_scrape.py `
  --url "<source-url>" `
  --out-dir "asset-folder/content/<slug>/source"
```

The wrapper auto-detects a local Firecrawl server on `http://localhost:3002`.
This is the local-model path. Do not route v3 web capture through the old
`webscraper` skill.

## Hard Source Rule

Do not invent content.

All text, slide ideas, quote-card text, and visual claims must come from the
source material. Use transcript/script when available. If captions or social
post text are blocked, empty, or noisy, use only verified metadata, public post
text, screenshots/pasted text, description, chapters, or a source brief.

If the full source is not available, stop and ask for the transcript, script,
screenshots, pasted text, or an authorized source export unless the user
explicitly accepts a metadata-derived draft.

Mark source confidence honestly in:

- `source/transcript.txt`
- `preview/preview.md`
- `manifest.json`

Allowed confidence examples:

- `transcript-derived`
- `auto-caption-derived`
- `metadata-derived`
- `script-derived`

## Folder Contract

Create each package under:

```text
AIS-OS/asset-folder/content/<source-title-slug>/
```

Use a readable Windows-safe title slug. Do not create timestamped run folders
for new work.

Required folders:

```text
source/
drafts/
  LinkedIn/
    images/
    text/
  Instagram/
    images/
    text/
  X/
    images/
    text/
  Facebook/
    images/
    text/
approved/
  LinkedIn/
    images/
    text/
  Instagram/
    images/
    text/
  X/
    images/
    text/
  Facebook/
    images/
    text/
published/
  LinkedIn/
    images/
    text/
  Instagram/
    images/
    text/
  X/
    images/
    text/
  Facebook/
    images/
    text/
preview/
manifest.json
```

Use platform folder names exactly:

- `LinkedIn`
- `Instagram`
- `X`
- `Facebook`

Use child folder names exactly:

- `images`
- `text`

## Required References

Before executing the skill, read:

```text
AIS-OS/.claude/skills/repurpose-youtube-video/SKILL.md
AIS-OS/.claude/skills/repurpose-youtube-video-v3/SKILL.md
AIS-OS/.claude/skills/repurpose-youtube-video/references/platform-rules.md
AIS-OS/.claude/skills/repurpose-youtube-video/references/visual-recipes.md
AIS-OS/workflows/repurpose-youtube-video-execution-sop.md
```

Before approval or publishing, also read:

```text
AIS-OS/.claude/skills/repurpose-youtube-video/references/publish-schema.md
AIS-OS/.claude/skills/repurpose-youtube-video-v3/references/firecrawl-local-model.md
AIS-OS/.claude/skills/repurpose-youtube-video-v3/references/instagram-cover-json-prompt-system.json
AIS-OS/.claude/skills/repurpose-youtube-video-v3/references/instagram-slide-json-prompt-system.json
```

## Recommended Setup Command

Use the skill helper when possible:

```powershell
python AIS-OS/.claude/skills/repurpose-youtube-video/scripts/create_run.py `
  --workspace AIS-OS/asset-folder/content `
  --source-type youtube_url `
  --source-value "<source URL>" `
  --project-title "<source title>" `
  --project-slug "<windows-safe-slug>" `
  --platforms all
```

If `python` is not available, use bundled Codex Python:

```powershell
& "C:\Users\DELL\.cache\codex-runtimes\codex-primary-runtime\dependencies\python\python.exe" <script>
```

## Source Capture Steps

1. Fetch or receive the source.
   - For a web URL, run Firecrawl first and save `source/firecrawl.json`,
     `source/firecrawl.md`, and `source/firecrawl.html` when available.
   - If Firecrawl cannot extract the public body, stop and ask for pasted text,
     screenshots, or an authorized export. Do not invent the source.
2. Extract verified metadata:
   - title
   - creator
   - source URL
   - published date if known
   - duration if known
   - description
   - chapters or timestamps
   - transcript or caption confidence
3. Save a raw or cleaned transcript to:

```text
source/transcript.txt
```

4. Write a source brief to:

```text
source/source-brief.md
```

`source/transcript.txt` must include:

- Source URL.
- Source title.
- Creator.
- Published date if known.
- Duration if known.
- Source confidence.
- Verified facts used for drafting.
- Caveats, such as noisy auto-captions or product-name errors.

`source/source-brief.md` must include:

- Core idea.
- Process insight.
- Proof points.
- Audience angles.
- Safety notes.
- What must not be claimed.

## Text Draft Files

Always create these editable text files:

```text
drafts/LinkedIn/text/post.txt
drafts/Instagram/text/post.txt
drafts/Instagram/text/caption.txt
drafts/X/text/post.txt
drafts/X/text/thread.txt
drafts/Facebook/text/post.txt
drafts/Facebook/text/caption.txt
```

Text drafting rules:

- Open with a strong hook.
- Instagram and Facebook captions must start with a scroll-stopping hook. A
  playful unrelated hook is allowed if it immediately apologizes or pivots back
  into the post.
- Use short lines.
- Use source-derived ideas only.
- Public-facing drafts, visual prompts, rendered image text, and Instagram JSON
  prompt copy must never say the post came from a source, article, reference,
  transcript, rewrite, or repurpose process. Keep that evidence in `source/`,
  `manifest.json`, and QA files only.
- Do not write audience-facing phrases such as `the source says`, `the article
  explains`, `I repurposed this`, `lesson learned`, `lessons from`, or `from
  this content`.
- If the content is about a tool, model, app, platform, or automation system,
  name that tool at the top of the post and at the top of relevant visuals.
  Be specific: `Claude Fable 5`, `Claude Code`, `ChatGPT`, `DaVinci Resolve`,
  `Firecrawl`, etc.
- Run the humanizer skill before handoff or rerender:
  `AIS-OS/.claude/skills/humanizer/SKILL.md`.
- Remove ambiguous model-speak. Say `strongest AI model` or the model name
  instead of vague phrases like `elite model calls`.
- Every platform draft must follow the same source-derived spine. The LinkedIn
  post, Instagram carousel, X thread, and Facebook post should not feel like
  unrelated drafts.
- Do not say Stanley did the source demo unless the source supports that.
- Do not promise revenue.
- Do not invent numbers.
- If proof came from the input material, rewrite it as a native claim only when
  it is safe and true. Do not tell the public audience where the claim came
  from unless Stanley explicitly asks for attribution.
- Use creator-style progression:
  - hook
  - stakes
  - core walkthrough
  - concrete steps
  - simple CTA

Good hook patterns:

- `Stop doing X.`
- `Most people use X wrong.`
- `This video is the best guide on X.`
- `The expensive mistake is X.`
- `I found X` only when Stanley actually found it or the source supports it.

Do not copy reference hooks word for word unless they are the user's own copy
and the user asks to use them.

If the user rejects a draft and asks for a rewrite:

- Preserve the current package as `versions/v1/` before editing.
- Write the active repaired files as v2.
- After rerendering and QA, preserve the repaired package as `versions/v2/`.
- Keep v1 untouched so the user can compare old and new work.
- Do not only rewrite the main post. Recheck every visual, prompt file, caption,
  thread, preview, and renderer string that may still contain stale language.

## Visual Prompt Files

Always create these prompt files:

```text
drafts/LinkedIn/images/thumbnail-prompt.txt
drafts/LinkedIn/images/visual-prompt.txt
drafts/Instagram/images/slide-01-cover-prompt.txt
drafts/Instagram/images/thumbnail-prompt.txt
drafts/Instagram/images/visual-prompt.txt
drafts/X/images/thumbnail-prompt.txt
drafts/X/images/visual-prompt.txt
drafts/Facebook/images/thumbnail-prompt.txt
drafts/Facebook/images/visual-prompt.txt
```

For Instagram, also create these JSON prompt files before rendering:

```text
drafts/Instagram/images/cover-prompt.json
drafts/Instagram/images/slide-blueprint.json
drafts/Instagram/images/slide-01-prompt.json
drafts/Instagram/images/slide-02-prompt.json
drafts/Instagram/images/slide-03-prompt.json
drafts/Instagram/images/slide-04-prompt.json
drafts/Instagram/images/slide-05-prompt.json
drafts/Instagram/images/slide-06-prompt.json
drafts/Instagram/images/slide-07-prompt.json
drafts/Instagram/images/slide-08-prompt.json
```

Use:

```powershell
python .claude/skills/repurpose-youtube-video-v3/scripts/generate_instagram_json_prompts.py `
  --run-dir "asset-folder/content/<slug>"
```

The cover prompt and slide prompts are planning files. They do not replace
rendering. The package is still incomplete until actual PNG/GIF files exist and
pass QA.

Prompt rules:

- Every platform needs an intro or thumbnail prompt.
- Visual text must be source-derived.
- Use Stanley's real avatar from:

```text
AIS-OS/asset-folder/Brand_Assets/Stan Avatar.png
```

- Do not use fake logos.
- Do not use fake metrics.
- Do not create a fake Stanley lookalike.
- If using a local renderer, keep the renderer in the package at:

```text
source/render_social_images.py
```

- Always save the exact code used to generate the images. If the executed
  renderer lives in `tools/` or a skill script, copy that exact script into the
  package as `source/render_social_images.py` after rendering.

## Mandatory Generated Media

Do not stop after writing text drafts and visual prompts.

For a full four-platform package, generate at minimum:

```text
drafts/LinkedIn/images/linkedin-thumbnail.png
drafts/LinkedIn/images/linkedin-diagram.png
drafts/LinkedIn/images/linkedin-animation.gif
drafts/Instagram/images/instagram-slide-01.png
drafts/Instagram/images/instagram-slide-02.png
drafts/Instagram/images/instagram-slide-03.png
drafts/Instagram/images/instagram-slide-04.png
drafts/Instagram/images/instagram-slide-05.png
drafts/Instagram/images/instagram-slide-06.png
drafts/Instagram/images/instagram-slide-07.png
drafts/Instagram/images/instagram-slide-08.png
drafts/X/images/x-quote-01.png
drafts/X/images/x-quote-02.png
drafts/X/images/x-quote-03.png
drafts/X/images/x-quote-04.png
drafts/X/images/x-quote-05.png
drafts/X/images/x-quote-06.png
drafts/X/images/x-quote.png
drafts/X/images/x-thumbnail.png
drafts/Facebook/images/facebook-thumbnail.png
drafts/Facebook/images/facebook-course-card.png
```

That is:

- 20 PNGs.
- 1 LinkedIn GIF when LinkedIn is process/framework educational content.

The GIF is the primary LinkedIn visual. The static LinkedIn diagram is a
poster/fallback.

## Visual Design Rules

### Shared

- Use cream/off-white graph-paper background.
- Use dark navy/black text.
- Use one accent color per teaching slide.
- Use Stanley's real avatar.
- Keep text readable at phone size.
- Dense does not mean cramped.
- Use most of the canvas with useful information.
- Avoid unnecessary blank space on teaching slides.
- Do not repeat the same module type on every slide.

### Instagram Slide 1

Slide 1 is always a clean intro cover.

It should include:

- Dark badge or pill.
- Huge hook headline.
- One rust/orange accent word or line.
- Short subhead.
- Stanley creator row near the lower-left.
- `01 / 08` footer.
- `SWIPE` cue.

Slide 1 must not include:

- Prompt box.
- Tech stack rows.
- Detailed teaching cards.
- Full workflow diagram.

### Instagram Slides 2-8

Slides 2-8 are dense teaching slides.

Each teaching slide should include:

- Top-right creator pill.
- Numbered circle that restarts at `1` after the cover.
- Colored title pill.
- Strong body hook.
- Upper visual block.
- Lower module panel.
- Bottom count and swipe cue.

Do not default every lower panel to a prompt box.

Choose the lower module that matches the slide:

- `PROMPT` or `PASTE THIS`: use when the viewer should copy an instruction.
- `INSTRUCTION`: use when the viewer should follow a rule but not copy a prompt.
- `TECH STACK`: use for tools, models, connectors, app surfaces, outputs.
- `TIPS`: use for tactical rules.
- `CHECKLIST`: use for review, acceptance criteria, or quality control.
- `QA GATE`: use when the lesson is about pass/fail checks.
- `WORKFLOW`: use for process stages, handoffs, or output pipelines.
- `ROUTINE`: use for recurring or scheduled workflows.
- `ROLES`: use for agent/team responsibilities.
- `TOOLS`: use for tool lists.
- `OUTPUT`: use when showing the deliverable.
- `SAVE THIS` or `USE THIS`: use for recap or decision filters.

If a prompt is not needed, do not force one. Use tech stack, tips, checklist,
workflow, roles, tools, output, routine rows, or QA gate instead.

Every module must say what it is. If it is a prompt box, the box or section must
say `PROMPT`. If it is a tip, say `TIPS`. If it is an instruction, say
`INSTRUCTION`. Do not use generic labels that make the viewer guess.

Before accepting any carousel, read each slide in order and ask:

- Does this slide match the main post?
- Does the number match the source sequence?
- Is the slide understandable without jargon?
- Does the lower module fit the lesson?
- Is the label accurate?
- Is any text clipped, crowded, or floating in empty space?

### LinkedIn

For process/framework posts:

- Create `linkedin-animation.gif` as the primary visual.
- Animate one step per frame.
- Keep a static `linkedin-diagram.png` poster/fallback.
- Include Stanley's real avatar.
- Keep the GIF readable without needing the caption.

### X

- Use clean tweet screenshot-style cards.
- Canvas: `920x458`.
- Use Stanley avatar, `Stanley`, verified badge, and `@stanleyai`.
- No fake engagement numbers.
- No timestamp.
- No action row.
- No decorative carousel frame.

### Facebook

- Beginner-friendly.
- Course-interest lane.
- No luxury imagery.
- No unrealistic income claims.
- Generous padding so text is not clipped.

## Local Renderer Requirements

When local rendering is used, create:

```text
source/render_social_images.py
```

The renderer should:

- Use Pillow.
- Use fonts from `C:\Windows\Fonts`.
- Use this avatar path logic:

```python
PROJECT = Path(__file__).resolve().parents[1]
ASSET_ROOT = PROJECT.parents[1]
AVATAR = ASSET_ROOT / "Brand_Assets" / "Stan Avatar.png"
```

- Generate all platform PNGs into `drafts/<Platform>/images`.
- Generate `drafts/LinkedIn/images/linkedin-animation.gif`.
- Include reusable helper functions for:
  - list rows
  - tool stack rows
  - comparison cards
  - command boxes
  - prompt panels
  - tips panels
  - checklist panels
  - workflow cards
  - workflow arrows
  - routine rows
  - QA/pass-condition strips
- Use module-specific labels.
- Avoid hardcoding an old project into a new renderer.

## Preview, QA, and Manifest

Always create or update:

```text
preview/preview.md
preview/image-qa.md
manifest.json
```

`preview/preview.md` must list:

- Source.
- Source confidence.
- Draft text files.
- Visual prompt files.
- Generated PNG files.
- Generated GIF files.
- Summary.
- Image QA note.
- Approval instruction.

`preview/image-qa.md` must state:

- Which images were generated.
- Whether the LinkedIn GIF exists and how many frames it has.
- Whether Stanley's real avatar is visible.
- Whether any generated lookalike was used.
- Whether representative images were inspected.
- Whether Instagram slide 1 uses the clean cover layout.
- Whether slides 2+ use varied dense module layouts.
- Whether module variety is present.
- Whether unnecessary blank space was avoided.
- Whether any clipping, overlap, or unreadable text remains.
- Known issues.

`manifest.json` must include:

- Project slug.
- Project title.
- Source URL.
- Source type.
- Source confidence.
- Platforms.
- Status.
- Notes.
- Generated image list.
- Generated animation list.
- Image count.
- Animation count.
- Primary LinkedIn visual.
- Instagram module types.
- Renderer path.
- QA files.

If PNGs or GIFs are generated, do not leave notes saying image generation is
pending.

## Exact Execution Steps

Follow these steps in order.

1. Read the user request.
2. Confirm `repurpose-youtube-video` applies.
3. Read the required references and this SOP.
4. Fetch or receive the source.
5. Extract metadata and transcript/source text.
6. If transcript/source text is missing and the user did not accept
   metadata-derived work, stop and ask for transcript, screenshots, pasted text,
   or an authorized source export.
7. Create the project folder with `create_run.py`.
8. Save source URL, transcript, and source brief.
9. Extract:
   - core idea
   - process insight
   - proof points
   - audience angles
   - safety notes
10. Draft all platform text files.
11. Run the humanizer pass on text drafts:
    - remove ambiguous phrases
    - simplify jargon
    - keep the same source-derived spine across platforms
    - confirm hooks and body are understandable
12. Write all visual prompt files.
13. Create or adapt `source/render_social_images.py`.
14. Build Instagram slide data:
    - slide 1: clean intro cover
    - slides 2-8: varied dense module layouts
    - slide numbers must match the post/source sequence
    - prompt, tip, checklist, QA, workflow, and instruction modules must be
      labeled accurately
15. Build LinkedIn visual data:
    - animated GIF primary
    - static PNG poster/fallback
16. Generate all PNGs and GIFs.
17. Open representative images:
    - Instagram slide 1
    - at least three Instagram teaching slides with different modules
    - one dense slide likely to clip
    - LinkedIn poster or GIF frame
    - X card
    - Facebook card
18. Fix any issue:
    - fake avatar
    - fallback avatar
    - clipped text
    - overlapping text
    - too much blank space
    - repeated prompt boxes
    - wrong title or stale hook
    - mismatched slide numbering
    - slide content not related to the post
    - missing `PROMPT`, `TIPS`, `INSTRUCTION`, `CHECKLIST`, or `QA GATE` label
      when that module is used
    - missing GIF
    - missing files
19. Rerender after fixes.
20. Count media.
21. Validate manifest JSON.
22. Search for stale placeholder, pending language, and stale rejected wording.
23. Update preview and QA files.
24. If this is a v2 repair, save `versions/v2/`.
25. Ask which platform(s) to approve next.

## Verification Commands

Use these from `C:\Users\DELL\Master Project\Stan OS`.

Count Instagram PNGs:

```powershell
(Get-ChildItem -LiteralPath "AIS-OS/asset-folder/content/<slug>/drafts/Instagram/images" -Filter *.png | Measure-Object).Count
```

Count all PNGs:

```powershell
(Get-ChildItem -LiteralPath "AIS-OS/asset-folder/content/<slug>/drafts" -Recurse -Filter *.png | Measure-Object).Count
```

Count GIFs:

```powershell
(Get-ChildItem -LiteralPath "AIS-OS/asset-folder/content/<slug>/drafts" -Recurse -Filter *.gif | Measure-Object).Count
```

Check LinkedIn GIF frames:

```powershell
$env:PYTHONUTF8='1'
@'
from PIL import Image
from pathlib import Path
p=Path(r"AIS-OS/asset-folder/content/<slug>/drafts/LinkedIn/images/linkedin-animation.gif")
im=Image.open(p)
print(f"gif_frames={getattr(im, 'n_frames', 1)} size={im.size}")
'@ | & "C:\Users\DELL\.cache\codex-runtimes\codex-primary-runtime\dependencies\python\python.exe" -
```

Validate manifest:

```powershell
& "C:\Users\DELL\.cache\codex-runtimes\codex-primary-runtime\dependencies\python\python.exe" `
  -m json.tool "AIS-OS/asset-folder/content/<slug>/manifest.json"
```

Find stale placeholders:

```powershell
rg -n "Replace this placeholder|PNG generation is pending|No PNGs|Visual Prompt$|Draft$|images_pending|linkedin.*pending|APPLY THIS" `
  "AIS-OS/asset-folder/content/<slug>"
```

Expected result:

- `instagram_png=8`
- `total_png=20`
- `gif=1`
- LinkedIn GIF has more than one frame.
- Manifest is valid JSON.
- Placeholder search has no matches.

## Failure Log and Fixes

### Failure: Stopped at drafts and prompts

What happened:
The workflow created text drafts and visual prompt files but did not generate
actual PNGs.

Fix:
Do not hand off until all required PNGs and GIFs exist and QA has been written.

### Failure: Python was not on PATH

What happened:
`python` failed in PowerShell.

Fix:
Use bundled Codex Python:

```text
C:\Users\DELL\.cache\codex-runtimes\codex-primary-runtime\dependencies\python\python.exe
```

### Failure: Bash heredoc syntax was used in PowerShell

What happened:
Commands like `python - <<'PY'` failed because PowerShell does not support Bash
heredocs.

Fix:
Use PowerShell here-strings:

```powershell
@'
print("hello")
'@ | & "C:\path\to\python.exe" -
```

### Failure: YouTube transcript tools were not installed

What happened:
`yt-dlp` and `youtube-transcript-api` were not available.

Fix:
Install into bundled Python user site when needed:

```powershell
& "C:\Users\DELL\.cache\codex-runtimes\codex-primary-runtime\dependencies\python\python.exe" `
  -m pip install --user yt-dlp youtube-transcript-api
```

### Failure: Windows console encoding broke metadata output

What happened:
A Unicode symbol in YouTube metadata caused a `cp1252` encode error.

Fix:
Set UTF-8 mode:

```powershell
$env:PYTHONUTF8='1'
```

### Failure: Wrong avatar path created fallback avatar

What happened:
The renderer looked in the wrong folder and used a fallback/fake avatar.

Fix:
Use:

```python
PROJECT = Path(__file__).resolve().parents[1]
ASSET_ROOT = PROJECT.parents[1]
AVATAR = ASSET_ROOT / "Brand_Assets" / "Stan Avatar.png"
```

Then rerender and visually confirm the real avatar appears.

### Failure: Existing renderer was hardcoded to an older package

What happened:
A renderer from an older package generated wrong-topic visuals.

Fix:
Create a source-specific renderer at:

```text
source/render_social_images.py
```

or update a generic renderer so all slide text comes from the current package.

### Failure: Instagram intro looked like a teaching slide

What happened:
Slide 1 used the same structure as slides 2+.

Fix:
Slide 1 must be a clean intro cover only: big hook, badge, accent line, short
subhead, creator row, count, swipe cue. No prompt panel or teaching cards.

### Failure: Every slide used a prompt or apply box

What happened:
The first visual pass used the same lower panel pattern too often.

Fix:
Choose modules per topic: tech stack, tips, checklist, workflow, routine, roles,
tools, output, QA gate, save this, use this, prompt, or paste this.

### Failure: Too much empty space

What happened:
Some teaching slides ended early and left a large blank lower area.

Fix:
Add useful module content such as support cards, pass-condition strips, routine
rows, tool rows, or checklist items. Keep the slide readable, but use the
canvas.

### Failure: Text clipped in a card

What happened:
One upper card had too much text for its box.

Fix:
Shorten the copy, reduce font size, or widen the card. Rerender and inspect
again.

### Failure: Button overlapped footer cue

What happened:
The orange prompt-panel button sat too low and collided visually with the swipe
button.

Fix:
Clamp the button position above the footer or move the module panel upward.

### Failure: LinkedIn was static only

What happened:
LinkedIn output was a static diagram, but the process/framework visual should
have been an animated GIF.

Fix:
Generate `drafts/LinkedIn/images/linkedin-animation.gif` and keep
`linkedin-diagram.png` as a poster/fallback.

### Failure: Post and slides did not match

What happened:
The LinkedIn post used one message, while Instagram slide text drifted into a
different framework. Some numbered slides referred to the wrong use case.

Fix:
Rewrite the package around one source-derived spine. For a five-use-case source,
slides numbered 1-5 must map to use cases 1-5 in order. Any extra slides should
be clearly named as filters, recaps, workflows, or save-this slides.

### Failure: Ambiguous or jargon-heavy copy

What happened:
Copy used unclear phrases such as `elite model calls` or abstract framework
language that did not help the reader understand the post.

Fix:
Run the humanizer skill. Replace vague model-speak with plain wording, explain
terms in context, and read the slide out loud. If a normal reader would ask
`what does this mean?`, rewrite it before rendering.

### Failure: Module label did not describe the content

What happened:
A slide used a prompt, tip, or instruction-style panel without clearly saying
what it was.

Fix:
Label the module accurately: `PROMPT`, `TIPS`, `INSTRUCTION`, `CHECKLIST`,
`QA GATE`, `TECH STACK`, `WORKFLOW`, `SAVE THIS`, or `USE THIS`.

## Dumb-Model Runbook: LinkedIn/Social Post Repurpose

Use this section when the user gives a LinkedIn/social post URL and asks to
repurpose it into platform assets. This is the exact workflow learned from the
`claude-skills-are-not-the-product` run.

### Goal

Turn one source post into a complete, editable, approved, and publishable social
content package:

- LinkedIn text plus a process image and GIF when the post teaches a framework.
- Instagram carousel with actual generated slide images.
- X post/thread text plus tweet-style images.
- Facebook post/caption plus course-interest visuals.
- Preview, image QA, manifest, approval package, and optional Google Drive
  upload.

The job is not finished at text drafts or prompt files. It is finished only when
the package has actual media, QA notes, a valid manifest, and the user knows
what to approve or publish next.

### Required First Move

Do not start designing from memory.

1. Open this SOP.
2. Open the skill file at `.claude/skills/repurpose-youtube-video/SKILL.md`.
   If the source is a web URL, also open
   `.claude/skills/repurpose-youtube-video-v3/SKILL.md`.
3. Open the required references:
   - `references/platform-rules.md`
   - `references/visual-recipes.md`
   - `references/publish-schema.md`
4. If the source is LinkedIn/social, also follow
   `workflows/client-trust-linkedin-scrape-and-recreate-sop.md`.
5. Inspect the actual project folder before editing. Do not assume paths.

### Source Capture

1. Create or use `AIS-OS/asset-folder/content/<slug>/`.
2. Save source material under `source/`:
   - `source/transcript.txt`
   - `source/source-brief.md`
3. For any web URL, run:

```powershell
python .claude/skills/repurpose-youtube-video-v3/scripts/firecrawl_scrape.py `
  --url "<source-url>" `
  --out-dir "asset-folder/content/<slug>/source"
```

4. If public scraping is blocked, stop and ask for pasted text or screenshots.
   Do not invent the source.
5. If only a public preview is available, mark the confidence honestly in
   `manifest.json`.

### Drafting Contract

Create all platform text files before rendering visuals:

```text
drafts/LinkedIn/text/post.txt
drafts/Instagram/text/post.txt
drafts/Instagram/text/caption.txt
drafts/X/text/post.txt
drafts/X/text/thread.txt
drafts/Facebook/text/post.txt
drafts/Facebook/text/caption.txt
```

Rules:

- Each platform post must stand alone.
- X cards must read like independent tweets, not a continuation of a previous
  card.
- Do not add visible meta labels to X images such as `LESSON`, `TIP`,
  `WORKFLOW`, or `Standalone post`.
- Do not claim Stanley created, downloaded, tested, or owns the source creator's
  assets unless the source proves it.
- Plain language beats jargon. Explain terms like workflows, QA, or handoff in
  the content itself.

### Visual Prompt Contract

Create these visual prompt files even when using a local renderer:

```text
drafts/LinkedIn/images/thumbnail-prompt.txt
drafts/LinkedIn/images/visual-prompt.txt
drafts/Instagram/images/slide-01-cover-prompt.txt
drafts/Instagram/images/thumbnail-prompt.txt
drafts/Instagram/images/visual-prompt.txt
drafts/X/images/thumbnail-prompt.txt
drafts/X/images/visual-prompt.txt
drafts/Facebook/images/thumbnail-prompt.txt
drafts/Facebook/images/visual-prompt.txt
```

Prompt files must describe the current desired output. If the user rejects a
visual convention, update the prompt file so the rejected convention cannot
return in a later render.

Before rendering Instagram, run the v3 JSON prompt generator. It must create a
cover prompt, a slide blueprint, and one JSON prompt file per slide. The
renderer may use local HTML/Python after that, but the JSON files must remain in
`drafts/Instagram/images/` as the design intent for the cover and slides.

### Image Generation Contract

Generate actual PNG/GIF files. Do not stop at SVG, prompts, or descriptions.

Required active media:

- LinkedIn:
  - `linkedin-thumbnail.png`
  - `linkedin-diagram.png`
  - `linkedin-animation.gif` when the content teaches a framework or process.
- Instagram:
  - `instagram-slide-01.png` through `instagram-slide-08.png`.
- X:
  - `x-thumbnail.png`
  - `x-quote-01.png` through `x-quote-06.png`
  - `x-quote.png`
- Facebook:
  - `facebook-thumbnail.png`
  - `facebook-course-card.png`

Use Stanley's real avatar from
`AIS-OS/asset-folder/Brand_Assets/Stan Avatar.png`. Do not accept a generated
lookalike.

### Instagram Design Rules

Slide 1:

- Clean intro cover.
- Strong headline.
- Useful subtext.
- May use small chips or a compact cue row.
- Do not turn the cover into a dense teaching slide.

Slides 2+:

- Each slide must be understandable as a standalone post.
- Use varied layouts: comparison, checklist, tips, instruction flow, tech stack,
  automation map, decision filter, QA gate, etc.
- Choose the slide order and structure from the source. Do not reuse the same
  slide sequence across unrelated projects just because the renderer can.
- Do not make every slide a prompt box.
- If a lower panel is used, label it accurately: `PROMPT`, `TIPS`,
  `INSTRUCTION`, `CHECKLIST`, `TECH STACK`, `WORKFLOW`, `QA GATE`,
  `SAVE THIS`, or `USE THIS`.
- Do not render internal QA/helper text into public visuals. Phrases like `this
  slide should make sense` are creator notes, not audience copy.
- Do not put the same `BOTTOM LINE` panel on most slides in future content. Vary
  the closing module or remove it when the main body already carries the lesson.
- Use the whitespace. Empty space should be intentional, not because the slide
  lacks information.

### LinkedIn Design Rules

The LinkedIn image/GIF should be a standalone lesson, not a vague continuation
of the source post.

For process/framework content:

- Use a clear title that makes sense alone.
- Use a 4-6 step structure.
- The static image and GIF must use the same content.
- The GIF should highlight one step per frame.

Failure to avoid:

- Bad title: `Prompt -> Skill -> Operating System` when it does not clearly
  explain the lesson.
- Better title style: `Stop Retyping AI Instructions`.

### X Design Rules

X images must look like normal tweet screenshots:

- White 920x458 canvas.
- Stanley avatar, name, verified badge, and `@stanleyai`.
- Tweet text only.
- No category pill.
- No footer.
- No timestamp.
- No fake engagement row.
- No decorative frame.
- No `Standalone post` wording.

The tweet can still be standalone in meaning. It should not look like a
presentation slide.

### Local Renderer Rules

If a local renderer exists for the package, edit the renderer rather than
manually editing exported images. The renderer is the source of truth for future
regeneration.

For the `claude-skills-are-not-the-product` run, the renderer was:

```text
asset-folder/content/claude-skills-are-not-the-product/source/render_social_images.py
```

When the user requests visual changes:

1. Patch the renderer.
2. Patch any affected prompt files.
3. Rerender images.
4. Inspect representative images with the image viewer.
5. Refresh `approved/` if the already approved package must be republished.
6. Republish to Google Drive if upload config exists and the user wants the
   Drive copy updated.

### QA Contract

Before final handoff:

1. Count active PNG/GIF files.
2. Open representative images:
   - Instagram cover.
   - At least two Instagram teaching slides.
   - LinkedIn diagram.
   - One X card.
   - One Facebook visual.
3. Check for:
   - Real Stanley avatar.
   - No clipped text.
   - No overlapping labels.
   - No stale visual labels.
   - No internal QA/helper text rendered into public visuals.
   - Correct platform shape.
   - Standalone slide/card meaning.
4. Update `preview/image-qa.md`.
5. Update `preview/preview.md`.
6. Validate `manifest.json`.

### Approval And Drive Publish

Approval is separate from drafting.

1. When the user approves all or specific platforms, run:

```powershell
& '<python.exe>' '.claude/skills/repurpose-youtube-video-v3/scripts/collect_approved.py' --run-dir '<content-project>' --platforms '<all-or-platforms>' --notes '<notes>'
```

2. The approval packager must copy every platform text file, not only
   `post.txt`.
3. Google Drive upload uses `approved/`, not `drafts/`.
4. Drive upload command:

```powershell
& '<python.exe>' '.claude/skills/repurpose-youtube-video-v3/scripts/publish_to_google_drive.py' --run-dir '<content-project>'
```

5. The Drive uploader creates or updates:

```text
<Master Folder>/
  <Project Title>/
    LinkedIn/
    Instagram/
    X/
    Facebook/
    Post/
```

6. Platform folders contain media only.
7. `Post/` contains separate Google Docs for approved text files.
8. Keep uploads private unless the user explicitly asks for sharing changes.
9. If credentials/config are missing, do not fake success. Tell the user exactly
   what path or setup step is missing.

### Mistakes From This Run And Fixes

Failure: blended two adjacent workflows.

Fix: If the user says `repurpose` and expects platform assets, use this
repurpose execution SOP. LinkedIn reference recreation is separate and should
not replace the full platform package.

Failure: stopped at prompts/SVGs instead of generated images.

Fix: Always create actual PNGs and the LinkedIn GIF when required. Validate the
counts.

Failure: LinkedIn title did not make sense as a standalone post.

Fix: Rewrite the LinkedIn graphic title so the image teaches the idea by itself.

Failure: Instagram slides looked too similar.

Fix: Use varied layouts and module types. Do not reuse the same prompt-box
structure across all slides.

Failure: Instagram slides had too much empty whitespace.

Fix: Add useful subtext, chips, grids, comparison cards, workflow rows, or
checklists. Make the space teach.

Failure: X cards were standalone in content but looked like labeled slides.

Fix: Remove structural labels and footer text. Make them look like normal tweet
screenshots.

Failure: approved package originally copied only `post.txt`.

Fix: `collect_approved.py` must copy all `*.txt` files from each platform text
folder.

Failure: Google Drive upload did not exist.

Fix: Add `publish_to_google_drive.py`, OAuth config, dry-run verification, and
private upload into the master folder.

Failure: uploaded Drive copy can become stale after a visual revision.

Fix: After changing approved visuals, rerun `collect_approved.py` for the
changed platform and rerun the Drive publisher.

Failure: SOP was updated but the batch builder ignored it.

Fix: Patch `AIS-OS/tools/repurpose_full_package_builder.py`, not only the skill
docs. New packages created by that builder must use dense Instagram slide
layouts, strict tweet-style X cards, explicit visual prompts, and honest QA
notes. If the generated package has `source/render_social_images.py` that calls
`tools/repurpose_full_package_builder.py`, the builder is the real renderer
source of truth.

## Approval Rules

Draft files are the source of truth. If the user edits a draft file, approve or
publish from the edited file, not from memory.

Supported approval commands:

- `Approve all`
- `Approve LinkedIn and X`
- `Skip Instagram`
- `Revise Facebook`

Use `scripts/collect_approved.py` when possible to copy approved platform
packages from `drafts/` to `approved/`.

Do not publish, upload, or log live URLs until the user approves.

## Publishing Rules

Publishing means preparing or sending approved assets to Google Drive and
Notion.

After approval:

1. Run approval packaging with
   `.claude/skills/repurpose-youtube-video-v3/scripts/collect_approved.py`.
2. If Google Drive config exists, run
   `.claude/skills/repurpose-youtube-video-v3/scripts/publish_to_google_drive.py`.
3. Return the Drive content-folder URL from `published/google-drive.json`.

Google Drive uploads must use `approved/`, not `drafts/`. The uploader creates
or updates this private Drive structure:

```text
<Master Folder>/
  <Project Title>/
    LinkedIn/
    Instagram/
    X/
    Facebook/
    Post/
```

Platform folders contain approved media only. `Post/` contains separate Google
Docs for each approved text file, such as `Instagram Caption`, `LinkedIn Post`,
or `X Thread`.

If Google Drive, Google Docs, or Notion access is missing, do not fake success.
Leave an upload-ready package in `published/` and tell the user what connection
or config is missing.

After a platform has a live URL, append it to both logs with
`scripts/update_published_log.py` when possible:

```text
AIS-OS/asset-folder/repurpose-youtube-video/published-posts.csv
AIS-OS/asset-folder/repurpose-youtube-video/published-posts.jsonl
```

## Dumb-Model Final Checklist

Before saying `done`, every answer must be yes:

- Did I create the package under `AIS-OS/asset-folder/content/<slug>/`?
- Did I save `source/transcript.txt`?
- Did I save `source/source-brief.md`?
- Did I create all seven text draft files?
- Did I create all required visual prompt files?
- Did I create actual PNG files?
- Did I create the LinkedIn GIF when LinkedIn is process/framework content?
- Did I use Stanley's real avatar?
- Did I inspect representative images?
- Did Instagram slide 1 use the clean intro cover layout?
- Did Instagram slides 2+ use dense, varied module layouts?
- Did I avoid using a prompt box on every slide?
- Did I fix clipped or overlapping text?
- Did I avoid unnecessary blank space on teaching slides?
- Did I update `preview/preview.md`?
- Did I update `preview/image-qa.md`?
- Did I validate `manifest.json`?
- Did I remove stale pending or placeholder language?
- Did I ask which platforms to approve next?

If any answer is no, the job is not done.
