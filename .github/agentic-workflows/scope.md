# Project scope

Read by the issue gate's scope check (Repo Concierge). The check is off for a repository without this file.

## Purpose

Compute the next semantic version and release tag from a release type (with a prerelease default) and guard against collisions.

## In scope

- Computing the next version and tag from `release-type`, including `premajor` and prerelease identifiers
- Deriving the current version from git tags, or from an explicit input, with the documented bootstrap and fork pull request behavior
- The action's inputs and outputs, documentation, tests, and release pipeline

## Out of scope

<!-- Every item here can close an issue automatically as not planned. Keep the list short and specific. -->

- Updating `package.json` or lock files, creating git tags or GitHub releases, or publishing. The action only computes release metadata; the release workflow handles the rest (stated in the README).

## Needs a maintainer

- Versioning schemes other than semantic versioning, such as CalVer
- Taking the current version from sources other than git tags, an explicit input or `package.json`

## Where to go instead

- Updating manifests: manifest-version-update-action. Preflight checks: release-preflight-action. Publishing: npm-trusted-publish-action.
