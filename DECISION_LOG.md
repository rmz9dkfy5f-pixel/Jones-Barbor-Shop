# Decision Log

Use this file for important decisions.

Do not use it for tiny task notes.

---

## Decision Template

### YYYY-MM-DD — Decision Title

Decision:

> [What did we choose?]

Reason:

> [Why did we choose it?]

Alternatives considered:

- [Alternative 1]
- [Alternative 2]

Risk:

> [What could go wrong?]

Review trigger:

> [When should we reconsider?]

Status:

```text
Active
```

---

## Decisions

### 2026-05-04 — Single-file HTML architecture

Decision:

> `index.html` is the single deployable entry point. All CSS and JavaScript are embedded inline. No build step, no framework, no bundler.

Reason:

> Simplest possible deployment for a static marketing site. GitHub Pages and Nginx both serve it directly. No toolchain means no toolchain failures.

Alternatives considered:

- React + Vite build
- Astro static site generator
- Separate CSS/JS files

Risk:

> File grows large and hard to maintain. Currently 2,400+ lines.

Review trigger:

> Reconsider if adding a CMS, multi-page routing, or complex component interactions.

Status:

```text
Active
```

---

### 2026-05-04 — Phase-gated vertical-slice planning with approval before file changes

Decision:

> Use phase-gated execution with a written approval step before any file edits. Every slice requires a written plan, stated scope, and explicit approval.

Reason:

> Prevents AI agents from overbuilding, editing unrelated files, or mixing planning with implementation. Keeps commits clean and reversible.

Alternatives considered:

- Freeform AI implementation
- Full upfront specification
- Single README-only planning

Risk:

> Process may feel heavy for trivial tasks.

Review trigger:

> Reconsider if the process slows down trivial tasks without reducing mistakes.

Status:

```text
Active
```

---

### 2026-05-04 — Placeholder content policy

Decision:

> Placeholder content (phone, address, email, Pexels images, fictional barber names) must remain clearly marked and must not be replaced with invented content. Replace only with real verified data.

Reason:

> Fabricating business information (metrics, phone numbers, addresses) would mislead real clients and damage trust.

Alternatives considered:

- Remove placeholders and leave fields blank
- Invent plausible-sounding placeholder data

Risk:

> Placeholder content ships to production if not caught before launch.

Review trigger:

> When real shop data is confirmed and ready to publish.

Status:

```text
Active
```

---

### 2026-06-15 — HTTPS path-prefix pattern for booking API

Decision:

> Serve the booking API at `https://jones-barbor-shop.craftandconscious.com/api` using nginx `/api/` path prefix stripping, rather than a separate subdomain.

Reason:

> The domain `jones-barbor-shop.craftandconscious.com` already had TLS configured. A path prefix avoids provisioning a new subdomain and a second Let's Encrypt cert. The nginx `proxy_pass http://127.0.0.1:3001/;` trailing slash strips the prefix cleanly.

Alternatives considered:

- Separate subdomain (`booking.jones-barbor-shop.craftandconscious.com`)
- Raw IP + port (rejected — not HTTPS)

Risk:

> Path prefix routing can break if nginx config is later edited without understanding the trailing-slash stripping rule.

Review trigger:

> If an admin subdomain is needed, revisit separate subdomain approach.

Status:

```text
Active
```

---

### 2026-06-15 — systemd over PM2 for booking platform process management

Decision:

> Use systemd (`booking-platform.service`) to manage the booking platform process on the VPS instead of PM2.

Reason:

> The existing Raleigh Spa app on the same VPS already uses systemd (`spa.service`). Matching that pattern keeps the server consistent and avoids installing PM2.

Alternatives considered:

- PM2 (documented in earlier planning — rejected for consistency)
- Docker Compose (not present on VPS)

Risk:

> No PM2 cluster mode — single-process only. Acceptable for current traffic.

Review trigger:

> If traffic grows and requires horizontal scaling or zero-downtime reloads.

Status:

```text
Active
```

---

### 2026-06-15 — Defer payments until Stripe keys are available

Decision:

> Deploy booking platform without Stripe/Resend/Twilio keys. Services are priced ($20–$65) but the checkout step will fail until keys are added.

Reason:

> Keys were not available at deployment time. Deferring avoids blocking the rest of the integration. The widget correctly shows services and availability; only checkout is broken.

Alternatives considered:

- Set all service prices to 0 temporarily (bypass Stripe)
- Wait for keys before deploying

Risk:

> Any customer who reaches the payment step will see an error. Must be resolved before promoting the booking widget publicly.

Review trigger:

> When Stripe keys are ready — add to `/srv/booking-platform/.env` and restart service.

Status:

```text
Active — Stripe keys pending
```

---

### 2026-06-14 — Commit project-starter-kit-v3.3 source to repo

Decision:

> The `project-starter-kit-v3.3/` reference folder is committed directly into the Jones Barber Shop repo rather than kept external.

Reason:

> The folder is actively used as the source for the ongoing v3.3 migration. Committing it keeps the migration source and the migrated repo in sync and traceable.

Alternatives considered:

- Keep the kit external (not committed)
- Add it to .gitignore

Risk:

> Adds 104 non-site files to a site repo, which may confuse future contributors.

Review trigger:

> After the v3.3 migration is complete. Consider moving to .gitignore once all templates have been installed.

Status:

```text
Active
```
