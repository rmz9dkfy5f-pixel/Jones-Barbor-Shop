# Context

Stable background for the Jones Barber Shop project.

## What This Project Is

A static single-page marketing and booking site for Jones Barber Shop, a community barbershop that has operated in the Joneswood District since 1998. The site presents real services, real barbers, and real shop culture to walk-in clients, regulars, and families.

## Stack

- Single HTML file: `index.html` (2,400+ lines — all CSS and JS embedded)
- No framework, no build step, no backend
- Vanilla HTML5 / CSS3 / JS with CSS custom properties
- Booking widget: UMD bundle (`assets/booking-widget.js`) from the `booking-platform` project
- Booking API: Fastify / TypeScript / Prisma / Neon PostgreSQL (separate repo: `booking-platform`)
- Hosting: IONOS VPS (74.208.9.49), Nginx, port 80
- Domain: jones-barbor-shop.craftandconscious.com
- Source control: GitHub (`rmz9dkfy5f-pixel/Jones-Barbor-Shop`)

## Key Design Constraints

- Dark theme: background `#050509` — do not introduce light mode
- 90s soul brand identity — do not genericize
- All placeholder content (phone, address, email, Pexels images) must be replaced with real data before production launch
- `index.html` is the single deployable entry point — do not split without an approved plan

## Canonical Docs

| File | Purpose |
|---|---|
| `CLAUDE.md` | Claude Code working rules |
| `ARCHITECTURE.md` | Stack, file layout, CSS variables |
| `docs/STRATEGY.md` | Business direction, audience, goals |
| `docs/DESIGN.md` | Visual system, color palette |
| `ROADMAP.md` | Planned and completed milestones |
| `CHANGELOG.md` | Version history |
| `RELEASE_NOTES.md` | GitHub-style release summaries |
| `STATUS.md` | Current project state (changes each session) |
