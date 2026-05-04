# Design

## Purpose

Defines the visual system and interaction rules for the Jones Barber Shop website.

## What Belongs Here

Color palette, typography, layout rules, spacing, animation, and design direction decisions.

## What Does Not Belong Here

Business strategy (see `docs/STRATEGY.md`), content rules (see `docs/CONTENT.md`), implementation code.

---

## Color Palette

All colors are defined as CSS custom properties in the `<style>` block of `index.html`.

| Variable | Value | Usage |
|---|---|---|
| `--bg-primary` | `#050509` | Page background |
| `--bg-secondary` | `#11111a` | Section backgrounds |
| `--bg-elevated` | `#181824` | Cards, modals, elevated surfaces |
| `--accent-red` | `#e0474c` | Secondary accent, badges |
| `--accent-blue` | `#3d6ee6` | Navigation highlights, links |
| `--accent-gold` | `#f5b544` | Primary CTAs, "Most Booked" badge, key highlights |
| `--text-primary` | `#f5f1e8` | Body copy, headings |
| `--text-secondary` | `#a09b8c` | Subtitles, supporting text |

**Rules:**
- Do not introduce new color values without updating this table and the CSS variables
- Gold is reserved for primary CTAs and premium highlights — do not overuse
- Do not introduce a light mode without a strategy-level decision

## Typography

- **Font stack:** System fonts — no external font dependencies
- **Headings:** Bold, uppercase or sentence case depending on section
- **Body:** Regular weight, `--text-primary` on dark backgrounds
- **Supporting text:** `--text-secondary`, smaller size

## Layout

- **Pattern:** Single-page vertical scroll with anchor navigation
- **Max-width:** Constrained content blocks centered on wide screens
- **Responsive:** Mobile-first — breakpoint at ~768px via media queries
- **Sticky header:** Glassmorphism effect (`backdrop-filter: blur()`), full width

## Spacing

- Section padding: generous vertical padding (~80px–120px desktop)
- Card grids: CSS Grid with responsive column collapse
- Gutters: consistent 1rem–2rem gap

## Visual Aesthetic

- **Identity:** 90s soul, neighborhood classic — dark, cinematic, warm
- **Effect:** Glassmorphism on header; radial gradient overlays on section backgrounds
- **Transitions:** `0.3s ease` standard for all hover/interactive states
- **Avoid:** Bright white backgrounds, generic barbershop stock aesthetics, over-animated UI

## Interaction Rules

- Hover states on all cards and buttons
- Gallery: lightbox opens on click; closes on Escape key or click outside
- Mobile nav: slides or toggles on hamburger click
- Booking form: client-side validation with inline error/success states

## Design References

Store visual references, screenshots, and brand assets in `design/references/`.
Store wireframes and layout sketches in `design/wireframes/`.

---

*Status: Active*
*Created: 2026-05-04*
