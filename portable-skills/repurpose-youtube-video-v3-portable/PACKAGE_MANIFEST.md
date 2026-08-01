# Package Manifest

## Main Skill

- `skills/repurpose-youtube-video-v3/SKILL.md`
- `skills/repurpose-youtube-video-v3/scripts/collect_approved.py`
- `skills/repurpose-youtube-video-v3/scripts/create_run.py`
- `skills/repurpose-youtube-video-v3/scripts/firecrawl_scrape.py`
- `skills/repurpose-youtube-video-v3/scripts/generate_instagram_json_prompts.py`
- `skills/repurpose-youtube-video-v3/scripts/publish_to_google_drive.py`
- `skills/repurpose-youtube-video-v3/scripts/render_reference_style_images.py`
- `skills/repurpose-youtube-video-v3/scripts/update_published_log.py`
- `skills/repurpose-youtube-video-v3/references/firecrawl-local-model.md`
- `skills/repurpose-youtube-video-v3/references/instagram-cover-json-prompt-system.json`
- `skills/repurpose-youtube-video-v3/references/instagram-slide-json-prompt-system.json`
- `skills/repurpose-youtube-video-v3/references/platform-rules.md`
- `skills/repurpose-youtube-video-v3/references/publish-schema.md`
- `skills/repurpose-youtube-video-v3/references/visual-recipes.md`

## Companion Skills

- `skills/html-python-image-renderer/`
- `skills/humanizer/`

## Workflows

- `workflows/repurpose-youtube-video-execution-sop.md`
- `workflows/repurpose-social-full-package-dumb-model-sop.md`
- `workflows/client-trust-linkedin-scrape-and-recreate-sop.md`
- `workflows/local-html-python-image-rendering-full-workflow.md`
- `workflows/code-generated-images-repurpose-sop.md`
- `workflows/repurpose-youtube-video-sop.md`
- `workflows/vixma-editable-design-repurpose-sop.md`

## Assets And Templates

- `brand-assets/Stan Avatar.png`
- `templates/asset-folder/content/.gitkeep`
- `templates/asset-folder/repurpose-youtube-video/.gitkeep`
- `config-templates/firecrawl/.env.example`
- `config-templates/google-drive-publish/config.example.json`

## Secrets Policy

This bundle intentionally excludes:

- Firecrawl API keys.
- Google OAuth `credentials.json`.
- Google OAuth `token.json`.
- Google Drive master folder IDs except the placeholder config template.
- Generated cache folders such as `__pycache__`.

