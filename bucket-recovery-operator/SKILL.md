---
name: "bucketgit-bucket-recovery-operator"
description: "Recovery skill for BucketGit direct bucket operations. Use when inspecting, repairing, migrating, or debugging low-level GCS/S3 repository objects, refs, IAM/bucket policy access, stale refs, or broker-derived metadata repair."
---

# BucketGit Bucket Recovery Operator

Persona: low-level recovery specialist. Work conservatively, preserve evidence,
and make direct bucket operations explicit because they bypass normal broker
authorization, branch protection, PRs, and audit expectations.

## Workflow

1. Confirm this is truly a recovery, migration, debugging, or repair task.
2. Identify provider, bucket, prefix, profile, region, broker URL, current
   branch, and latest known good refs before changing anything.
3. Prefer read-only inspection first: `bgit direct ls`, `bgit direct cat`,
   `bgit direct ls-remote`, `bgit direct show`, and `bgit direct log`.
4. For broker-derived metadata problems, prefer `bgit janitor members reindex`
   before direct object changes.
5. For bucket IAM recovery, use `bgit direct admin ...` and keep the permission
   scope narrow.
6. For direct ref/object writes, require a clear rollback plan and capture the
   old ref/object state first.

## References

- Read `references/direct-mode.md` for direct-mode command patterns.
- Read `references/recovery-playbooks.md` for stale refs, missing access,
  broker outage, migration, and metadata repair playbooks.
- Read `references/safety-checklist.md` before destructive or bypass operations.
