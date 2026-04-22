# ELMS 2026 — Guest Tracker

Internal tool for the Kessel Racing / Ferrari 296 GT3 team to track guests across the 2026 ELMS season (Romain Leroux).

**Live URL:** https://romainlrx171-ui.github.io/elms-guests/guests.html

## Features
- Tab per race (Prologue + 6 rounds), Paul Ricard highlighted as HOME RACE
- Season + per-race stats (confirmed / pending / ticket source breakdown)
- Search, filter, sortable columns
- Add / edit / delete guests directly from the dashboard — **no GitHub account needed**
- **Real-time sync** via Firebase Firestore — all teammates see changes instantly
- **Bulk add** via paste (one guest per line, CSV-style)
- **CSV export** (current race or whole season)
- **Quick confirm** button — one click to flip invited → confirmed
- **Clone to another race** — duplicate a recurring guest across rounds
- **Print view** — clean paper-friendly layout for race-day handoff
- **"Added by"** per guest — track who added / last edited each entry
- **Keyboard shortcuts**: `N` add guest · `B` bulk add · `/` search · `Esc` close

## For team members (no GitHub account needed)
1. Open the live URL above
2. Click **⚙ Edit mode** top-right
3. Enter your name + the team password (ask Romain)
4. Add / edit / remove guests — everyone sees changes live

## One-time Firebase setup (for Romain)
1. Go to https://console.firebase.google.com/ → **Add project** → name it `elms-guests` → skip Analytics → Create
2. In the project, left sidebar → **Build → Firestore Database** → **Create database** → choose **Start in test mode** → pick region `eur3 (europe-west)`
3. Left sidebar → **Project settings (gear icon) → General** → scroll to **Your apps** → click the `</>` web icon → nickname `guests` → Register app
4. Copy the `firebaseConfig` object shown
5. Open `guests.html`, find the `FIREBASE_CONFIG` constant near the top of `<script id="app">`, and paste your config values
6. Change `TEAM_PASSWORD` to whatever password you want to share with the team
7. Commit + push → share the URL with your team

Optional security tightening: go to **Firestore Database → Rules** and paste the contents of `firestore.rules` (then click Publish). Rules here are wide-open by design — the team password + obscure URL are the gate. Fine for an internal tool.

## Data model (Firestore)
- Collection `guests` (one doc per guest): `{ id, race, name, company, ticket, status, notes, updatedAt, updatedBy }`
- Collection `races` (seeded automatically on first load)
- Collection `config` → doc `meta`: `{ season, team, driver }`

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

## Backup
Firestore auto-backups are on the paid plan. For free backups, export the full season via **📤 Export CSV → Whole season** periodically and commit the CSV to the repo.

## Legacy
`guests-data.json` is the old data file (pre-Firestore). Kept as historical reference only — the live dashboard reads/writes Firestore.
