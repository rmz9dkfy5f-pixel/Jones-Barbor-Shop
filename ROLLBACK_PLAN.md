# Rollback Plan

Use this file to preserve an escape path for migrations, risky changes, dependency updates, refactors, and deployment work.

## Current Change

| Field | Value |
|---|---|
| Date | 2026-06-14 |
| Branch | main |
| Current commit before change | TBD |
| Change type | v3.3 starter-kit migration (additive only) |
| Risk level | Low |
| Person/agent making change | Claude Code |

## Pre-Change State

```bash
# Record before changing files
git status --short
git branch --show-current
git rev-parse --short HEAD
```

## Files Added

- `DONE_CRITERIA.md`
- `CHANGE_CONTROL.md`
- `REPO_HEALTH_CHECK.md`
- `ROLLBACK_PLAN.md`
- `PROJECT_RISK_REGISTER.md`
- `ai/agents/AGENT_REVIEW_GATES.md`

## Files Modified

- None

## Files Moved

- None

## Files Quarantined

- None

## Files Not Touched Intentionally

- `index.html` — source code, not part of this migration slice
- All existing `docs/` files — not overwritten
- `ARCHITECTURE.md`, `CLAUDE.md`, `CHANGELOG.md` — not overwritten

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

- [ ] Rollback not needed
- [x] Rollback plan ready
- [ ] Rollback completed
- [ ] Rollback failed
- [ ] Needs human review
