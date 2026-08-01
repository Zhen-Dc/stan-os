---
name: repurpose-blog
description: Rewrite public blog posts, articles, or pasted web content into Stanley-brand professional blog posts, preserving the original facts and structure while removing false first-person/project ownership claims. Use when the user asks to scrape or repurpose a blog post from a URL, rewrite an article for their brand voice, create an educational how-it-works tutorial from someone else's project or technique, save the finished post under AIS-OS/asset-folder/content, approve a rewritten blog, or hand an approved blog script to the repurpose-youtube-video-v3 skill for all-platform social drafting.
---

# Repurpose Blog

## Purpose

Turn a source blog/article into a Stanley-brand professional blog post, then prepare the approved article as a script source for `repurpose-youtube-video-v3`.

Use this skill for awareness and education posts. Do not write as though Stanley personally built, tested, shipped, earned, discovered, or performed the source project unless the user explicitly says that he did.

## Workspace

Create every project under:

```text
AIS-OS/asset-folder/content/<article-title-slug>/
  source/
    original-url.txt
    source-article.md
  blog/
    original-blog.txt
    repurposed-blog.txt
    draft.md
    approved.txt
    approved.md
    metadata.json
  preview/
    blog-preview.md
  handoff/
    repurpose-youtube-script.txt
  manifest.json
```

Use `scripts/create_blog_project.py` when possible to create the folder, source files, `blog/original-blog.txt`, `blog/repurposed-blog.txt`, metadata, and preview shell.

## Intake Rules

Accept:

- A public article/blog URL.
- Pasted article text.
- A local source file.

Before writing, summarizing, extracting, or repurposing anything, save the full original post first. This is a hard workflow rule: no rewrite draft should be created until `blog/original-blog.txt` contains the full scraped, pasted, or authorized source article body.

When given a URL, fetch only public content that is accessible without login or bypassing access controls. Use Firecrawl through `.claude/skills/repurpose-youtube-video-v3/scripts/firecrawl_scrape.py` for the capture step. The expected output is the full extracted article body, not a summary. If the website blocks scraping, returns empty body text, requires login, or appears restricted, explain the blocker and ask for pasted text or an authorized export. Do not substitute source notes, summaries, metadata, or guesses for the original post.

Save the original source URL in `source/original-url.txt` and include it in the final article metadata. Always keep the original full post and repurposed rewrite side by side in the same folder:

- `blog/original-blog.txt`
- `blog/repurposed-blog.txt`

Save the complete extracted article body into `blog/original-blog.txt`. If pasted text or an authorized export is provided, save that full text there. If the full body cannot be extracted from a URL, stop and ask the user for the article text instead of creating a partial original.

## Rewrite Rules

Preserve the source article's facts, sequence, main examples, and structure. Rewrite the expression, framing, and teaching angle for Stanley's brand voice.

Use a professional blog tone: clear, useful, practical, and credible. Avoid hype, fake personal proof, fake client proof, or fake behind-the-scenes claims.

Always convert "someone did/built/achieved this" framing into educational/process framing unless the user explicitly says Stanley did the work. For example:

- Avoid: "I built a loop prompting workflow that improved my outputs."
- Use: "Loop prompting is a workflow where the model critiques and improves its own output in repeated passes."
- Avoid: "We used this exact system for a client."
- Use: "A practical way to apply this system is to map the workflow, define the review loop, and repeat until the output meets the target."

If the source article is about a named person or company, keep attribution factual and detached:

- "The article describes how X approached Y."
- "The useful lesson is the process: ..."
- "For teams trying to understand this method, the workflow breaks down into ..."

## Required Blog Shape

Write each final article with this structure unless the user asks for a different format:

1. Title
2. Hook
3. Introduction
4. What it is
5. Why it matters
6. Step-by-step process
7. Practical example
8. Common mistakes
9. Final takeaway
10. CTA

Keep the article educational first. The CTA can invite readers to follow, comment, ask a question, or explore how the workflow applies to their business.

## Metadata

Create `blog/metadata.json` with:

- `title`
- `slug`
- `source_url`
- `source_type`
- `source_attribution`
- `source_confidence`
- `tone`
- `audience`
- `excerpt`
- `tags`
- `seo_keywords`
- `title_options`
- `visual_prompts`
- `ownership_note`
- `status`

Use `status: "draft"` until the user says the article is approved.

## Workflow

1. Gather the source from URL, pasted text, or file.
2. Create the content project with `scripts/create_blog_project.py`.
3. Save the full source article in `blog/original-blog.txt` and keep `source/original-url.txt` for attribution before any rewriting begins.
4. Extract the source outline and key facts.
5. Rewrite into `blog/repurposed-blog.txt` using the required blog shape.
6. Add metadata, SEO fields, tags, title options, and visual prompts.
7. Save a short preview in `preview/blog-preview.md`.
8. Ask the user to review and approve the article.

Keep `blog/draft.md` as a Markdown compatibility copy when useful, but treat `blog/repurposed-blog.txt` as the primary draft file.

Do not push to `repurpose-youtube-video` until the user explicitly says the post is approved.

## Approval And Handoff

When the user says the blog is approved:

1. Reread `blog/draft.md` from disk. If the user edited it, use the edited file.
2. Prefer `blog/repurposed-blog.txt` if it exists; otherwise fall back to `blog/draft.md`.
3. Copy the approved article to `blog/approved.txt` and `blog/approved.md`.
4. Run `scripts/approve_to_repurpose.py` when possible.
5. The script writes `handoff/repurpose-youtube-script.txt` and `source/script.txt`.
6. Then use `repurpose-youtube-video-v3` with the approved blog as a script source.
7. Draft all platforms by default: LinkedIn, Instagram, X, and Facebook.

Treat the approved blog article as the script. The social drafts must be derived from the approved article and the saved source attribution, not from memory.

## Cross-Skill Handoff

After approval, trigger or continue with `repurpose-youtube-video-v3` using:

```text
source_type: script
source_value: <content-project>/source/script.txt
project_title: <approved blog title>
project_slug: <same content slug>
platforms: all
```

Keep the handoff inside the same `AIS-OS/asset-folder/content/<slug>/` project whenever possible so blog, source, social drafts, approvals, and publishing records stay together.

## Output To User

After drafting, respond with:

- Project folder path.
- Original blog TXT path.
- Repurposed blog TXT path.
- Metadata path.
- Preview path.
- Original source URL.
- A direct request for approval before social repurposing.

After approval handoff, respond with:

- Approved article path.
- Handoff script path.
- Confirmation that `repurpose-youtube-video-v3` should now draft all platforms from the approved script.
