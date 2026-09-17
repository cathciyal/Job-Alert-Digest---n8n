# Job Alert Digest (n8n)

Automated pipeline that turns messy LinkedIn/Indeed job alert emails into a clean, deduplicated Google Sheet of Working Student & Internship postings — no manual scrolling through Gmail required.

## What it does

Every day at 3 PM, the workflow:

1. **Fetches** new LinkedIn and Indeed job-alert emails from Gmail
2. **Parses** the raw email text into structured postings (title, company, location, link)
3. **Filters** to keep only Working Student / Intern roles, dropping anything with a hard German-language requirement
4. **Deduplicates** postings that show up across multiple overlapping saved searches
5. **Caps growth** — clears older entries once the sheet passes 50 rows, so it never gets unmanageable
6. **Appends** new results to Google Sheets and **emails a summary notification**

## Why

Job alert emails are noisy, repetitive, and easy to miss in a crowded inbox. This turns that noise into a single, always-current spreadsheet — so checking for new roles takes seconds, not minutes.

## Stack

- **n8n** — workflow orchestration (Schedule Trigger, Gmail, Code, Google Sheets nodes)
- **JavaScript** (Code nodes) — email parsing, filtering, and dedup logic
- **Google Sheets API** — persistent storage
- **Gmail API** — source data + notifications

## Setup

1. Import `workflow.json` into your n8n instance
2. Connect your **Gmail** and **Google Sheets** credentials (Sheets API must be enabled in your Google Cloud project)
3. Point the Google Sheets node at your own spreadsheet (header row: `company | position | title | location | link`)
4. Adjust the German-requirement phrase list and position keywords in the Code node to fit your own search criteria
5. **Publish** the workflow in n8n to activate the schedule

## Notes

- Parsing relies on the current plain-text layout of LinkedIn/Indeed alert emails — if either service changes its email template, the parser may need updating.
- No API keys or credentials are stored in this repo; connect your own via n8n credentials.

## Author
- Aruna Cathciyal Gilbert Radjou
