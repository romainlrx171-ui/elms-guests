# ELMS 2026 — Guest Tracker

Internal tool for the Kessel Racing / Ferrari 296 GT3 team to track guests across the 2026 ELMS season (Romain Leroux).

**Live URL:** https://romainlrx171-ui.github.io/elms-guests/guests.html

## Features
- Tab per race (Prologue + 6 rounds), Paul Ricard highlighted as HOME RACE
- Season + per-race stats (confirmed / pending / ticket source breakdown)
- Filters: search, status, ticket source
- **Add / edit / delete guests directly from the dashboard** — commits straight to GitHub
- Anyone with the link can view; only users with a GitHub token can edit

## Editing from the dashboard
1. Click **⚙ Settings** in the top-right
2. Create a fine-grained GitHub PAT: https://github.com/settings/personal-access-tokens/new
   - Repository access: only `romainlrx171-ui/elms-guests`
   - Permissions → Repository → **Contents: Read and write**
3. Paste the token. It's stored in your browser's localStorage only.
4. The **＋ Add guest** button, Edit and Delete row actions appear.

Each change creates a real git commit visible in the repo history.

## Data model
`guests-data.json` — fetched at page load.
- **Guest**: `{ id, race, name, company, ticket, status, notes }`
- **ticket**: `kessel` · `us` · `themselves` · `vip`
- **status**: `confirmed` · `invited` · `declined` · `noreply`
- **race**: `prologue` · `r1` · `r2` · `r3` · `r4` · `r5` · `r6`
