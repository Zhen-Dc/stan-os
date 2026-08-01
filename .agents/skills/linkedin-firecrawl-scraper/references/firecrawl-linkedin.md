# Firecrawl LinkedIn Reference

## Firecrawl Only Rule

This skill must only use Firecrawl to capture LinkedIn pages. Do not use any other scraping provider, LinkedIn scraper MCP, browser automation, direct `curl` page capture, or manual copy/paste as the scraping path for this skill.

## Config Resolution

The script checks config in this order:

1. `--env-file`
2. Environment variables
3. `.env` in the current workspace
4. `%USERPROFILE%\.codex\firecrawl\.env`
5. `%USERPROFILE%\.config\firecrawl\.env`
6. local Firecrawl URLs such as `http://localhost:3002`

Use:

- `FIRECRAWL_API_KEY` for hosted Firecrawl.
- `FIRECRAWL_API_URL` for a local or self-hosted Firecrawl endpoint.

## LinkedIn URL Shapes

Use exact URLs when the user provides them. For job search, construct a LinkedIn jobs search URL:

```text
https://www.linkedin.com/jobs/search/?keywords=<encoded keywords>&location=<encoded location>
```

Useful keyword sets:

- `AI Automation Specialist`
- `AI Agent Developer`
- `AI Agent Specialist`
- `AI Integration Automation Specialist`
- `AI Automation n8n Make Zapier`
- `Claude Code automation specialist`

Firecrawl may return partial content if LinkedIn blocks anonymous access. Keep the raw Markdown and state that results are a Firecrawl-captured sample.

## Extraction Checklist

From each captured page, extract:

- Company
- Role title
- Location and work mode
- Business team served
- Expected tasks
- Required tools
- AI/LLM skills
- Integration surfaces: APIs, webhooks, CRM, ATS, docs, email, calendar, data warehouse, tickets
- Proof metrics: time saved, ROI, adoption, accuracy, self-service, reduced support volume
- Claude Code content/demo angle

## Analysis Rules

- Keep source capture and interpretation separate.
- Preserve source URL and scrape timestamp.
- Do not expose private personal data in final content.
- Do not claim comprehensive market coverage from a small Firecrawl sample.
- Convert job requirements into practical business tasks Stanley can speak about or demonstrate.
