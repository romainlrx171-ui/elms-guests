# ELMS 2026 — Guest Tracker

Internal tool for the Kessel Racing / Ferrari 296 GT3 team to track guests across the 2026 ELMS season (Romain Leroux).

**Live URL:** https://romainlrx171-ui.github.io/elms-guests/guests.html

## Features
- Tab per race (Prologue + 6 rounds), Paul Ricard highlighted as HOME RACE
- Season + per-race stats (confirmed / pending / ticket source breakdown)
- Search, filter, sortable columns
- Add / edit / delete guests directly from the dashboard — commits straight to GitHub
- **Bulk add** via paste (one guest per line, CSV-style)
- **CSV export** (current race or whole season)
- **Quick confirm** button — one click to flip invited → confirmed
- **Clone to another race** — duplicate a recurring guest across rounds
- **Print view** — clean paper-friendly layout for race-day handoff
- **Keyboard shortcuts**: `N` add guest · `B` bulk add · `/` search · `Esc` close
- Anyone with the link can view; only users with a GitHub token can edit

## Editing from the dashboard (one-time setup)
1. Click **⚙ Settings** in the top-right
2. Create a fine-grained GitHub PAT: https://github.com/settings/personal-access-tokens/new
   - Repository access: only `romainlrx171-ui/elms-guests`
   - Permissions → Repository → **Contents: Read and write**
3. Paste the token — stored in your browser's localStorage only, per device.
4. Add / edit / delete actions and the `＋ Add guest` / `📥 Bulk add` buttons appear.

Every change creates a real git commit visible in the repo history.

## Data model (`guests-data.json`)
- **Guest**: `{ id, race, name, company, ticket, status, notes }`
- **ticket**: `kessel` · `us` · `themselves` · `vip`
- **status**: `confirmed` · `invited` · `declined` · `noreply`
- **race**: `prologue` · `r1` · `r2` · `r3` · `r4` · `r5` · `r6`

## Bulk add format
One guest per line: `Name, Company, Ticket, Status, Notes`

Only `Name` is required. `Ticket` defaults to `us`, `Status` defaults to `invited`. Wrap values containing commas in `"double quotes"`.

Example:
```
John Doe, Infovista, us, confirmed, Hotel booked
Jane Smith, Telit, vip, invited, Bringing +1
"Smith, Jr.", Acme, kessel
```
