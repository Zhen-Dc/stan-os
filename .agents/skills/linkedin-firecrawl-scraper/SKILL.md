---
name: linkedin-firecrawl-scraper
description: Scrape LinkedIn jobs, company hiring signals, posts, company pages, or profile pages using Firecrawl only. Use when Stanley needs LinkedIn research, AI automation hiring intelligence, job/task extraction, company requirement analysis, or content ideas based on LinkedIn data. Captures LinkedIn pages with FIRECRAWL_API_KEY or a local FIRECRAWL_API_URL, saves Markdown/JSON, and summarizes automation opportunities for Claude Code, n8n, Make, Zapier, APIs, MCP, and AI agents.
---

# LinkedIn Firecrawl Scraper

## Purpose

Use Firecrawl as the only LinkedIn data path when a task needs repeatable capture of jobs, company hiring signals, public posts, or profile/company pages. Prefer this skill over manual LinkedIn browsing when the user needs structured evidence, comparisons, lists, or content based on LinkedIn pages.

## Required Setup

1. Use Firecrawl only. Do not call any other scraping provider, LinkedIn scraper MCP, browser scraping path, or ad hoc HTML fetcher from this skill.
2. Read Firecrawl config from the environment, `--env-file`, `%USERPROFILE%\.codex\firecrawl\.env`, `.env`, or a local `FIRECRAWL_API_URL`.
3. Never write Firecrawl API keys into Markdown, logs, datasets, or chat.
4. Capture LinkedIn search URLs, job URLs, company URLs, or profile URLs as Markdown/JSON before analysis.
5. If Firecrawl fails because config is missing, stop and tell the user exactly where to set `FIRECRAWL_API_KEY` or `FIRECRAWL_API_URL`.

## Core Workflow

1. Clarify the target if missing: role keywords, location, date range, and whether the user wants jobs, posts, companies, or profiles.
2. Build a LinkedIn search URL or use the exact LinkedIn URL supplied by the user.
3. Run `scripts/firecrawl_linkedin.py scrape-search` for job searches, or `scripts/firecrawl_linkedin.py scrape-url` for a specific LinkedIn URL.
4. Save raw Firecrawl JSON and Markdown under the requested project folder, or under `.tmp/linkedin-firecrawl/` if no durable output is requested.
5. Run `scripts/firecrawl_linkedin.py analyze-jobs` on captured Markdown files to extract:
   - companies hiring
   - role titles and locations
   - repeated automation tasks
   - required tools and skills
   - Claude Code automation angles
   - content hooks for Stanley
6. For content, match `references/voice.md`: practical, proof-driven, direct, workflow-focused, and tied to business outcomes.

## Recommended Commands

Scrape a LinkedIn jobs search page through Firecrawl:

```powershell
python .agents\skills\linkedin-firecrawl-scraper\scripts\firecrawl_linkedin.py scrape-search `
  --keywords "AI Automation Specialist" `
  --location "United States" `
  --out-dir .tmp\linkedin-firecrawl\ai-automation-specialist
```

Scrape a specific LinkedIn job URL:

```powershell
python .agents\skills\linkedin-firecrawl-scraper\scripts\firecrawl_linkedin.py scrape-url `
  --url "https://www.linkedin.com/jobs/view/..." `
  --out-dir .tmp\linkedin-firecrawl\job-page
```

Analyze captured Firecrawl Markdown:

```powershell
python .agents\skills\linkedin-firecrawl-scraper\scripts\firecrawl_linkedin.py analyze-jobs `
  --input-dir .tmp\linkedin-firecrawl `
  --out .tmp\linkedin-firecrawl\linkedin-job-analysis.md
```

## Output Rules

- Keep raw scraped data separate from interpreted research.
- Include source URL, query, location, Firecrawl API URL, and scrape time in the analysis.
- Do not claim LinkedIn data is complete. State that it is a Firecrawl-captured sample.
- When creating public content, avoid exposing private emails, personal phone numbers, or applicant-sensitive data.
- When the task is about jobs, convert requirements into specific business tasks, then map each task to automation demos Stanley can build with Claude Code.

## References

Read `references/firecrawl-linkedin.md` when choosing LinkedIn URL shapes, Firecrawl config, output folders, or analysis rules.
