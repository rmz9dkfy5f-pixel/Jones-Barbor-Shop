# Testing

## Purpose

Defines the QA checklist and manual testing process for the Jones Barber Shop website.

## What Belongs Here

Manual QA steps, browser/device testing expectations, and validation rules before each push.

## What Does Not Belong Here

Deployment steps (see `docs/DEPLOYMENT.md`), accessibility audit (see `docs/ACCESSIBILITY.md`), implementation code.

---

## Testing Approach

This is a static site with no automated test suite. All testing is manual. Run the checklist below before committing any change that touches `index.html`.

## Pre-Commit Checklist

### General

- [ ] Open `index.html` in Chrome (desktop)
- [ ] Open `index.html` in Firefox (desktop)
- [ ] Open `index.html` in Safari (if on macOS)
- [ ] Test mobile viewport at 375px width (Chrome DevTools)
- [ ] Test tablet viewport at 768px width

### Navigation

- [ ] Sticky header remains visible on scroll
- [ ] All nav links scroll to the correct section
- [ ] "Book Now" CTA scrolls to `#booking`
- [ ] Mobile hamburger toggles the nav panel open and closed
- [ ] Mobile nav closes after selecting a link

### Sections

- [ ] Hero: headline, subtitle, CTA buttons, and metrics card all render correctly
- [ ] About: four key-point cards visible
- [ ] Services: six service cards with correct pricing
- [ ] Barbers: four barber profile cards with bios and badges
- [ ] Gallery: six images render; lightbox opens on click
- [ ] Pricing: six pricing cards; "Most Booked" and "Premium" badges visible
- [ ] Booking: form fields visible; labels paired with inputs
- [ ] Location: hours table, address, and map placeholder visible
- [ ] Reviews: four testimonial cards visible
- [ ] Footer: nav links, social icons, and dynamic copyright year

### Interactive Features

- [ ] Gallery lightbox: opens on image click
- [ ] Gallery lightbox: closes on Escape key
- [ ] Gallery lightbox: closes on click outside the image
- [ ] Booking form: required fields prevent submission when empty
- [ ] Booking form: form shows success state when submitted (even if no backend)
- [ ] Footer year: displays current year (not a hardcoded value)

### Responsive

- [ ] No horizontal scroll at 375px
- [ ] Nav collapses to hamburger below 768px
- [ ] All card grids collapse to single column on mobile
- [ ] Hero section readable and CTA accessible on mobile

## Accessibility Spot Check

- [ ] Tab through the page — all interactive elements reachable
- [ ] Booking form completable via keyboard
- [ ] Lightbox closable via Escape key
- [ ] No obvious contrast failures (dark text on dark background)

## Before Production Launch (one-time)

- [ ] All placeholder images replaced with real photography
- [ ] Real address, phone, and email in place
- [ ] Testimonials verified or replaced
- [ ] Meta title and description added
- [ ] Open Graph tags added
- [ ] Favicon added
- [ ] Contrast audit run on all text/background combinations
- [ ] Booking form connected to a real submission handler

---

*Status: Active*
*Created: 2026-05-04*
