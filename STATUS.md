# Status

Last updated: 2026-05-19. Current version: v1.9.9.

## Live

- URL: jones-barbor-shop.craftandconscious.com
- Host: IONOS VPS (74.208.9.49), Nginx
- Entry: /var/www/jones-barbor-shop/index.html

## Where We Left Off

v1.9.9 — reverted `data-api-url` to `http://localhost:3000` for local dev (v1.9.8 had incorrectly set it to the VPS address, breaking the widget locally).

Before that: v1.9.8 fixed the booking widget UMD bundle (`process.env.NODE_ENV` crash), added offline fallback UI, applied dark-theme CSS overrides. The booking-platform API is NOT yet deployed to the VPS.

## What's Next

1. Deploy booking-platform API to VPS (PM2 on port 3001)
   - Upload via WinSCP to /var/www/booking-api/: dist/, package.json, package-lock.json, prisma/schema.prisma, .env.production (rename to .env)
   - SSH: npm install --omit=dev → npx prisma generate → pm2 start dist/server.js --name booking-api
   - sudo ufw allow 3001/tcp
   - Verify: curl http://localhost:3001/health → {"status":"ok"}
2. Upload updated index.html to /var/www/jones-barbor-shop/
3. Test booking widget end-to-end on live site

## Open Audit Items

- C-2: Contact info fictional (phone, address, email)
- H-1: Skip link permanently invisible (no :focus on .visually-hidden)
- H-2: No focus styles on nav/buttons
- H-5: ARCHITECTURE.md stale
- M-series: prefers-reduced-motion absent, missing ARIA roles

## Blocker

Booking API not deployed to VPS — widget will fail all API calls until PM2 is running on port 3001.
