# Repo Planning

## 1. Project Summary

This repo contains the Jones Barber Shop website — a single-page static marketing and booking-inquiry site for a community barbershop located in the Joneswood District. The shop has been operating since 1998 and serves walk-in clients, regulars, and families. The site is not a web application. It does not have a backend, API, database, or authentication system. Current stage: existing codebase, actively maintained.

## 2. Repo Strategy

**Classification: Lean Website Repo**

A single HTML file with embedded CSS and JavaScript constitutes the entire frontend. There is no build step, no framework, no package manager, and no deployment pipeline beyond pushing to GitHub. A lean documentation set is appropriate. Enterprise folders, microservice infra, and API contracts are not justified.

## 3. Documentation Philosophy

- Fewer useful docs over many empty docs
- One source of truth per topic
- Root files stay minimal — only files that GitHub or collaborators need at the root level
- Detailed docs live in `/docs`
- Avoid duplicate files; if a doc exists in root it should not also exist in `/docs`
- Docs must reflect real project facts — no invented content, metrics, or features

## 4. Required Root Files

| File | Purpose | Why Root | What Not To Put Here |
|---|---|---|---|
| `README.md` | Public entry point for anyone visiting the repo | GitHub renders it on the repo homepage | Strategy details, architecture decisions |
| `CHANGELOG.md` | Release history following Keep a Changelog format | GitHub convention; already exists | Versioning rules (those go in `docs/VERSIONING.md`) |
| `ARCHITECTURE.md` | Technical structure of the site | Quick access for agents and collaborators | Business strategy, content rules |
| `CLAUDE.md` | Claude Code operating guide | Claude Code looks here first | Project business content |
| `ROADMAP.md` | Planned features and deferred decisions | Visible to collaborators | Implementation detail |
| `CONTRIBUTING.md` | How to contribute | GitHub convention | Process workflow |
| `REPO_PLANNING.md` | This file — repo setup decisions | Documents the repo strategy | Ongoing task plans |
| `RELEASE_NOTES.md` | Human-readable notes for the latest release | Already exists | Full changelog history |

## 5. Required `/docs` Files

| File | Purpose | Source-of-Truth For | Preserves |
|---|---|---|---|
| `docs/STRATEGY.md` | Business direction, audience, offering | Brand, messaging, goals | Who the shop is, who it serves, what it offers |
| `docs/DESIGN.md` | Visual system and interaction rules | Color palette, layout rules, typography | Dark theme, 90s soul aesthetic, glassmorphism |
| `docs/CONTENT.md` | Copy rules, tone, CTAs, metadata | All text in the site | Authentic voice, no fake metrics |
| `docs/ACCESSIBILITY.md` | Semantic HTML, keyboard, ARIA, contrast | Accessibility expectations | Current and future a11y decisions |
| `docs/PERFORMANCE.md` | Asset strategy, image optimization, loading | Performance rules | External image dependencies (Pexels) |
| `docs/TESTING.md` | QA checklist, validation steps | Manual QA process | How to test the site before each push |
| `docs/DEPLOYMENT.md` | How the site is deployed | Hosting target, push process | GitHub Pages steps |
| `docs/VERSIONING.md` | Semver rules, release codenames, bump logic | Version number decisions | MAJOR/MINOR/PATCH rules from reference doc |
| `docs/workflow/claude-code-workflow.md` | Step-by-step Claude Code process | Agent operating procedure | Plan-first, slice-approval workflow |

## 6. Required Workflow / Agent Files

| File | Decision |
|---|---|
| `CLAUDE.md` | **Create now** — active repo with Claude Code usage |
| `.claude/settings.json` | **Create now** — harness config needed |
| `docs/workflow/claude-code-workflow.md` | **Create now** — defines the working process |
| `plans/PLAN_TEMPLATE.md` | **Create now** — needed for all non-trivial future tasks |
| `plans/open-decisions.md` | **Create now** — captures unresolved project decisions |

## 7. Optional Files/Folders to Defer

| File/Folder | Trigger to Add |
|---|---|
| `docs/API.md` / `openapi.yaml` | If a booking API or CMS is added |
| `migrations/` | If a database is introduced |
| `infra/` / `terraform/` | If cloud infrastructure beyond GitHub Pages is used |
| `monitoring/` | If uptime monitoring or analytics dashboard is added |
| `localization/` | If the site serves multiple languages |
| `docs/SECURITY.md` | If a contact form backend, auth, or payment system is added |
| `CODEOWNERS` | If more than one developer is regularly committing |
| `LICENSE` | If the repo is made public and open source |
| `metrics/` | If performance data is tracked over time |
| `tech-debt/` | If technical debt becomes formally tracked |
| `mock-server/` | Not applicable — no backend |
| `graphql/schema.graphql` | Not applicable — no API |

## 8. Duplicate Source-of-Truth Prevention

| Topic | Official Location | Do Not Also Create |
|---|---|---|
| Versioning rules | `docs/VERSIONING.md` | `VERSIONING.md` in root, `version_number_system.md` |
| Business strategy | `docs/STRATEGY.md` | Root `STRATEGY.md` |
| Content rules | `docs/CONTENT.md` | Root `CONTENT.md` |
| Accessibility | `docs/ACCESSIBILITY.md` | Root `ACCESSIBILITY.md` |
| Security | `docs/SECURITY.md` (deferred) | Root `SECURITY.md` |
| PR template | `.github/PULL_REQUEST_TEMPLATE.md` | Root `PULL_REQUEST_TEMPLATE.md` |

## 9. Recommended Initial File Tree

```
Jones-Barbor-Shop/
├── index.html
├── Jones Barbor Shop.css
├── ARCHITECTURE.md
├── CHANGELOG.md
├── CLAUDE.md
├── CONTRIBUTING.md
├── README.md
├── RELEASE_NOTES.md
├── REPO_PLANNING.md
├── ROADMAP.md
├── .claude/
│   └── settings.json
├── .env.example
├── .github/
│   ├── ISSUE_TEMPLATE.md
│   └── PULL_REQUEST_TEMPLATE.md
├── Documents/
│   └── [setup documents — not executed on each run]
├── design/
│   ├── README.md
│   ├── references/
│   │   └── README.md
│   └── wireframes/
│       └── README.md
├── docs/
│   ├── ACCESSIBILITY.md
│   ├── CONTENT.md
│   ├── DEPLOYMENT.md
│   ├── DESIGN.md
│   ├── PERFORMANCE.md
│   ├── STRATEGY.md
│   ├── TESTING.md
│   ├── VERSIONING.md
│   └── workflow/
│       └── claude-code-workflow.md
├── plans/
│   ├── open-decisions.md
│   └── PLAN_TEMPLATE.md
└── sample-data/
    └── README.md
```

## 10. Scaffolding Instructions

```
ARCHITECTURE.md
CHANGELOG.md
CLAUDE.md
CONTRIBUTING.md
README.md
RELEASE_NOTES.md
REPO_PLANNING.md
ROADMAP.md
.claude/settings.json
.env.example
.github/ISSUE_TEMPLATE.md
.github/PULL_REQUEST_TEMPLATE.md
design/README.md
design/references/README.md
design/wireframes/README.md
docs/ACCESSIBILITY.md
docs/CONTENT.md
docs/DEPLOYMENT.md
docs/DESIGN.md
docs/PERFORMANCE.md
docs/STRATEGY.md
docs/TESTING.md
docs/VERSIONING.md
docs/workflow/claude-code-workflow.md
plans/open-decisions.md
plans/PLAN_TEMPLATE.md
sample-data/README.md
```

## 11. Agent Execution Rules

- Inspect before editing — read relevant docs before proposing any change
- Read `CLAUDE.md` at the start of every session
- Read `docs/STRATEGY.md` before any copy, brand, or content change
- Read `ARCHITECTURE.md` before any structural or layout change
- Create or update a plan in `plans/` before non-trivial work
- Avoid creating duplicate source-of-truth files
- Update relevant docs when architecture or strategy decisions change
- Do not delete existing work without stating why in the plan
- Do not create new docs unless justified by REPO_PLANNING.md
- Preserve the project's authentic 90s-soul aesthetic and community identity
- Validate after each slice before moving to the next

## 12. First Implementation Step

Create `README.md` using real project content from `index.html`. Keep it short: project name, one-line description, live URL placeholder, and tech stack. Do not build the full scaffold until `REPO_PLANNING.md` is reviewed and approved.

---

*Status: Active*
*Created: 2026-05-04*
