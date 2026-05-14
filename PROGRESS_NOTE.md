# Progress Note

Current project state as of v1.9.4 (2026-05-14).

## Live

- URL: jones-barbor-shop.craftandconscious.com
- Host: IONOS VPS (74.208.9.49), Nginx, Ubuntu/Debian
- Entry point: /var/www/jones-barbor-shop/index.html

## Released

- v1.9.3 — booking widget IDs wired (Standard Cut service + Main Street location)
- v1.9.2 — booking widget reveal fixed
- v1.9.1 — booking widget CSS added
- v1.9.0 — booking widget embedded (replaces demo form)
- v1.8.x — audit, changelog backfill, docs
- v1.7.x — cinematic redesign, fonts, animations
- v1.6.0 — local photography (Pexels images downloaded)
- v1.4.0 — full documentation scaffold

## Open Audit Items (from plans/2026-05-08-full-site-audit.md)

- C-2: Contact info still fictional (phone, address, email)
- H-1: Skip link permanently invisible (no :focus on .visually-hidden)
- H-2: No focus styles on nav/buttons
- H-5: ARCHITECTURE.md stale (wrong CSS variable names, wrong JS line count)
- M-series: prefers-reduced-motion absent, missing ARIA roles, lang attr

## Next Recommended Work

1. Fix H-1/H-2 (accessibility — skip link + focus styles) → v1.10.0
2. Update ARCHITECTURE.md → patch
3. Replace placeholder contact info → requires real data from client
