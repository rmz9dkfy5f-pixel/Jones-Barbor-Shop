# Deployment

## Purpose

Defines how the Jones Barber Shop website reaches its visitors, and how to put it back.

## What Belongs Here

Deployment steps, hosting configuration, environment variables, and rollback process.

## What Does Not Belong Here

Testing steps (see `docs/TESTING.md`), versioning rules (see `docs/VERSIONING.md`), implementation code.

> **Corrected 2026-11-18** from a read-only look at the server and from the booking platform's own records. The previous version said the site is deployed by pushing to GitHub Pages and that the booking API runs under PM2. Both were wrong for production: the live site is served by nginx on a VPS and changes only when files are copied there; the booking API runs under systemd. The authoritative description of the server and of the API release procedure is `docs/DEPLOYMENT.md` in the `booking-platform` repository (section 1 and section 6a).

---

## Hosting Target

**The live site** `https://jones-barbor-shop.craftandconscious.com/` is served by **nginx on the IONOS VPS** (`74.208.9.49`, Ubuntu).

| Item | Value |
|---|---|
| nginx site | `jones-barbor-shop` (`/etc/nginx/sites-available/`, enabled by symlink) |
| Web root | `/var/www/jones-barbor-shop/` (directory `www-data:www-data` 755) |
| Page | `index.html` in the web root |
| Widget files | `assets/` in the web root: the old `booking-widget.js` and `booking-widget.css` (kept), and the hash-named `booking-widget.<8 hex>.js`, `booking-widget.<8 hex>.css`, `booking-widget.theme.<8 hex>.css` that the page uses since 2026-11-18 |
| Caching | `location /` is `try_files $uri $uri/ =404` with no `expires` or `add_header`, so the server sends **no `Cache-Control`**; returning visitors can keep a file for days to weeks. This is why widget files carry their content hash in the name: a changed widget gets new names, and the page that names them is copied last |
| Git on the server | none (no `.git` in the web root) |
| SSH | `ssh -i ~/.ssh/jones_vps_rsa root@74.208.9.49` |

**GitHub Pages mirror (secondary).** Pages is enabled on this repository (checked with the GitHub API on 2026-11-18: legacy build, branch `main`, path `/`), so every push to `main` rebuilds a public copy at `https://rmz9dkfy5f-pixel.github.io/Jones-Barbor-Shop/`. It is **not** the live site. The production booking API allows requests only from the shop's own origin (its CORS response names `https://jones-barbor-shop.craftandconscious.com`), so a booking cannot be made from the mirror. A push to `main` therefore **never changes what the shop's customers see**; only copying files to the VPS does.

## Deployment Steps (static site)

Files are placed by hand, as root over SSH. Rules that came out of the 2026-11-18 widget release:

1. **Take the exact bytes from git**, not from the working copy: `git show <commit>:<path> > <staged file>`. The Windows working copy has CRLF line endings, which would not match a hash in a file name. Check the hash against the name (for `assets/booking-widget.<8>.js|css`, the first 8 hex of the file's SHA-256).
2. **Preflight, read only:** the target names and their temporary names (`.<name>.part`) are absent (or, for a replacement, the current file hashes as recorded); `nginx -t` passes; free disk; record the hash, size, owner and mtime of the live files.
3. **Add before you replace.** New asset files first, each written to `.<name>.part`, then `chown root:root`, `chmod 644`, the hash checked on the server, then `mv -n` to the final name (never overwrites). The page that names them goes **last**.
4. **Replacing a live file** (for example `index.html`) only after a snapshot of the whole web root: `cp -a /var/www/jones-barbor-shop /var/www/jones-barbor-shop.snapshot-pre-<id>-<UTC>` (a sibling directory, never served; the server's own convention). Write the new bytes to `.index.html.part`, check the hash, then `mv -f` it over `index.html` (an atomic rename within one directory).
5. **Verify:** public `GET` of each file returns 200 with the expected hash and content type; a before and after listing of every file (`find . -type f -printf '%p %s %U %m %T@\n' | sort`) differs only in the files you meant to change; `nginx -t`; the API's `NRestarts`; for the booking widget, load the public page and walk it to the time screen **without submitting**: submitting books for real.
6. Nothing in this procedure needs an nginx reload or a service restart.

Then land the repository change on `main` (a plain fast-forward after `git ls-remote`; never force) so the repository equals the server.

## Pre-Deployment Checklist

- [ ] Run the QA checklist from `docs/TESTING.md`
- [ ] Confirm `git status` is clean
- [ ] Confirm commit message follows conventional commit format
- [ ] Update `CHANGELOG.md` for release-worthy changes
- [ ] The owner has accepted the change (a live customer-facing page changes only on their word)
- [ ] Create and push tag: `vMAJOR.MINOR.PATCH__codename__commit-SHORTHASH` (when a release is cut)

## Environment Variables

No environment variables are required for the static site itself. The booking widget reads its config from three `data-*` attributes on the `<script>` tag in `index.html`: `data-api-url`, `data-service-id`, `data-location-id`.

Booking platform variables live in `/srv/booking-platform/.env` on the VPS (`root:root` 600, never committed, never printed). Production has only `DATABASE_URL`, `JWT_SECRET`, `CORS_ORIGIN`, `NODE_ENV`, `PORT`, `CUSTOMER_BASE_URL` (key names, checked 2026-11-18); none of the provider keys (Stripe, Resend, Twilio) are set.

## Booking Platform (API) Deployment

**Corrected 2026-11-18** (an earlier correction, dated 2026-07-24, said PM2; that was also wrong for production). The booking API runs as the **systemd** unit `booking-platform.service` (`node /srv/booking-platform/dist/server.js`, port 3001, `EnvironmentFile=/srv/booking-platform/.env`, logs with `journalctl -u booking-platform`). A stopped PM2 duplicate named `booking-platform` was deleted on 2026-10-15; other apps on the VPS still use PM2, this one does not. The database is the local PostgreSQL 16 on the VPS.

The API is **released from the `booking-platform` repository** by its own procedure (a build from a tag, a pre-deploy database dump, a release marker readable at `/api/release`, a restart with health checks), not by syncing source with `rsync` or running `npm install` on the server. Follow that repository's `docs/DEPLOYMENT.md` and its owner-authorization rule: every deploy needs the owner's explicit word. Never use `pm2 restart` for this app.

Adding Stripe, Resend or Twilio keys changes production configuration and starts real messages to real customers: it needs an approved plan in the `booking-platform` repository first (see its `plans/` and risk R-018). Do not edit `/srv/booking-platform/.env` by hand from this repository's instructions.

## Rollback

**Static site (what the 2026-11-18 release used).** The whole web root was copied to `/var/www/jones-barbor-shop.snapshot-pre-widget-v2-20261118T182440Z` before `index.html` was replaced. To put the old page back, copy that snapshot's `index.html` over the live one the same way (a temporary name, then `mv -f`), and check that it hashes (SHA-256 prefix) `c5806afedf8f20ec`. The old `assets/booking-widget.js` and `.css` were never removed, so the old page works at once. No restart, no database change. Keep a snapshot until the owner says it can go.

**Repository.** `git revert <commit-hash>` then a plain push (never a force push; a reset to a tag or a force push needs the owner's explicit approval). A revert changes the repository and the GitHub Pages mirror only; it does **not** change the VPS until the files are copied there.

**Booking API.** Per the `booking-platform` repository's `docs/DEPLOYMENT.md` section 6 (swap the previous release back, restart, check health). To stop the booking API without touching the static site: `systemctl stop booking-platform` on the VPS, owner's word first (customers then cannot book).

Tag snapshots provide a clean restore point for every release.

---

*Status: Active*
*Created: 2026-05-04*
*Corrected: 2026-11-18*
