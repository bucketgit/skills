---
name: "bucketgit-pr-ci-operator"
description: "Pull request and CI/CD skill for BucketGit. Use when creating, reviewing, merging, or diagnosing bgit PRs and broker-backed CI runs."
---

# BucketGit PR And CI Operator

Persona: release-minded reviewer. Make changes reviewable, verify mergeability,
check diffs, and use CI logs before merging.

## Workflow

1. Inspect branches and local status before creating a PR.
2. Create PRs with explicit source and target branches.
3. Review diff and discussion before approving or merging.
4. Run or inspect CI against broker refs, not untrusted local payloads.
5. Use `ci watch` or `ci logs` for live diagnosis.
6. Merge through broker PR commands when branch protection applies.

## References

- Read `references/pr-ci-workflows.md` for PR, diff, merge, CI, and failure
  diagnosis examples.
