# Plan: New booking widget, first on a parallel page, then on the live page

Date: 2026-11-18. Status: **DRAFTED LOCALLY on branch `feat/new-booking-widget-parallel-page`; NOT pushed, NOT deployed.** Nothing in this plan reaches the live site until the owner says so, per slice.
Written for: the owner.
Parent plan (the real plan and its approval live in the booking platform repository): `booking-platform/plans/2026-11-18-release-widget-r017-and-provider-readiness-r018.md`, approved by the owner 2026-11-18 ("approve the plan and go with the defaults"), slice 1 only. Its Model Selection Brief covers this work.

## 1. Objective

Put the rebuilt booking widget (grouped times, accessibility, "Add to calendar") on the Jones page in the shop's dark gold look, without ever making the live booking page the test bed, and with a one-file way back.

## 2. Request Summary

**In scope:** three new versioned asset files, a parallel page `booking-next.html` (not linked, `noindex`), and the proposed change to `index.html` (kept as a separate, unlanded commit).
**Out of scope:** any deploy or copy to the VPS (the owner's word, in the platform plan's slices 3 and 4); nginx or cache-header changes; the stale `docs/DEPLOYMENT.md` (to be corrected from what the server inspection finds); changing the page's content, copy or layout.

## 3. Current State (verified 2026-11-18)

- The live `index.html`, `assets/booking-widget.js` and `assets/booking-widget.css` equal this repository's `main` once carriage returns are ignored (SHA-256 prefixes `c5806afedf8f20ec`, `2c9d82a2ae196c5d`, `bb2499ce3347a308`).
- The page loads the stylesheet by `<link>` and the script by `<script src>` from unversioned paths; the server sends no `Cache-Control`, so returning visitors may keep old files for days to weeks.
- About 29 inline `.bw-*` rules (a 2,442-character block) recolour the OLD widget class by class; four of the classes no longer exist in the new widget.
- Three of the shop's colour pairs failed WCAG 2.1 AA (white on the red button 4.06:1, "no times" text 3.30:1, input border 1.78:1).

- **Server facts (read-only SSH look, 2026-11-18, nothing changed):** the web root is `/var/www/jones-barbor-shop` (nginx site `jones-barbor-shop`; directory owned by `www-data`; the page and the old widget files owned by uid 501, group `staff`, with their original times, so they were copied from the owner's Mac); there is no git checkout; the nginx site sets no `expires` or `add_header`, hence no `Cache-Control`; the live SHA-256 prefixes equal this repository's `main`. New files are therefore copied as root over SSH with mode 644 and checked by SHA-256 on the server. Full findings: booking-platform `plans/2026-11-18-release-widget-r017-and-provider-readiness-r018.md`, section 15, Slice 2.

## 4. Source-of-Truth Docs Reviewed

`CLAUDE.md`, `CHANGE_CONTROL.md` (deployment is "ask before editing": this branch does not touch deployment), `docs/TESTING.md` (manual checklist, to be run by the owner on the parallel page), `docs/DEPLOYMENT.md` (stale; not relied on).

## 5. Files to Change

| File | Change | Risk |
|---|---|---|
| `assets/booking-widget.39815412.js`, `assets/booking-widget.70e439a1.css`, `assets/booking-widget.theme.856c0ad2.css` (new) | the built widget, its stylesheet, the shop theme; names carry the first 8 hex of each file's SHA-256 | low (new files beside the old; nothing overwritten) |
| `booking-next.html` (new) | the page with the new files wired in, `noindex`, title prefixed `[Preview]` | low |
| `index.html` (separate commit) | links the new stylesheet and theme in that order, replaces the 29 colour rules with a 3-rule layout block, loads the new script | **high** (the live page) |
| `CHANGELOG.md`, this plan | records | low |

Full SHA-256 of the built files (from a clean export of booking-platform commit `fed5f34`, reproduced byte for byte against a working-tree build):
- script `3981541277fa2304d7bc951aea330ed4db3b46446a8c6392eed0ca039957a902` (161,013 bytes)
- stylesheet `70e439a1238bc7a86954e681897895048eab025bdaa27d13e14323f2bd4ef823` (6,063 bytes)
- theme `856c0ad2a6d7f30913a6a66d4c6e8e26e7e426cd839eeff594168e5dad95902a` (`widget/themes/jones.css`)

## 6. Slice Plan

### Slice 1 (commit 1): additive files and the parallel page

**Planned edits.** The three assets and `booking-next.html`, nothing else. Safe to place on the server beside the live files: nothing existing changes.
**Validation (done, in jsdom against two real APIs; not a browser).** The page loads from a local web server with its real `<link>` and `<script src>` tags and the shop's three data attributes pointed at a throwaway API: the widget mounts; the stylesheet is linked before the theme; no unversioned widget file is referenced; the theme colours are the ones in force (`--bw-primary` `#c73b3f`, `--bw-bg` `#0d0d14`); no leftover rules for removed classes; `noindex` and the `[Preview]` title present; no widget script errors. 12 of 12 pass. The same checks run against today's `index.html` fail 7 of 10, as they should.
**Stop condition.** The owner's by-hand pass on the parallel page (phone and desktop screenshots beside the live page, keyboard-only, 200% zoom, a screen reader, the `.ics` in real calendar apps), per the platform plan's slice 3. Placing the files on the server is the owner's go-ahead, not part of this plan.

### Slice 2 (commit 2): cutover of `index.html`

**Planned edits.** `index.html` takes the same content as `booking-next.html` without the `noindex` tag and the `[Preview]` title. The new `index.html` is copied to the server last, after the new assets are already there. The old `booking-widget.js` and `.css` stay on the server. Before `index.html` is replaced the whole web root is copied to a sibling directory, `cp -a /var/www/jones-barbor-shop /var/www/jones-barbor-shop.snapshot-pre-widget-v2-<UTC>` (the server's own convention for other sites; never served), so rolling back is copying `index.html` back from that snapshot.
**Validation.** 10 of 10 on the same smoke test; after the copy, public `GET` hashes equal this repository's files; the owner confirms the page.
**Stop condition.** The owner's go-ahead for this slice, after slice 1 is accepted.

## 7. Rollback

Slice 1: delete the three assets and `booking-next.html`. Slice 2: copy `index.html` back from the snapshot directory (the old script and stylesheet were never removed), or revert the cutover commit and copy that. No restart, no database change.

## 8. Risks

| Risk | Mitigation |
|---|---|
| Browser caches mixing old and new files | new, hash-named files for all three; the page naming them is copied last; old files kept |
| A new element unreadable on the dark surface | the theme is a tested set of colour variables (WCAG 2.1 AA); the parallel page is reviewed by the owner before the live one |
| The selected time is now red (the widget uses one colour for the primary button and the selected time); on the old page it was gold | shown to the owner on the parallel page; a separate variable is a possible later change to the widget |
| The jsdom checks miss a visual problem | they prove wiring, not looks; the owner's screenshots and walk-through are the gate |

## 9. Open Questions

None here; the defaults for Q1 to Q8 are recorded in the parent plan.

## 10. Approval Checkpoint

> Nothing in this branch is deployed, pushed or landed. Slice 1's files may be placed on the server, and slice 2 landed and copied, only on the owner's word for each.

## 11. Completion Notes

*To be filled when slices 1 and 2 are placed and accepted.*
