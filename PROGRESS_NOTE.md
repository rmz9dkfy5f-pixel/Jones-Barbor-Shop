# Progress Note

Session ended 2026-05-19. Covered v1.9.8.

---

## Milestone

**v1.9.8** — Booking widget rendering fixed.

---

## Tasks Completed

- Diagnosed blank booking section: widget div was empty, fallback text not showing
- Found root cause: `booking-widget.js` UMD bundle shipped `process.env.NODE_ENV` as a live runtime reference — browsers have no `process` global, causing silent `ReferenceError` before React initialised
- Fixed `widget/vite.config.ts` in booking-platform repo: added `define: { 'process.env.NODE_ENV': '"production"' }`
- Rebuilt widget: bundle reduced from 483 kB to 154 kB (dev React excluded), `process.env` count = 0
- Added `.bw-fallback` HTML + CSS to `#booking-widget`: shows "Online booking is loading… call (919) 555-1234 or walk in" when API is unreachable instead of a blank box
- Prepended dark-theme CSS overrides to `booking-widget.css`: slots, inputs, loading state, error state now visible on `#12121e` surface
- Seeded local database (`npx prisma db seed` in booking-platform)
- Added `JWT_SECRET` to booking-platform `.env`
- Started local dev server (`npm run dev` on port 3000) for local widget testing
- Restored `data-api-url` to `http://74.208.9.49:3001` before production commit
- Updated `data-service-id` and `data-location-id` to current seed values
- Tagged and pushed v1.9.8 to GitHub
- Tagged and pushed Booking Platform v0.10.20 (vite.config.ts fix)
- Created repo snapshots for both repos

---

## Git Commits

| Hash | Message |
|---|---|
| `2975d62` | fix(booking): rebuild widget bundle, add offline fallback, restore VPS API URL |

---

## Git Tags

| Tag | Applied To |
|---|---|
| `v1.9.8__widget-render__commit-2975d62` | docs commit (release notes) |

---

## Files Changed

| File | Change |
|---|---|
| `index.html` | Fallback div added, dark CSS added, API URL restored, seed IDs updated |
| `assets/booking-widget.js` | Rebuilt (process.env fix, 154 kB) |
| `assets/booking-widget.css` | Rebuilt + dark theme overrides prepended |
| `CHANGELOG.md` | v1.9.8 entry added |
| `RELEASE_NOTES.md` | v1.9.8 entry prepended |
| `releases/v1.9.8-2026-05-19-Widget-Render.md` | Created |
| `ROADMAP.md` | v1.9.8 added to Completed |
| `PROGRESS_NOTE.md` | This file |
| `CONTEXT.md` | Widget note updated |
| `STATUS.md` | Updated to v1.9.8 |

---

## What's Next

1. Deploy booking-platform API to VPS (PM2 on port 3001)
   - Upload via WinSCP to /var/www/booking-api/: dist/, package.json, package-lock.json, prisma/schema.prisma, .env.production (rename to .env)
   - SSH: npm install --omit=dev → npx prisma generate → pm2 start dist/server.js --name booking-api
   - sudo ufw allow 3001/tcp
   - Verify: curl http://localhost:3001/health → {"status":"ok"}
2. Upload updated index.html to /var/www/jones-barbor-shop/
3. Test booking widget end-to-end on live site
