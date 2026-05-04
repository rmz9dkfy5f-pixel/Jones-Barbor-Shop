# Performance

## Purpose

Defines performance expectations and asset strategy for the Jones Barber Shop website.

## What Belongs Here

Image strategy, loading rules, external dependency decisions, and performance benchmarks.

## What Does Not Belong Here

Visual design (see `docs/DESIGN.md`), deployment (see `docs/DEPLOYMENT.md`), implementation code.

---

## Current State

The site is a single HTML file (~69KB) with no build step, no JavaScript framework, and no external CSS framework. CSS and JS are inline. Performance overhead is low by default.

**Primary performance risk:** External Pexels CDN images — these are placeholders and introduce external dependency load times.

## Image Strategy

| Image | Current Source | Status | Action |
|---|---|---|---|
| Hero background | Pexels CDN | Placeholder | Replace with optimized local image |
| Barber headshots (4) | Pexels CDN | Placeholder | Replace with real photography |
| Gallery images (6) | Pexels CDN | Placeholder | Replace with real shop photos |
| Map placeholder | Pexels CDN | Placeholder | Replace with real map embed or screenshot |

**Rules for production images:**
- WebP format preferred; JPEG as fallback
- Max width: 1200px for full-bleed; 600px for cards
- Compress before committing — aim for <200KB per image
- Store in `/assets/images/` (create this folder when real images are ready)
- Use descriptive filenames: `hero-shop-exterior.webp`, not `IMG_001.jpg`

## Lazy Loading

- Add `loading="lazy"` to all images below the fold once real images are in place
- Hero image should remain eager-loaded (above the fold)

## External Dependencies

| Dependency | Type | Status | Notes |
|---|---|---|---|
| Pexels CDN | Image hosting | Placeholder only | Remove at launch |
| System fonts | Typography | Confirmed | No external font load |
| Google Fonts | — | Not used | Do not add without justification |
| Analytics scripts | — | Not used | Add only with owner approval |
| Third-party JS | — | Not used | No CDN-hosted JS libraries |

## CSS and JS

- All CSS and JS are inline — no separate file requests
- No render-blocking external stylesheets
- JS is at the bottom of `<body>` — non-blocking
- Minification: not required for current file size; consider if file grows significantly

## Performance Targets (pre-launch)

| Metric | Target |
|---|---|
| First Contentful Paint | < 2s on 4G |
| Largest Contentful Paint | < 3s on 4G |
| Total page weight | < 1MB with real images |
| External requests | 0 (after images are local) |

---

*Status: Active*
*Created: 2026-05-04*
