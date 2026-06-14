# Status

Last updated: 2026-06-14. Current version: v1.14.0 + post-audit hygiene.

## Live

- URL: jones-barbor-shop.craftandconscious.com
- Host: IONOS VPS (74.208.9.49), Nginx
- Entry: /var/www/jones-barbor-shop/index.html

## Where We Left Off

Post-audit hygiene complete. Full site audit run after v3.3 Groups 1–4 install. Slices B–G executed: `.nojekyll` added, SVG favicon added, `docs/VERSIONING.md` updated to v1.14.0, `Documents/` marked as legacy archive, `REPO_HEALTH_CHECK.md` and `ROLLBACK_PLAN.md` refreshed, root working files updated. `data-api-url` is still `http://localhost:3000` — not yet pushed to VPS.

## What's Next

### Production Deployment (Pending)
1. Deploy booking-platform API to VPS (PM2 on port 3001)
2. Update `index.html` `data-api-url` to `http://74.208.9.49:3001`
3. Upload updated `index.html` + assets to `/var/www/jones-barbor-shop/`
4. Test booking widget end-to-end on live site

### Content (Before Launch)
- Replace placeholder phone, address, email with real shop data
- Replace Pexels images with real shop photography

## Open Audit Items

- C-2: Contact info fictional (phone, address, email)
- H-1: Skip link permanently invisible (no :focus on .visually-hidden)
- H-2: No focus styles on nav/buttons
- H-5: ARCHITECTURE.md stale
- M-series: prefers-reduced-motion absent, missing ARIA roles

## Blocker

Booking API not deployed to VPS — widget will fail all API calls until PM2 is running on port 3001.
