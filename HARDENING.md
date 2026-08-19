<!-- markdownlint-disable -->

# Hardening Report: rdlf0--comment-released-prs-action/v3.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **rdlf0--comment-released-prs-action/v3.0.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file uses a mutable tag reference instead of a pinned 40-character commit SHA. `uses: rdlf0/comment-released-prs-action@v3` uses the tag `@v3`, which can be silently moved to point to different (potentially malicious) code at any time. It should be pinned to a full SHA, e.g. `uses: rdlf0/comment-released-prs-action@<40-char-sha> # v3`.

Locations:

- `.github/workflows/main.yml:16`

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and the only job (`test_job`) also has no job-level `permissions:` key. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad. A minimal `permissions:` block (e.g. `contents: read`) should be added at the top level or per-job.

Locations:

- `.github/workflows/main.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both findings in .github/workflows/main.yml: (1) Pinned `rdlf0/comment-released-prs-action@v3` to its full commit SHA `249f57bed533baa7f883fe9d9a834424f153c3cb` with a `# v3` comment for readability. (2) Added a top-level `permissions:` block with `contents: read` (for release event access), `pull-requests: write` (for commenting on PRs), and `issues: write` (for adding labels) — the minimum permissions required for this action to comment on released PRs and add labels.

