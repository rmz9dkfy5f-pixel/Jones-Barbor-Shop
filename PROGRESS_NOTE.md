# Progress Note

Session ended 2026-05-19. Covered v1.9.8 and v1.9.9.

---

## Milestone

**v1.9.8** — Booking widget rendering fixed.
**v1.9.9** — data-api-url reverted to localhost:3000 for local dev.

---

## Tasks Completed

- Rebuilt `booking-widget.js` with `process.env.NODE_ENV` inlined at build time (was crashing silently in browser)
- Added `.bw-fallback` HTML + CSS to `#booking-widget`: phone CTA shown when API is offline
- Prepended dark-theme CSS overrides to `booking-widget.css`
- Updated seed IDs in `index.html`
- Tagged and pushed v1.9.8
- Reverted `data-api-url` back to `http://localhost:3000` (v1.9.8 had incorrectly set it to VPS address)
- Tagged and pushed v1.9.9
- Updated all .md docs for v1.9.9

---

## Git Commits

| Hash | Message |
|---|---|
| `2975d62` | fix(booking): rebuild widget bundle, add offline fallback, restore VPS API URL |
| `78b9bde` | docs(release): v1.9.8 Widget Render — changelog and snapshot |
| `eaa2b40` | fix(booking): revert data-api-url to localhost:3000 for local dev |

---

## Git Tags

| Tag | Applied To |
|---|---|
| `v1.9.8__widget-render__commit-2975d62` | `78b9bde` (release commit) |
| `v1.9.9__dev-api-url__commit-eaa2b40` | docs commit (this release) |

---

## Files Changed

| File | Change |
|---|---|
| `index.html` | Fallback div, dark CSS, seed IDs, api-url revert |
| `assets/booking-widget.js` | Rebuilt (process.env fix, 154 kB) |
| `assets/booking-widget.css` | Rebuilt + dark theme overrides |
| `CHANGELOG.md` | v1.9.8 and v1.9.9 entries added |
| `RELEASE_NOTES.md` | v1.9.8 and v1.9.9 entries prepended |
| `releases/v1.9.8-2026-05-19-Widget-Render.md` | Created |
| `releases/v1.9.9-2026-05-19-Dev-API-URL.md` | Created |
| `ROADMAP.md` | v1.9.8 and v1.9.9 added to Completed |
| `PROGRESS_NOTE.md` | This file |
| `STATUS.md` | Updated to v1.9.9 |

---

## What's Next

1. Deploy booking-platform API to VPS (PM2 on port 3001)
   - Upload via WinSCP to /var/www/booking-api/: dist/, package.json, package-lock.json, prisma/schema.prisma, .env.production (rename to .env)
   - SSH: npm install --omit=dev → npx prisma generate → pm2 start dist/server.js --name booking-api
   - sudo ufw allow 3001/tcp
   - Verify: curl http://localhost:3001/health → {"status":"ok"}
2. Once API is on VPS: update index.html data-api-url to http://74.208.9.49:3001
3. Upload updated index.html to /var/www/jones-barbor-shop/
4. Test booking widget end-to-end on live site
