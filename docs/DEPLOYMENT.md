# Deployment

## Purpose

Defines how the Jones Barber Shop website is built and deployed.

## What Belongs Here

Deployment steps, hosting configuration, environment variables, and rollback process.

## What Does Not Belong Here

Testing steps (see `docs/TESTING.md`), versioning rules (see `docs/VERSIONING.md`), implementation code.

---

## Hosting Target

**GitHub Pages** — static hosting from the `main` branch, served from the repo root.

Entry point: `index.html` (repo root) — this is the default document served by GitHub Pages.

## Deployment Steps

### First-Time Setup

1. Push `main` branch to GitHub (already done)
2. Go to the repo on GitHub → **Settings** → **Pages**
3. Under **Source**, select branch: `main`, folder: `/ (root)`
4. Click **Save**
5. GitHub will provide a live URL: `https://rmz9dkfy5f-pixel.github.io/Jones-Barbor-Shop/`
6. Add this URL to `README.md`

### Ongoing Deployment

Every push to `main` automatically redeploys via GitHub Pages. No additional steps required.

```bash
git push origin main
```

## Pre-Deployment Checklist

Before pushing a release to `main`:

- [ ] Run full QA checklist from `docs/TESTING.md`
- [ ] Confirm `git status` is clean
- [ ] Confirm commit message follows conventional commit format
- [ ] Update `CHANGELOG.md` for release-worthy changes
- [ ] Create and push tag: `vMAJOR.MINOR.PATCH__codename__commit-SHORTHASH`

## Environment Variables

No environment variables are required for the static site itself. The booking widget reads its config from `data-*` attributes on the `<script>` tag in `index.html`.

Booking platform env vars are stored in `/srv/booking-platform/.env` on the VPS (not committed).

## Booking Platform Deployment

The booking API runs as a systemd service on the VPS alongside the static site.

### VPS Paths

| Item | Path |
|---|---|
| Static site root | `/var/www/jones-barbor-shop/` |
| Widget assets | `/var/www/jones-barbor-shop/assets/` |
| Booking platform app | `/srv/booking-platform/` |
| Booking platform env | `/srv/booking-platform/.env` |
| systemd unit | `/etc/systemd/system/booking-platform.service` |
| nginx config | `/etc/nginx/sites-enabled/jones-barbor-shop` |

### nginx Booking API Proxy Block

The following block lives inside the `jones-barbor-shop.craftandconscious.com` server block:

```nginx
location /api/ {
    proxy_pass http://127.0.0.1:3001/;
    proxy_http_version 1.1;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
    proxy_read_timeout 30s;
    proxy_connect_timeout 5s;
}
```

The trailing `/` on `proxy_pass` strips the `/api/` prefix before forwarding to the app.

### Updating the Booking Platform on VPS

```bash
# Build locally
cd /Users/ant/Projects/GitHub/booking-platform
npm run build

# Sync to VPS (excludes node_modules, .env, .git)
rsync -av --exclude=node_modules --exclude=.env --exclude=.git \
  --exclude=dist . root@74.208.9.49:/srv/booking-platform/
rsync -av dist/ root@74.208.9.49:/srv/booking-platform/dist/

# On VPS: install prod deps and restart
ssh -i ~/.ssh/jones_vps root@74.208.9.49
cd /srv/booking-platform && npm install --omit=dev
systemctl restart booking-platform
systemctl status booking-platform
curl -s https://jones-barbor-shop.craftandconscious.com/api/health
```

### Updating Widget Assets

```bash
rsync -av /Users/ant/Projects/GitHub/Jones-Barbor-Shop/assets/ \
  root@74.208.9.49:/var/www/jones-barbor-shop/assets/
```

### Adding Stripe / Resend / Twilio Keys

```bash
ssh -i ~/.ssh/jones_vps root@74.208.9.49
nano /srv/booking-platform/.env
# Add: STRIPE_SECRET_KEY, STRIPE_WEBHOOK_SECRET, STRIPE_SUCCESS_URL, STRIPE_CANCEL_URL
# Add: RESEND_API_KEY, RESEND_FROM
# Add: TWILIO_ACCOUNT_SID, TWILIO_AUTH_TOKEN, TWILIO_FROM_NUMBER
systemctl restart booking-platform
```

## Rollback

To roll back to a prior release:

```bash
# Option 1: Revert the commit
git revert <commit-hash>
git push origin main

# Option 2: Reset to a prior tag (destructive — confirm with user)
git checkout <tag-name>
# Then create a new branch or force-push (requires explicit user approval)
```

To stop the booking API without touching the static site:

```bash
ssh -i ~/.ssh/jones_vps root@74.208.9.49
systemctl stop booking-platform
```

Tag snapshots provide a clean restore point for every release.

---

*Status: Active*
*Created: 2026-05-04*
