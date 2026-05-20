# Status

Last updated: 2026-05-19. Current version: v1.9.8.

## Live

- URL: jones-barbor-shop.craftandconscious.com
- Host: IONOS VPS (74.208.9.49), Nginx
- Entry: /var/www/jones-barbor-shop/index.html

## Where We Left Off

v1.9.8 — booking widget rendering fixed. The UMD bundle was crashing silently in the browser (`ReferenceError: process is not defined`) because `process.env.NODE_ENV` was shipped as a live runtime reference. Fixed `widget/vite.config.ts` in booking-platform, rebuilt the bundle (154 kB, was 483 kB), added `.bw-fallback` offline CTA, applied dark-theme CSS overrides, restored `data-api-url` to VPS.

Before that: v1.9.7 added CONTEXT.md and STATUS.md. v1.9.6 corrected `data-api-url` to the deployed VPS address. The booking-platform API is NOT yet deployed to the VPS.

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
