# Repo Health Check

Use this before major work, after starter-kit migration, and before cleanup/refactor work.

## Snapshot

| Field | Value |
|---|---|
| Date | 2026-06-14 |
| Repo name | Jones-Barbor-Shop |
| Branch | main |
| Latest commit | `b7ef9d8` |
| Current version | v1.14.0 (Sub-Agents) |
| Starter kit version | v3.3 (fully integrated) |
| Health status | Healthy — post-audit |

## Detected Stack

| Area | Detected value | Evidence |
|---|---|---|
| Language/runtime | HTML/CSS/JS (vanilla) | `index.html`, no build tool |
| Framework | None | Single-file static site |
| Package manager | None | No `package.json` |
| Build tool | None | No build step |
| Test framework | None | Manual QA per `docs/TESTING.md` |
| Lint/typecheck | None | No toolchain |
| Deployment target | GitHub Pages | `docs/DEPLOYMENT.md` |
| Database/storage | None | Static site |
| Auth/session model | None | No backend |

## Important Files

| Purpose | File/path | Notes |
|---|---|---|
| App entry | `index.html` | Single deployable file |
| Main routes/pages | `index.html` | One-page site |
| Components | Inline in `index.html` | No component system |
| State/data | Inline JS in `index.html` | No external state |
| Config | `ARCHITECTURE.md` | Structural truth |
| Tests | `docs/TESTING.md` | Manual QA checklist |
| Docs | `docs/` | Strategy, design, content, a11y, perf, versioning |
| Deployment | `docs/DEPLOYMENT.md` | GitHub Pages |

## Available Commands

| Command type | Command | Result |
|---|---|---|
| Install | N/A — no dependencies | N/A |
| Dev | Open `index.html` in browser | Manual |
| Build | N/A | N/A |
| Test | Manual per `docs/TESTING.md` | Manual |
| Lint | N/A | N/A |
| Typecheck | N/A | N/A |
| Format | N/A | N/A |

## Verification Status

| Check | Status | Evidence |
|---|---|---|
| Build | N/A | Static file, no build step |
| Tests | Manual | See `docs/TESTING.md` |
| Lint | N/A | No toolchain |
| Typecheck | N/A | No toolchain |
| Manual smoke test | Unknown | Run before each push |
| Security review | Unknown | Review before launch |

## Risks Found

| Risk | Level | Evidence | Mitigation | Status |
|---|---|---|---|---|
| Placeholder content (address, phone, barber names, images) | High | `index.html`, `docs/CONTENT.md`, `plans/open-decisions.md` | Replace before production launch | Open |
| No automated tests | Medium | No test toolchain | Manual QA per `docs/TESTING.md` | Open |
| Booking widget API URL set to localhost | Medium | `index.html` `data-api-url` attribute | Must be updated to production URL before launch | Open |
| Single-file architecture limits modularity | Low | `index.html` is 2,400+ lines | Accepted constraint per `ARCHITECTURE.md` | Accepted |
| `Jones Barbor Shop.css` at repo root | Low | 68 KB legacy file, not linked | Do not link or edit; remove with explicit plan approval | Open |

## Missing Information

- Confirmed production domain and DNS setup
- Real shop address, phone number, and barber photo releases
- Production booking API URL

## Recommended Next Cleanup

- Replace all placeholder content (address, phone, barber info) before launch
- Set production API URL in `index.html` before deploying booking widget
- Add real photography when available

## Recommended Next Slice

- Content: replace placeholder address, phone, and barber info in `index.html`

## Notes

This file is a repo baseline. Do not treat it as proof of correctness unless verification commands have actually been run.
