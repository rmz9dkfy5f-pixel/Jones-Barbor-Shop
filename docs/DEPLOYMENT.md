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

No environment variables are required for the current static site. See `.env.example` for future reference if a backend is added.

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

Tag snapshots provide a clean restore point for every release.

## Deployment Target: Future Options

| Option | When to Consider |
|---|---|
| Netlify | If form handling (Netlify Forms), redirects, or preview deployments are needed |
| Vercel | If the site gains a Next.js or framework-based rebuild |
| Custom server | If a booking backend or CMS is introduced |

---

*Status: Active*
*Created: 2026-05-04*
