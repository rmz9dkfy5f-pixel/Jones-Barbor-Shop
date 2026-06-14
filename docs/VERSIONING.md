# Versioning

## 1. Purpose

This document controls version bumps, release notes, and migration expectations for the Jones Barber Shop website. `CHANGELOG.md` records what changed. This file defines the rules for how and when versions change.

## 2. Version Format

Semantic versioning: `MAJOR.MINOR.PATCH`

Example: `1.3.0`

## 3. MAJOR Version Rules

Major versions mark breaking changes or stable production milestones.

Increment MAJOR when:
- The site reaches a confirmed production-ready state (real content, real images, real booking)
- A significant redesign changes the core visual identity
- A backend or CMS is introduced, changing how content is managed
- Backward compatibility with prior deployments is broken

Major releases must include migration notes explaining what changed and what needs to be updated in dependent systems or docs.

## 4. MINOR Version Rules

Minor versions mark new features that do not break existing behavior.

Increment MINOR when:
- A new page section is added (e.g. blog, FAQ, promotions)
- A new interactive feature is added (e.g. booking backend, lightbox upgrade)
- Real photography replaces placeholder images
- SEO meta tags, Open Graph, or favicon are added
- A new barber profile is added
- Non-breaking documentation infrastructure is added

## 5. PATCH Version Rules

Patch versions mark fixes and small non-breaking improvements.

Increment PATCH when:
- Bug fixes (JS behavior, form validation, nav toggle)
- UI polish (spacing, color adjustments, mobile tweaks)
- Text corrections or label changes
- Accessibility improvements to existing markup
- Non-breaking cleanup or refactor
- Documentation-only changes with no release impact use `none`

## 6. Non-Negotiable Rules

1. Every release gets release notes
2. No silent changes — all changes are committed and tagged
3. Patch does not mean feature
4. Major versions require migration notes
5. Version impact must be identified before completing a task
6. `CHANGELOG.md` must be updated for release-worthy changes
7. Every tag includes the real commit hash in its name

## 7. Relationship to CHANGELOG.md

- `docs/VERSIONING.md` (this file) — defines the rules
- `CHANGELOG.md` — records what changed, in what version, on what date
- Task plans should identify expected version impact before implementation begins
- Do not update `CHANGELOG.md` with invented history

## 8. Version Impact Labels

Use these labels in plans and completion notes:

| Label | When to Use |
|---|---|
| `none` | Documentation, planning, or internal tooling with no release impact |
| `patch` | Fix, polish, text change, minor cleanup |
| `minor` | New non-breaking feature, section, or significant content addition |
| `major` | Breaking change, production milestone, or significant architectural shift |

## 9. Release Codenames

Codenames are used for all releases in this project. They are paired with the version number and included in the tag name.

**Format:** `vMAJOR.MINOR.PATCH__codename-slug__commit-SHORTHASH`

**Release history:**

| Version | Date | Codename | Description |
|---|---|---|---|
| v1.0.0 | 2026-04-03 | Foundation | Initial website import and repo scaffolding |
| v1.1.0 | 2026-05-03 | Marquee | Rename entry point to `index.html`; add `RELEASE_NOTES.md` |
| v1.2.0 | 2026-05-03 | Stable-Changelog | Add `CHANGELOG.md` |
| v1.3.0 | 2026-05-04 | Docs-Scaffold | Add `Documents/` folder with planning and reference materials |
| v1.4.0 | 2026-05-04 | Blueprint | Full repo scaffold — `ARCHITECTURE.md`, `CLAUDE.md`, `docs/`, `plans/`, `design/` |
| v1.4.1 | 2026-05-04 | DS-Store-Ignore | Add `.DS_Store` to `.gitignore` |
| v1.5.0 | 2026-05-04 | Release-Notes-Vault | Add `releases/` folder with individual release note files |
| v1.6.0 | 2026-05-04 | Local-Photography | Add `pics/` with 15 Pexels images; swap CDN URLs for local paths |
| v1.7.0 | 2026-05-04 | The-Chair | Full cinematic redesign — fonts, animations, JS modules, all sections |
| v1.7.1 | 2026-05-04 | Lined-Up | Line-up and nav polish pass |
| v1.7.2 | 2026-05-04 | True-Line | Alignment and layout corrections |
| v1.8.0 | 2026-05-08 | Sharp-Eye | Full site audit and documentation review |
| v1.8.1 | 2026-05-08 | Full-Record | CHANGELOG backfill — all missing entries reconstructed |
| v1.8.2 | 2026-05-08 | Open-Book | RELEASE_NOTES.md backfill — full coverage v1.0.0–v1.8.1 |
| v1.9.0 | 2026-05-13 | Booking-Widget-Embed | Embed booking widget into `index.html` |
| v1.9.1 | 2026-05-13 | Fix-Widget-CSS | Fix widget stylesheet cascade issues |
| v1.9.2 | 2026-05-13 | Fix-Widget-Reveal | Fix widget section reveal/animation |
| v1.9.3 | 2026-05-14 | Fix-Widget-IDs | Fix duplicate element IDs in widget |
| v1.9.4 | 2026-05-14 | Open-Record | Backfill release records; update ROADMAP and PROGRESS_NOTE |
| v1.9.5 | 2026-05-14 | Prompt-Vault | Add `prompts/` folder with snapshot and commit templates |
| v1.9.6 | 2026-05-15 | Fix-API-URL | Correct booking widget API endpoint URL |
| v1.9.7 | 2026-05-15 | Full-Context | Backfill session records for v1.9.4–v1.9.6 |
| v1.9.8 | 2026-05-19 | Widget-Render | Fix widget rendering issues |
| v1.9.9 | 2026-05-19 | Dev-API-URL | Revert API URL to localhost for local development |
| v1.10.0 | 2026-05-20 | Three-Step | Redesign booking widget to 3-step flow with live API integration |
| v1.11.0 | 2026-06-14 | Quality-Gates | Install v3.3 quality gates — DONE_CRITERIA, CHANGE_CONTROL, REPO_HEALTH_CHECK, ROLLBACK_PLAN, PROJECT_RISK_REGISTER, AGENT_REVIEW_GATES |
| v1.11.1 | 2026-06-14 | State-Sync | Sync ROADMAP, STATUS, PROGRESS_NOTE, CONTEXT to v1.11.0 |
| v1.12.0 | 2026-06-14 | Root-Tracking | Install v3.3 root project control files — PHASE_GATES, BACKLOG, PLAN, DECISION_LOG, LESSONS_LEARNED, SLICE_REVIEWS, PROGRESS_NOTES |
| v1.13.0 | 2026-06-14 | AI-System | Install v3.3 AI engineering memory system — `ai/` folder with agents, sessions, templates |
| v1.14.0 | 2026-06-14 | Sub-Agents | Install v3.3 sub-agent roster — 7 Claude Code agents in `.claude/agents/` |

## 10. Agent Rules

Future AI/code agents must:
- Read this file before proposing a version bump
- Update `CHANGELOG.md` when release-worthy changes are made
- Include version impact label in task plans
- Not silently change version numbers
- Not invent release history
- Ask before bumping MAJOR versions
- Use the tag format: `vMAJOR.MINOR.PATCH__codename-slug__commit-SHORTHASH`

## 11. Open Questions

| Question | Status |
|---|---|
| Is `v1.0.0` the right starting version, or should the project start at `v0.1.0`? | Decided: `v1.0.0` — site was imported as a working product |
| What is the release cadence? | Open — driven by owner/developer availability |
| Are pre-production versions tracked separately? | Open — not currently needed |

---

*Status: Active*
*Created: 2026-05-04*
*Source: `Documents/01 Reference Documents/VERSIONING.md`*
