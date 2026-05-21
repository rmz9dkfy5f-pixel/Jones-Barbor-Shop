# Status

Last updated: 2026-05-20. Current version: v1.10.0.

## Live

- URL: jones-barbor-shop.craftandconscious.com
- Host: IONOS VPS (74.208.9.49), Nginx
- Entry: /var/www/jones-barbor-shop/index.html

## Where We Left Off

v1.10.0 Three Step — booking widget redesigned to a 3-step flow: (1) customer info, (2) service + preferred barber dropdowns loaded live from the API, (3) available time slots with 12-hour AM/PM format + notes. Dark theme updated to gold labels and warm cream text. Step indicator alignment fixed. `data-api-url` is still `http://localhost:3000` for local dev.

## What's Next

1. Deploy booking-platform API to VPS (PM2 on port 3001)
   - Upload via WinSCP to /var/www/booking-api/: dist/, package.json, package-lock.json, prisma/schema.prisma, .env.production (rename to .env)
   - SSH: npm install --omit=dev → npx prisma generate → pm2 start dist/server.js --name booking-api
   - sudo ufw allow 3001/tcp
   - Verify: curl http://localhost:3001/health → {"status":"ok"}
2. Update index.html `data-api-url` to `http://74.208.9.49:3001` for production
3. Upload updated index.html to /var/www/jones-barbor-shop/
4. Test booking widget end-to-end on live site

## Open Audit Items

- C-2: Contact info fictional (phone, address, email)
- H-1: Skip link permanently invisible (no :focus on .visually-hidden)
- H-2: No focus styles on nav/buttons
- H-5: ARCHITECTURE.md stale
- M-series: prefers-reduced-motion absent, missing ARIA roles

## Blocker

Booking API not deployed to VPS — widget will fail all API calls until PM2 is running on port 3001.
