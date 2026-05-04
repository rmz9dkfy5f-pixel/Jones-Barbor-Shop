# Architecture

## 1. Architecture Summary

Jones Barber Shop is a static single-page website. The entire frontend lives in one HTML file (`index.html`) with all CSS embedded in a `<style>` block and all JavaScript embedded in a `<script>` block. There is no build step, no framework, no package manager, no backend, no database, and no authentication. Deployment target is GitHub Pages or equivalent static hosting.

## 2. Tech Stack

| Area | Tool / Technology | Status | Notes |
|---|---|---|---|
| Frontend | Vanilla HTML5 | Confirmed | Single file: `index.html` |
| Styling | Embedded CSS (custom properties) | Confirmed | ~1,450 lines in `<style>` tag |
| Scripting | Embedded Vanilla JS | Confirmed | ~100 lines in `<script>` tag |
| Images | Pexels CDN (external URLs) | Confirmed — placeholder | Must be replaced with real photography |
| Fonts | System font stack | Confirmed | No external font dependencies |
| Build Tool | None | Confirmed | Open in browser or Live Server |
| Backend | None | Confirmed — none planned yet | Booking form has no submission handler |
| Database | None | Confirmed — none planned | N/A |
| Authentication | None | Confirmed — none planned | N/A |
| Hosting | GitHub Pages (candidate) | Assumed | `index.html` in repo root is ready |
| Testing | Manual QA only | Confirmed | No automated tests |
| Analytics | None | Confirmed | No tracking scripts present |

## 3. Repo Structure

| Path | Purpose | Belongs Here | Does Not Belong Here |
|---|---|---|---|
| `/` (root) | Repo entry point and primary docs | `index.html`, `CHANGELOG.md`, `CLAUDE.md`, `ARCHITECTURE.md`, `README.md`, `ROADMAP.md` | Implementation sub-files, test data |
| `Jones Barbor Shop.css` | Duplicate of `index.html` — not a separate stylesheet | Legacy file — do not reference in HTML | Production styles (those are in `index.html`) |
| `docs/` | Project documentation | Strategy, design, content, accessibility, performance, testing, deployment, versioning docs | Source code, plans |
| `docs/workflow/` | Claude Code operating procedure | `claude-code-workflow.md` | Business strategy |
| `plans/` | Task execution plans | Dated plan files, `PLAN_TEMPLATE.md`, `open-decisions.md` | Permanent architecture docs |
| `design/` | Visual references and wireframes | Mockups, screenshots, brand references | Source code |
| `sample-data/` | Test/dev content | Placeholder content for future dynamic features | Production data |
| `.claude/` | Claude Code harness config | `settings.json` | Project docs |
| `.github/` | GitHub-specific templates | `PULL_REQUEST_TEMPLATE.md`, `ISSUE_TEMPLATE.md` | Business logic |
| `Documents/` | Setup documents — one-time use | Core prompts, reference templates | Generated project files |

## 4. Routing / Page Structure

This is a single-page site with anchor-based navigation. No client-side router.

| Section | Anchor | Nav Label |
|---|---|---|
| Hero | `#home` | Home |
| About | `#about` | (no nav item) |
| Services | `#services` | Services |
| Barbers | `#barbers` | Barbers |
| Gallery | `#gallery` | Gallery |
| Pricing | `#pricing` | Pricing |
| Booking form | `#booking` | Booking |
| Location & Hours | `#location` | Location |
| Reviews | (inline) | (no nav item) |
| Footer / Contact | `#contact` | Contact |

- No 404 page — GitHub Pages serves its default
- No deep-linking beyond anchor scrolling
- Navigation: sticky header (glassmorphism), hamburger on mobile

## 5. Component Architecture

No component system — single HTML file. Logical sections:

- **Header/Nav:** Sticky, glassmorphism effect, mobile hamburger toggle
- **Hero:** Full-viewport, CTA buttons, metrics overlay card
- **About:** Four key-point cards (community, expertise, modern, welcoming)
- **Services:** Six service cards with pricing ranges
- **Barbers:** Four barber profile cards with bios and specialty badges
- **Gallery:** Six image cards with lightbox
- **Pricing:** Six pricing cards with badge variants
- **Booking:** Split layout — form left, info sidebar right
- **Location:** Address, hours, map placeholder
- **Reviews:** Four testimonial cards
- **Footer:** Brand lockup, nav links, social icons, dynamic copyright year

Rules:
- New sections should follow the existing `.section-title` / `.section-subtitle` / card pattern
- Do not extract sections into separate files — keep all markup in `index.html`
- Use existing CSS custom properties for all new styling

## 6. Styling / Design System Structure

All styles are embedded in the `<style>` block of `index.html` (~lines 16–1470).

**CSS Custom Properties (root variables):**

```css
--bg-primary: #050509
--bg-secondary: #11111a
--bg-elevated: #181824
--accent-red: #e0474c
--accent-blue: #3d6ee6
--accent-gold: #f5b544
--text-primary: #f5f1e8
--text-secondary: #a09b8c
```

**Design rules:**
- Dark theme only — do not introduce light mode
- Glassmorphism: `backdrop-filter: blur()` on header
- Responsive: mobile-first, breakpoint at ~768px via media queries
- No external CSS frameworks (no Bootstrap, Tailwind, etc.)
- Transitions: `0.3s ease` standard
- Gradients used for section backgrounds and overlays
- Gold (`#f5b544`) reserved for primary CTAs and badges

## 7. Data Flow and State Management

The site is fully static. No global state.

**Local JS state (in `<script>`):**
- Mobile nav open/closed toggle
- Gallery lightbox open/closed + active image
- Booking form validation state (client-side only — no submission)
- Footer year (dynamic via `new Date().getFullYear()`)

No caching, no API calls, no forms that submit to a real backend. Form currently logs to console or shows a success message without sending data.

## 8. API / Backend Contract

No API exists. No backend planned at this time.

**Trigger to add `docs/API.md`:** If a booking service (Square, Booksy, custom endpoint) is connected to the booking form, document the contract there.

**Trigger to add `openapi.yaml`:** If a REST API is built for this project.

## 9. Content Architecture

All content is hardcoded in `index.html`. No CMS.

- **Barber info:** Names, roles, bios in HTML — fictional placeholders
- **Pricing:** Hardcoded — $20–$65 range
- **Hours:** Mon–Thu 10AM–7PM, Fri 10AM–8PM, Sat 9AM–6PM, Sun Closed
- **Address:** 123 Fade Street, Suite B, Joneswood District — placeholder
- **Phone:** (919) 555-1234 — placeholder
- **Images:** Pexels URLs — placeholders, not production-ready
- **Update trigger:** Edit `index.html` directly; update `docs/CONTENT.md` when copy rules change

## 10. Accessibility Architecture

- Semantic HTML: `<header>`, `<nav>`, `<main>`, `<section>`, `<footer>` in use
- Mobile nav: hamburger button uses `aria-label`; panel uses `id` for targeting
- Gallery lightbox: Escape key closes; click outside closes
- Form: Labels paired with inputs; required fields marked
- Color contrast: Dark bg / light text — generally passes WCAG AA; gold CTAs need verification
- Keyboard navigation: nav links focusable; lightbox needs focus trap audit
- Update `docs/ACCESSIBILITY.md` when accessibility decisions are made

## 11. Performance Architecture

- No JavaScript framework overhead
- No external CSS framework
- External image dependency: Pexels CDN — replace with optimized local images for production
- No lazy loading currently implemented — add when real images are in place
- No bundle — single file load
- Critical CSS is inline (no render-blocking stylesheet)
- Update `docs/PERFORMANCE.md` when image optimization decisions are made

## 12. Security Architecture

- No user data stored
- No authentication
- No backend — no server-side attack surface
- Booking form: client-side validation only — no injection risk as data is not submitted
- `.env.example` present but no secrets in use
- No third-party scripts (no analytics, no ad scripts)
- Content Security Policy: not implemented — low risk for static site; add if dynamic features are introduced

## 13. Testing Strategy

Manual QA only. No automated test suite.

**Manual QA checklist before each push:**
- Open `index.html` in Chrome and Firefox
- Test mobile viewport (375px)
- Check sticky nav and mobile hamburger toggle
- Verify all anchor links scroll to correct sections
- Test gallery lightbox: open, close via Escape, close via click outside
- Test booking form validation (required fields, phone format)
- Confirm footer year updates correctly

See `docs/TESTING.md` for full QA checklist.

## 14. Build and Deployment

- **Local dev:** Open `index.html` in browser or `Live Server` (VS Code, port 5501)
- **Build command:** None required
- **Deployment:** Push `main` branch to GitHub; enable GitHub Pages in repo Settings → Pages → Branch: main
- **Rollback:** Revert commit via `git revert` or restore previous tag
- **Environment variables:** None required for current static site

See `docs/DEPLOYMENT.md` for step-by-step deployment instructions.

## 15. File and Naming Conventions

- **HTML file:** `index.html` (single entry point)
- **Plan files:** `plans/YYYY-MM-DD-task-name.md`
- **Branch names:** `feature/description` or `fix/description`
- **Commit style:** Conventional commits — `feat:`, `fix:`, `docs:`, `style:`, `refactor:`
- **Tag format:** `vMAJOR.MINOR.PATCH__slug__commit-SHORTHASH`
- **Folder names:** lowercase with hyphens (e.g. `sample-data`, `docs`)

## 16. Agent Editing Rules

- Read `CLAUDE.md` before every session
- Read `docs/STRATEGY.md` before any copy or content change
- Read this file before any structural or layout change
- Do not create duplicate architecture docs
- Do not move files without updating references
- Do not add dependencies (external JS libs, CSS frameworks) without a plan-approved justification
- Do not touch `Jones Barbor Shop.css` — it is a legacy duplicate, not an active stylesheet
- Keep all changes to `index.html` — do not split into separate HTML/CSS/JS files without a full plan
- Update this file when structural decisions change

## 17. Known Risks / Technical Debt

| Risk | Impact | Mitigation | Priority |
|---|---|---|---|
| All content in one file | Hard to maintain at scale | Acceptable for current scope; reassess if sections exceed 3,000 lines | Low |
| Pexels placeholder images | Not production-ready | Replace with real photography before launch | High |
| Booking form has no submit handler | Visitors cannot actually book | Connect to booking service or backend — see Roadmap | High |
| Fictional contact info | Clients cannot reach the shop | Replace with real phone, email, address before launch | High |
| `Jones Barbor Shop.css` exists but is a duplicate | Confusing — not used by the site | Leave as-is or remove; do not reference in `index.html` | Low |
| No SEO meta tags | Poor search discoverability | Add title, description, OG tags | Medium |
| No favicon | Unprofessional browser tab | Add favicon when real branding is confirmed | Medium |

## 18. Open Architecture Questions

| Question | Options | Recommended Default | Continue Without? |
|---|---|---|---|
| Should CSS and JS be extracted into separate files? | Keep inline / extract | Keep inline — simpler for solo static site | Yes |
| Should `Jones Barbor Shop.css` be deleted? | Delete / rename / keep | Keep until owner confirms it is unused | Yes |
| Deployment: GitHub Pages or Netlify? | GitHub Pages / Netlify / other | GitHub Pages — simplest for current setup | Yes |
| Booking backend: Square, Booksy, custom? | Multiple options | Defer until owner selects a service | Yes |

---

*Status: Active*
*Created: 2026-05-04*
