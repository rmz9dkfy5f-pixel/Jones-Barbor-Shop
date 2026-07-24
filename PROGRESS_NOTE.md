# Progress Note

Session ended 2026-07-24. Covered v1.15.2 — backfilled missing rows in the version history table.

---

## Milestone

**v1.15.2 Versioning Table Sync.** `docs/VERSIONING.md`'s release history table stopped at v1.14.0
despite the repo being at v1.15.1; backfilled the two missing rows (v1.15.0, v1.15.1) using the
real commit/tag data already recorded in `CHANGELOG.md` and git tags. Also added
`docs/governance/REPOSITORY_HANDOFF_CONFIG.md`. Workflow/docs only; the live site, code, and
runtime behavior are unchanged. No deployment occurred.

Work commits: `f674697`, `b770fb2`. Tag: `v1.15.2__versioning-table-sync__commit-b770fb2`
(applied at final HEAD).

---

## Previous Milestone (v1.15.1)

**Snapshot Naming Prompt.** Added a refined repo push/handoff/snapshot/tag workflow prompt under
`prompts/` — strict descriptive snapshot-folder naming and a mandatory RepoBackups path confirmation
step. Workflow tooling only; the live site, code, and runtime behavior were unchanged from v1.15.0
(HTTPS booking platform integration).

Work commit: `ee6d64b`. Tag: `v1.15.1__snapshot-naming-prompt__commit-ee6d64b`.

---

## Tasks Completed

- Deployed booking platform to VPS at `/srv/booking-platform/` (rsync of source + local build)
- Created systemd service `booking-platform.service` (port 3001, matches existing `spa.service` pattern)
- Provisioned local PostgreSQL database (`booking_platform` user + DB), ran migrations, seeded data
- Configured Let's Encrypt TLS; nginx `/api/` reverse proxy block added to site config
- Deployed `assets/booking-widget.js` and `assets/booking-widget.css` to `/var/www/jones-barbor-shop/assets/`
- Updated `index.html`: `data-api-url` → HTTPS production URL, seed IDs updated
- Confirmed widget loads and shows services/availability; health check passes
- Payments deferred (no Stripe/Resend/Twilio keys yet)

---

## Git Commits

| Hash | Message |
|---|---|
| `1394ef5` | deploy: connect website to HTTPS booking platform |

---

## Files Changed

| File | Change |
|---|---|
| `index.html` | `data-api-url`, `data-service-id`, `data-location-id` updated to production values |

---

## What's Next

1. Add Stripe keys to `/srv/booking-platform/.env` when ready; restart service
2. Add Resend/Twilio keys when ready; restart service
3. Replace placeholder content (phone, address, barber info, photos)
