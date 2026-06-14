# Project Risk Register

Use this to track risks that could affect correctness, security, delivery, maintainability, data safety, client trust, or deployment stability.

## Risk Rating

| Level | Meaning |
|---|---|
| Low | Minor inconvenience or cleanup issue |
| Medium | Could slow delivery or create visible defects |
| High | Could break core functionality, data, deployment, or trust |
| Critical | Could cause data loss, security exposure, production outage, or irreversible damage |

## Open Risks

| ID | Risk | Area | Impact | Likelihood | Level | Mitigation | Owner | Status |
|---|---|---|---|---|---|---|---|---|
| JBS-001 | Placeholder content (address, phone, photos) goes live | client content | High | Medium | High | Replace all placeholders before production launch | TBD | Open |
| JBS-002 | Single `index.html` file makes large changes high-risk | architecture | Medium | Medium | Medium | Break work into small reviewed slices | TBD | Open |
| JBS-003 | No automated tests — regressions go undetected | testing/verification | Medium | Medium | Medium | Manual QA per `docs/TESTING.md` before each push | TBD | Open |
| JBS-004 | External CDN dependencies (Google Fonts) create load risk | dependency/versioning | Low | Low | Low | Fonts are display-only; site degrades gracefully | TBD | Open |
| JBS-005 | GitHub Pages outage affects site availability | deployment | High | Low | Medium | No mitigation — accepted platform risk | TBD | Open |

## Closed Risks

| ID | Risk | Resolution | Date closed |
|---|---|---|---|
| JBS-R01 | `.DS_Store` tracked in git | Removed with `git rm --cached`, `.gitignore` updated | 2026-05-04 |
| JBS-R02 | File with invalid Windows path (colon in name) tracked in git | Removed with `git rm --cached` | 2026-05-04 |

## Risk Categories

Use these categories when adding risks:

- scope drift
- architecture
- data/schema
- imports/exports
- auth/security
- secrets/privacy
- deployment
- dependency/versioning
- testing/verification
- performance
- accessibility
- client content
- documentation drift
- AI workflow/process

## Review Cadence

Review this file:

- before implementation of risky work
- after bugs
- before deployment
- before dependency upgrades
- before client handoff
- at the end of each major slice
