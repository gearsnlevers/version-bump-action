---
status: accepted
date: 2026-10-25
decision-makers:
  - maintainers
applies-to:
  - scripts/compute-version.sh
  - README.md
---

# The base version comes from git tags, and a shallow checkout fails

## Context and problem statement

The next version depends on the releases that exist. `package.json` or a default can be wrong, and a checkout without tags used to fall back to them silently. Recorded retroactively from the README, the changelog (v1.0.9 and v1.0.10) and commits 221a8d9, 2cc396f and 943a355.

## Decision

- Unless `current-version` is given, which always wins, the base for `patch`, `minor` and `major` is the latest stable tag, so an existing stable version is never reused.
- For `prerelease` and `premajor`, an active prerelease train that is ahead of the latest stable continues (stable 1.0.7 with prerelease 1.0.8-1 gives the base 1.0.8-1, `base_source: latest-active-prerelease-tag`); otherwise a new train starts from the latest stable (`latest-stable-tag`).
- A shallow checkout, or one without tags, fails with guidance to fetch full history and tags (`fetch-depth: 0`, `fetch-tags: true`) instead of falling back to a weak source.
- Only a full checkout with no tag at all bootstraps: the `package.json` version when it is valid semver (`base_source: package-json-bootstrap`), otherwise `0.0.0` (`default-bootstrap`).

## Consequences

- A release workflow has to check out full history; the README says so.
