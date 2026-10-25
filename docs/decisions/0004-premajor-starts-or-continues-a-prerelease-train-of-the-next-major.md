---
status: accepted
date: 2026-10-25
decision-makers:
  - maintainers
applies-to:
  - scripts/compute-version.sh
  - action.yml
  - README.md
issues:
  - vscheuber/version-bump-action#1
---

# premajor starts or continues a prerelease train of the next major

## Context and problem statement

Preparing the next major version needs prereleases that do not look like patches of the current one. Recorded retroactively from #1.

## Decision

- `premajor` turns a stable base into the first prerelease of the next major (`4.18.0` to `5.0.0-1`, published with tag `next`).
- A base that is itself an `X.0.0` prerelease continues the train (`5.0.0-1` to `5.0.0-2`, `5.0.0-rc.1` to `5.0.0-rc.2`, `5.0.0-beta` to `5.0.0-beta.1`); any other base starts a new train.
- The tag scan treats `premajor` like `prerelease`, so an active next-major train is picked up as the base, while unrelated prerelease trains are rejected by the `X.0.0` guard.

## Consequences

- The sibling actions accept `premajor` too: npm-trusted-publish-action treats it exactly like `prerelease`.
