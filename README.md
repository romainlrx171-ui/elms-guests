# ELMS 2026 — Guest Tracker

Internal tool for the Kessel Racing / Ferrari 296 GT3 team to track guests across the 2026 ELMS season (Romain Leroux).

**Live URL:** https://romainlrx171-ui.github.io/elms-guests/guests.html

## Fields tracked per guest
`name` · `company` · `ticket` (kessel / us / themselves / vip) · `status` (confirmed / invited / declined / noreply) · `notes` · `race` (prologue / r1 / r2 / r3 / r4 / r5 / r6)

## How to update
1. Edit `guests-data.js` — add or modify guests in `GUESTS_DATA.guests`
2. `git commit && git push`
3. GitHub Pages redeploys in ~30s — refresh the page
