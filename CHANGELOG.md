# Changelog

All notable changes to this project will be documented in this file.
Format based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) and [Semantic Versioning](https://semver.org/).

---

## [Unreleased]

---

## [1.9.3] - 2026-05-14 - Fix Widget IDs

### Fixed
- `data-service-id` — replaced placeholder with real service ID `cmp4e8n600004nocrj01r59y6` ([`9b20ce4`](../../commit/9b20ce4))
- `data-location-id` — replaced placeholder with real location ID `cmp4e8n570002nocre1fi7bvk` ([`9b20ce4`](../../commit/9b20ce4))

### Tag / Snapshot
`v1.9.3__fix-widget-ids__commit-9b20ce4`

---

## [1.9.2] - 2026-05-13 - Fix Widget Reveal

### Fixed
- Removed `data-reveal` from booking widget container — scroll-reveal animation was hiding the widget on initial load ([`f6aef01`](../../commit/f6aef01))

### Tag / Snapshot
`v1.9.2__fix-widget-reveal__commit-f6aef01`

---

## [1.9.1] - 2026-05-13 - Fix Widget CSS

### Fixed
- Booking widget container CSS — corrected styles affecting widget display within `#booking` section ([`81cb25a`](../../commit/81cb25a))

### Tag / Snapshot
`v1.9.1__fix-widget-css__commit-81cb25a`

---

## [1.9.0] - 2026-05-13 - Booking Widget Embed

### Added
- Live booking widget embedded in `#booking` section — replaces the non-functional 3-step placeholder form and demo-only success message ([`91ad411`](../../commit/91ad411))

### Removed
- Placeholder multi-step booking form with no submit handler
- Demo-only success message

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

[Unreleased]: ../../compare/v1.9.3__fix-widget-ids__commit-9b20ce4...HEAD
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
