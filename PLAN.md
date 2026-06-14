# Plan

This is the active project plan.

Do not use this for every possible future idea. Use `BACKLOG.md` and `ROADMAP.md` for that.

---

## Planning Rule

Plan only as far as needed to reach the next phase gate.

---

## Active Objective

Unblock production deployment: deploy booking API to VPS, update `data-api-url`, replace placeholder content.

---

## Current Validation Question

Is the live site at `jones-barbor-shop.craftandconscious.com` serving real content with a working booking widget?

---

## Current Vertical Slice

### Slice Name

Production deployment — booking API

### Purpose

Deploy the booking-platform API to the VPS (PM2 on port 3001) so the booking widget functions end-to-end on the live site.

### User/Operator Outcome

Visitors can submit a booking inquiry through the widget on the live site.

### Systems Touched

- [ ] Documentation
- [ ] UI
- [ ] API (booking-platform on VPS)
- [ ] Database
- [ ] Filesystem (`index.html` data-api-url update)

### Final Work Deferred

- [ ] Replace placeholder content (phone, address, barber info, photos)
- [ ] Accessibility fixes (H-1 skip link, H-2 focus styles, M-series)

---

## Success Criteria

This slice is done when:

- [ ] booking-platform API running on VPS (PM2, port 3001)
- [ ] `index.html` `data-api-url` updated to `http://74.208.9.49:3001`
- [ ] Updated files uploaded to `/var/www/jones-barbor-shop/`
- [ ] Booking widget tested end-to-end on live site
- [ ] Changes committed, tagged, and pushed

---

## Expected Files To Change

- [ ] `index.html` — update `data-api-url` attribute

---

## Out of Scope

Do not build these during this slice:

- [ ] Placeholder content replacement
- [ ] Accessibility fixes
- [ ] Any visual/layout changes

---

## Next Slices

1. Deploy booking API to VPS (current)
2. Replace placeholder content (phone, address, barber bios, photos)
3. Accessibility pass (skip link, focus styles, ARIA roles)
4. Production photography swap
