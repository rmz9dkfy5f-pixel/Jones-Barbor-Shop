# Plan

This is the active project plan.

Do not use this for every possible future idea. Use `BACKLOG.md` and `ROADMAP.md` for that.

---

## Planning Rule

Plan only as far as needed to reach the next phase gate.

---

## Active Objective

Complete Project Starter Kit v3.3 migration (Groups 2–4) and then unblock production deployment.

---

## Current Validation Question

Are all v3.3 tracking, AI memory, and sub-agent files installed without overwriting existing project files?

---

## Current Vertical Slice

### Slice Name

v3.3 Migration — Group 2: Root Tracking Files

### Purpose

Install 10 missing root-level tracking files from the v3.3 template layer.

### User/Operator Outcome

The repo has a full set of project control files so any AI agent or new contributor can orient immediately from `START_HERE.md`.

### Systems Touched

- [x] Documentation
- [ ] UI
- [ ] API
- [ ] Database
- [ ] Filesystem (new files only — no moves)

### Final Work Deferred

- [ ] Group 3 — ai/ folder system
- [ ] Group 4 — .claude/agents/ sub-agent roster
- [ ] Production deployment (API + index.html update)
- [ ] Replace placeholder content

---

## Success Criteria

This slice is done when:

- [x] Initial check has been run
- [x] All 10 Group 2 files created
- [x] No existing files overwritten
- [x] Tracking files updated
- [x] Changes committed and pushed
- [x] Release tagged

---

## Expected Files To Change

- [x] `START_HERE.md` — created
- [x] `PROJECT_BRIEF.md` — created
- [x] `PLAN.md` — created (this file)
- [x] `PHASE_GATES.md` — created
- [x] `BACKLOG.md` — created
- [x] `SLICE_REVIEWS.md` — created
- [x] `LESSONS_LEARNED.md` — created
- [x] `AGENTS.md` — created
- [x] `PROGRESS_NOTES.md` — created
- [x] `DECISION_LOG.md` — created

---

## Out of Scope

Do not build these during this slice:

- [ ] ai/ folder system (Group 3)
- [ ] .claude/agents/ roster (Group 4)
- [ ] Any changes to index.html
- [ ] Any changes to existing docs/

---

## Next Slices

1. Group 3 — ai/ folder system
2. Group 4 — .claude/agents/ sub-agent roster
3. Deploy booking API to VPS
4. Update data-api-url to production address
5. Replace placeholder content
