# Progress Note

Session ended 2026-05-20. Covered v1.10.0 Three Step.

---

## Milestone

**v1.10.0 Three Step** — booking widget redesigned to a 3-step form matching the mobile app UX.

---

## Tasks Completed

- Added `GET /catalog/options?locationId=X` endpoint to Booking Platform API (services + staff)
- Redesigned widget from slot-picker-first to 3-step flow:
  - Step 1: Full Name, Phone, Email (name + phone required)
  - Step 2: Service dropdown + Preferred Barber dropdown (loaded live from `/catalog/options`)
  - Step 3: Available time slots with date nav + notes textarea + REQUEST APPOINTMENT
- Gold step indicator dots with connecting lines — active dot fills gold, done dot fades gold
- 12-hour AM/PM time format on slot grid (timezone-aware via `res.timezone` from availability API)
- Rebuilt widget bundle and copied to `assets/booking-widget.js` and `assets/booking-widget.css`
- Updated dark theme: gold labels (`#f5b544`), warm cream text (`#f0ede4`), gold-tinted borders
- Moved dark theme overrides to end of `booking-widget.css` so cascade order works correctly
- Fixed step indicator misalignment: `line-height: 1`, `align-self: center`, `min-width/height: 28px`
- Removed redundant `.form-card` padding (`#booking-widget { padding: 0 }`)
- Removed nested `.bw-root` border/radius (`.form-card` provides outer border)
- Added `select` and `option` dark theme styles to index.html override block
- Fixed local API: killed stale process, restarted with updated routes, seeded local database
- Tagged and pushed v1.10.0

---

## Git Commits (Jones-Barbor-Shop)

| Hash | Message |
|---|---|
| `17a9246` | feat(booking): update widget bundle — 3-step form redesign |
| `67a1a19` | fix(booking): 12-hr time format, gold/cream theme, step indicator alignment |

## Git Commits (Booking-Platform)

| Hash | Message |
|---|---|
| `bc8a4d6` | feat(catalog): add public /catalog/options endpoint for services and staff listing |
| `3aac2ae` | feat(widget): redesign to 3-step flow — customer info, service picker, slot and notes |

---

## Git Tags

| Tag | Repo |
|---|---|
| `v1.10.0__three-step__commit-67a1a19` | Jones-Barbor-Shop (applied to docs commit) |

---

## Files Changed

| File | Change |
|---|---|
| `index.html` | Step indicator fixes, padding/border overrides, select styles |
| `assets/booking-widget.js` | Rebuilt — 3-step flow, 12-hr time |
| `assets/booking-widget.css` | Rebuilt + gold/cream dark theme, overrides at end |
| `CHANGELOG.md` | v1.10.0 entry added |
| `RELEASE_NOTES.md` | v1.10.0 entry prepended |
| `ROADMAP.md` | v1.10.0 added to Completed |
| `STATUS.md` | Updated to v1.10.0 |
| `PROGRESS_NOTE.md` | This file |
| `CONTEXT.md` | Updated to v1.10.0 |

---

## What's Next

1. Deploy booking-platform API to VPS (PM2 on port 3001)
   - Upload via WinSCP to /var/www/booking-api/: dist/, package.json, package-lock.json, prisma/schema.prisma, .env.production (rename to .env)
   - SSH: npm install --omit=dev → npx prisma generate → pm2 start dist/server.js --name booking-api
   - sudo ufw allow 3001/tcp
   - Verify: curl http://localhost:3001/health → {"status":"ok"}
2. Update index.html `data-api-url` to `http://74.208.9.49:3001` for production
3. Upload updated index.html + assets to /var/www/jones-barbor-shop/
4. Test booking widget end-to-end on live site
