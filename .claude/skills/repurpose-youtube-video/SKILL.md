---
name: repurpose-youtube-video
description: Repurpose a YouTube URL, LinkedIn/social post URL, transcript, source brief, or pasted script into platform-specific social media drafts, visuals, previews, approvals, Google Drive upload packages, Notion handoff records, and published URL logs. Use when the user asks to turn source content into LinkedIn, Instagram, X/Twitter, or Facebook posts; prepare drafts for an AI social media manager; generate faceless educational carousel visuals; create key-takeaway graphics; prepare selective platform approvals; or publish approved social content from editable draft files.
---

# Repurpose YouTube Video

## Purpose

Support Stanley's AI social media manager by turning one source into four platform-ready content packages. The source can be a YouTube/video transcript, a pasted script, an approved blog handoff, or a public LinkedIn/social post that has first been analyzed through the client-trust LinkedIn SOP. The AI social media manager is the operator using this skill; this skill is the reusable repurposing workflow, folder contract, drafting process, visual process, approval process, and publishing handoff.

- LinkedIn: AI automation services and educational authority.
- X: sharp automation insight, quote, or concise educational thread.
- Instagram: educational carousel that feels like tweet-style thought cards.
- Facebook: course-interest and course-sales content for people who may learn AI skills from Stanley.

Always create local drafts first. The user previews and approves platforms one by one before any Drive or Notion publishing step.

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
- `references/publish-schema.md` before packaging approvals, updating logs, or preparing Notion records.

## Intake

Accept either:

1. A YouTube URL.
2. A LinkedIn/social post URL that has public text, screenshot evidence, pasted text, or a saved source brief.
3. A pasted YouTube video script.
4. A transcript file or pasted transcript.
5. A handoff script or approved source brief from another AIS-OS workflow.

If the user provides only a YouTube URL and transcript extraction is unavailable, ask for the transcript or script. If the user provides a LinkedIn/social URL and public text is blocked, ask for screenshots or pasted text. Do not invent the source content.

If metadata is available but the transcript body is blocked or empty, create only a clearly labeled metadata-derived review draft when the user still wants something to preview. Mark `source_confidence: metadata-derived` in the manifest and draft frontmatter, and request the transcript before final approval.

All post copy, slide copy, and quote-card text must come from the source material: transcript/script when available, otherwise verified public post text, title, description, chapters, and source brief. Use lessons, facts, frameworks, or useful takeaways from what the source actually discusses. Do not use random motivational text or unrelated AI advice.

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
   - Before rendering visuals, run a humanizer pass: remove ambiguous model-speak, explain jargon, keep the post tied to the source, and confirm the carousel/script follows the same sequence as the main post.
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
6. For structured educational carousels, sliders, quote cards, and clean infographic-style posts, prefer the local deterministic renderer first:
   - `scripts/render_reference_style_images.py --project-dir <content-project>`
   - This creates editable, reference-style PNGs without using GPT image generation.
   - Use this when the user asks for the former/local technique, reference-style carousel images, clean structured slides, or no GPT image generation.
7. Generate visuals with `gpt-image-2` only when the user wants model-generated raster imagery or when local rendering cannot satisfy the visual requirement. Use the image generation tool available in the current environment if it clearly maps to OpenAI image generation. If image generation is not available, save the prompts and mark images as pending.
   - When the user provides a local brand/profile photo, use it in local rendered visuals if the current image tool cannot directly ingest local files. Keep the prompt file alongside the preview so alternate renders can still be generated later.
8. Save a preview summary in `preview/preview.md` with links to all drafts, visual prompts, and generated images.
9. Ask the user to approve platforms one by one.

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

Every generated visual set must include a first intro/thumbnail image. For carousel or slider posts, this is slide 1. For single-image platform posts, this is the primary thumbnail. The thumbnail should preview the topic with the same visual pattern as Stanley's reference examples: paper/grid background, strong oversized headline, one colored accent word/number, small badge/pill, creator row, and a swipe/slide cue when relevant.

If the image contains unreadable text, regenerate or simplify the text. For important claims, prefer fewer words on the graphic and put detail in the caption.

Every slide must make sense by itself and as part of the post. Recheck every carousel slide for correct numbering, source alignment, plain language, and clear module labels. If the lower panel is a prompt, label it `PROMPT`. If it is a tip, label it `TIPS`. If it is an instruction, label it `INSTRUCTION`. Do not use a generic label when a specific one is available.

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
