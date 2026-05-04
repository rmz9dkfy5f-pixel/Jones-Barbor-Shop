# CLAUDE.md

## Project Identity

This repository is for the **Jones Barber Shop** website — a static single-page marketing and booking-inquiry site for a community barbershop that has operated in the Joneswood District since 1998. The site presents real services, real barbers, and real shop culture to walk-in clients, regulars, and families. Do not invent decisions that the repository does not support. When strategy is ambiguous, flag it rather than guessing.

## Canonical Source-of-Truth Files

| File | Controls | Claude Must Use It For |
|---|---|---|
| `docs/STRATEGY.md` | Business/project direction | Audience, messaging, goals, brand voice, constraints |
| `ARCHITECTURE.md` | Technical structure | Stack, file layout, CSS variables, conventions, risks |
| `docs/DESIGN.md` | Visual system | Color palette, layout rules, aesthetic direction |
| `docs/CONTENT.md` | Content and copy rules | Tone, CTAs, metadata, what claims to avoid |
| `docs/ACCESSIBILITY.md` | Accessibility expectations | Semantic HTML, keyboard, focus, ARIA, contrast |
| `docs/PERFORMANCE.md` | Performance rules | Image strategy, loading, CDN dependencies |
| `docs/TESTING.md` | QA checklist | Manual testing steps before each push |
| `docs/DEPLOYMENT.md` | Release and deploy process | GitHub Pages steps, rollback, environment |
| `docs/VERSIONING.md` | Version bump rules | MAJOR/MINOR/PATCH decisions, release notes |
| `plans/` | Active task plans | Scoped execution, slice approval, validation |

## Working Mode

Follow this order for every non-trivial task:

1. Inspect the repo root and relevant canonical docs
2. Summarize current state
3. Create or update a plan in `plans/` using `plans/PLAN_TEMPLATE.md`
4. Get approval for the first slice
5. Execute one slice
6. Validate
7. Report what changed, what remains, and any new risks

For git-related work:

```
check → fix → verify → commit → push
```

Never skip the check step. Never push without a clean working tree.

## Planning Rules

- Use Plan Mode for any non-trivial task
- Create a plan file in `plans/` with filename format `YYYY-MM-DD-task-name.md`
- Use `plans/PLAN_TEMPLATE.md` as the base
- Break work into small slices — one section, one feature, one fix at a time
- Each slice must define: goal, planned edits, files affected, validation, stop condition
- Do not start broad edits without a written plan

## Editing Guardrails

Claude must not:
- Rewrite unrelated files
- Create duplicate source-of-truth documents
- Move files without updating all references
- Delete existing work without explaining why in the plan
- Invent business claims, metrics, testimonials, pricing, or capabilities not in the site
- Add external libraries or dependencies without plan-approved justification
- Combine strategy, design, content, and implementation into one unreviewed edit
- Touch `Jones Barbor Shop.css` — it is a legacy duplicate, not an active stylesheet
- Split `index.html` into separate files without a full approved plan

## Documentation Update Rules

| When this changes... | Update this file |
|---|---|
| Repo structure or tech stack | `ARCHITECTURE.md` |
| Business direction, audience, goals | `docs/STRATEGY.md` |
| Visual design or color rules | `docs/DESIGN.md` |
| Copy, tone, CTAs, content rules | `docs/CONTENT.md` |
| Accessibility approach | `docs/ACCESSIBILITY.md` |
| Performance strategy | `docs/PERFORMANCE.md` |
| QA/testing process | `docs/TESTING.md` |
| Deployment or build process | `docs/DEPLOYMENT.md` |
| Version bump or release | `docs/VERSIONING.md` + `CHANGELOG.md` |

## Repo Interpretation Rules

- Treat `docs/STRATEGY.md` as project truth — not a checklist, not optional reading
- Treat `ARCHITECTURE.md` as structural truth — inspect it before changing layout
- Treat files in `plans/` as temporary execution artifacts — not permanent docs
- Flag conflicts between docs and implementation instead of guessing
- Separate confirmed facts from assumptions explicitly
- Do not overwrite strategic ambiguity with invented certainty

## Content Rules

- Use direct, plain language rooted in real shop services and culture
- Do not fabricate metrics, testimonials, awards, or capabilities
- Do not change the 90s soul aesthetic without a strategy-level decision
- Keep CTAs explicit: "Book Now" and phone number are the primary actions
- Placeholder content (fictional address, phone, Pexels images) must be clearly marked as such and must be replaced before production launch

## Response Standard

When reporting work:
1. What was inspected
2. What was found
3. What changed
4. Files changed
5. Validation performed
6. Risks or follow-up
7. Next recommended slice

## Definition of Done

A task is not done until:
- Approved scope is complete
- Relevant canonical docs are updated if structure or strategy changed
- Validation has been run or skipped with a stated reason
- Changed files are listed
- Known risks are stated
- Next step is clear

## Project-Specific Rules

- Preserve the dark theme (`#050509` background) — do not introduce light mode
- Preserve the 90s soul brand identity — do not genericize the visual direction
- Do not replace placeholder content with invented content — mark it or leave it
- Keep `index.html` as the single deployable entry point
- Commit style: conventional commits (`feat:`, `fix:`, `docs:`, `style:`, `refactor:`)
- Tag format: `vMAJOR.MINOR.PATCH__slug__commit-SHORTHASH`
- Every release gets a tag, a commit, and updated `CHANGELOG.md`

---

*Status: Active*
*Created: 2026-05-04*
