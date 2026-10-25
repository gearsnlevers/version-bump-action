---
status: accepted
date: 2026-10-25
decision-makers:
  - maintainers
applies-to:
  - action.yml
  - scripts/compute-version.sh
  - README.md
---

# The action computes release metadata and changes nothing

## Context and problem statement

A release needs its next version and tag decided in one place, apart from the steps that edit files, tag and publish. Recorded retroactively from the README, `.github/agentic-workflows/scope.md` and the sibling actions.

## Decision

- The action computes the next semantic version and tag from a release type and outputs them: `newVersion`, `newTag`, `preRelease`, `publishTag` (`next` for a prerelease, `latest` otherwise), `action_release_type` (`prerelease` or `full`, for the changelog action) and where the base came from (`base`, `base_source`, `base_ref`). The default release type is `prerelease`.
- It does not update `package.json` or lock files, create tags or releases, or publish. Those are other actions: version-bump-action (computes the version), release-preflight-action (checks collisions and drift), manifest-version-update-action (writes the version), ai-changelog-action (writes the changelog) and npm-trusted-publish-action (publishes).
- Versioning other than semantic versioning, or a base taken from anything but git tags, an explicit input or `package.json`, needs a maintainer's decision.

## Consequences

- Callers keep working through compatibility outputs (`normalized`, `tag`, `is_prerelease`) beside the documented ones.
