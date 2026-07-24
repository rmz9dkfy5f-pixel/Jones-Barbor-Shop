# Repository Handoff Configuration

Adapted from `20_TOOLS/KITS/handoff-repository/templates/TEMPLATE_REPOSITORY_HANDOFF_CONFIG.md` (in
the AntBrainOS vault) for the Jones Barber Shop repository. Store operational coordinates here,
never credentials.

## Repository Identity

- Project name: Jones Barber Shop
- Repository root: /Users/ant/Projects/GitHub/Jones-Barbor-Shop
- Canonical remote: https://github.com/rmz9dkfy5f-pixel/Jones-Barbor-Shop.git
- Default branch: main
- Canonical handoff file: `CONTEXT.md` (stable background) + `PROGRESS_NOTE.md` (rolling
  per-release milestone) + `STATUS.md` — this repo has no single `HANDOFF_TO_CLAUDE.md` equivalent;
  its own `CLAUDE.md` documents this split explicitly

## Validation Contract

- Install command: none — static HTML/CSS/JS site, no build step, no framework, no package manager
  (per this repo's own `ARCHITECTURE.md`)
- Focused test commands: none automated — see `docs/TESTING.md`'s manual QA checklist
- Full test command: none automated
- Lint/type-check commands: none
- Production build command: none
- Runtime smoke test: manual visual check + booking widget health check
  (`https://jones-barbor-shop.craftandconscious.com/api` returns `{"status":"ok"}`)
- Manual or device checks: full QA checklist in `docs/TESTING.md` before any release touching
  `index.html` or the booking widget

## Snapshot Contract

- Snapshot required: yes
- Naming rule: final_tag (this repo's own convention:
  `vMAJOR.MINOR.PATCH__codename-slug__commit-SHORTHASH`, per `COMMIT_NOTES.md`)
- Exclusions: none
- Verification method: file listing + SHA-256 checksum manifest
- Checksum requirement: yes
- Retention policy: keep indefinitely (real client project) — manual review before any deletion
- Restore/rollback procedure: this repo has its own `ROLLBACK_PLAN.md` — defer to it; otherwise
  re-clone from GitHub at the tag or restore from the snapshot's checksum-verified copy

### Snapshot Destination by Machine

Same `RepoBackups/<name>` convention already used for `AntBrainOS` and `K_to_Career_Website`.

```bash
scutil --get ComputerName 2>/dev/null || hostname
```

| Machine | Detection | Snapshot destination | Notes |
|---|---|---|---|
| Ant’s Mac Mini (4) | `/Volumes/AntNVMe1TB` exists | `/Volumes/AntNVMe1TB/WorkSync/Projects/RepoBackups/Jones_Barber_Shop/` | current machine |

If the current machine does not match any row above, or more than one row could plausibly match,
**stop and ask the user** for the correct destination — do not guess or infer a path pattern.

## Deployment Contract

- Deployment in scope: **yes** — real IONOS VPS deployment exists and is live
- VPS/server alias: IONOS VPS `74.208.9.49` (`jones-barbor-shop.craftandconscious.com`)
- Deployment root: `/var/www/jones-barbor-shop/` (static site); booking API at
  `/srv/booking-platform/` (separate `booking-platform` repo, systemd service)
- Deployment branch or artifact: `main` branch, static files copied to server root; booking API
  deployed separately via its own repo
- Service/container names: `booking-platform.service` (systemd), Nginx (reverse proxy `/api/` →
  `127.0.0.1:3001`)
- Read-only health checks: `curl https://jones-barbor-shop.craftandconscious.com/api` → expect
  `{"status":"ok"}` (read-only, safe to run without authorization)
- Log locations: not documented in this config — see server directly if authorized to access it
- Rollback target: see this repo's own `ROLLBACK_PLAN.md`
- **Actions requiring approval: any file copy to `/var/www/jones-barbor-shop/`, any
  `systemctl restart/reload booking-platform`, any Nginx config change, any `.env` edit on the VPS —
  all require separate, explicit, per-session authorization. Not authorized this session.**

## Safety Boundaries

- Protected paths: `Jones Barbor Shop.css` (legacy duplicate, not an active stylesheet — do not
  touch, per this repo's own `CLAUDE.md`)
- Secret-bearing files: VPS `.env` (Stripe/Resend/Twilio keys, when added) — never in this repo,
  never in this config
- Prohibited actions: force-push to `main`, rewriting published history, deploying without separate
  explicit authorization, restarting the live booking-platform service without separate explicit
  authorization
- Commit/push authorization rule: authorized per the Repo Push Super Prompt's authorization envelope
- Tag/release authorization rule: authorized_by_super_prompt
- Deploy/merge authorization rule: requires_separate_explicit_authorization — **not granted this
  session; this pilot stage is explicitly non-deploying**
