# Context

Stable background for the Jones Barber Shop project.

## What This Project Is

A static single-page marketing and booking site for Jones Barber Shop, a community barbershop that has operated in the Joneswood District since 1998. The site presents real services, real barbers, and real shop culture to walk-in clients, regulars, and families.

## Stack

- Single HTML file: `index.html` (2,400+ lines — all CSS and JS embedded, plus inline `<style>` block for booking widget dark theme overrides)
- No framework, no build step, no backend
- Vanilla HTML5 / CSS3 / JS with CSS custom properties
- Booking widget: UMD bundle (`assets/booking-widget.js`) from the `booking-platform` project — production-safe build with `process.env.NODE_ENV` inlined at build time
- Booking API: Fastify / TypeScript / Prisma / local PostgreSQL on VPS (separate repo: `booking-platform`); live at `https://jones-barbor-shop.craftandconscious.com/api`
- Hosting: IONOS VPS (74.208.9.49), Nginx + HTTPS (Let's Encrypt); nginx proxies `/api/` to `http://127.0.0.1:3001/`; booking platform runs as systemd `booking-platform.service`
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
| `DONE_CRITERIA.md` | Definition of done for every slice type |
| `CHANGE_CONTROL.md` | What AI agents may edit freely vs. requires approval |
| `REPO_HEALTH_CHECK.md` | Baseline repo health snapshot |
| `ROLLBACK_PLAN.md` | Rollback procedures for risky changes |
| `PROJECT_RISK_REGISTER.md` | Open and closed risk log |
| `ai/agents/AGENT_REVIEW_GATES.md` | Mandatory agent gate rules by change type |
