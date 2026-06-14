# Phase Gates

Phase gates prevent uncontrolled building.

A phase is not complete because work was attempted. It is complete only when gate criteria pass.

---

## Gate 1 — Project Defined

Status:

```text
Complete
```

Pass criteria:

- [x] Project goal is written.
- [x] User/operator is identified.
- [x] Core action is defined.
- [x] Validation question is written.
- [x] Smallest useful version is defined.
- [x] Out-of-scope items are listed.
- [x] Risks and assumptions are listed.

---

## Gate 2 — First Slice Approved

Status:

```text
Complete
```

Pass criteria:

- [x] First vertical slice is selected.
- [x] Slice is small enough to verify.
- [x] Success criteria are testable.
- [x] Expected files are listed.
- [x] Check command is known.
- [x] Verification method is known.
- [x] Approval before changes is documented.

---

## Gate 3 — Technical Path Validated

Status:

```text
Complete
```

Pass criteria:

- [x] Hardest technical uncertainty has been tested.
- [x] Failure mode is understood.
- [x] Required access/config/paths are known.
- [x] Rollback path exists.
- [x] Findings are documented.

---

## Gate 4 — Minimum Usable Slice Complete

Status:

```text
Complete — site live at jones-barbor-shop.craftandconscious.com
```

Pass criteria:

- [x] Core action works.
- [x] User/operator can verify behavior.
- [x] System survives restart if relevant.
- [x] Errors are visible or documented.
- [x] `STATUS.md` is updated.
- [x] `SLICE_REVIEWS.md` is updated.
- [x] `PROGRESS_NOTE.md` is updated.
- [x] `COMMIT_NOTES.md` is updated.
- [x] Changes are committed and pushed if required.

---

## Gate 5 — Reliability Pass

Status:

```text
In progress
```

Pass criteria:

- [ ] Logging exists if needed.
- [ ] Error handling exists.
- [x] Backup/rollback path exists — git revert + ROLLBACK_PLAN.md.
- [ ] Basic tests or verification commands exist.
- [x] Security-sensitive defaults reviewed — no auth, static site.
- [ ] Known limitations documented — see PROJECT_RISK_REGISTER.md.

---

## Gate 6 — Polish and Expansion

Status:

```text
Not started
```

Allowed after this gate:

- UI polish
- extra features
- automation
- dashboard improvements
- multi-user support
- performance tuning
- advanced integrations
