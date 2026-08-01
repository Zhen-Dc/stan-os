# Firecrawl For Local Models

Use `scripts/firecrawl_scrape.py` for every web source in v3. This makes
Firecrawl available to weak or local models through a normal command instead of
requiring the model to know an MCP protocol.

## Config

The script checks these locations in order:

1. Process environment:
   - `FIRECRAWL_API_KEY`
   - `FIRECRAWL_API_URL`
2. `--env-file <path>`
3. `.env` in the current workspace
4. `%USERPROFILE%\.codex\firecrawl\.env`
5. `%USERPROFILE%\.config\firecrawl\.env`
6. `C:\Users\DELL\Master Project\master hermes\tools\hermes_gateway\.env`
7. A running local Firecrawl server:
   - `http://localhost:3002`
   - `http://127.0.0.1:3002`

If no config file is present but local Firecrawl is running, the script uses it
automatically. This is the preferred path for local models.

Recommended local-model setup:

```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.codex\firecrawl"
Set-Content "$env:USERPROFILE\.codex\firecrawl\.env" "FIRECRAWL_API_KEY=fc-your-key-here"
```

For a self-hosted Firecrawl server:

```powershell
Set-Content "$env:USERPROFILE\.codex\firecrawl\.env" "FIRECRAWL_API_URL=http://localhost:3002"
```

The config file is optional when the local server is already running on port
`3002`.

## Usage

```powershell
python .claude/skills/repurpose-youtube-video-v3/scripts/firecrawl_scrape.py `
  --url "https://example.com/post" `
  --out-dir "asset-folder/content/example/source"
```

## Local Self-Hosted Server

This workspace has a local Firecrawl checkout at:

```text
AIS-OS/tools/firecrawl-self-host/
```

Start or restart it with Docker:

```powershell
docker compose -f "tools/firecrawl-self-host/docker-compose.yaml" up -d api
```

The local API is expected at:

```text
http://localhost:3002
```

The scraper wrapper auto-detects that URL, so a local model only needs to run
the `firecrawl_scrape.py` command. It does not need to know the Firecrawl MCP
protocol or hold an API key.

Expected outputs:

- `source/firecrawl.json`
- `source/firecrawl.md`
- `source/firecrawl.html` when HTML is returned

If config is missing, the script exits with code `2` and prints
`FIRECRAWL_CONFIG_MISSING`.
