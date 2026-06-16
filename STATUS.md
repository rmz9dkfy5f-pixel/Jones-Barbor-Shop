# Status

Last updated: 2026-06-16. Current version: v1.15.0.

## Live

- URL: jones-barbor-shop.craftandconscious.com
- Host: IONOS VPS (74.208.9.49), Nginx + HTTPS (Let's Encrypt)
- Entry: /var/www/jones-barbor-shop/index.html
- Booking API: https://jones-barbor-shop.craftandconscious.com/api (nginx `/api/` proxy → port 3001)

## Where We Left Off

HTTPS booking platform integration complete. Booking platform deployed to VPS via systemd (`booking-platform.service`, port 3001). Nginx reverse-proxies `/api/` to the backend; TLS via Let's Encrypt. Widget assets (`assets/booking-widget.js`, `assets/booking-widget.css`) deployed to static root. `index.html` `data-api-url` updated to `https://jones-barbor-shop.craftandconscious.com/api`. Widget loads and displays services and availability. Health check confirmed `{"status":"ok"}`.

Payments deferred — no Stripe/Resend/Twilio keys in production `.env`. Services are priced ($20–$65); checkout will fail until Stripe keys are added.

## What's Next

### Payments (When Ready)
- Add `STRIPE_SECRET_KEY`, `STRIPE_WEBHOOK_SECRET`, `STRIPE_SUCCESS_URL`, `STRIPE_CANCEL_URL` to `/srv/booking-platform/.env` on VPS
- `systemctl restart booking-platform`
- Test end-to-end checkout

### Notifications (When Ready)
- Add `RESEND_API_KEY`, `RESEND_FROM`, `TWILIO_*` to `/srv/booking-platform/.env`
- `systemctl restart booking-platform`

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
