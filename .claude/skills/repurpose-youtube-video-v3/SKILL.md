---
name: repurpose-youtube-video-v3
description: V3 repurpose workflow for YouTube URLs, LinkedIn/social URLs, articles, Substack posts, transcripts, source briefs, or pasted scripts. Uses Firecrawl-first web capture for every web source, creates platform drafts, generates Instagram cover and slide JSON prompt files, renders actual PNG/GIF media, prepares approvals, and supports Google Drive publishing.
---

# Repurpose YouTube Video V3

## Purpose

Support Stanley's AI social media manager by turning one source into four platform-ready content packages. The source can be a YouTube/video transcript, a pasted script, an approved blog handoff, or a public LinkedIn/social post that has first been analyzed through the client-trust LinkedIn SOP. The AI social media manager is the operator using this skill; this skill is the reusable repurposing workflow, folder contract, drafting process, visual process, approval process, and publishing handoff.

- LinkedIn: AI automation services and educational authority.
- X: sharp automation insight, quote, or concise educational thread.
- Instagram: educational carousel that feels like tweet-style thought cards.
- Facebook: course-interest and course-sales content for people who may learn AI skills from Stanley.

Always create local drafts first. The user previews and approves platforms one by one before any Drive or Notion publishing step.

## V3 Additions

V3 keeps the normal repurpose package contract, but changes two things:

1. Every web source is captured through Firecrawl first.
2. Every Instagram carousel gets structured JSON prompt files before rendering:
   - `drafts/Instagram/images/cover-prompt.json`
   - `drafts/Instagram/images/slide-blueprint.json`
   - `drafts/Instagram/images/slide-01-prompt.json`
   - `drafts/Instagram/images/slide-02-prompt.json`
   - up to `drafts/Instagram/images/slide-08-prompt.json`

The JSON prompt files guide composition and layout selection. They do not
replace rendering. V3 still renders the actual PNG files and LinkedIn GIF. The
LinkedIn GIF must highlight one row per frame with a bright theme accent color
such as orange, not a plain white active row.

Local-model rule: use deterministic scripts in this skill. Do not require the
local model to operate an MCP server directly. For web capture, the model runs
`scripts/firecrawl_scrape.py`, which reads Firecrawl config from environment,
`--env-file`, `%USERPROFILE%\.codex\firecrawl\.env`, or the local self-hosted
URL.

## Workspace

Use `AIS-OS/asset-folder/content/` as the project workspace for repurposed content.

Each source should use a readable Windows-safe title slug, not a timestamped run folder:

```text
youtube-title-slug/
  source/
  drafts/
    Instagram/
      images/
      text/
    X/
      images/
      text/
    LinkedIn/
      images/
      text/
    Facebook/
      images/
      text/
  approved/
    Instagram/
      images/
      text/
    X/
      images/
      text/
    LinkedIn/
      images/
      text/
    Facebook/
      images/
      text/
  preview/
  published/
    Instagram/
      images/
      text/
    X/
      images/
      text/
    LinkedIn/
      images/
      text/
    Facebook/
      images/
      text/
  manifest.json
```

Use title-case platform folders and lowercase asset folders:

- `Instagram/images`, `Instagram/text`
- `X/images`, `X/text`
- `LinkedIn/images`, `LinkedIn/text`
- `Facebook/images`, `Facebook/text`

Keep the running published logs at:

- `AIS-OS/asset-folder/repurpose-youtube-video/published-posts.csv`
- `AIS-OS/asset-folder/repurpose-youtube-video/published-posts.jsonl`

## Legacy Layout

Older packages may still exist as timestamped folders:

```text
run-YYYYMMDD-HHMMSS/
  visual-prompts/
  visuals/
```

Treat those as legacy input. New work should be created or migrated into `AIS-OS/asset-folder/content/<youtube-title-slug>/`.

## Required References

Read only the reference files needed for the task:

- `AIS-OS/workflows/repurpose-social-full-package-dumb-model-sop.md` is the
  single canonical execution SOP for full-package repurpose work. Use it for
  package creation, visuals, QA, preview, manifest validation, and approval
  handoff.
- Do not read or follow any other repurpose SOP for package execution.
- `AIS-OS/.claude/skills/humanizer/SKILL.md` before rewriting or repairing social copy, especially when creating a v2 after user feedback.
- `references/platform-rules.md` for platform voice, format, CTA, and visual rules.
- `references/visual-recipes.md` before writing visual prompts or generating images.
- `references/firecrawl-local-model.md` before scraping any web source.
- `references/instagram-cover-json-prompt-system.json` before creating the
  Instagram cover prompt.
- `references/instagram-slide-json-prompt-system.json` before creating the
  Instagram slide blueprint and slide prompt JSON files.
- `references/publish-schema.md` before packaging approvals, updating logs, or preparing Notion records.

## Intake

Accept either:

1. A YouTube URL.
2. A LinkedIn/social post URL that has public text, screenshot evidence, pasted text, or a saved source brief.
3. A pasted YouTube video script.
4. A transcript file or pasted transcript.
5. A handoff script or approved source brief from another AIS-OS workflow.

If the user provides only a YouTube URL and transcript extraction is unavailable, ask for the transcript or script. If the user provides a LinkedIn/social URL and public text is blocked, ask for screenshots or pasted text. Do not invent the source content.

For every LinkedIn/social post, analyze both the caption/body text and the
attached image, GIF, screenshot, or carousel before drafting. The caption is
often enough for the repurpose when it contains the full framework, list,
proof, CTA, or step-by-step explanation. In that case, mark the source as
`caption-derived` or `public-preview-derived`, let the caption drive the
repurpose, and use the visual primarily for layout/style/proof cues. If the
image contains essential proof, numbers, screenshots, or missing context, do
not draft until that visual is captured or honestly marked blocked.

If metadata is available but the transcript body is blocked or empty, create only a clearly labeled metadata-derived review draft when the user still wants something to preview. Mark `source_confidence: metadata-derived` in the manifest and draft frontmatter, and request the transcript before final approval.

All post copy, slide copy, and quote-card text must come from the source material: transcript/script when available, otherwise verified public post caption/body text, visible image/GIF/carousel evidence, title, description, chapters, and source brief. Use facts, frameworks, workflows, and useful takeaways from what the source actually discusses. Do not use random motivational text or unrelated AI advice.

Public-facing copy rule:
- Never tell the audience the post was repurposed, rewritten, based on a source, based on an article, or based on a lesson learned. That belongs in `source/`, `manifest.json`, and internal QA only.
- Do not write phrases like `the source says`, `the article explains`, `I repurposed this`, `lesson learned`, or `from this content` in `drafts/<Platform>/text/`, visual text, image prompts, or Instagram JSON prompt copy.
- If the topic is a tool, model, app, platform, or automation system, name that tool at the top of the post and visual. Be specific: `Claude Fable 5`, `Claude Code`, `ChatGPT`, `DaVinci Resolve`, `Firecrawl`, etc. Do not open with generic language when a concrete tool is the point.
- Rewrite the insight as Stanley-native educational content while keeping the internal evidence trail honest.

For any web URL, run Firecrawl before drafting:

```powershell
python .claude/skills/repurpose-youtube-video-v3/scripts/firecrawl_scrape.py `
  --url "<source-url>" `
  --out-dir "asset-folder/content/<slug>/source"
```

If Firecrawl config is missing, use a self-hosted Firecrawl URL when available:

```powershell
$env:FIRECRAWL_API_URL="http://localhost:3002"
```

Do not fall back to the old `webscraper` skill for v3 web capture. If Firecrawl
cannot scrape after local/cloud config is checked, stop with the exact error and
save the source URL.

Ask clarifying questions one at a time until you are confident about:

- The content angle.
- The intended audience lane: services, course, or both.
- The proof/result that can safely be mentioned.
- Any confidentiality limits.
- Whether the user wants all platforms drafted or only a subset.

Do not block on small missing details. Use the default platform lanes unless the user overrides them.

In v1, create content for all four platform folders by default. Selective approval applies to publishing, not to whether draft folders get content, unless the user explicitly says not to draft a platform.

## Drafting Workflow

1. Create a title-slug project folder with `scripts/create_run.py` when possible.
2. Save the source into `source/`.
3. Extract:
   - Core idea.
   - Manual pain or current workflow.
   - Automation/process insight.
   - Result or proof.
   - Audience benefit.
   - CTA.
4. Draft editable plain text files in each platform text folder:
   - `drafts/LinkedIn/text/post.txt`
   - `drafts/Instagram/text/post.txt`
   - `drafts/Instagram/text/caption.txt`
   - `drafts/X/text/post.txt`
   - `drafts/X/text/thread.txt`
   - `drafts/Facebook/text/post.txt`
   - `drafts/Facebook/text/caption.txt`
   - Use `post.txt` for the main post/thread or carousel script. Use `caption.txt` when the platform needs a paste-ready caption separate from slide text.
   - Before rendering visuals, run a humanizer pass: remove ambiguous model-speak, explain jargon, keep the post tied to the verified idea, and confirm the carousel/script follows the same sequence as the main post.
5. Create visual prompts and generated PNG images in each platform image folder:
   - Always create an intro/thumbnail prompt first. This cover should introduce what the post or carousel is about before the detailed slides/graphics begin.
   - `drafts/LinkedIn/images/thumbnail-prompt.txt`
   - `drafts/Instagram/images/slide-01-cover-prompt.txt`
   - `drafts/X/images/thumbnail-prompt.txt`
   - `drafts/Facebook/images/thumbnail-prompt.txt`
   - `drafts/LinkedIn/images/visual-prompt.txt`
   - `drafts/Instagram/images/visual-prompt.txt`
   - `drafts/X/images/visual-prompt.txt`
   - `drafts/Facebook/images/visual-prompt.txt`
   - Do not store the primary generated deliverables in a separate loose `visuals/` folder. The platform folders above are the deliverable contract.
6. For Instagram, generate JSON prompt files before rendering:
   - `drafts/Instagram/images/cover-prompt.json`
   - `drafts/Instagram/images/slide-blueprint.json`
   - `drafts/Instagram/images/slide-01-prompt.json`
   - `drafts/Instagram/images/slide-02-prompt.json`
   - continue through the final carousel slide.
   Use:

```powershell
python .claude/skills/repurpose-youtube-video-v3/scripts/generate_instagram_json_prompts.py `
  --run-dir "asset-folder/content/<slug>"
```

   The cover prompt uses the accepted premium editorial cover system from the
   Fable 5 carousel: oversized 1-3 line H1 that dominates about 60% of the
   canvas, warm cream engineering grid, fixed small tool tag directly above the
   title, subtitle directly below the title, compact profile pill directly under
   the subtitle, and one orange highlighted phrase. Use `chima-stanley-chukwu`
   as the name, `@chima-stanley-chukwu` as the visible username, and store
   `https://www.linkedin.com/in/chima-stanley-chukwu/` as `profile_url` metadata
   unless Stanley provides a replacement. The slide prompts use semantic layout
   selection: hero, card grid, comparison, process flow, timeline, dashboard,
   pyramid, ratio/pie chart, or key takeaways based on the slide meaning.
   Do not use one fixed body structure across the carousel. Shared profile,
   footer, and brand chrome are fine, but each teaching slide must choose a
   meaning-specific structure such as a leak meter, anatomy diagram, command
   menu, scanner, timeline, matrix, receipt, extraction flow, or decision tree.
   When repairing a deck, record the correction with placeholders in the
   canonical SOP: `[CONTENT_SLUG]`, `[SLIDE_NUMBER_OR_VISIBLE_MARKER]`,
   `[WHAT_LOOKED_WRONG]`, `[CAUSE]`, `[FIX]`, `[MODULE_NAME]`, and
   `[QA_PROOF]`. Public slide copy must never mention internal words such as
   caption, source, repurpose, or creator unless the audience actually needs
   that context.
   Approved 2026-07-27 repair pattern: if the cover is large but not bold
   enough, increase perceived title weight; if a slide says caption/source/
   repurpose, rewrite it as audience-facing teaching; if bottom text exits a
   diagram, use bounded drawing or shorter copy; if a technical phrase appears,
   define it in plain terms on the slide.
7. For structured educational carousels, sliders, quote cards, and clean infographic-style posts, prefer the local deterministic renderer first:
   - `scripts/render_reference_style_images.py --project-dir <content-project>`
   - This creates editable, reference-style PNGs without using GPT image generation.
   - Use this when the user asks for the former/local technique, reference-style carousel images, clean structured slides, or no GPT image generation.
   - Always save the exact renderer/code used for image generation in the content package, preferably at `source/render_social_images.py`. If a shared tool script generated the images, copy the executed script into that package after rendering.
8. Generate visuals with `gpt-image-2` only when the user wants model-generated raster imagery or when local rendering cannot satisfy the visual requirement. Use the image generation tool available in the current environment if it clearly maps to OpenAI image generation. If image generation is not available, save the prompts and mark images as pending.
   - When the user provides a local brand/profile photo, use it in local rendered visuals if the current image tool cannot directly ingest local files. Keep the prompt file alongside the preview so alternate renders can still be generated later.
9. Save a preview summary in `preview/preview.md` with links to all drafts, visual prompts, JSON prompt files, and generated images.
10. Ask the user to approve platforms one by one.

## Approval Rules

The draft files are the source of truth. If the user edits `drafts/LinkedIn/text/post.txt`, publish from the edited file, not from memory.

Support these approval patterns:

- "Approve all" -> copy all platform draft packages to `approved/`.
- "Approve LinkedIn and X" -> approve only those platforms.
- "Skip Instagram" -> leave Instagram in drafts and exclude it from publishing.
- "Revise Facebook" -> edit only Facebook, then preview again.

Use `scripts/collect_approved.py` to package approved platforms when possible.
It copies every approved platform text file (`post.txt`, `caption.txt`,
`thread.txt`, etc.) plus generated media into `approved/`.

## Publishing Rules

Publishing means preparing or sending approved assets to Google Drive and Notion.

For Google Drive, use `scripts/publish_to_google_drive.py` after approval when
the local Google config exists. The uploader uses OAuth and expects:

- `%USERPROFILE%\.codex\google-drive-publish\credentials.json`
- `%USERPROFILE%\.codex\google-drive-publish\token.json` after first login
- `%USERPROFILE%\.codex\google-drive-publish\config.json` with
  `master_folder_id`

The Drive folder structure is:

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
Docs for each approved text file, named like `Instagram Caption` or `X Thread`.
Keep uploads private to the Gmail/Drive account unless the user explicitly asks
to change sharing.

Use connectors if available. If Google Drive, Google Docs, or Notion access is
unavailable, do not fake success. Leave an upload-ready package in `published/`
and tell the user which connection is missing.

After a platform has a live URL, append it to both published logs with `scripts/update_published_log.py` when possible.

The log must include at least: date, run_id, source, platform, status, draft_path, visual_path, drive_link, notion_link, live_url, and notes.

## Image QA

Use `gpt-image-2` for visuals when available, but verify generated text manually. The OpenAI image generation docs note that image models can create text-rich images, but text placement and clarity still need review.

Every generated visual set must include a first intro/thumbnail image. For carousel or slider posts, this is slide 1 and must be generated from `cover-prompt.json`, not from the normal slide prompt. For single-image platform posts, this is the primary thumbnail. The thumbnail should preview the topic with the same visual pattern as Stanley's accepted reference examples: paper/grid background, huge oversized headline, one colored accent word/number, small badge/pill, real Stanley avatar, creator row/profile pill, and a swipe/slide cue when relevant.

If the image contains unreadable text, regenerate or simplify the text. For important claims, prefer fewer words on the graphic and put detail in the caption.

Every slide must make sense by itself and as part of the post. Use enough public-facing information for each slide to work as a single post, but never render internal QA instructions such as `stand alone`, `single post`, `contain enough information`, or `this slide should make sense`. Recheck every carousel slide for correct numbering, source alignment, plain language, clear module labels, and text clipping. If the lower panel is a prompt, label it `PROMPT`. If it is a tip, label it `TIPS`. If it is an instruction, label it `INSTRUCTION`. Do not use a generic label when a specific one is available.

For Instagram slides 2-8, start the first content section close under the title/subtitle instead of leaving a large blank band. Fill whitespace with useful modules: comparison boxes, workflow rows, route maps, cost maps, checklists, matrices, dashboards, prompt boxes, ratio charts, or save-this summaries. Do not make every slide share the same structure.

For future carousel work, avoid placing the same `BOTTOM LINE` panel on most
slides. Vary closing modules and panel placement, or let the main body carry the
lesson when a repeated footer would make the slides feel identical.

Before submitting any generated visual, open the final PNG with the image viewer and confirm the creator avatar uses Stanley's brand avatar from `AIS-OS/asset-folder/Brand_Assets/Stan Avatar.png`. Do not accept a generated lookalike or a fake stock avatar. If the model creates the wrong person, repair or regenerate the image before handoff.

When adding Stanley's profile picture, replace the generated avatar area cleanly. Do not paste the real profile image on top of another generated face in a way that leaves both visible.

Keep a short QA note in the preview folder confirming which platform images were inspected and whether the real brand profile picture is visible.

## Style Inspiration

Charlie Hills and Walid Boulanouar are inspiration references for concise automation insight and visual social proof. If live LinkedIn content is inaccessible, ask the user for screenshots, copied post text, or specific examples. Do not claim you inspected inaccessible posts.

## Output To User

After drafting, respond with:

- Project folder path.
- Draft paths for each platform.
- Visual prompt paths and generated visual paths.
- A short preview summary.
- A direct request for which platform(s) to approve next.

Keep the response short. The artifacts live in files.
