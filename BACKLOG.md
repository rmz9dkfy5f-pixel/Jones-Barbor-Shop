# Backlog

Use this for work queue control.

Do not let `BACKLOG.md` become the active plan. The active plan belongs in `PLAN.md`.

---

## Build Now

Required for the current phase gate.

- [ ] Complete v3.3 migration Group 2 (root tracking files — in progress)
- [ ] Complete v3.3 migration Group 3 (ai/ folder system)
- [ ] Complete v3.3 migration Group 4 (.claude/agents/ sub-agent roster)

---

## Build Next

Likely needed after the current slice.

- [ ] Deploy booking-platform API to VPS (PM2 on port 3001)
- [ ] Update `index.html` `data-api-url` to `http://74.208.9.49:3001`
- [ ] Upload updated `index.html` + assets to `/var/www/jones-barbor-shop/`
- [ ] Test booking widget end-to-end on live site

---

## Build Later

Useful but not needed yet.

- [ ] Replace Pexels placeholder images with real shop photography
- [ ] Add real barber headshots
- [ ] Add real shop address and map embed
- [ ] Update phone number and email to live contacts
- [ ] SEO meta tags and Open Graph setup
- [ ] Favicon and web app manifest
- [ ] Fix accessibility audit items (H-1, H-2, H-5, M-series)

---

## Maybe

Interesting but unproven.

- [ ] Blog or news section
- [ ] Online payment integration
- [ ] CMS for content updates

---

## Do Not Build

Rejected or harmful to current scope.

- [ ] Multi-language support (not in scope)
- [ ] Admin dashboard (not in scope)

---

## Scope Decision Rules

Every new idea must be placed into one category:

```text
Build now
Build next
Build later
Maybe
Do not build
```

If it does not support the current validation question, it should usually not be in `Build Now`.
