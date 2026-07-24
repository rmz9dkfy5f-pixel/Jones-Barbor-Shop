# Status

Last updated: 2026-07-24. Current version: v1.15.3.

v1.15.2 backfilled two missing rows (v1.15.0, v1.15.1) in `docs/VERSIONING.md`'s release history
table. v1.15.3 corrects a real documentation-vs-reality gap: the booking API's process manager was
documented as systemd but has actually run under PM2 since 2026-06-16. Both are workflow/docs
corrections — no site, code, or runtime behavior change; no deployment or restart was performed.

## Live

- URL: jones-barbor-shop.craftandconscious.com
- Host: IONOS VPS (74.208.9.49), Nginx + HTTPS (Let's Encrypt)
- Entry: /var/www/jones-barbor-shop/index.html
- Booking API: https://jones-barbor-shop.craftandconscious.com/api (nginx `/api/` proxy → port 3001)

## Where We Left Off

HTTPS booking platform integration complete. Booking platform deployed to VPS, running as a PM2
process (`booking-platform`, cluster mode, port 3001) — **corrected 2026-07-24: this had been
documented as a systemd service, but `booking-platform.service` has actually been inactive since
2026-06-16, the same day the real process was migrated to PM2; this file, `CONTEXT.md`, and this
repo's first-drafted `docs/governance/REPOSITORY_HANDOFF_CONFIG.md` all still said systemd until
verified and fixed today.** Nginx reverse-proxies `/api/` to the backend; TLS via Let's Encrypt. Widget assets (`assets/booking-widget.js`, `assets/booking-widget.css`) deployed to static root. `index.html` `data-api-url` updated to `https://jones-barbor-shop.craftandconscious.com/api`. Widget loads and displays services and availability. Health check confirmed `{"status":"ok"}` at `/api/health` (not bare `/api`, which 404s).

Payments deferred — no Stripe/Resend/Twilio keys in production `.env`. Services are priced ($20–$65); checkout will fail until Stripe keys are added.

v1.15.1 adds a refined push/snapshot/tag workflow prompt under `prompts/` — workflow tooling only, no change to the live site, code, or runtime behavior. v1.15.2 backfilled the versioning table; v1.15.3 corrects this systemd→PM2 documentation gap.

## What's Next

### Payments (When Ready)
- Add `STRIPE_SECRET_KEY`, `STRIPE_WEBHOOK_SECRET`, `STRIPE_SUCCESS_URL`, `STRIPE_CANCEL_URL` to `/srv/booking-platform/.env` on VPS
- `pm2 restart booking-platform` (not `systemctl restart` — see correction above)
- Test end-to-end checkout

### Notifications (When Ready)
- Add `RESEND_API_KEY`, `RESEND_FROM`, `TWILIO_*` to `/srv/booking-platform/.env`
- `pm2 restart booking-platform` (not `systemctl restart` — see correction above)

### Content (Before Launch)
- Replace placeholder phone, address, email with real shop data
- Replace Pexels images with real shop photography

## Open Audit Items

- C-2: Contact info fictional (phone, address, email)
- H-1: Skip link permanently invisible (no :focus on .visually-hidden)
- H-2: No focus styles on nav/buttons
- H-5: ARCHITECTURE.md stale
- M-series: prefers-reduced-motion absent, missing ARIA roles

## Blockers

None. Booking widget is live and functional. Payment step will fail until Stripe keys are added.
