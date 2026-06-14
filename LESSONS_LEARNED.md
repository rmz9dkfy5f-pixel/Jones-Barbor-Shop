# Lessons Learned

Use this file to improve future planning and execution.

This is not a changelog.

`CHANGELOG.md` records what changed.

`LESSONS_LEARNED.md` records what should be done better next time.

---

## Lesson Template

### YYYY-MM-DD — Lesson Title

Context:

> [What happened?]

Lesson:

> [What should be learned?]

Cause:

> [Why did it happen?]

Correction:

> [What should change next time?]

Reusable rule:

> [Turn the lesson into a future rule.]

---

## Lessons

### 2026-06-14 — Do not include "changelog and snapshot" in release note commit messages for docs-only commits

Context:

> The commit message for `v1.11.1` (`docs(release): v1.11.1 State Sync — changelog and snapshot`) incorrectly described a docs state-sync commit as updating the changelog and snapshot. The commit only updated ROADMAP, STATUS, PROGRESS_NOTE, and CONTEXT.

Lesson:

> Release note commit descriptions should accurately name what changed — not copy a boilerplate pattern.

Cause:

> Copied commit message pattern from a prior release that did update the changelog and snapshot.

Correction:

> Write the description based on what the commit actually changes. Use `— release note` as the suffix for `/releases/` file commits.

Reusable rule:

> `docs(release): vX.Y.Z Codename — release note` for new release note files. Not "changelog and snapshot" unless the changelog was actually changed.

---

### 2026-06-14 — Take the local backup snapshot before starting a group install

Context:

> Group 2 files were partially written before the user asked for a local backup snapshot. The snapshot was taken mid-write, capturing an inconsistent state.

Lesson:

> Always take the local RepoBackups snapshot before starting a new group install or any multi-file commit slice.

Cause:

> Snapshot step was not part of the install workflow — it was a separate user request that arrived mid-execution.

Correction:

> Add snapshot step to the pre-commit checklist for every release.

Reusable rule:

> Before any multi-file commit: snapshot first to `/Users/ant/WorkSync/Projects/RepoBackups/Jones Barbor Shop/<tag-name>/`.

---

### 2026-05-04 — Disk space on /private/tmp blocks Write and Bash tools

Context:

> ENOSPC errors blocked all Write and Bash tool calls. The `/private/tmp` volume was full, affecting both the Write tool's file operations and the Bash tool's output buffering.

Lesson:

> Both Write and Bash tools require free space on the system volume. If either fails with ENOSPC, clear disk space before continuing.

Cause:

> `/private/tmp` and the project disk share the same macOS volume. When full, all writes fail regardless of target path.

Correction:

> Check available disk space before large installs. Free space if below ~2GB.

Reusable rule:

> If Write or Bash fails with ENOSPC: clear disk space first, then retry. Do not attempt workarounds.
