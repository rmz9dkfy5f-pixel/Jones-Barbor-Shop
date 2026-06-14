# Status

Last updated: 2026-06-14. Current version: v1.13.0.

## Live

- URL: jones-barbor-shop.craftandconscious.com
- Host: IONOS VPS (74.208.9.49), Nginx
- Entry: /var/www/jones-barbor-shop/index.html

## Where We Left Off

v1.13.0 AI System — Project Starter Kit v3.3 Group 3 installed. 20 files added to the ai/ folder: README, config, 3 agent support docs, 8 folder placeholders, and 7 session/checkpoint/prompt/pattern templates. No existing files were modified. `data-api-url` is still `http://localhost:3000` for local dev.

## What's Next

### v3.3 Migration (Final Group)
- Group 4 — `.claude/agents/` sub-agent roster: `repo-cartographer.md`, `project-steward.md`, `slice-planner.md`, `debugger.md`, `test-verifier.md`, `security-reviewer.md`, `docs-promoter.md`

### Production Deployment (Pending)
1. Deploy booking-platform API to VPS (PM2 on port 3001)
2. Update `index.html` `data-api-url` to `http://74.208.9.49:3001`
3. Upload updated `index.html` + assets to `/var/www/jones-barbor-shop/`
4. Test booking widget end-to-end on live site

## Open Audit Items

- C-2: Contact info fictional (phone, address, email)
- H-1: Skip link permanently invisible (no :focus on .visually-hidden)
- H-2: No focus styles on nav/buttons
- H-5: ARCHITECTURE.md stale
- M-series: prefers-reduced-motion absent, missing ARIA roles

## Blocker

Booking API not deployed to VPS — widget will fail all API calls until PM2 is running on port 3001.
