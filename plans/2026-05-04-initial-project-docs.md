# Plan: Initial Project Documentation Setup

## 1. Objective

Complete and validate the initial repo documentation scaffold created by executing `Documents/00 Core Documents/00_RUN_FIRST.md`. Documentation only — no source code changes.

## 2. Request Summary

- **What was asked:** Execute `00_RUN_FIRST.md` and build out the full doc scaffold
- **In scope:** All docs listed in `REPO_PLANNING.md` — strategy, architecture, design, content, accessibility, performance, testing, deployment, versioning, workflow, plans, and Claude operating guide
- **Out of scope:** Source code changes to `index.html`, booking backend, deployment, image replacement

## 3. Current State

**Scaffold created by `00_RUN_FIRST.md` execution:**

| File | Status |
|---|---|
| `REPO_PLANNING.md` | Created — Active |
| `README.md` | Created — Active |
| `ARCHITECTURE.md` | Created — Active, real stack documented |
| `CLAUDE.md` | Created — Active, project-specific rules |
| `ROADMAP.md` | Created — Active |
| `CONTRIBUTING.md` | Created — Active |
| `.env.example` | Created — Active |
| `.claude/settings.json` | Created — Active |
| `docs/STRATEGY.md` | Created — Active, real site content |
| `docs/DESIGN.md` | Created — Active, real palette documented |
| `docs/CONTENT.md` | Created — Active, placeholder inventory |
| `docs/ACCESSIBILITY.md` | Created — Active, known gaps listed |
| `docs/PERFORMANCE.md` | Created — Active, image strategy |
| `docs/TESTING.md` | Created — Active, full QA checklist |
| `docs/DEPLOYMENT.md` | Created — Active, GitHub Pages steps |
| `docs/VERSIONING.md` | Created — Active, real version history |
| `docs/workflow/claude-code-workflow.md` | Created — Active |
| `plans/PLAN_TEMPLATE.md` | Created — Active |
| `plans/open-decisions.md` | Created — Active, 6 open decisions |
| `plans/2026-05-04-initial-project-docs.md` | This file |
| `design/README.md` | Created — Placeholder |
| `design/wireframes/README.md` | Created — Placeholder |
| `design/references/README.md` | Created — Active, design direction documented |
| `sample-data/README.md` | Created — Placeholder |
| `.github/PULL_REQUEST_TEMPLATE.md` | Created — Active |
| `.github/ISSUE_TEMPLATE.md` | Created — Active |

**Preserved (not overwritten):**
- `CHANGELOG.md` — non-empty, preserved
- `RELEASE_NOTES.md` — non-empty, preserved
- `index.html` — not touched
- `Jones Barbor Shop.css` — not touched

## 4. Source-of-Truth Docs Reviewed

| Doc | Status |
|---|---|
| `CLAUDE.md` | Created — reviewed |
| `docs/STRATEGY.md` | Created — reviewed |
| `ARCHITECTURE.md` | Created — reviewed |
| `docs/DESIGN.md` | Created — reviewed |
| `docs/CONTENT.md` | Created — reviewed |
| `docs/ACCESSIBILITY.md` | Created — reviewed |
| `docs/PERFORMANCE.md` | Created — reviewed |
| `docs/TESTING.md` | Created — reviewed |
| `docs/DEPLOYMENT.md` | Created — reviewed |
| `docs/VERSIONING.md` | Created — reviewed |

## 5. Assumptions

| Assumption | Why Reasonable | Risk if Wrong |
|---|---|---|
| Target repo is `/Users/ant/Projects/GitHub/Jones-Barbor-Shop` | Confirmed by `00_RUN_FIRST.md` | Low — path verified |
| Site content is Jones Barber Shop (barbershop, since 1998) | Derived from `index.html` | Low — confirmed from source |
| Placeholder content (address, phone, images) is intentional | Common in site builds | Low — flagged in `docs/CONTENT.md` and `open-decisions.md` |
| `Jones Barbor Shop.css` is a legacy duplicate, not in use | Not referenced in `index.html` | Low — confirmed by inspection |

## 6. Constraints

- Do not touch `index.html` or `Jones Barbor Shop.css`
- Do not overwrite non-empty existing files (`CHANGELOG.md`, `RELEASE_NOTES.md`)
- Do not write generated files into `Documents/` setup folder
- Do not invent business content — use only what is in `index.html`

## 7. Files to Review

| File | Why Review It |
|---|---|
| `index.html` | Source of all real project content |
| `CHANGELOG.md` | Existing — preserve, do not overwrite |
| `RELEASE_NOTES.md` | Existing — preserve, do not overwrite |
| `Documents/00 Core Documents/00_RUN_FIRST.md` | Execution controller |

## 8. Files to Change

*(All files in this plan were created new — none overwrote existing non-empty files)*

| File | Change | Risk |
|---|---|---|
| All scaffold files listed in section 3 | Created new | Low |

## 9. Slice Plan

### Slice 1: Scaffold creation (completed)
**Goal:** Create all scaffold files via `00_RUN_FIRST.md` execution order

**Files created:** See section 3

**Validation:** `git status` shows all new files; no existing files overwritten

**Stop condition:** Any file that already exists and is non-empty — skip and log

### Slice 2: Commit, tag, and push (next)
**Goal:** Commit all new scaffold files as a single versioned release

**Planned edits:**
- `git add` all new files
- Commit with `feat: scaffold project docs via 00_RUN_FIRST.md execution`
- Tag as `v1.4.0__blueprint__commit-SHORTHASH`
- Push branch and tag to `origin main`

**Validation:**
- `git log --oneline -3` confirms new commit
- `git ls-remote origin refs/tags/*` confirms tag on remote
- `git ls-tree -r --name-only HEAD` shows all new files on GitHub

## 10. Validation Plan

- [ ] `git status` — confirm all new files are untracked (ready to stage)
- [ ] `git diff --stat` — confirm no changes to existing files
- [ ] File count check — all 26 scaffold files present
- [ ] Spot-check 3 docs for real content (not empty placeholders)
- [ ] Confirm `CHANGELOG.md` unchanged

## 11. Rollback Plan

- All files are new — rollback means deleting them
- `git clean -f -d` would remove untracked files (use only if needed, with user confirmation)
- No existing files were modified — no revert needed

## 12. Risks

| Risk | Impact | Mitigation |
|---|---|---|
| Docs contain invented content | Misleading | All content derived from `index.html` — verified |
| Duplicate source-of-truth | Confusion | `REPO_PLANNING.md` section 8 prevents this |
| CHANGELOG.md overwritten | Data loss | Stop condition enforced — not overwritten |

## 13. Open Questions

See `plans/open-decisions.md` for all 6 open project decisions.

## 14. Approval Checkpoint

> Slice 2 (commit, tag, push) requires user approval before executing.

## 15. Version Impact

- [x] `minor` — new non-breaking documentation infrastructure

## 16. Completion Notes

*(To be filled after Slice 2)*

- What changed: Full documentation scaffold created
- Files changed: 26 new files
- Validation run: Pending Slice 2
- Next recommended slice: Commit, tag `v1.4.0__blueprint`, push
