# Contributing

## Purpose

Guidelines for contributing to the Jones Barber Shop website repo.

## What Belongs Here

How to propose changes, coding standards, and branch/PR expectations.

## What Does Not Belong Here

Project strategy, architecture decisions, deployment steps.

---

## Getting Started

1. Fork or clone the repo
2. Open `index.html` in a browser or start Live Server (port 5501)
3. Make changes to `index.html` (HTML, CSS in `<style>`, JS in `<script>`)

## Branching

- `main` — stable, deployable
- Feature branches: `feature/short-description`
- Fix branches: `fix/short-description`

## Commit Style

Use conventional commit prefixes:

```
feat: add barber profile section
fix: correct mobile nav close behavior
docs: update ARCHITECTURE.md
style: adjust hero padding for mobile
refactor: consolidate gallery JS into single function
```

## Pull Requests

- Use `.github/PULL_REQUEST_TEMPLATE.md`
- One concern per PR
- Include before/after screenshots for visual changes

## Code Standards

- No external libraries without a plan-approved justification
- Preserve the existing dark theme and CSS variable system
- Test on mobile and desktop before opening a PR
- Do not fabricate business content (real shop info only)

## Documentation

- Update `CHANGELOG.md` for release-worthy changes
- Update `ARCHITECTURE.md` if structure changes
- Update `docs/STRATEGY.md` if business content changes

---

*Status: Active*
