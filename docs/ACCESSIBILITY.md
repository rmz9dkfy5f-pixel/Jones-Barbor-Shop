# Accessibility

## Purpose

Defines accessibility expectations and requirements for the Jones Barber Shop website.

## What Belongs Here

Semantic HTML rules, keyboard navigation expectations, ARIA usage, contrast requirements, and known accessibility gaps.

## What Does Not Belong Here

Visual design (see `docs/DESIGN.md`), content rules (see `docs/CONTENT.md`), implementation code.

---

## Semantic HTML

- Landmark elements in use: `<header>`, `<nav>`, `<main>`, `<section>`, `<footer>`
- Headings: `<h1>` through `<h3>` used in hierarchy — do not skip heading levels
- Lists used for nav items and service/pricing cards where appropriate
- Form fields: `<label>` elements paired with all `<input>` and `<select>` fields

## Keyboard Navigation

- All nav links are focusable via keyboard
- "Book Now" and phone CTAs are keyboard-accessible
- Booking form fields are tab-navigable
- Mobile nav hamburger button must have visible focus state
- Gallery lightbox: currently closable via Escape key — confirm focus trap is implemented

## Focus Management

- Mobile nav open: focus should move to the first nav link inside the panel
- Gallery lightbox open: focus should move into the lightbox
- Modal/lightbox close: focus should return to the triggering element
- **Known gap:** Focus trap in gallery lightbox needs audit

## Color Contrast

- Background `#050509` with text `#f5f1e8` — high contrast, passes WCAG AA
- Secondary text `#a09b8c` on `#050509` — needs verification at small sizes
- Gold `#f5b544` on dark background — verify contrast ratio for CTA buttons
- **Action:** Run contrast audit on all text/background combinations before launch

## ARIA Usage

- Mobile nav hamburger: `aria-label="Toggle navigation"` present
- Gallery lightbox: verify `role="dialog"` and `aria-label` are present
- Form required fields: `required` attribute present; confirm error messages are announced

## Images

- All images require meaningful `alt` attributes
- Current Pexels placeholder images: verify `alt` text is descriptive, not empty
- Decorative images (backgrounds, overlays): use `alt=""` or CSS background-image

## Forms

- All form fields have `<label>` associations
- Required fields marked with `required` attribute
- Validation error messages: must be visible and programmatically associated
- Success/error states must not rely on color alone

## Known Gaps

| Issue | Priority | Action |
|---|---|---|
| Gallery lightbox focus trap | High | Audit and implement before launch |
| Contrast ratio for `#a09b8c` text | Medium | Run WCAG contrast check |
| Gold CTA button contrast | Medium | Verify `#f5b544` on dark meets AA |
| Image alt text audit | High | Audit all images before launch |
| Form error announcements | Medium | Verify screen reader compatibility |

---

*Status: Active*
*Created: 2026-05-04*
