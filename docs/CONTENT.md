# Content

## Purpose

Defines copy rules, tone, voice, CTA strategy, and metadata expectations for the Jones Barber Shop website.

## What Belongs Here

Writing guidelines, tone rules, content decisions, placeholder inventory, and metadata requirements.

## What Does Not Belong Here

Business strategy (see `docs/STRATEGY.md`), visual design (see `docs/DESIGN.md`), implementation code.

---

## Tone and Voice

- **Tone:** Direct, warm, confident — the voice of a shop that has been in the neighborhood for 28 years
- **Voice:** Authentic and community-first — not corporate, not trendy, not generic
- **Reading level:** Plain language — 7th to 8th grade
- **Avoid:** Chain-store marketing language, invented superlatives, vague promises

## Key Messages

- Sharp cuts. Real conversations.
- Neighborhood classic. 90s soul.
- Since 1998.
- Walk-ins welcome.
- Community, expertise, culture.

## CTA Strategy

| CTA | Location | Action |
|---|---|---|
| "Book Now" | Hero, sticky nav | Scrolls to `#booking` form |
| Phone number | Header, footer, location section | Direct call |
| "Walk-Ins Welcome" | Hero badge | Reassurance, no action required |
| "Book Your Cut" | Booking section | Submits form (currently non-functional) |

Primary conversion path: Book Now → form → shop visit.

## Content Inventory

| Section | Status | Notes |
|---|---|---|
| Hero headline | Active — placeholder | "Sharp Cuts. Real Conversations. Jones Barber Shop." |
| About | Active — placeholder | Since 1998, community, expertise, welcoming |
| Services (6) | Active — placeholder prices | Fades, tapers, line-ups, kids cuts, beard trims, designs, waves, locs |
| Barbers (4) | Active — fictional | Marcus Jones, Renee Carter, Devin Moore, Trey Collins |
| Gallery (6 images) | Placeholder | Pexels CDN images — must replace before launch |
| Pricing (6 cards) | Active — placeholder prices | $20–$65 range |
| Booking form | Active — no submit handler | Fields: name, phone, email, service, barber, date/time, notes |
| Location & Hours | Placeholder | 123 Fade Street (fictional), (919) 555-1234 (fictional) |
| Reviews (4) | Placeholder | Fictional testimonials — verify or replace before launch |
| Footer | Active | Social links (Instagram, TikTok, Facebook) — no real URLs |

## Placeholder Inventory

All of the following must be replaced with real content before production launch:

- [ ] Shop address: "123 Fade Street, Suite B, Joneswood District"
- [ ] Phone: "(919) 555-1234"
- [ ] Email: placeholder in booking form
- [ ] All 6 gallery images (Pexels URLs)
- [ ] Hero background image (Pexels URL)
- [ ] All 4 barber headshot images (Pexels URLs)
- [ ] Map placeholder image
- [ ] All 4 client testimonials (names and quotes)
- [ ] Social media URLs (Instagram, TikTok, Facebook)
- [ ] Barber names and bios (confirm if real or fictional)

## Metadata

Currently missing from `index.html` — add before production launch:

- `<title>` tag (currently placeholder)
- `<meta name="description">` — one sentence, 150–160 characters
- Open Graph tags (`og:title`, `og:description`, `og:image`, `og:url`)
- Canonical URL tag

## What Not to Claim

- Do not invent ratings counts or review platform scores
- Do not state award wins unless confirmed by the shop owner
- Do not inflate "150+ weekly cuts" without owner confirmation
- Do not use testimonial names that are not real or consented

---

*Status: Active*
*Created: 2026-05-04*
