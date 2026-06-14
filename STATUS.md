# Status

Last updated: 2026-06-14. Current version: v1.14.0.

## Live

- URL: jones-barbor-shop.craftandconscious.com
- Host: IONOS VPS (74.208.9.49), Nginx
- Entry: /var/www/jones-barbor-shop/index.html

## Where We Left Off

v1.14.0 Sub Agents — Project Starter Kit v3.3 migration complete. 7 Claude Code sub-agent definition files installed in `.claude/agents/`: repo-cartographer, project-steward, slice-planner, debugger, test-verifier, security-reviewer, docs-promoter. No existing files were modified. `data-api-url` is still `http://localhost:3000` for local dev.

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
