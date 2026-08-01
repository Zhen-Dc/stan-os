# Tools

This folder holds deterministic scripts for the WAT framework.

Use tools for work that should be reliable and repeatable:

- API calls
- Data scraping
- File operations
- Data cleaning and transformations
- Report generation
- Export/import steps

Rules:

- Check for an existing tool before creating a new one.
- Keep each tool focused on one job.
- Read credentials from `.env`; never hard-code secrets.
- Write temporary outputs to `.tmp/`.
- If a tool fails, fix and retest it, then update the relevant workflow with what you learned.
