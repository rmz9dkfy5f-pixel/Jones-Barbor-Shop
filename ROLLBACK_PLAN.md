# Rollback Plan

Use this file to preserve an escape path for migrations, risky changes, dependency updates, refactors, and deployment work.

## Current Change

| Field | Value |
|---|---|
| Date | 2026-06-16 |
| Branch | main |
| Commit | `1394ef5` |
| Change type | Production deployment — HTTPS booking API connection, `data-api-url` update |
| Risk level | Medium — live site now makes real API calls; checkout fails without Stripe keys |
| Person/agent making change | Claude Code |

## Pre-Change State

v1.14.0. `data-api-url` was `http://localhost:3000` (no live booking connection). Widget loaded but all API calls failed.

## Booking API Rollback (VPS)

If the booking platform needs to be taken offline:

```bash
ssh -i ~/.ssh/jones_vps root@74.208.9.49
systemctl stop booking-platform
systemctl disable booking-platform
```

To revert `data-api-url` in the website:
```bash
# In index.html, change data-api-url back to http://localhost:3000
# Then commit and push
git revert 1394ef5
git push origin main
```

To redeploy the booking platform:
```bash
systemctl enable booking-platform
systemctl start booking-platform
systemctl status booking-platform
```

## VPS Deployment State (v1.15.0)

- Service file: `/etc/systemd/system/booking-platform.service`
- App directory: `/srv/booking-platform/`
- Environment: `/srv/booking-platform/.env` (chmod 600)
- Database: `postgresql://booking_platform:***@localhost:5432/booking_platform`
- Port: 3001
- nginx config: `/etc/nginx/sites-enabled/jones-barbor-shop` (proxies `/api/` to port 3001)

## Files Added (audit slices B–F)

- `.nojekyll` — disables Jekyll on GitHub Pages
- `Documents/README.md` — marks Documents/ as legacy archive

## Files Modified (audit slices B–F)

- `index.html` — SVG favicon added to `<head>` (3 lines)
- `docs/VERSIONING.md` — release history table extended to v1.14.0
- `REPO_HEALTH_CHECK.md` — snapshot and risks updated to post-audit state
- `ROLLBACK_PLAN.md` — this file updated to reflect completed migration

## Files Moved

- None

## Files Quarantined

- None

## Files Not Touched Intentionally

- All site source code beyond favicon line in `index.html`
- `docs/STRATEGY.md`, `docs/DESIGN.md`, `docs/CONTENT.md`, `docs/ACCESSIBILITY.md`, `docs/PERFORMANCE.md`, `docs/TESTING.md`, `docs/DEPLOYMENT.md`
- `ARCHITECTURE.md`, `CLAUDE.md`, `CHANGELOG.md`, `AGENTS.md`
- `.claude/agents/` — all 7 agent specs unchanged

## Rollback Method

### Preferred Git Rollback

Use this only after confirming it will not discard unrelated work.

```bash
git status --short
git restore <file-path>
```

For a committed change:

```bash
git revert <commit-hash>
```

### Manual Rollback

1. Remove files listed under "Files Added" if they are not needed.
2. Restore modified files from git or backup.
3. Move quarantined files back only after review.
4. Rerun verification.

## Verification After Rollback

| Check | Command/Method | Expected Result | Actual Result |
|---|---|---|---|
| Git status | `git status --short` | Clean or expected changes only | TBD |
| Build | N/A (static site) | N/A | N/A |
| Test | Manual smoke test in browser | Site loads correctly | TBD |
| Manual smoke test | Open `index.html` | All sections render | TBD |

## Irreversible or High-Risk Actions

- None for this migration slice — all changes are additive new files only.

## Final Rollback Status

- [x] Rollback not needed — all changes additive or low-risk doc updates
- [ ] Rollback plan ready
- [ ] Rollback completed
- [ ] Rollback failed
- [ ] Needs human review
