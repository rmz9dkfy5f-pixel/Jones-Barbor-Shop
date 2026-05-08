# Full Site Diagnostic Audit — Jones Barber Shop
**Date:** 2026-05-08  
**Auditor:** Claude Code (Sonnet 4.6)  
**Mode:** Review only — no code output, no fixes

---

## 1. Review Scope

### Inputs Available
- Full source: `index.html` (2,479 lines, all HTML/CSS/JS embedded, read in full)
- All canonical docs: `ARCHITECTURE.md`, `docs/STRATEGY.md`, `docs/DESIGN.md`, `docs/CONTENT.md`, `docs/ACCESSIBILITY.md`, `docs/PERFORMANCE.md`, `docs/TESTING.md`, `docs/DEPLOYMENT.md`, `docs/VERSIONING.md`
- Plans directory: `plans/open-decisions.md`, `plans/PLAN_TEMPLATE.md`, `plans/2026-05-04-initial-project-docs.md`
- `CHANGELOG.md`, `ROADMAP.md`, `README.md`, `ARCHITECTURE.md`, `CONTRIBUTING.md`
- All 9 release note files in `/releases/`
- `.gitignore`, `.env.example`
- `Jones Barbor Shop.css` (legacy file)
- `/pics/` directory listing (15 image files)
- Git log (recent commits via context)

### What Was Missing
- **No live URL** — site has not been deployed to GitHub Pages yet; review is source-only
- **No browser console logs or network traces** — cannot confirm runtime errors in a live environment
- **No screenshots** — visual rendering not directly observable
- **No screen reader test results** — ARIA and keyboard findings are based on source analysis
- **No WCAG contrast measurement tool output** — contrast findings are inferred from color values
- **No Pexels license confirmation** — commercial licensing status of placeholder images is unverified
- **No shop owner confirmation** — which barber names, pricing, and stats are real vs. fictional is partially unknown

### What Could and Could Not Be Verified
- **Could verify:** All source code structure, JS logic, HTML semantics, ARIA usage, form behavior, external dependencies, meta tags, CSS custom properties, file inventory, documentation accuracy vs. code
- **Could not verify:** Actual render output, live network behavior, Lighthouse/Core Web Vitals, real screen reader UX, production image availability, Pexels CDN uptime

---

## 2. Executive Summary

**Overall Site Health: Pre-Production / Not Launch-Ready**

The site is a well-structured, technically clean static single-page application. Vanilla HTML/CSS/JS, no frameworks, no backend, no exposed secrets. The code quality is above average for its category. There are no critical security vulnerabilities.

However, the site is **not production-ready** in any sense that matters to the business:
- The booking form silently captures nothing and tells real customers "Demo only"
- All contact information is fictional
- All photography is Pexels CDN stock
- The most critical accessibility failure (invisible skip link, no focus styles on interactive elements) would fail a basic WCAG audit
- Documentation has drifted significantly from the codebase it describes

**Most Serious Issues (in order):**
1. The booking form is a non-functional demo that would expose users to a "Demo only" message
2. All contact information is unreachable fictional data
3. The "Skip to main content" link is permanently invisible to sighted keyboard users (WCAG failure)
4. No visible focus styles on navigation, buttons, or interactive elements (WCAG failure)
5. Open Graph metadata points to `example.com` — broken social sharing
6. ARCHITECTURE.md and CHANGELOG.md are materially stale

**Program Page:**
There is **no "Program" page, section, or feature** anywhere in this codebase. The word "program" appears once in `docs/ACCESSIBILITY.md` as an adjective. No navigation item, section ID, HTML block, JavaScript reference, plan entry, or roadmap item corresponds to a "Program page." This must be clarified — see Section 7, Open Questions.

---

## 3. Findings by Severity

---

### CRITICAL

---

**C-1: Booking form is non-functional and exposes a "Demo only" message to real customers**
- **Severity:** Critical
- **Affected area:** `#booking` section — the site's primary conversion point
- **What is happening:** The multi-step booking form (`index.html:2463–2469`) intercepts submit with `e.preventDefault()`, runs client-side validation, then displays this verbatim text to the user: `"Your request is captured. We'll contact you to confirm. (Demo only – connect a backend to go live.)"` No data is sent anywhere. No appointment is recorded. The confirmation resets after 5 seconds.
- **Evidence:** `index.html:2466` — `status.textContent = "Your request is captured. We'll contact you to confirm. (Demo only – connect a backend to go live.)";`
- **Likely cause:** Intentional placeholder awaiting a backend decision (OD-003 in `plans/open-decisions.md`)
- **User impact:** A customer who completes the three-step form believes they have requested an appointment. They have not. No follow-up will occur. The "Demo only" text is visible to them.
- **Business/security impact:** Missed bookings, broken trust, zero conversion. If the site goes live in this state, every submitted form is lost.
- **Confidence:** Confirmed
- **Next step:** Resolve OD-003 — select a backend (Netlify Forms, Formspree, Square, Booksy) before any public deployment

---

**C-2: All contact information is fictional and unreachable**
- **Severity:** Critical
- **Affected area:** Header CTAs, Location section (`#location`), Hero (`#home`), `Jones Barbor Shop.css`
- **What is happening:** Phone `(919) 555-1234`, address `123 Fade Street, Suite B, Joneswood District, Your City, ST 12345`, and email `hello@jonesbarbershop.com` are all placeholder values. The phone `tel:` links and the address callout text are embedded directly in the HTML. The email's placeholder status is NOT explicitly documented in `docs/CONTENT.md` (only phone and address are flagged there — potential oversight).
- **Evidence:** `index.html:1487`, `index.html:2054`, `index.html:2047–2048`, `index.html:2060`; `docs/CONTENT.md` placeholder inventory; `ARCHITECTURE.md:134–135`
- **Likely cause:** Intentional — OD-001 requires shop owner to supply real contact data
- **User impact:** Customers cannot call, visit, or email the shop. Phone link will connect to a non-shop number. Address will not be findable on a map.
- **Business/security impact:** Complete breakdown of customer contact flow. If the site is indexed by search engines, the false address and phone could propagate.
- **Confidence:** Confirmed
- **Next step:** Resolve OD-001 — shop owner must provide real phone, address, and email before launch

---

### HIGH

---

**H-1: "Skip to main content" link is permanently invisible to sighted keyboard users**
- **Severity:** High
- **Affected area:** `index.html:1416` — global accessibility
- **What is happening:** The skip link `<a href="#home" class="visually-hidden">Skip to main content</a>` uses `.visually-hidden` (lines 211–215). That class applies `position: absolute; width: 1px; height: 1px; clip: rect(0,0,0,0)` with no `:focus` exception. The link is permanently hidden from all users, including sighted keyboard users who tab to it. It provides no functional benefit in its current state.
- **Evidence:** CSS at `index.html:211–215` — no `:focus` variant of `.visually-hidden` exists anywhere in the stylesheet. Confirmed via full CSS grep.
- **Likely cause:** Implementation oversight — skip links require a `:focus` CSS rule to become visible when focused
- **User impact:** Sighted keyboard users cannot skip navigation. Screen reader users can still navigate to it, but the UX is broken for everyone else.
- **Business/security impact:** WCAG 2.4.1 (Bypass Blocks) failure. Would fail a basic accessibility audit.
- **Confidence:** Confirmed
- **Next step:** Add `.visually-hidden:focus { position: static; width: auto; height: auto; clip: auto; }` (diagnostic only — no code output until approved)

---

**H-2: No visible focus styles on navigation links, buttons, or most interactive elements**
- **Severity:** High
- **Affected area:** Site-wide — all navigation, CTAs, gallery, social links, lightbox controls
- **What is happening:** The only `:focus` rule in the entire 1,450-line CSS targets form inputs (`index.html:1196`). Navigation links (`<a>` in `.nav-links`), the "Book Now" button, "Call the Shop" button, the hamburger toggle, gallery items, social links, and the lightbox close button have no `:focus-visible` or `:focus` styles. When a keyboard user tabs to these elements, there is no visible ring, outline, or indicator of focus position.
- **Evidence:** Full grep of `:focus` in `index.html` returns only 2 results — the form input style and a `f.focus()` call in JavaScript. No button, anchor, or nav element has a focus style.
- **Likely cause:** Omission — CSS reset at line 47 uses `box-sizing: border-box; margin: 0; padding: 0` but does not explicitly remove browser focus outlines via `outline: none`. Browser defaults may partially compensate depending on browser, but the custom UI (glassmorphism header, dark theme) likely suppresses them visually.
- **User impact:** Keyboard-only users cannot track where they are on the page. Blind users relying on focus order are unaffected, but low-vision users who use keyboard + sight are fully impacted.
- **Business/security impact:** WCAG 2.4.7 (Focus Visible) failure. Would fail any accessibility audit.
- **Confidence:** Confirmed (no `:focus` styles found for these elements)
- **Next step:** Add visible focus indicators (gold ring consistent with brand token `--color-gold`) to all interactive elements

---

**H-3: Open Graph metadata points to example.com — broken social sharing**
- **Severity:** High
- **Affected area:** `<head>` — all social media sharing
- **What is happening:** `og:url` is set to `https://example.com/` and `og:image` is set to `https://example.com/placeholder-jones-barber-shop.jpg`. When the site URL is shared on Facebook, WhatsApp, LinkedIn, or Instagram Stories, the platform will fetch a broken image and display the wrong canonical URL.
- **Evidence:** `index.html:13–14`
- **Likely cause:** Intentional placeholder awaiting a real domain and real social image (listed in ROADMAP.md "Planned" section as "SEO meta tags and Open Graph setup")
- **User impact:** Any social share of the site will produce broken card previews
- **Business/security impact:** Direct reputational impact every time a customer or the shop owner shares the link. The `og:image` referencing `example.com` is also misleading metadata.
- **Confidence:** Confirmed
- **Next step:** Pre-launch: set `og:url` to the real GitHub Pages URL, set `og:image` to a hosted real image

---

**H-4: CHANGELOG.md is 11 releases behind — unreliable audit trail**
- **Severity:** High
- **Affected area:** `CHANGELOG.md` — project documentation integrity
- **What is happening:** `CHANGELOG.md` documents only v1.0.0 (2026-04-03) and v1.1.0 (2026-05-03). The current version is v1.7.2. Releases v1.2.0 through v1.7.2 — including the complete v1.7.0 cinematic redesign that rewrote most of `index.html` — are not in the changelog. The `/releases/` directory has these versions but the central changelog does not.
- **Evidence:** `CHANGELOG.md` (last entry v1.1.0); `/releases/` directory contains 9 files up to v1.7.2
- **Likely cause:** Releases were documented in `/releases/` individual files but were never merged back into `CHANGELOG.md`
- **User impact:** None directly
- **Business/security impact:** Anyone using `CHANGELOG.md` as an audit trail (future devs, contributors, the owner) gets a materially incomplete picture of what changed and when
- **Confidence:** Confirmed
- **Next step:** Backfill `CHANGELOG.md` from the `/releases/` files

---

**H-5: ARCHITECTURE.md contains stale facts that contradict the live code**
- **Severity:** High
- **Affected area:** `ARCHITECTURE.md` — ground truth document
- **What is happening:** Three specific claims in ARCHITECTURE.md are false as of the current codebase:
  1. Line 13: "~100 lines in `<script>` tag" — actual JS is ~342 lines
  2. Lines 88–96: CSS variable names listed as `--bg-primary`, `--bg-secondary`, `--bg-elevated`, `--text-primary`, `--text-secondary` — these names do not exist in the actual CSS. Real names are `--color-bg`, `--color-bg-alt`, `--color-surface`, `--color-offwhite`, `--color-muted`, etc.
  3. Line 154: "No lazy loading currently implemented" — `loading="lazy"` is applied to 10+ images in the current `index.html`
- **Evidence:** `ARCHITECTURE.md:13`, `ARCHITECTURE.md:88–96`, `ARCHITECTURE.md:154`; cross-referenced against `index.html` CSS and HTML
- **Likely cause:** ARCHITECTURE.md was scaffolded before the v1.7.0 redesign and was not updated when the CSS variable naming convention changed
- **User impact:** None directly
- **Business/security impact:** Anyone (including Claude Code) reading ARCHITECTURE.md as ground truth and using its variable names or assumptions will produce incorrect code
- **Confidence:** Confirmed
- **Next step:** Update ARCHITECTURE.md to reflect current CSS variable names, JS line count, and lazy loading status

---

**H-6: Pexels placeholder images are external CDN dependencies in production paths**
- **Severity:** High
- **Affected area:** All image content (12 unique images, 13 `<img>` tags)
- **What is happening:** All 12 images on the site are loaded from the local `/pics/` directory, which contains 15 Pexels-sourced JPG files. These are stock photos of strangers in unrelated barbershops. The site currently presents them as the shop's own photography.
- **Evidence:** All `<img>` tags reference `pics/pexels-*.jpg`; `docs/CONTENT.md` placeholder inventory; `plans/open-decisions.md` OD-002
- **Likely cause:** Intentional placeholder — OD-002 is open, awaiting real photography
- **User impact:** Clients who visit the real shop will not recognize the barbers or location from the site. Photos of specific named barbers (Marcus Jones, Renee Carter, etc.) show stock model strangers.
- **Business/security impact:** Potential Pexels licensing violation if used commercially without verifying license terms. Reputational risk from misrepresenting the shop's actual staff and space. CONTENT.md explicitly flags this as blocking for launch.
- **Confidence:** Confirmed
- **Next step:** Resolve OD-002 — commission or collect real photography before launch; verify Pexels license terms for current use

---

### MEDIUM

---

**M-1: Lightbox dialog has no focus trap — keyboard users can escape the modal**
- **Severity:** Medium
- **Affected area:** Gallery lightbox (`#lightbox`, `index.html:2128–2133`, JS `index.html:2382–2405`)
- **What is happening:** The lightbox has `role="dialog"` and `aria-modal="true"`. When open, it contains only one interactive element (the close button). The JS has no focus trap — a keyboard user pressing Tab inside the open lightbox will tab to elements behind it in the DOM (the footer, etc.). The Escape key does close it correctly.
- **Evidence:** `index.html:2382–2405` — no focus trap logic; `docs/ACCESSIBILITY.md` acknowledges this as a known gap: "Gallery lightbox focus trap | High | Audit and implement before launch"
- **Likely cause:** Known gap — documented in `docs/ACCESSIBILITY.md` as requiring implementation before launch
- **User impact:** Screen reader users and keyboard users may lose their place in the page when the lightbox is open
- **Business/security impact:** WCAG 2.4 failure for keyboard-only users. Lower severity than H-1/H-2 because the lightbox is a secondary feature.
- **Confidence:** Confirmed
- **Next step:** Implement focus trap in lightbox JS

---

**M-2: Form validation is incomplete — phone format, email format, and date range not checked**
- **Severity:** Medium
- **Affected area:** Booking form — `validateStep()` at `index.html:2441–2449`
- **What is happening:** The form uses `novalidate` (line 1924), disabling browser HTML5 validation. The custom `validateStep()` function only checks `if (!f.value.trim())` for fields with `required`. This means:
  - Phone: checked only for non-empty, not for valid format or length
  - Email: optional, so never validated — any string (or "notanemail") passes
  - Date/time: checked for non-empty, but not validated to be a future date, not within business hours, not a Sunday (when the shop is closed)
- **Evidence:** `index.html:2441–2449`; form fields at `index.html:1931`, `1936`, `1943`, `1993`
- **Likely cause:** Intentional minimal implementation for a demo form
- **User impact:** A customer could submit a booking request for a past date, a Sunday, or outside business hours. The date/time would be silently accepted (though the form currently submits nowhere anyway).
- **Business/security impact:** When a real backend is connected, invalid or past-date bookings will need server-side validation. Customers may receive confirmation for impossible appointment times.
- **Confidence:** Confirmed
- **Next step:** When backend is connected, add future-date validation, Sunday/closed-day check, and business-hours range check; add phone format validation

---

**M-3: Form validation failures produce no error message — not announced to screen readers**
- **Severity:** Medium
- **Affected area:** Booking form — `validateStep()` and form step navigation
- **What is happening:** When a required field is empty and the user clicks "Next," `validateStep()` returns false and focuses the first empty field, but no error text is displayed to any user (visual or assistive). The `<p id="form-status">` with `aria-live="polite"` is only written to on final form submission, not on step validation failures.
- **Evidence:** `index.html:2441–2449` — `ok = false; f.focus()` with no error text; `index.html:2005` — `form-status` paragraph is empty until submit
- **Likely cause:** Omission — validation feedback was not implemented
- **User impact:** Users who fill out a field incorrectly or leave it blank get no explanation. Screen reader users get no announcement. The UI just fails to advance.
- **Business/security impact:** WCAG 3.3.1 (Error Identification) — required fields that fail validation must have error messages. Poor UX may cause form abandonment.
- **Confidence:** Confirmed
- **Next step:** Add inline error messages per field on validation failure; populate `form-status` or per-field error containers; ensure `aria-live` region announces the error

---

**M-4: Social links use `href="#"` — scrolls to page top unexpectedly**
- **Severity:** Medium
- **Affected area:** Footer social links — `index.html:2114–2116`
- **What is happening:** Three social links (Instagram, TikTok, Facebook) use `href="#"` as a placeholder. Clicking them scrolls the page to the top without navigating to any social profile. The `aria-label` attributes are correct, but the click behavior is deceptive.
- **Evidence:** `index.html:2114–2116`
- **Likely cause:** Intentional placeholder — OD-005 in `plans/open-decisions.md`
- **User impact:** Users clicking social links are scrolled to the top of the page. No social profile is reached.
- **Business/security impact:** Mild trust erosion. Not a security issue.
- **Confidence:** Confirmed
- **Next step:** Resolve OD-005 (get real URLs) or change `href="#"` to `href="javascript:void(0)"` or add `aria-disabled="true"` until real URLs are available

---

**M-5: Unverified business claims displayed as facts**
- **Severity:** Medium
- **Affected area:** Hero stats (`index.html:1489–1501`), About stats, Hero card metrics (`index.html:1510–1524`)
- **What is happening:** The site displays animated counters for "150+ Weekly cuts" and "25+ Years in the game" and static metrics for "★ 5 Rated" and "$30 Starting". `docs/CONTENT.md` explicitly states: "Do not inflate '150+ weekly cuts' without owner confirmation" and "Do not invent ratings counts." These appear to be unconfirmed placeholder values.
- **Evidence:** `index.html:1491–1500` (hero counters); `index.html:1510–1523` (hero card — aria-hidden, so decorative); CONTENT.md claims policy
- **Likely cause:** Realistic-sounding placeholder values used during design
- **User impact:** Customers may make decisions based on stats the shop cannot substantiate
- **Business/security impact:** If incorrect, this is false advertising. The "★ 5 Rated" metric implies a verified review platform score that does not exist.
- **Confidence:** Confirmed that these are unverified; whether they are accurate is unverified
- **Next step:** Confirm with shop owner before launch; remove or replace unconfirmed stats

---

**M-6: Reviews are fictional and may constitute false testimonials**
- **Severity:** Medium
- **Affected area:** Reviews section (`#reviews`) — `index.html:1840–1869`
- **What is happening:** Six testimonial review cards are displayed with names (Chris M., Jasmine T., Marcus & Little MJ, Deon L., Anthony R., Kevin D.) and five-star reviews. `docs/CONTENT.md` states: "Do not use testimonial names that are not real or consented."
- **Evidence:** `index.html:1840–1869`; `docs/CONTENT.md` claims policy
- **Likely cause:** Fictional placeholder reviews for design purposes
- **User impact:** Customers rely on these reviews to evaluate the shop. If fictional, they constitute misleading content.
- **Business/security impact:** Potential FTC violation if false reviews are presented as real customer opinions. Legal risk before launch.
- **Confidence:** Confirmed that these are undocumented and unverified; whether they are real is unconfirmed
- **Next step:** Confirm with shop owner — are these real customers? Get consent if so. Replace or remove if not.

---

### LOW

---

**L-1: No favicon**
- **Severity:** Low
- **Affected area:** `<head>`
- **What is happening:** No `<link rel="icon">` or `<link rel="apple-touch-icon">` tag exists. The browser tab shows a generic page icon.
- **Evidence:** Absence confirmed by full `<head>` read (`index.html:1–20`)
- **Likely cause:** Listed in ROADMAP.md "Planned" section as "Favicon and web app manifest"
- **Confidence:** Confirmed

---

**L-2: No Twitter/X Card meta tags**
- **Severity:** Low
- **Affected area:** `<head>` social sharing
- **What is happening:** Only Open Graph tags are present. Twitter/X will fall back to OG data but without `twitter:card`, `twitter:site`, or `twitter:creator`, the sharing card format on Twitter is degraded.
- **Evidence:** `index.html:9–14` — only `og:*` tags present
- **Confidence:** Confirmed

---

**L-3: No canonical URL tag**
- **Severity:** Low
- **Affected area:** `<head>` SEO
- **What is happening:** No `<link rel="canonical">` tag. For a single-page site this is minor, but if the site is ever accessible at multiple URLs (with/without www, http/https, trailing slash), it could create duplicate content issues.
- **Confidence:** Confirmed

---

**L-4: No robots.txt or sitemap.xml**
- **Severity:** Low
- **Affected area:** Repo root — SEO and crawler control
- **What is happening:** No `robots.txt` or `sitemap.xml` exist. Search engines will crawl freely. Without a sitemap, discovery of the single page may be slower.
- **Evidence:** File listing — neither file exists
- **Confidence:** Confirmed

---

**L-5: Lightbox close button text includes ✕ symbol that screen readers may announce**
- **Severity:** Low
- **Affected area:** `index.html:2130`
- **What is happening:** `<button class="lightbox-close" type="button">Close ✕</button>` — the ✕ character may be announced by some screen readers as "multiplication sign," "X mark," or similar. The button has no `aria-label` override.
- **Evidence:** `index.html:2130`
- **Confidence:** Confirmed (character present); screen reader announcement varies by reader/browser

---

**L-6: Lightbox `<img>` has empty `src=""` at page load**
- **Severity:** Low
- **Affected area:** `index.html:2131`
- **What is happening:** `<img src="" alt="Expanded gallery image" />` — an empty `src` attribute. Some browsers make a network request to the current page URL when `src=""`. HTML validators will flag this as invalid.
- **Evidence:** `index.html:2131`
- **Confidence:** Confirmed

---

**L-7: Custom cursor RAF animation loop runs indefinitely even when cursor is stationary**
- **Severity:** Low
- **Affected area:** JS — custom cursor IIFE (`index.html:2147–2172`)
- **What is happening:** The LERP-based cursor animation uses `requestAnimationFrame` in a loop that never terminates while the page is open. Even when the cursor hasn't moved, the RAF fires every frame (~60/sec), applying near-identical transforms. This is a minor but continuous performance cost.
- **Evidence:** `index.html:2160–2166` — `(function loop() { ... requestAnimationFrame(loop); })()`
- **Likely cause:** Standard LERP pattern; cursor is disabled on touch devices which mitigates most of the impact
- **Confidence:** Confirmed

---

**L-8: `Jones Barbor Shop.css` is a complete HTML document with a .css extension**
- **Severity:** Low
- **Affected area:** Repo root
- **What is happening:** The file `Jones Barbor Shop.css` (70KB) contains a complete HTML document (`<!DOCTYPE html>`, `<html>`, `<head>`, `<body>`) — not CSS. It is a legacy copy of the old `index.html`. It is not referenced by any file. It contains the same placeholder contact info (phone, address, email) in multiple places.
- **Evidence:** File listing; agent confirmed it contains DOCTYPE declaration; `ARCHITECTURE.md:211`, `CLAUDE.md` both explicitly forbid touching it; OD-006 in `plans/open-decisions.md` proposes deleting it
- **Likely cause:** Was renamed from the original HTML file name before `index.html` was created
- **Confidence:** Confirmed

---

**L-9: Hero card metrics section is `aria-hidden="true"` — three visible stats inaccessible**
- **Severity:** Low
- **Affected area:** Hero section — `index.html:1505`
- **What is happening:** The hero card (`<div class="hero-card-wrap" aria-hidden="true">`) containing "$30 Starting", "4+ Barbers", and "★ 5 Rated" is decorative per current markup. These three metrics are visible on-screen but not accessible to screen readers. This may be intentional (decorative overlay) or an omission.
- **Evidence:** `index.html:1505–1525`
- **Confidence:** Confirmed; whether this is intentional is unverified

---

### UNVERIFIED / NEEDS CONFIRMATION

---

**U-1: Color contrast ratios not measured**
- **What needs verification:** `--color-muted: #9996a0` on `--color-bg: #050509` — contrast ratio unverified at body text sizes. `docs/ACCESSIBILITY.md` flags this as needing verification before launch. `--color-gold: #f5b544` on dark backgrounds for CTAs also requires a WCAG AA check.
- **Why it matters:** Could be a WCAG 1.4.3 (Contrast Minimum) failure
- **How to verify:** Run hex values through a WCAG contrast checker (e.g., WebAIM)

---

**U-2: Barber names — real or fictional?**
- **What needs verification:** Marcus Jones, Renee Carter, Devin Moore, Trey Collins appear in the barbers section and in the booking form. ARCHITECTURE.md describes them as "fictional placeholders." Whether these are real employees with consent, or invented names, determines whether they must be changed before launch.
- **Why it matters:** Real names without consent is a privacy issue; fictional names that go live are misrepresentation
- **How to verify:** Confirm with shop owner

---

**U-3: Email `hello@jonesbarbershop.com` — real or placeholder?**
- **What needs verification:** `docs/CONTENT.md` documents the address and phone as fictional but does NOT explicitly flag the email as a placeholder. The email appears in `index.html:2060` as a `mailto:` link. Whether this email address is real, registered, and monitored is unknown.
- **Why it matters:** Customers clicking the email link would send to a potentially unmonitored or invalid address
- **How to verify:** Confirm with shop owner

---

**U-4: Pexels image licensing for commercial/production use**
- **What needs verification:** All 15 images in `/pics/` are Pexels-sourced. Pexels free license allows use in websites, but specific terms around use in a commercial business context, attributions, and whether hosting locally (rather than via Pexels CDN) is permitted should be verified.
- **Why it matters:** Licensing violation risk if images go to production under incorrect terms
- **How to verify:** Review Pexels license agreement; intended moot once real photography replaces them

---

**U-5: `prefers-reduced-motion` is absent — confirmed**
- **Status: Confirmed during audit — promoted from Unverified to Medium**
- **What is happening:** A grep of all 2,479 lines of `index.html` returned zero matches for `prefers-reduced-motion`. The site includes substantial animation on nearly every section (preloader, custom cursor, scroll reveal, counter animation, text scramble, hero parallax, 3D card tilt, marquee reviews, drag-scroll) with no reduced-motion fallback. Users who have enabled "reduce motion" in their OS accessibility settings will receive the full animation suite.
- **Why it matters:** WCAG 2.3.3 (Animation from Interactions) — unexpected motion can cause dizziness, nausea, or seizures in users with vestibular disorders
- **Severity:** Medium — should be addressed before launch

---

## 4. Program Page Deep Review

**Finding: The "Program page" does not exist in this codebase.**

After a thorough search of all 2,479 lines of `index.html`, all documentation files, all plan files, and all release notes:

- The word "program" appears **once** in the entire codebase — in `docs/ACCESSIBILITY.md` line 62, as the adjective in "programmatically associated" (referring to form error messages)
- There is no HTML section with ID `#program`
- There is no navigation item labeled "Program"
- There is no JavaScript module related to a program feature
- There is no plan entry or roadmap item for a "Program" section
- The site's nine sections are: Home, About, Services, Barbers, Gallery, Pricing, Booking, Location, Reviews/Contact

**Possible interpretations (unverified):**
- The user may be referring to a planned feature not yet built (loyalty program, apprenticeship program, referral program)
- The user may be referring to a page on a different version of the site not in this repo
- The user may be referring to the booking form "program" (multi-step flow) or the "program" of services
- This may be a mismatch between the user's mental model and the current site structure

**Impact:** Any targeted audit of the "Program page" cannot be performed — there is nothing to audit. See Section 7, Open Question OQ-1 for the clarifying question required.

---

## 5. Cross-Site Risks

**XR-1: Documentation drift undermines trust in canonical docs**  
ARCHITECTURE.md and CHANGELOG.md contain material inaccuracies. If these docs are used as ground truth (by future contributors, AI agents, or the owner), errors will propagate. The pattern of documentation falling behind code is a structural risk that will worsen unless a post-release documentation audit is included in the Definition of Done.

**XR-2: No global focus style system — affects every interactive element on the page**  
The missing `:focus-visible` implementation (H-2) is a cross-site failure that touches every link, button, and form control. A single CSS rule block would fix it globally, but the risk affects the entire site.

**XR-3: Placeholder content in multiple sections — coordinated replacement needed**  
The phone number, address, email, barber names and photos, gallery photos, hero background, location photo, testimonials, and social links all need to be replaced in coordination. Replacing some but not others risks inconsistency (e.g., real photos but fake phone number).

**XR-4: `novalidate` on the form propagates to all future backend integrations**  
When a backend is added, the `novalidate` attribute means the browser will never catch bad inputs before they reach the server. All validation must be handled in JS. The current JS validation is minimal. A future developer connecting a backend may not realize the scope of validation work required.

**XR-5: No Content Security Policy**  
Currently low risk (static site, no user data). If a booking backend, analytics, or chat widget is added, the absence of a CSP creates an XSS risk surface. Should be added proactively before any dynamic features are introduced.

**XR-6: External font dependency (Google Fonts)**  
Google Fonts is the only external runtime dependency. Network failure causes font fallback to `"Impact", system-ui, sans-serif`. The display font `Bebas Neue` has no close system equivalent — fallback may cause layout reflow. Considered low risk but worth noting as the single point of CDN failure.

**XR-7: Unverified `prefers-reduced-motion` support**  
Animation is used throughout every major section. If `prefers-reduced-motion` is not respected (U-5), it could cause accessibility issues for a broad class of users across the entire site simultaneously.

---

## 6. Priority Order

Issues ranked by urgency for resolution:

| # | Finding | Why First |
|---|---------|-----------|
| 1 | **C-2 — Fictional contact info** | Site cannot serve its real-world purpose without it |
| 2 | **C-1 — Booking form submits nowhere + "Demo only" message** | Primary conversion action is broken and self-declares as broken |
| 3 | **U-3 — Email address status unknown** | Must confirm before any user-facing deployment |
| 4 | **H-1 — Skip link permanently invisible** | WCAG hard failure; one CSS rule to fix |
| 5 | **H-2 — No focus styles on interactive elements** | WCAG hard failure; broad impact across every element |
| 6 | **U-5 — prefers-reduced-motion absent (confirmed)** | Confirmed missing; broad accessibility harm across all animated sections |
| 7 | **H-3 — Open Graph points to example.com** | Every social share is broken; easy fix once domain is known |
| 8 | **M-3 — Form validation errors not announced** | Accessibility gap in the primary user action on the site |
| 9 | **M-5/M-6 — Unverified stats and fictional reviews** | Legal and trust risk; must be owner-confirmed before launch |
| 10 | **M-1 — Lightbox focus trap missing** | Documented known gap; must be closed before launch |
| 11 | **H-4 — CHANGELOG.md stale** | Breaks audit trail integrity |
| 12 | **H-5 — ARCHITECTURE.md stale variables/facts** | Stale docs lead to developer errors |
| 13 | **M-2 — Form validation gaps (phone, date, hours)** | Required when backend is connected |
| 14 | **H-6 — Pexels images; verify licensing** | Resolve OD-002 + confirm license terms |
| 15 | **L-1 — No favicon** | Quick win; unprofessional without it |

---

## 7. Open Questions

**OQ-1 — RESOLVED: "Program page" refers to a different site/version**  
Confirmed by user: the Program page is not part of this codebase. It belongs to a different site or a version of the site not present in this repo. The audit of this codebase is complete without it. No findings from this repo apply to the Program page.

**OQ-2: Is `hello@jonesbarbershop.com` a real, monitored inbox?**  
`docs/CONTENT.md` flags phone and address as placeholders but does not flag this email. Is it real?

**OQ-3: Are the barber names real employees or fictional?**  
Marcus Jones, Renee Carter, Devin Moore, Trey Collins — which (if any) are real? This affects the placeholder replacement scope.

**OQ-4: Are any of the six testimonials real customers?**  
Chris M., Jasmine T., Marcus & Little MJ, Deon L., Anthony R., Kevin D. — real or invented? Determines whether there is a FTC compliance issue.

**OQ-5: Have the hero stats been confirmed by the shop owner?**  
"150+ Weekly cuts" and "★ 5 Rated" are explicit examples that `docs/CONTENT.md` flags as requiring owner confirmation before use.

**OQ-6: RESOLVED — `prefers-reduced-motion` is confirmed absent**  
Grep of full `index.html` returned zero matches. This is a confirmed Medium finding, not an open question.

---

*Audit complete. No code, patches, or implementation steps will be produced until fixes are explicitly requested.*
