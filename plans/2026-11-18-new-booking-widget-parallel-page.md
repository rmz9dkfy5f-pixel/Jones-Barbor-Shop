# Plan: New booking widget, first on a parallel page, then on the live page

Date: 2026-11-18. Status: **Slice 1 PLACED ON THE SERVER as a preview on 2026-11-18** (the three asset files and `booking-next.html`, four new files, additive; owner: "do slice 3, put the parallel page on the server"). **Slice 2 (the cutover of `index.html`) was DONE on 2026-11-18** on the owner's written accept ("I accept, put the new widget on the live page"): the live page now uses the new widget (section 11). Slice 1's commits were landed on `main` first (`f04f1c6`), the cutover and these notes after the copy.
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

> Slice 1's files were placed and landed, and slice 2 was copied and landed, each on the owner's word (2026-11-18). Nothing further is pending in this plan.

## 11. Completion Notes

**Slice 2 executed 2026-11-18.** Bytes of `index.html` taken with `git show b67482f:index.html` (91,649 bytes, LF, sha256 prefix `5363991a9bd8401e`): the accepted preview page without the `noindex` tag and the `[Preview]` title (the only two differences, checked with `diff`). Read-only preflight on the server passed (the three live files still `c5806afedf8f20ec`, `2c9d82a2ae196c5d`, `bb2499ce3347a308`; the three new asset files present; no `.part` leftovers; `nginx -t` ok; `booking-platform` active, `NRestarts=0`; 57 GB free). Then `cp -a /var/www/jones-barbor-shop /var/www/jones-barbor-shop.snapshot-pre-widget-v2-20261118T182440Z` (its `index.html` is `c5806afedf8f20ec`), the new bytes streamed to `.index.html.part`, `root:root` 644, hash checked, and renamed over `index.html` (the only overwriting step).

**Verification.** Public `GET` of `/` and `/index.html` return 200 `text/html` with `5363991a9bd8401e`; the script, stylesheet and theme return the expected hashes and types; the old `booking-widget.js` and `.css` and `booking-next.html` are unchanged. A before and after listing of every file (path, size, owner, mode, mtime) differs in exactly one line, `index.html`; no other file changed. The page has no `noindex`, the normal title and no link to the preview. `nginx -t` ok, `NRestarts=0`, 0 journal entries at level 50 or above in the 15 minutes after, no new nginx error lines (today's lines are other sites on the server). The public page was walked in jsdom against the real production API up to the time screen, without submitting: 9 of 9 (new versioned files only, theme after the stylesheet, widget mounts, `--bw-primary` `#c73b3f`, 7 services, real times grouped Afternoon 9 and Evening 3, radio set with a legend, request button disabled, only GET requests).

**Rollback (not run).** `ssh -i ~/.ssh/jones_vps_rsa root@74.208.9.49` then, in `/var/www/jones-barbor-shop`, copy the snapshot's `index.html` back (`cp -p /var/www/jones-barbor-shop.snapshot-pre-widget-v2-20261118T182440Z/index.html .index.html.part && mv -f .index.html.part index.html`) and check it hashes `c5806afedf8f20ec`; the old widget files were never removed. No restart, no database change.

**Cleanup executed 2026-11-18 (owner: "do the cleanup, remove the preview page").** `booking-next.html` was removed from the server (its hash `ec1cb2997c543af8` checked first; `rm --` of that single path; public `GET` now 404; the listing of every other file is identical before and after; `nginx -t` ok; `NRestarts=0`) and from the repository (restore with `git show f04f1c6:booking-next.html`). `docs/DEPLOYMENT.md` was rewritten from verified facts. **Found while doing this:** GitHub Pages is enabled on this repository and rebuilds a public copy of `main` on every push, so the preview page, and later the new `index.html`, were also reachable at `https://rmz9dkfy5f-pixel.github.io/Jones-Barbor-Shop/`; the copy cannot book (the API's CORS allows only the shop's origin). Removing the page from `main` removes it from that copy once Pages rebuilds.

**Still the owner's.** Looking at the live page on a real phone and desktop. A selected time is red (one colour with the primary button), where the old page showed gold; a separate gold variable remains a possible later change in the widget.
