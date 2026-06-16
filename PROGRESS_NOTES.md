# Progress Notes

Historical project progress notes.

Current active progress belongs in `PROGRESS_NOTE.md`.

When a progress note is complete, copy it here with a date.

---

## Entry Template

### YYYY-MM-DD — Progress Summary

Phase:

```text
[Phase]
```

Completed:

- [Item]

Blocked:

- [Item]

Checks run:

```bash
# commands
```

Commit:

```text
<commit hash>
```

Next action:

> [Next action]

---

## Notes

### 2026-06-16 — v1.15.0 HTTPS Booking Platform Integration

Phase:

```text
Phase 3 — Production deployment
```

Completed:

- Deployed booking platform to VPS at `/srv/booking-platform/` via rsync + local build
- Created systemd unit `booking-platform.service` on port 3001
- Provisioned local PostgreSQL, ran migrations, seeded 7 services and 4 staff
- Configured Let's Encrypt TLS; nginx `/api/` reverse proxy added to site vhost
- Deployed `assets/booking-widget.js` and `assets/booking-widget.css` to VPS static root
- Updated `index.html` `data-api-url` to `https://jones-barbor-shop.craftandconscious.com/api`
- Updated widget `data-service-id` and `data-location-id` to seeded production IDs
- Confirmed widget loads; health check `{"status":"ok"}` over HTTPS
- Payments deferred — no Stripe/Resend/Twilio keys in `.env`

Blocked:

- Stripe/Resend/Twilio keys not yet available; checkout step will fail

Commit:

```text
1394ef5 deploy: connect website to HTTPS booking platform
```

Next action:

> Add Stripe keys to `/srv/booking-platform/.env` when ready; restart service. Then add Resend/Twilio. Replace placeholder content last.

---

### 2026-06-14 — v1.14.0 Sub Agents + Post-Audit Hygiene

Phase:

```text
Phase 2 — v3.3 migration complete; post-audit hygiene slices B–F
```

Completed:

- Installed Group 4 sub-agent roster (7 `.claude/agents/` files) — v1.14.0
- v3.3 migration 100% complete (Groups 1–4)
- Site audit: confirmed git tracks images as `pics/` (no 404); added `.nojekyll`; added SVG favicon; updated `docs/VERSIONING.md` release history to v1.14.0; marked `Documents/` as legacy archive; refreshed `REPO_HEALTH_CHECK.md` and `ROLLBACK_PLAN.md`
- Updated `PLAN.md`, `PROGRESS_NOTE.md`, `STATUS.md` to post-audit state

Blocked:

- Booking API not yet deployed to VPS

Commit:

```text
9341635 chore: install v3.3 sub-agent roster — Group 4
dee44af chore: add .nojekyll to disable Jekyll on GitHub Pages
ad8241c feat: add SVG favicon — scissors icon, gold on dark background
c1f4ae8 docs: update VERSIONING.md release history to v1.14.0
b7ef9d8 docs: mark Documents/ as legacy archive with README
487d01b docs: refresh REPO_HEALTH_CHECK and ROLLBACK_PLAN to post-audit state
```

Next action:

> Deploy booking-platform API to VPS (PM2 on port 3001); update `data-api-url` in `index.html`.

---

### 2026-05-20 — v1.10.0 Three Step

Phase:

```text
Phase 2 — Implementation
```

Completed:

- Redesigned booking widget to 3-step flow: customer info → service/barber selection → slots + notes
- Added `/catalog/options?locationId=X` API endpoint integration
- 12-hour AM/PM time format on slot grid
- Gold/cream dark theme for widget
- Fixed step indicator misalignment
- Tagged and pushed v1.10.0

Blocked:

- Booking API not yet deployed to VPS

Commit:

```text
67a1a19 fix(booking): 12-hr time format, gold/cream theme, step indicator alignment
17a9246 feat(booking): update widget bundle — 3-step form redesign
```

Next action:

> Deploy booking-platform API to VPS on port 3001.

---

### 2026-06-14 — v1.11.0 Quality Gates + v3.3 Migration Start

Phase:

```text
Phase 2 — Implementation (v3.3 migration)
```

Completed:

- Cleared ENOSPC disk space issue
- Installed Group 1 quality gate layer (6 files)
- Updated all root tracking/handoff docs
- Committed project-starter-kit-v3.3 source (106 files)
- Fixed RELEASE_NOTES.md (v1.11.1 entry missing)
- Took local snapshot to RepoBackups
- Started Group 2 install (10 root tracking files)

Blocked:

- Booking API not yet deployed to VPS

Commit:

```text
c047563 chore: install v3.3 quality gate layer
999a753 docs(state): sync all tracking docs to v1.11.0
7cab694 chore: commit project starter kit v3.3 source and update prompts
62e2305 docs(release): v1.11.1 State Sync — add to RELEASE_NOTES
```

Next action:

> Complete Group 2 install, then proceed to Group 3 (ai/ folder system).
