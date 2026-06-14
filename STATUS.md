# Status

Last updated: 2026-06-14. Current version: v1.11.0.

## Live

- URL: jones-barbor-shop.craftandconscious.com
- Host: IONOS VPS (74.208.9.49), Nginx
- Entry: /var/www/jones-barbor-shop/index.html

## Where We Left Off

v1.11.0 Quality Gates — Project Starter Kit v3.3 Group 1 installed. Six quality gate files added to the repo root and `ai/agents/`: `DONE_CRITERIA.md`, `CHANGE_CONTROL.md`, `REPO_HEALTH_CHECK.md`, `ROLLBACK_PLAN.md`, `PROJECT_RISK_REGISTER.md`, `ai/agents/AGENT_REVIEW_GATES.md`. No existing files were modified. `data-api-url` is still `http://localhost:3000` for local dev.

## What's Next

### v3.3 Migration (In Progress)
- Group 2 — 10 root tracking files: `START_HERE.md`, `PROJECT_BRIEF.md`, `PLAN.md`, `PHASE_GATES.md`, `BACKLOG.md`, `SLICE_REVIEWS.md`, `LESSONS_LEARNED.md`, `AGENTS.md`, `PROGRESS_NOTES.md`, `DECISION_LOG.md`
- Group 3 — `ai/` folder system: `ai/README.md`, `ai/ai.config.json`, `ai/sessions/`, `ai/checkpoints/`, `ai/prompts/`, `ai/patterns/`, `ai/reports/`
- Group 4 — `.claude/agents/` sub-agent roster: `repo-cartographer`, `project-steward`, `slice-planner`, `debugger`, `test-verifier`, `security-reviewer`, `docs-promoter`

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
