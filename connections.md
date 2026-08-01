# Connections

Registry of every system Stanley's AIOS can reach. Filled from onboarding and expanded over time as tools are wired. `/audit` checks this file for domain coverage and freshness.

| # | Domain | Tool | Mechanism | Auth | Last checked |
|---|---|---|---|---|---|
| 1 | Revenue / Financials | Client-dependent payment rails; foreign client payments vary by client and project | not yet connected | - | - |
| 2 | Customer interactions | LinkedIn DMs, email, WhatsApp, social DMs, calls, and any client-originating platform | not yet connected | - | - |
| 3 | Calendar | Calendar not confirmed; likely tied to email or client invite links | not yet connected | - | - |
| 4 | Communication | Multi-channel inbox across LinkedIn, email, WhatsApp, social platforms, calls, and client-preferred channels | not yet connected | - | - |
| 5 | Project / task tracking | Notion | not yet connected | - | - |
| 6 | Meeting intelligence | Google Drive; client call notes and recordings not yet standardized | not yet connected | - | - |
| 7 | Knowledge / files | Google Drive | not yet connected | - | - |

**Mechanism options:** `mcp` (MCP server), `script` (Python/Bash hitting an API, in `scripts/`), `export` (CSV/JSON dump pipeline), `key+ref` (`.env` key + `references/{tool}-api.md` guide), `not yet connected`.

When you wire a new tool, also save `references/{tool}-api.md` capturing endpoints, auth flow, and common queries - researched once, saved forever.
