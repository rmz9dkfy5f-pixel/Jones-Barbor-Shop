# Release Notes — Jones Barber Shop

All releases, newest first. Individual release files live in [`/releases/`](./releases/).

---

# v1.8.1 - 2026-05-08 - Full Record

> **Full Record** — CHANGELOG.md is now a complete, accurate history of the project. This patch backfills all ten releases (v1.0.0 – v1.8.0) that were missing from the log, reconstructs the previously undocumented v1.6.0 Local Photography release from git history, and wires all version diff links to their real tags.

## What's Changed

### Fixed
- `CHANGELOG.md` — backfilled missing entries for v1.2.0 through v1.8.0, reconstructed undocumented v1.6.0 Local Photography from git history, all version diff links wired to real tags
- `releases/v1.8.1-2026-05-08-Full-Record.md` — release snapshot added

> 1 file changed — `CHANGELOG.md` only

## Snapshot

| Field | Value |
|---|---|
| Tag | `v1.8.1__full-record__commit-263dcae` |
| Commit | `263dcae` |
| Branch | `main` |
| Date | 2026-05-08 |
| Author | CyberAntAI |

## Full Changelog

- [`263dcae`](../../commit/263dcae) — docs: backfill CHANGELOG.md through v1.8.0 — all 10 releases logged

**Previous release:** [`eb79816`](../../commit/eb79816) — v1.8.0 Sharp Eye

---

# v1.8.0 - 2026-05-08 - Sharp Eye

> **Sharp Eye** — full site diagnostic. A complete read-only audit of the Jones Barber Shop website covering source code, accessibility, security, SEO, performance, structural integrity, and documentation drift. No source files were modified. All findings are filed in `plans/2026-05-08-full-site-audit.md` for staged remediation.

## What's Changed

### Added
- `plans/2026-05-08-full-site-audit.md` — comprehensive diagnostic report:
  - 2 Critical findings (non-functional booking form, fictional contact info)
  - 6 High findings (WCAG failures, stale docs, broken OG metadata, Pexels CDN risk)
  - 6 Medium findings (form validation gaps, focus trap, social link placeholders, unverified claims, fictional reviews)
  - 9 Low findings (favicon, Twitter Cards, canonical URL, robots.txt, sitemap, cursor RAF loop, lightbox issues)
  - `prefers-reduced-motion` confirmed absent — promoted from Unverified to Medium
  - "Program page" clarified — belongs to a different site/version, not this repo

> 2 files changed — `CHANGELOG.md` updated, `plans/2026-05-08-full-site-audit.md` created

## Snapshot

| Field | Value |
|---|---|
| Tag | `v1.8.0__sharp-eye__commit-eb79816` |
| Commit | `eb79816` |
| Branch | `main` |
| Date | 2026-05-08 |
| Author | CyberAntAI |

## Full Changelog

- [`eb79816`](../../commit/eb79816) — docs: add full site diagnostic audit — v1.8.0 Sharp Eye

**Previous release:** [`4781540`](../../commit/4781540) — v1.7.2 True Line

---

# v1.7.2 - 2026-05-04 - True Line

> **True Line** — precision patch. Corrects the optical centering of text inside the Book Now nav button by applying asymmetric horizontal padding, pulling the text left to achieve true visual center inside the pill.

## What's Changed

### Fixed
- `.btn-primary` — applied asymmetric horizontal padding (`right: 1.8rem / left: 1.2rem`) to compensate for the optical right-shift of uppercase text inside the pill button, achieving visual dead-center alignment

> 1 file changed — `index.html` only

## Snapshot

| Field | Value |
|---|---|
| Tag | `v1.7.2__true-line__commit-299bf11` |
| Commit | `299bf11` |
| Branch | `main` |
| Date | 2026-05-04 |
| Author | CyberAntAI |

## Full Changelog

- [`299bf11`](../../commit/299bf11) — fix: shift btn-primary text left — right:1.8rem left:1.2rem padding

**Previous release:** [`98aec0f`](../../commit/98aec0f) — v1.7.1 Lined Up

---

# v1.7.1 - 2026-05-04 - Lined Up

> **Lined Up** — precision patch. Corrects two visual issues with the Book Now button in the fixed navigation bar: button position in the header layout and text centering inside the pill.

## What's Changed

### Fixed
- `.header-inner` — switched from `flex` + `justify-content: space-between` to a 3-column CSS grid (`auto 1fr auto`) so the nav anchors to the center column and the CTA sits right-aligned without excessive gap ([`0894640`](../../commit/0894640))
- `.header-inner nav` — added `display: flex; justify-content: center` so nav links sit centered in the grid's middle column ([`0894640`](../../commit/0894640))
- `.nav-cta` — reduced `gap` from `1rem` to `0.75rem` to tighten the walk-in label and button grouping ([`77cf282`](../../commit/77cf282))
- `.btn-primary` — reduced `letter-spacing` from `0.16em` → `0.06em` → `0` to eliminate the invisible trailing-space offset that made button text appear left-shifted inside the pill ([`98aec0f`](../../commit/98aec0f))

> 1 file changed across 4 commits — `index.html` only

## Snapshot

| Field | Value |
|---|---|
| Tag | `v1.7.1__lined-up__commit-98aec0f` |
| Commit | `98aec0f` |
| Branch | `main` |
| Date | 2026-05-04 |
| Author | CyberAntAI |

## Full Changelog

- [`98aec0f`](../../commit/98aec0f) — fix: remove letter-spacing on btn-primary to fully center button text
- [`d0ec3f3`](../../commit/d0ec3f3) — fix: revert asymmetric padding, reduce btn-primary letter-spacing to 0.06em
- [`77cf282`](../../commit/77cf282) — fix: increase btn-primary left-padding compensation for letter-spacing
- [`0894640`](../../commit/0894640) — fix: correct Book Now button alignment in nav header

**Previous release:** [`f70fe7f`](../../commit/f70fe7f) — v1.7.0 The Chair

---

# v1.7.0 - 2026-05-04 - The Chair

> **The Chair** — cinematic, interactive redesign of the Jones Barber Shop site. Elevates the single-file `index.html` into a 2026-era dark-cinema experience while preserving the 90s soul identity, all in vanilla HTML/CSS/JavaScript with no dependencies and no build step.

## What's Changed

### Added — Fonts
- `Bebas Neue` — display headings (imported from Google Fonts)
- `Space Grotesk` — body text replacing system-ui stack

### Added — CSS Animations
- `float` — hero card levitates continuously
- `pulse-glow` — gold elements breathe with light
- `gradient-shift` — primary button background bleeds through colors
- `marquee` — reviews auto-scroll in seamless horizontal loop
- `scanline` — subtle CRT scanline sweeps the hero
- `preloader-spin` — barber pole stripe animation on load screen
- `bounce-down` — scroll indicator chevron pulses down

### Added — JavaScript Modules

| Module | What it does |
|---|---|
| Preloader | Barber pole + studio name fade in for 1.8s, then reveals page |
| Custom cursor | Gold 10px dot follows mouse with lerp lag; scales 3× on hover |
| Scroll progress bar | 3px gold-red-blue line at top fills 0→100% as page scrolls |
| Scroll-aware header | Nav collapses on scroll down, reappears on scroll up |
| Intersection Observer | `[data-reveal]` elements slide up as they enter viewport |
| Animated counters | Stats count from 0 with eased animation when scrolled into view |
| Text scramble | Hero headline resolves from random chars after preloader clears |
| Hero parallax | Background shifts ±15px on mouse move for subtle depth |
| 3D card tilt | Barber cards track mouse → `rotateX/Y` perspective transform |
| Magnetic button | Hero CTA attracts to mouse within proximity |
| Drag-scroll gallery | Gallery is drag-scrollable with momentum; touch-enabled |
| Marquee reviews | Review cards loop in a seamless auto-scrolling strip |
| Multi-step booking | 3-step wizard: Who → What → When, animated dot indicator |

### Changed — Section Redesigns
Header/Nav, Hero, About, Services, Barbers, Gallery, Pricing, Reviews, Booking, Footer — all redesigned as cinematic dark-cinema treatment

### Preserved
- All section content, section IDs, image references, booking form fields
- Dark theme (`#050509` background) and 90s soul brand identity
- Single-file `index.html` architecture

> 1 file changed, 1816 insertions(+), 1612 deletions(−)

## Snapshot

| Field | Value |
|---|---|
| Tag | `v1.7.0__the-chair__commit-f70fe7f` |
| Commit | `f70fe7f` |
| Branch | `main` |
| Date | 2026-05-04 |
| Author | CyberAntAI |

## Full Changelog

- [`f70fe7f`](../../commit/f70fe7f) — feat: redesign site as The Chair – cinematic interactive experience

**Previous release:** [`7114ae4`](../../commit/7114ae4) — v1.6.0 Local Photography

---

# v1.6.0 - 2026-05-04 - Local Photography

> **Local Photography** — images come home. This release adds the `pics/` folder with 15 local barbershop JPG files and updates `index.html` to reference them directly, removing the external Pexels CDN dependency from all image paths.

## What's Changed

### Added
- `pics/` — 15 local barbershop JPG files (Pexels-sourced placeholders, to be replaced with real shop photography before launch)

### Changed
- `index.html` — replaced all external Pexels CDN `src` URLs with local `pics/` paths across all barber profile cards, gallery images, hero card, and location photo

> 2 commits — `pics/` folder created, `index.html` image paths updated

## Snapshot

| Field | Value |
|---|---|
| Tag | `v1.6.0__local-photography__commit-7114ae4` |
| Commit | `7114ae4` |
| Branch | `main` |
| Date | 2026-05-04 |
| Author | CyberAntAI |

## Full Changelog

- [`7114ae4`](../../commit/7114ae4) — feat: add pics/ folder with 15 local barbershop photos
- [`95a66d0`](../../commit/95a66d0) — feat: replace placeholder images with local photos from pics/

**Previous release:** [`ea5608b`](../../commit/ea5608b) — v1.5.0 Release Notes Vault

---

# v1.5.0 - 2026-05-04 - Release Notes Vault

> **Release Notes Vault** — every release now has its own 1-click `.md` file. This release adds the `releases/` folder with individual GitHub-style release notes covering the full project history from v1.1.0 Marquee through v1.4.1 DS Store Ignore.

## What's Changed

### Added
- `releases/v1.1.0-2026-05-03-Marquee.md`
- `releases/v1.2.0-2026-05-03-Stable-Changelog.md`
- `releases/v1.3.0-2026-05-04-Docs-Scaffold.md`
- `releases/v1.4.0-2026-05-04-Blueprint.md`
- `releases/v1.4.1-2026-05-04-DS-Store-Ignore.md`

Each file includes title, code name description, What's Changed, snapshot table with real commit hash, tag, branch, date, and author, and a linked Full Changelog with previous release pointer.

> 5 files, 217 insertions

## Snapshot

| Field | Value |
|---|---|
| Tag | `v1.5.0__release-notes-vault__commit-ea5608b` |
| Commit | `ea5608b` |
| Branch | `main` |
| Date | 2026-05-04 |
| Author | CyberAntAI |

## Full Changelog

- [`ea5608b`](../../commit/ea5608b) — docs: add individual release note files for v1.1.0 through v1.4.1

**Previous release:** [`61abcc2`](../../commit/61abcc2) — v1.4.1 DS Store Ignore

---

# v1.4.1 - 2026-05-04 - DS Store Ignore

> **DS Store Ignore** — housekeeping patch. Adds `.DS_Store` to `.gitignore` so macOS metadata files never enter version control, including nested instances inside subfolders like `Documents/`.

## What's Changed

### Fixed
- `.gitignore` — added `.DS_Store` and `**/.DS_Store` to prevent macOS metadata files from entering version control

> No content, source code, or documentation was changed.

## Snapshot

| Field | Value |
|---|---|
| Tag | `v1.4.1__ds-store-ignore__commit-61abcc2` |
| Commit | `61abcc2` |
| Branch | `main` |
| Date | 2026-05-04 |
| Author | CyberAntAI |

## Full Changelog

- [`61abcc2`](../../commit/61abcc2) — chore: ignore .DS_Store files

**Previous release:** [`5b4804a`](../../commit/5b4804a) — v1.4.0 Blueprint

---

# v1.4.0 - 2026-05-04 - Blueprint

> **Blueprint** — the repo gets its full structural foundation. This release executes all 10 steps of `00_RUN_FIRST.md`, generating the complete planning and documentation scaffold from real Jones Barber Shop site content. No source code was changed.

## What's Changed

### Added — Root
- `README.md`, `ARCHITECTURE.md`, `CLAUDE.md`, `REPO_PLANNING.md`, `ROADMAP.md`, `CONTRIBUTING.md`, `.env.example`

### Added — Configuration
- `.claude/settings.json`, `.github/PULL_REQUEST_TEMPLATE.md`, `.github/ISSUE_TEMPLATE.md`

### Added — Docs
- `docs/STRATEGY.md`, `docs/DESIGN.md`, `docs/CONTENT.md`, `docs/ACCESSIBILITY.md`, `docs/PERFORMANCE.md`, `docs/TESTING.md`, `docs/DEPLOYMENT.md`, `docs/VERSIONING.md`, `docs/workflow/claude-code-workflow.md`

### Added — Plans
- `plans/PLAN_TEMPLATE.md`, `plans/open-decisions.md`, `plans/2026-05-04-initial-project-docs.md`

### Added — Design and Sample Data
- `design/README.md`, `design/wireframes/README.md`, `design/references/README.md`, `sample-data/README.md`

> 26 files, 2,194 insertions — `CHANGELOG.md`, `RELEASE_NOTES.md`, `index.html` preserved untouched

## Snapshot

| Field | Value |
|---|---|
| Tag | `v1.4.0__blueprint__commit-5b4804a` |
| Commit | `5b4804a` |
| Branch | `main` |
| Date | 2026-05-04 |
| Author | CyberAntAI |

## Full Changelog

- [`5b4804a`](../../commit/5b4804a) — feat: scaffold project docs via 00_RUN_FIRST.md execution

**Previous release:** [`db584c2`](../../commit/db584c2) — v1.3.0 Docs Scaffold

---

# v1.3.0 - 2026-05-04 - Docs Scaffold

> **Docs Scaffold** — planning infrastructure enters version control. This release adds the full `Documents/` folder containing core prompts, reference templates, and optional planning guides for the Jones Barber Shop project.

## What's Changed

### Added
- `Documents/00 Core Documents/` — 11 files (`00_RUN_FIRST.md` through `10_FIRST_TASK_PLAN_PROMPT.md`)
- `Documents/01 Reference Documents/` — 18 files including `VERSIONING.md` and full `project-planning-stack-template/`
- `Documents/03 Optional Documents/` — `10_CODEX_AND_CLAUDE_IMPLEMENTATION_BRIDGE.md`
- `Documents/# Snapshot Info.md`

> 37 files, 2,810 insertions

## Snapshot

| Field | Value |
|---|---|
| Tag | `v1.3.0__docs-scaffold__commit-db584c2` |
| Commit | `db584c2` |
| Branch | `main` |
| Date | 2026-05-04 |
| Author | CyberAntAI |

## Full Changelog

- [`db584c2`](../../commit/db584c2) — docs: add Documents folder with project planning and reference materials

**Previous release:** [`f038b92`](../../commit/f038b92) — v1.2.0 Stable Changelog

---

# v1.2.0 - 2026-05-03 - Stable Changelog

> **Stable Changelog** — project history now lives in a single, structured source of truth. This release adds the Keep a Changelog formatted `CHANGELOG.md` covering all commits from the initial import through v1.1.0 Marquee.

## What's Changed

### Added
- `CHANGELOG.md` — Keep a Changelog format, Semantic Versioning, covering Foundation (v1.0.0) and Marquee (v1.1.0) with diff links between all versions

## Snapshot

| Field | Value |
|---|---|
| Tag | `v1.2.0__stable-changelog__commit-f038b92` |
| Commit | `f038b92` |
| Branch | `main` |
| Date | 2026-05-03 |
| Author | CyberAntAI |

## Full Changelog

- [`f038b92`](../../commit/f038b92) — docs: add CHANGELOG.md

**Previous release:** [`62c3f70`](../../commit/62c3f70) — v1.1.0 Marquee

---

# v1.1.0 - 2026-05-03 - Marquee

> **Marquee** — the front-facing sign of the shop. This release establishes `index.html` as the official, visible entry point of the Jones Barber Shop website.

## What's Changed

### Renamed
- `Jones Barbor Shop.html` → `index.html` — removes spaces from the filename that break URL encoding on most servers, fixes the `"Barbor"` typo in the filename, and makes the site the default document served by GitHub Pages, Netlify, Apache, and nginx

> No content was changed. Markup, styles, and JavaScript are identical.

## Snapshot

| Field | Value |
|---|---|
| Tag | `v1.1.0__index-rename__commit-62c3f70` |
| Commit | `62c3f70` |
| Branch | `main` |
| Date | 2026-05-03 |
| Author | CyberAntAI |

## Full Changelog

- [`62c3f70`](../../commit/62c3f70) — rename: Jones Barbor Shop.html → index.html
- [`72b5629`](../../commit/72b5629) — docs: add v1.1.0 Marquee release notes

**Previous release:** [`75314be`](../../commit/75314be) — v1.0.0 Foundation

---

# v1.0.0 - 2026-04-03 - Foundation

> **Foundation** — the original import. The Jones Barber Shop website and bare repository scaffolding enter version control for the first time.

## What's Changed

### Added
- Initial single-page website — hero, about, services, barbers, gallery, pricing, booking, location, and reviews sections
- `.gitignore`, `.gitattributes`, `.vscode/settings.json` — bare repository scaffolding

## Snapshot

| Field | Value |
|---|---|
| Tag | — |
| Commit | `75314be` |
| Branch | `main` |
| Date | 2026-04-03 |
| Author | CyberAntAI |

## Full Changelog

- [`75314be`](../../commit/75314be) — Initial website import
- [`96bb8b2`](../../commit/96bb8b2) — Initial commit
