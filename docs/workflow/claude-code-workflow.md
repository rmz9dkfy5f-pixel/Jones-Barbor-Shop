# Claude Code Workflow

## 1. Purpose

This document defines the repeatable working process Claude Code must follow when working in the Jones Barber Shop repo. It is not a strategy document. It is a procedure.

## 2. Required Start Procedure

Every session must begin with:

1. Confirm the repo root: `/Users/ant/Projects/GitHub/Jones-Barbor-Shop`
2. Inspect the top-level structure with `ls` or equivalent
3. Read `CLAUDE.md`
4. Read the canonical source-of-truth doc most relevant to the task
5. Check `git status` — confirm the working tree is clean before editing
6. Summarize current state before proposing any changes

## 3. Required Workflow Pattern

```
inspect → plan → approve → edit → validate → summarize
```

For git work:

```
check → fix → verify → commit → push
```

**inspect:** Read relevant files before proposing changes. The repo state wins over any assumption.

**plan:** Write a plan in `plans/YYYY-MM-DD-task-name.md` using `plans/PLAN_TEMPLATE.md` for non-trivial work.

**approve:** Get user approval for the plan or first slice before editing.

**edit:** Make only the approved slice changes. Nothing else.

**validate:** Run the narrowest useful check (open in browser, check links, verify markup).

**summarize:** Report what changed, what remains, and any risks.

## 4. Plan-First Rule

Before any non-trivial edit:

1. Create or update a plan in `plans/`
2. Filename format: `plans/YYYY-MM-DD-task-name.md`
3. Use `plans/PLAN_TEMPLATE.md`
4. List files to review
5. List files to change
6. Define slice boundaries
7. Define validation
8. Define rollback
9. Identify open questions

Do not start broad edits without a written plan in place.

## 5. Slice Approval Standard

Work must be broken into narrow slices. Get approval before each slice.

**Good slices:**
- One section of `index.html` (e.g. Services section only)
- One doc file
- One bug fix
- One CSS variable change
- One git operation

**Bad slices:**
- Redesign the entire page
- Update all docs and code at once
- Combine strategy, content, design, and implementation into one change
- Touch unrelated files

## 6. Inspection Rules

Before editing, Claude must inspect:
- Existing file content — never assume what is there
- CSS custom property values (all in `<style>` block of `index.html`)
- Current section markup before replacing it
- `ARCHITECTURE.md` before changing layout or structure
- `docs/STRATEGY.md` before changing copy or content
- `git status` before any commit operation

The repo state wins. If it differs from the plan, flag the difference before proceeding.

## 7. Editing Rules

- Make the smallest useful change
- Preserve existing intent and aesthetic
- Avoid unrelated formatting changes
- Do not create duplicate source-of-truth docs
- Do not add external dependencies without plan approval
- Do not use placeholder content as if it were real (fictional address, phone, images)
- Update relevant docs when structural or strategic decisions change

## 8. Validation Rules

After each meaningful slice, validate with the narrowest useful check:

- Open `index.html` in browser
- Check the specific section that changed
- Test mobile viewport (375px)
- Verify anchor links still work
- For JS changes: test the interactive feature
- For form changes: test validation behavior
- For git operations: run `git log --oneline -3` and `git ls-remote origin --tags` to confirm

If validation cannot run, explain why and provide the next best verification.

## 9. Rollback Rules

Every plan must define how to reverse the change.

Options:
- Revert the edited file to its prior state
- `git revert <commit>` for a clean undo
- Restore prior content from a tag snapshot
- Remove an added file or folder

## 10. Open Decisions

Use `plans/open-decisions.md` for decisions that block or materially affect the project.

Each entry must include:
- Decision needed
- Why it matters
- Options
- Recommended default
- Owner
- Status

## 11. When to Stop

Stop and ask for direction when:
- Requirements conflict
- A destructive change is needed (file deletion, large rewrite)
- Source-of-truth docs disagree with the request
- The requested task exceeds the approved slice
- Validation fails and the fix is not obvious
- Continuing would require inventing a business or technical decision

## 12. Completion Report

At the end of each slice:

- Files changed
- Summary of changes
- Validation performed
- Issues found
- Risks
- Next recommended action

---

*Status: Active*
*Created: 2026-05-04*
