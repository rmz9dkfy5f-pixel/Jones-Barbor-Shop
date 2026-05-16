# Progress Note

Session ended 2026-05-15. Covered v1.9.4 – v1.9.6.

---

## Milestone

**v1.9.4 – v1.9.6** — docs catch-up, prompt vault, and booking widget API URL fix.

---

## Tasks Completed

- Updated ROADMAP.md: added Completed section, removed resolved Active/Planned items
- Created COMMIT_NOTES.md documenting commit convention and tag format
- Created PROGRESS_NOTE.md (placeholder, now replaced with this session-end version)
- Updated CHANGELOG.md with v1.9.4, v1.9.5, and v1.9.6 entries and diff links
- Created release snapshots for v1.9.4, v1.9.5, and v1.9.6 in releases/
- Tagged and pushed v1.9.4, v1.9.5, and v1.9.6 to GitHub
- Committed four prompt template files (prompts/) as v1.9.5 Prompt Vault
- Created repo backup snapshot at E:\Projects\RepoBackups\Jones-Barbor-Shop\v1.9.4__open-record__commit-2039482
- Diagnosed booking widget failure: data-api-url was pointing to http://localhost:3000 (dev server never deployed)
- Built booking-platform Fastify API locally (npm run build → dist/)
- Created .env.production for VPS deployment (NODE_ENV=production, PORT=3001, Neon DATABASE_URL, CORS_ORIGIN=*)
- Fixed index.html: data-api-url updated from http://localhost:3000 to http://74.208.9.49:3001

---

## Git Commits

| Hash | Message |
|---|---|
| `2039482` | docs: open record — update roadmap, add commit notes and progress note |
| `2798649` | docs(release): v1.9.4 Open Record — changelog and snapshot |
| `dfedf5d` | docs(prompts): add prompt vault — commit notes, snapshot, update, and backend data model templates |
| `2875301` | docs(release): v1.9.5 Prompt Vault — changelog and snapshot |
| `0fbc068` | fix(booking): point widget data-api-url to deployed VPS API |
| `e5fa0b3` | docs(release): v1.9.6 Fix API URL — changelog and snapshot |

---

## Git Tags

| Tag | Applied To |
|---|---|
| `v1.9.4__open-record__commit-2039482` | `2798649` (release commit) |
| `v1.9.5__prompt-vault__commit-dfedf5d` | `2875301` (release commit) |
| `v1.9.6__fix-api-url__commit-0fbc068` | `e5fa0b3` (release commit) |

---

## Files Changed

| File | Change |
|---|---|
| `ROADMAP.md` | Updated |
| `COMMIT_NOTES.md` | Created |
| `PROGRESS_NOTE.md` | Created |
| `CHANGELOG.md` | Updated |
| `releases/v1.9.4-2026-05-14-Open-Record.md` | Created |
| `prompts/Commit notes` | Created |
| `prompts/Snapshot` | Created |
| `prompts/Update.md` | Created |
| `prompts/FIRST_PROMPT_BACKEND_DATA_MODEL.md` | Created |
| `releases/v1.9.5-2026-05-14-Prompt-Vault.md` | Created |
| `index.html` | Fixed |
| `releases/v1.9.6-2026-05-15-Fix-API-URL.md` | Created |

---

## What's Next

**Next milestone: v1.9.7 — Live Booking Widget**

Deploy the booking-platform Fastify API to the IONOS VPS so the widget functions end-to-end on jones-barbor-shop.craftandconscious.com.

**Steps remaining:**
1. Upload via WinSCP to /var/www/booking-api/: dist/, package.json, package-lock.json, prisma/schema.prisma, .env.production (rename to .env)
2. SSH: npm install --omit=dev → npx prisma generate → pm2 start dist/server.js --name booking-api
3. Open port 3001: sudo ufw allow 3001/tcp
4. Verify: curl http://localhost:3001/health → {"status":"ok"}
5. Upload updated index.html to /var/www/jones-barbor-shop/
6. Test widget on live site

**Blocker:** API not yet deployed to VPS — widget will 404 on all API calls until Steps 1–5 are complete.
