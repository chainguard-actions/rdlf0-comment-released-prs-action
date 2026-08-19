<!-- markdownlint-disable -->

# Hardening Report: rdlf0--comment-released-prs-action/v3.1.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **rdlf0--comment-released-prs-action/v3.1.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow references `rdlf0/comment-released-prs-action@v3`, which is pinned to a mutable version tag rather than an immutable 40-character commit SHA. A tag can be moved to point to a different (potentially malicious) commit at any time, enabling supply-chain attacks.

Locations:

- `.github/workflows/main.yml:15`

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and the only job (`test_job`) also has no job-level `permissions:` key. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be broader than necessary (e.g., write access). A minimal explicit permissions block such as `permissions: contents: read` should be added.

Locations:

- `.github/workflows/main.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

1. Pinned `rdlf0/comment-released-prs-action@v3` to its full commit SHA `249f57bed533baa7f883fe9d9a834424f153c3cb` with a `# v3` comment for readability. 2. Added a top-level `permissions:` block with `contents: read`, `pull-requests: write`, and `issues: write` — the minimum permissions needed for the action to comment on released PRs and add labels.

