# Commit Notes

Documents the commit and release convention used in this repository.

## Commit Message Format

Conventional Commits style:

    <type>(<scope>): <short description>

Types: feat, fix, docs, style, refactor, chore

## Tag Format

    vMAJOR.MINOR.PATCH__codename-slug__commit-SHORTHASH

- Hash is the work commit, not the release notes commit
- Tag is applied to the release notes commit
- Every release gets: tag + commit + CHANGELOG entry + /releases/ snapshot

## Version Rules

- MAJOR — production-ready milestone
- MINOR — new feature or section
- PATCH — bug fix, docs, style, or chore

## No Co-Authored-By

Never add `Co-Authored-By:` trailers to commits in this repo.

## Push Protocol

Apply tag → push branch → push tag

    git tag vX.Y.Z__slug__commit-HASH
    git push origin main
    git push origin vX.Y.Z__slug__commit-HASH
