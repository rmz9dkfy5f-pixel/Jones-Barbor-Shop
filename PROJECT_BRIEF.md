# Project Brief

## Project Goal

A static single-page marketing and booking-inquiry site for Jones Barber Shop — a community barbershop operating in the Joneswood District since 1998.

---

## Problem

Walk-in clients, regulars, and families need a way to find the shop, see services and barbers, and book appointments online.

---

## User or Operator

- **Primary:** Walk-in clients, regulars, and families looking to book a haircut
- **Secondary:** Shop staff and owner managing the public-facing brand

---

## Core Action

A visitor can land on the site, see the shop's services and barbers, and submit a booking inquiry.

---

## Validation Question

Can a visitor find the shop, understand the services, and complete a booking request without confusion?

---

## Smallest Useful Version

A single deployable HTML page with: hero section, services, barber profiles, and a working booking widget linked to the booking API.

---

## Success Criteria

The project is initially successful when:

- [x] Site loads and renders on desktop and mobile
- [x] All major sections visible: hero, services, barbers, reviews, booking
- [x] Booking widget renders and accepts input
- [ ] Booking widget connects to live production API (pm2 on VPS port 3001)
- [ ] All placeholder content replaced with real shop data (address, phone, photos)
- [ ] Site passes manual QA per `docs/TESTING.md`

---

## Out of Scope For Now

- [ ] CMS for content updates
- [ ] Online payment integration
- [ ] Blog or news section
- [ ] Multi-language support
- [ ] Admin dashboard

---

## Biggest Risks

- [ ] Placeholder content (address, phone, images) goes live before replacement
- [ ] Booking API not deployed — widget fails all API calls
- [ ] No automated tests — regressions go undetected

---

## Assumptions

- [ ] Site will remain a single-file static HTML deployment
- [ ] Booking API will be hosted on the same IONOS VPS
- [ ] GitHub Pages or Nginx/IONOS VPS is the deployment target

---

## Approval State

Phase 1 planning approved?

```text
Yes — site is in active production
```

Phase 2 implementation approved?

```text
Yes — ongoing iterative improvements
```
