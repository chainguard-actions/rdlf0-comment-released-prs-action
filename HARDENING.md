<!-- markdownlint-disable -->

# Hardening Report: rdlf0--comment-released-prs-action/v3.2.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **rdlf0--comment-released-prs-action/v3.2.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow references 'rdlf0/comment-released-prs-action@v3' using a mutable version tag instead of a pinned 40-character commit SHA. A tag can be moved to point to a different (potentially malicious) commit at any time, enabling supply-chain attacks.

Locations:

- `.github/workflows/main.yml:17`

### missing-permissions (severity: medium)

The workflow file has no top-level 'permissions:' key and the only job ('test_job') also has no job-level 'permissions:' key. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad. Minimal required permissions (e.g. 'contents: read') should be declared explicitly.

Locations:

- `.github/workflows/main.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

1. Pinned 'rdlf0/comment-released-prs-action@v3' to full commit SHA '249f57bed533baa7f883fe9d9a834424f153c3cb' with '# v3' comment for readability. 2. Added top-level 'permissions:' block with 'contents: read', 'pull-requests: write', and 'issues: write' — the minimum permissions needed for the action to comment on PRs and add labels.

