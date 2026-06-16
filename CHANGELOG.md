# Changelog

All notable changes to this project will be documented in this file.
Format based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) and [Semantic Versioning](https://semver.org/).

---

## [Unreleased]

---

## [1.15.0] — 2026-06-16

### Changed
- `index.html` — `data-api-url` changed from `http://localhost:3000` to `https://jones-barbor-shop.craftandconscious.com/api` (production HTTPS endpoint)
- `index.html` — `data-service-id` updated to `cmqejj538000412vsed526d5u` (seeded production ID)
- `index.html` — `data-location-id` updated to `cmqejj534000212vsf1pmccpy` (seeded production ID)

### Added
- HTTPS booking API live: Let's Encrypt TLS, nginx `/api/` reverse proxy, systemd `booking-platform.service` on port 3001
- `assets/booking-widget.js` and `assets/booking-widget.css` deployed to VPS static root

### Tag / Snapshot
`v1.15.0__https-booking-platform__commit-91d81a0`

---

## [1.14.0] — 2026-06-14

### Added
- `.claude/agents/repo-cartographer.md` — repo structure mapper, read-only ([`9341635`](../../commit/9341635))
- `.claude/agents/project-steward.md` — source-of-truth alignment checker, read-only ([`9341635`](../../commit/9341635))
- `.claude/agents/slice-planner.md` — vertical slice planner, read-only ([`9341635`](../../commit/9341635))
- `.claude/agents/debugger.md` — single-bug investigator, minimal fix ([`9341635`](../../commit/9341635))
- `.claude/agents/test-verifier.md` — safe verification runner, pass/fail reporter ([`9341635`](../../commit/9341635))
- `.claude/agents/security-reviewer.md` — security risk reviewer, read-only ([`9341635`](../../commit/9341635))
- `.claude/agents/docs-promoter.md` — session-to-docs promotion advisor, read-only ([`9341635`](../../commit/9341635))

### Tag / Snapshot
`v1.14.0__sub-agents__commit-9341635`

---

## [1.13.0] — 2026-06-14

### Added
- `ai/README.md` — AI engineering memory folder guide ([`c0164b3`](../../commit/c0164b3))
- `ai/ai.config.json` — AI memory config: paths, rules, version ([`c0164b3`](../../commit/c0164b3))
- `ai/agents/AGENT_HANDOFF_TEMPLATE.md` — sub-agent invocation template ([`c0164b3`](../../commit/c0164b3))
- `ai/agents/AGENT_ROSTER.md` — available agents and when to use them ([`c0164b3`](../../commit/c0164b3))
- `ai/agents/AGENT_USAGE_RULES.md` — agent guardrails, workflow, hard limits ([`c0164b3`](../../commit/c0164b3))
- `ai/checkpoints/`, `ai/patterns/`, `ai/prompts/`, `ai/reports/` — folder placeholders ([`c0164b3`](../../commit/c0164b3))
- `ai/sessions/debug/`, `ai/sessions/designs/`, `ai/sessions/features/`, `ai/sessions/optimization/` — session folder placeholders ([`c0164b3`](../../commit/c0164b3))
- `ai/templates/` — 7 session templates: ai_prompt, api_design, checkpoint, debug, design, feature, pattern ([`c0164b3`](../../commit/c0164b3))

### Tag / Snapshot
`v1.13.0__ai-system__commit-c0164b3`

---

## [1.12.0] — 2026-06-14

### Added
- `START_HERE.md` — unified project starter kit orientation and workflow guide ([`10a5f0a`](../../commit/10a5f0a))
- `PROJECT_BRIEF.md` — project goal, users, core action, success criteria, risks ([`10a5f0a`](../../commit/10a5f0a))
- `PLAN.md` — active project plan and current vertical slice ([`10a5f0a`](../../commit/10a5f0a))
- `PHASE_GATES.md` — phase gate status (Gates 1–4 complete, Gate 5 in progress) ([`10a5f0a`](../../commit/10a5f0a))
- `BACKLOG.md` — work queue: Build Now / Build Next / Build Later / Maybe / Do Not Build ([`10a5f0a`](../../commit/10a5f0a))
- `SLICE_REVIEWS.md` — post-slice review log; seeded with Group 1 review ([`10a5f0a`](../../commit/10a5f0a))
- `LESSONS_LEARNED.md` — lessons log; seeded with 3 lessons from this session ([`10a5f0a`](../../commit/10a5f0a))
- `AGENTS.md` — agent instructions, commit rules, sub-agent workflow, quality gate rules ([`10a5f0a`](../../commit/10a5f0a))
- `PROGRESS_NOTES.md` — historical progress log; seeded with v1.10.0 and v1.11.0 entries ([`10a5f0a`](../../commit/10a5f0a))
- `DECISION_LOG.md` — key decisions log; seeded with 4 active decisions ([`10a5f0a`](../../commit/10a5f0a))

### Tag / Snapshot
`v1.12.0__root-tracking__commit-10a5f0a`

---

## [1.11.0] — 2026-06-14

### Added
- `DONE_CRITERIA.md` — defines done criteria for every slice type (feature, debug, design, migration) ([`c047563`](../../commit/c047563))
- `CHANGE_CONTROL.md` — defines what AI agents may edit freely, what requires approval, and what is never automatic ([`c047563`](../../commit/c047563))
- `REPO_HEALTH_CHECK.md` — baseline snapshot of repo stack, important files, risks, and verification status ([`c047563`](../../commit/c047563))
- `ROLLBACK_PLAN.md` — escape path template for migrations and risky changes ([`c047563`](../../commit/c047563))
- `PROJECT_RISK_REGISTER.md` — open and closed risk log, seeded with known Jones Barber Shop risks ([`c047563`](../../commit/c047563))
- `ai/agents/AGENT_REVIEW_GATES.md` — mandatory gate rules for sub-agent invocation by change type ([`c047563`](../../commit/c047563))

### Tag / Snapshot
`v1.11.0__quality-gates__commit-c047563`

---

## [1.10.0] — 2026-05-20

### Added
- `assets/booking-widget.js` — booking widget redesigned to 3-step flow: (1) customer info, (2) service + preferred barber dropdowns loaded live from API, (3) available time slots + notes ([`17a9246`](../../commit/17a9246))
- `assets/booking-widget.js` — new `GET /catalog/options?locationId=X` API endpoint integration; services and barbers are fetched dynamically, not hardcoded ([`17a9246`](../../commit/17a9246))
- `assets/booking-widget.js` — 12-hour AM/PM time format on slot grid (e.g. "9:00 AM", "2:30 PM") ([`67a1a19`](../../commit/67a1a19))

### Changed
- `assets/booking-widget.css` — dark theme color scheme: gold labels (`#f5b544`), warm cream text (`#f0ede4`), gold-tinted borders; overrides moved to end of file so cascade order is correct ([`67a1a19`](../../commit/67a1a19))
- `index.html` — booking widget `<style>` block: `#booking-widget { padding: 0 }` removes redundant outer padding; `.bw-root { border: none }` removes nested inner border (`.form-card` provides the outer border); `select` and `option` elements styled for dark theme ([`67a1a19`](../../commit/67a1a19))

### Fixed
- `index.html` — step indicator misalignment: `line-height: 1` corrects Space Grotesk vertical offset inside dot circles; `align-self: center` anchors the 2px connecting line in the flex row ([`67a1a19`](../../commit/67a1a19))

### Tag / Snapshot
`v1.10.0__three-step__commit-67a1a19`

---

## [1.9.9] — 2026-05-19

### Fixed
- `index.html` — reverted `data-api-url` to `http://localhost:3000` for local dev; previous release (`v1.9.8`) incorrectly set it to the VPS address ([`eaa2b40`](../../commit/eaa2b40))

### Tag / Snapshot
`v1.9.9__dev-api-url__commit-eaa2b40`

---

## [1.9.8] — 2026-05-19

### Fixed
- `assets/booking-widget.js` — rebuilt with `process.env.NODE_ENV` replaced at build time; widget no longer crashes silently in browser ([`2975d62`](../../commit/2975d62))
- `assets/booking-widget.css` — rebuilt from latest source; dark-theme overrides prepended so widget UI is visible on `#12121e` surface ([`2975d62`](../../commit/2975d62))
- `index.html` — `data-api-url` restored to `http://74.208.9.49:3001`; seed IDs updated to current database values ([`2975d62`](../../commit/2975d62))

### Added
- `index.html` — `.bw-fallback` HTML + CSS: displays phone CTA when booking API is unreachable instead of a blank box ([`2975d62`](../../commit/2975d62))

### Tag / Snapshot
`v1.9.8__widget-render__commit-2975d62`

---

## [1.9.7] — 2026-05-15

### Added
- `CONTEXT.md` — stable project background: what this project is, stack, design constraints, canonical docs ([`82bf7c7`](../../commit/82bf7c7))
- `STATUS.md` — present project state: current version, live deployment, what's next, open audit items, blockers ([`82bf7c7`](../../commit/82bf7c7))

### Changed
- `RELEASE_NOTES.md` — backfilled v1.9.4, v1.9.5, and v1.9.6 entries; file now covers v1.0.0–v1.9.6 ([`82bf7c7`](../../commit/82bf7c7))
- `ROADMAP.md` — added v1.9.6 to Completed ([`82bf7c7`](../../commit/82bf7c7))
- `PROGRESS_NOTE.md` — replaced placeholder with full session-end summary (v1.9.4–v1.9.6) ([`82bf7c7`](../../commit/82bf7c7))
- `prompts/Update.md` — added CONTEXT.md and STATUS.md to the target file list ([`82bf7c7`](../../commit/82bf7c7))
- `prompts/Snapshot` — added Mac path option alongside Windows path ([`82bf7c7`](../../commit/82bf7c7))

### Removed
- `prompts/FIRST_PROMPT_BACKEND_DATA_MODEL.md` — moved out of this repo (belongs in booking-platform) ([`82bf7c7`](../../commit/82bf7c7))

### Tag / Snapshot
`v1.9.7__full-context__commit-82bf7c7`

---

## [1.9.6] — 2026-05-15

### Fixed
- `index.html` — `data-api-url` corrected from `http://localhost:3000` to `http://74.208.9.49:3001`; the widget was unable to reach any API on the live site because the dev server address was never replaced ([`0fbc068`](../../commit/0fbc068))

### Tag / Snapshot
`v1.9.6__fix-api-url__commit-0fbc068`

---

## [1.9.5] — 2026-05-14

### Added
- `prompts/Commit notes` — template for GitHub-style commit notes with real hashes, no Co-Authored-By, tag and push convention
- `prompts/Snapshot` — template for archiving repo snapshots to `E:\Projects\RepoBackups\Jones-Barbor-Shop\` named after commit tag
- `prompts/Update.md` — template for multi-file docs updates (RELEASE_NOTES, ROADMAP, CHANGELOG, etc.)
- `prompts/FIRST_PROMPT_BACKEND_DATA_MODEL.md` — Phase 1 backend data model build prompt (TypeScript, Node.js, PostgreSQL, Prisma, 13 models, 10 enums)

### Tag / Snapshot
`v1.9.5__prompt-vault__commit-dfedf5d`

---

## [1.9.4] — 2026-05-14

### Added
- `COMMIT_NOTES.md` — documents commit message format, tag convention, version rules, and push protocol for this repository
- `PROGRESS_NOTE.md` — snapshot of live deployment status, released versions, open audit items, and next recommended work as of v1.9.4

### Changed
- `RELEASE_NOTES.md` — backfilled v1.8.2 and v1.9.0–v1.9.3 entries; file now covers all releases v1.0.0–v1.9.3
- `ROADMAP.md` — added Completed section (v1.4.0 docs, v1.7.0 redesign, v1.9.0–v1.9.3 widget, live deployment); removed resolved Active and Planned items

### Tag / Snapshot
`v1.9.4__open-record__commit-2039482`

---

## [1.9.3] — 2026-05-14

### Fixed
- `index.html` — replaced placeholder `data-service-id` and `data-location-id` on the widget `<script>` tag with real Neon database IDs from seeded Jones Barber Shop data (Standard Cut: `cmp4e8n600004nocrj81r59y6`, Main Street: `cmp4e8n570002nocre1fi7bvk`) ([`9b20ce4`](../../commit/9b20ce4))

### Tag / Snapshot
`v1.9.3__fix-widget-ids__commit-9b20ce4`

---

## [1.9.2] — 2026-05-14

### Fixed
- `index.html` — removed `data-reveal` attribute from the `#booking-widget` container; the scroll-reveal IntersectionObserver does not fire correctly for React-injected content, leaving the widget invisible at `opacity: 0` ([`f6aef01`](../../commit/f6aef01))

### Tag / Snapshot
`v1.9.2__fix-widget-reveal__commit-f6aef01`

---

## [1.9.1] — 2026-05-14

### Fixed
- `assets/booking-widget.css` — added; Vite library builds emit CSS separately from the JS bundle. Only the JS was copied initially, leaving the widget unstyled ([`81cb25a`](../../commit/81cb25a))
- `index.html` — added `<link rel="stylesheet" href="./assets/booking-widget.css">` to `<head>`

### Tag / Snapshot
`v1.9.1__fix-widget-css__commit-81cb25a`

---

## [1.9.0] — 2026-05-13

### Added
- `assets/booking-widget.js` — booking widget UMD bundle, built from booking-platform widget source

### Changed
- `index.html` — replaced the 3-step placeholder booking form (`form-card` div) with `<div id="booking-widget" class="form-card">` container; removed the dead multi-step form JS handler block; added Jones dark-theme CSS overrides (`.bw-*` class targeting); added widget `<script>` tag with `data-api-url`, `data-container`, `data-service-id`, `data-location-id` attributes ([`91ad411`](../../commit/91ad411))

### Tag / Snapshot
`v1.9.0__booking-widget-embed__commit-91ad411`

---

## [1.8.2] - 2026-05-08 - Open Book

### Fixed
- `RELEASE_NOTES.md` — backfilled all 11 releases (v1.0.0 – v1.8.1) including previously undocumented v1.6.0 Local Photography; file now matches the `/releases/` vault in full ([`b6d766b`](../../commit/b6d766b))
- `releases/v1.8.2-2026-05-08-Open-Book.md` — release snapshot added

### Tag / Snapshot
`v1.8.2__open-book__commit-b6d766b`

---

## [1.8.1] - 2026-05-08 - Full Record

### Fixed
- `CHANGELOG.md` — backfilled all missing entries from v1.2.0 through v1.8.0, reconstructed undocumented v1.6.0 Local Photography from git history, and wired all version diff links to real tags ([`263dcae`](../../commit/263dcae))
- `releases/v1.8.1-2026-05-08-Full-Record.md` — release snapshot added

### Tag / Snapshot
`v1.8.1__full-record__commit-263dcae`

---

## [1.8.0] - 2026-05-08 - Sharp Eye

### Added
- `plans/2026-05-08-full-site-audit.md` — full site diagnostic audit covering runtime behavior, accessibility, security, SEO, performance, structural integrity, and documentation drift across all canonical docs and `index.html`
- `releases/v1.8.0-2026-05-08-Sharp-Eye.md` — release snapshot

### Tag / Snapshot
`v1.8.0__sharp-eye__commit-eb79816`

---

## [1.7.2] - 2026-05-04 - True Line

### Fixed
- `.btn-primary` — applied asymmetric horizontal padding (`right: 1.8rem / left: 1.2rem`) to compensate for the optical right-shift of uppercase text inside the pill button, achieving visual dead-center alignment ([`299bf11`](../../commit/299bf11))

### Tag / Snapshot
`v1.7.2__true-line__commit-299bf11`

---

## [1.7.1] - 2026-05-04 - Lined Up

### Fixed
- `.header-inner` — switched from `flex` + `justify-content: space-between` to a 3-column CSS grid (`auto 1fr auto`) so nav anchors to the center column and the CTA sits right-aligned ([`0894640`](../../commit/0894640))
- `.header-inner nav` — added `display: flex; justify-content: center` so nav links sit centered in the grid's middle column ([`0894640`](../../commit/0894640))
- `.nav-cta` — reduced `gap` from `1rem` to `0.75rem` to tighten the walk-in label and button grouping ([`77cf282`](../../commit/77cf282))
- `.btn-primary` — reduced `letter-spacing` from `0.16em` → `0.06em` → `0` to eliminate the invisible trailing-space offset that made button text appear left-shifted inside the pill ([`98aec0f`](../../commit/98aec0f))

### Tag / Snapshot
`v1.7.1__lined-up__commit-98aec0f`

---

## [1.7.0] - 2026-05-04 - The Chair

### Added — Fonts
- `Bebas Neue` — display headings via Google Fonts
- `Space Grotesk` — body text replacing system-ui stack

### Added — CSS Animations
- `float` — hero card continuous levitate
- `pulse-glow` — gold elements breathe with light
- `gradient-shift` — primary button background color bleed
- `marquee` — reviews auto-scroll in seamless horizontal loop
- `scanline` — CRT scanline sweep across hero
- `preloader-spin` — barber pole stripe animation on load screen
- `bounce-down` — scroll indicator chevron pulse

### Added — JavaScript Modules
- Preloader, Custom cursor, Scroll progress bar, Scroll-aware header, Intersection Observer reveal, Animated counters, Text scramble, Hero parallax, 3D card tilt, Magnetic button, Drag-scroll gallery, Marquee reviews, Multi-step booking wizard

### Changed — Full Section Redesign
- Header/Nav, Hero, About, Services, Barbers, Gallery, Pricing, Reviews, Booking, Footer — cinematic dark-cinema treatment preserving all content, section IDs, dark theme, and 90s soul identity ([`f70fe7f`](../../commit/f70fe7f))

### Tag / Snapshot
`v1.7.0__the-chair__commit-f70fe7f`

---

## [1.6.0] - 2026-05-04 - Local Photography

### Added
- `pics/` — 15 local barbershop JPG files sourced from Pexels ([`7114ae4`](../../commit/7114ae4))

### Changed
- `index.html` — replaced all external Pexels CDN `src` URLs with local `pics/` paths, removing the external image dependency ([`95a66d0`](../../commit/95a66d0))

### Tag / Snapshot
`v1.6.0__local-photography__commit-7114ae4`

---

## [1.5.0] - 2026-05-04 - Release Notes Vault

### Added
- `releases/` — individual GitHub-style release note files for v1.1.0 through v1.4.1, each with title, code name description, What's Changed, snapshot table, and linked Full Changelog ([`ea5608b`](../../commit/ea5608b164091ed17bce0dabc5616660c3665cb5))

### Tag / Snapshot
`v1.5.0__release-notes-vault__commit-ea5608b`

---

## [1.4.1] - 2026-05-04 - DS Store Ignore

### Fixed
- `.gitignore` — added `.DS_Store` and `**/.DS_Store` to prevent macOS metadata files from entering version control ([`61abcc2`](../../commit/61abcc26fd46a61054b5f8a7bae6262e74ad6b99))

### Tag / Snapshot
`v1.4.1__ds-store-ignore__commit-61abcc2`

---

## [1.4.0] - 2026-05-04 - Blueprint

### Added
- `README.md`, `ARCHITECTURE.md`, `CLAUDE.md`, `REPO_PLANNING.md`, `ROADMAP.md`, `CONTRIBUTING.md`, `.env.example` — full root-level documentation scaffold
- `.claude/settings.json` — Claude Code harness configuration
- `.github/PULL_REQUEST_TEMPLATE.md`, `.github/ISSUE_TEMPLATE.md`
- `docs/STRATEGY.md`, `docs/DESIGN.md`, `docs/CONTENT.md`, `docs/ACCESSIBILITY.md`, `docs/PERFORMANCE.md`, `docs/TESTING.md`, `docs/DEPLOYMENT.md`, `docs/VERSIONING.md`, `docs/workflow/claude-code-workflow.md`
- `plans/PLAN_TEMPLATE.md`, `plans/open-decisions.md`, `plans/2026-05-04-initial-project-docs.md`
- `design/`, `sample-data/` scaffolding

> 26 files, 2,194 insertions — `CHANGELOG.md`, `RELEASE_NOTES.md`, `index.html` preserved untouched ([`5b4804a`](../../commit/5b4804a063d6fcab360266438e34bc8f085c8e10))

### Tag / Snapshot
`v1.4.0__blueprint__commit-5b4804a`

---

## [1.3.0] - 2026-05-04 - Docs Scaffold

### Added
- `Documents/00 Core Documents/` — 11 ordered setup prompts (`00_RUN_FIRST.md` through `10_FIRST_TASK_PLAN_PROMPT.md`)
- `Documents/01 Reference Documents/` — 18 files including `VERSIONING.md` and full `project-planning-stack-template/`
- `Documents/03 Optional Documents/` — `10_CODEX_AND_CLAUDE_IMPLEMENTATION_BRIDGE.md`

> 37 files, 2,810 insertions ([`db584c2`](../../commit/db584c2356b6067b2fdb4207bf4a8ee019a89782))

### Tag / Snapshot
`v1.3.0__docs-scaffold__commit-db584c2`

---

## [1.2.0] - 2026-05-03 - Stable Changelog

### Added
- `CHANGELOG.md` — Keep a Changelog format covering Foundation (v1.0.0) and Marquee (v1.1.0), with diff links between all versions ([`f038b92`](../../commit/f038b928c6fec511a0d326fb8b526df520b8446d))

### Tag / Snapshot
`v1.2.0__stable-changelog__commit-f038b92`

---

## [1.1.0] - 2026-05-03 - Marquee

### Added
- `RELEASE_NOTES.md` — GitHub-style release notes for v1.1.0 ([`72b5629`](../../commit/72b56294fa0376e135db9a97a2a16ba37d75ef53))

### Renamed
- `Jones Barbor Shop.html` → `index.html` — establishes the web-standard entry point, removes spaces from filename, and corrects the "Barbor" typo ([`62c3f70`](../../commit/62c3f70adc63a37659efeb6fd99ab89481b659d4))

### Tag / Snapshot
`v1.1.0__index-rename__commit-62c3f70`

---

## [1.0.0] - 2026-04-03 - Foundation

### Added
- Initial website import — full single-page site for Jones Barber Shop including hero, services, barbers, gallery, pricing, booking, location, and reviews sections ([`75314be`](../../commit/75314be45448429ce0c4fdbac4130cd9c2c7d3bd))
- Repository scaffolding — `.gitignore`, `.gitattributes`, `.vscode/settings.json` ([`96bb8b2`](../../commit/96bb8b2e4fc5cfb7b9042a269a6b2468d12a6bb9))

---

[Unreleased]: ../../compare/v1.9.7__full-context__commit-82bf7c7...HEAD
[1.9.7]: ../../compare/v1.9.6__fix-api-url__commit-0fbc068...v1.9.7__full-context__commit-82bf7c7
[1.9.6]: ../../compare/v1.9.5__prompt-vault__commit-dfedf5d...v1.9.6__fix-api-url__commit-0fbc068
[1.9.5]: ../../compare/v1.9.4__open-record__commit-2039482...v1.9.5__prompt-vault__commit-dfedf5d
[1.9.4]: ../../compare/v1.9.3__fix-widget-ids__commit-9b20ce4...v1.9.4__open-record__commit-2039482
[1.9.3]: ../../compare/v1.9.2__fix-widget-reveal__commit-f6aef01...v1.9.3__fix-widget-ids__commit-9b20ce4
[1.9.2]: ../../compare/v1.9.1__fix-widget-css__commit-81cb25a...v1.9.2__fix-widget-reveal__commit-f6aef01
[1.9.1]: ../../compare/v1.9.0__booking-widget-embed__commit-91ad411...v1.9.1__fix-widget-css__commit-81cb25a
[1.9.0]: ../../compare/v1.8.2__open-book__commit-b6d766b...v1.9.0__booking-widget-embed__commit-91ad411
[1.8.2]: ../../compare/v1.8.1__full-record__commit-263dcae...v1.8.2__open-book__commit-b6d766b
[1.8.1]: ../../compare/v1.8.0__sharp-eye__commit-eb79816...v1.8.1__full-record__commit-263dcae
[1.8.0]: ../../compare/v1.7.2__true-line__commit-299bf11...v1.8.0__sharp-eye__commit-eb79816
[1.7.2]: ../../compare/v1.7.1__lined-up__commit-98aec0f...v1.7.2__true-line__commit-299bf11
[1.7.1]: ../../compare/v1.7.0__the-chair__commit-f70fe7f...v1.7.1__lined-up__commit-98aec0f
[1.7.0]: ../../compare/v1.6.0__local-photography__commit-7114ae4...v1.7.0__the-chair__commit-f70fe7f
[1.6.0]: ../../compare/v1.5.0__release-notes-vault__commit-ea5608b...v1.6.0__local-photography__commit-7114ae4
[1.5.0]: ../../compare/v1.4.1__ds-store-ignore__commit-61abcc2...v1.5.0__release-notes-vault__commit-ea5608b
[1.4.1]: ../../compare/v1.4.0__blueprint__commit-5b4804a...v1.4.1__ds-store-ignore__commit-61abcc2
[1.4.0]: ../../compare/v1.3.0__docs-scaffold__commit-db584c2...v1.4.0__blueprint__commit-5b4804a
[1.3.0]: ../../compare/v1.2.0__stable-changelog__commit-f038b92...v1.3.0__docs-scaffold__commit-db584c2
[1.2.0]: ../../compare/v1.1.0__index-rename__commit-62c3f70...v1.2.0__stable-changelog__commit-f038b92
[1.1.0]: ../../compare/96bb8b2...v1.1.0__index-rename__commit-62c3f70
[1.0.0]: ../../commit/96bb8b2e4fc5cfb7b9042a269a6b2468d12a6bb9
