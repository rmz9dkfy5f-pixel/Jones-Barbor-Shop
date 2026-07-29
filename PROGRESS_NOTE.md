# Progress Note

Session ended 2026-07-29. Covered v1.15.4 — added the mandatory model-selection gate.

---

## Milestone

**v1.15.4 Model Selection Gate.** Added `MODEL_SELECTION_GATE.md` and
`PROMPT_MODEL_SELECTION_GATE.md`, wired the required brief into `AGENTS.md` and `CLAUDE.md`, and
added a model usage record section to `ai/agents/AGENT_HANDOFF_TEMPLATE.md`. Governance/docs only —
no site, code, deployment, or runtime behavior change.

Work commit: `b915062`. Tag: `v1.15.4__model-selection-gate__commit-b915062`.

---

## Previous Milestone (v1.15.3)

**v1.15.3 PM2 Docs Correction.** `STATUS.md`, `CONTEXT.md`, `ROLLBACK_PLAN.md`,
`docs/DEPLOYMENT.md`, and `docs/governance/REPOSITORY_HANDOFF_CONFIG.md` all documented the booking
API as running under systemd. Verified via read-only checks on the live VPS (health check
`/api/health` → `{"status":"ok"}`; `systemctl status booking-platform` → inactive since 2026-06-16;
`pm2 describe booking-platform` → online, id 0, cluster mode) that the real process has run under
PM2 since the same day it was documented as systemd. Corrected every command and reference,
including the safety-critical `ROLLBACK_PLAN.md`. Docs-only — no restart, deploy, or config change
performed on the VPS.

Work commit: `42b3b77`. Tag: `v1.15.3__pm2-docs-correction__commit-42b3b77`.

---

**Versioning Table Sync.** `docs/VERSIONING.md`'s release history table stopped at v1.14.0 despite
the repo being at v1.15.1; backfilled the two missing rows (v1.15.0, v1.15.1) using the real
commit/tag data already recorded in `CHANGELOG.md` and git tags. Also added
`docs/governance/REPOSITORY_HANDOFF_CONFIG.md`. Workflow/docs only; the live site, code, and
runtime behavior were unchanged. No deployment occurred.

Work commits: `f674697`, `b770fb2`. Tag: `v1.15.2__versioning-table-sync__commit-b770fb2`.

---

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

1. Add Stripe keys to `/srv/booking-platform/.env` when ready; `pm2 restart booking-platform`
2. Add Resend/Twilio keys when ready; `pm2 restart booking-platform`
3. Replace placeholder content (phone, address, barber info, photos)
