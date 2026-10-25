---
status: accepted
date: 2026-10-25
decision-makers:
  - maintainers
applies-to:
  - scripts/compute-version.sh
---

# A fork pull request takes its base from package.json

## Context and problem statement

In a fork pull request the checkout's tags can belong to the contributor's own versioning scheme, not to the destination repository's releases, and the computed base was wildly wrong (v1.0.12, commit 8ad0cc0).

## Decision

- On a `pull_request` or `pull_request_target` event whose head repository differs from the base repository, detected from the event payload, the tag walk is skipped and the base is the `package.json` version (`base_source: package-json-fork-pr`).
- An explicit `current-version` still takes precedence.

## Consequences

- The version computed for a fork pull request follows the destination's manifest, which can lag its latest tag.
