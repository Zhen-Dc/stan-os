# Publish Schema

## Run Manifest

`manifest.json` fields:

- `project_slug`
- `project_title`
- `created_at`
- `source_type`: `youtube_url`, `linkedin_post`, `social_post`, `script`, `transcript`, or `source_brief`
- `source_value`
- `workspace`
- `platforms`
- `status`: `draft`, `preview`, `approved`, `packaged`, or `published`
- `notes`

## Draft Files

Each platform draft lives at `drafts/<Platform>/text/post.txt` and is plain text.

The file contains the final editable post copy. The publish step must reread this file from disk.

Platforms may also include additional text files such as `caption.txt` and
`thread.txt`. Approval packaging must copy every `*.txt` file from
`drafts/<Platform>/text/` into `approved/<Platform>/text/`.

Each platform image prompt lives at `drafts/<Platform>/images/visual-prompt.txt`. Generated visuals should be PNG files under `drafts/<Platform>/images/`.

## Approval State

`approved/approval.json`:

```json
{
  "project_slug": "building-beautiful-websites-with-claude-code-is-too-easy",
  "approved_platforms": ["linkedin", "x"],
  "skipped_platforms": ["instagram", "facebook"],
  "approved_at": "2026-06-25T12:00:00+01:00",
  "notes": "",
  "packaged": {
    "linkedin": {
      "text_paths": ["approved/LinkedIn/text/post.txt"],
      "visual_paths": ["approved/LinkedIn/images/linkedin-thumbnail.png"]
    }
  }
}
```

## Published Logs

CSV columns:

```text
date,run_id,project_slug,project_title,source,platform,status,draft_path,visual_path,drive_link,notion_link,live_url,notes
```

JSONL fields mirror the CSV and may include extra metadata.

## Google Drive Publish

Use `.claude/skills/repurpose-youtube-video/scripts/publish_to_google_drive.py`
after platform approval.

Local config defaults:

```text
%USERPROFILE%\.codex\google-drive-publish\credentials.json
%USERPROFILE%\.codex\google-drive-publish\token.json
%USERPROFILE%\.codex\google-drive-publish\config.json
```

`config.json` must contain:

```json
{
  "master_folder_id": "google-drive-folder-id"
}
```

The upload source is `approved/`, not `drafts/`. The top-level content folder is
named from `manifest.json.project_title`. Platform folders receive approved
media files only. The separate `Post/` folder receives one Google Doc per
approved text file, named `{Platform} {Text File Stem}`.

The publish step writes `published/google-drive.json` with the Drive folder,
platform folder, media, and Google Doc URLs. Existing folders/files/docs with the
same names are updated instead of duplicated.

## Notion Handoff Fields

- Title
- Platform
- Status
- Source
- Project slug
- Draft file
- Visual file
- Drive link
- Live URL
- Publish date
- Notes

If Notion connector access is missing, create `published/notion-row.md` with these fields instead of pretending to upload.
