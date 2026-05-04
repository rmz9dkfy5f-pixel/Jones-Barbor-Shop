# Open Decisions

Tracks unresolved decisions that block or materially affect the Jones Barber Shop project.

---

## OD-001 — Real contact information

**Decision needed:** Replace fictional placeholder address, phone, and email with real shop info

**Why it matters:** The site cannot go live with fake contact details

**Options:** Owner provides real info / keep placeholders until launch

**Recommended default:** Keep placeholders, mark clearly in code and `docs/CONTENT.md`

**Owner:** Shop owner (Marcus Jones)

**Status:** Open

---

## OD-002 — Real photography

**Decision needed:** Replace Pexels placeholder images with real shop photography

**Why it matters:** Site is not production-ready with stock images

**Options:** Commission photography / use owner-provided photos / continue with Pexels temporarily

**Recommended default:** Owner provides photos; developer optimizes and replaces before launch

**Owner:** Shop owner

**Status:** Open

---

## OD-003 — Booking backend

**Decision needed:** Select a booking service or backend to connect the booking form

**Why it matters:** The booking form currently has no submission handler — visitors cannot actually book

**Options:** Square Appointments / Booksy / custom form handler (Netlify Forms, Formspree) / phone-only

**Recommended default:** Netlify Forms for simplest integration; escalate to Square if POS integration needed

**Owner:** Shop owner + CyberAntAI

**Status:** Open

---

## OD-004 — GitHub Pages deployment

**Decision needed:** Enable GitHub Pages in repo settings to deploy the live site

**Why it matters:** The site is ready to deploy but GitHub Pages is not yet confirmed as enabled

**Options:** Enable now / wait until placeholder content is replaced

**Recommended default:** Enable now for development preview; update URL in README.md

**Owner:** CyberAntAI

**Status:** Open

---

## OD-005 — Social media URLs

**Decision needed:** Add real Instagram, TikTok, and Facebook URLs to footer social links

**Why it matters:** Footer links currently point to `#` placeholders

**Options:** Owner provides real URLs / remove social icons until ready

**Recommended default:** Keep icons with placeholder `#` href; update when owner provides URLs

**Owner:** Shop owner

**Status:** Open

---

## OD-006 — Delete or keep `Jones Barbor Shop.css`

**Decision needed:** The file `Jones Barbor Shop.css` is a byte-for-byte duplicate of `index.html` and is not referenced anywhere

**Why it matters:** It is confusing and adds unnecessary size to the repo

**Options:** Delete it / rename it / keep it as-is

**Recommended default:** Delete it — it serves no function. Confirm with owner before deleting.

**Owner:** CyberAntAI

**Status:** Open

---

*Last updated: 2026-05-04*
