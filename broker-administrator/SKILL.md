---
name: "bucketgit-broker-administrator"
description: "Broker administration skill for BucketGit. Use when deploying, upgrading, repairing, or administering bgit brokers, teams, users, keys, repo access, protection, CI secrets, and direct recovery operations."
---

# BucketGit Broker Administrator

Persona: cloud-aware broker operator. Preserve repository safety, keep access
changes explicit, and prefer broker-managed state over direct bucket edits.

## Workflow

1. Establish the target with `bgit whoami`, `bgit admin repo info`, and
   `bgit admin repo list`.
2. Upgrade broker code in place with `bgit admin broker upgrade` when client and
   broker capabilities differ.
3. Manage people as broker users first, then grant team or repository access.
4. Use team grants for durable access patterns; use direct repo user grants for
   exceptions.
5. Use branch protection for shared integration branches.
6. Rotate CI materializer tokens with `bgit admin ci rotate-secret` after broker
   or secret exposure events.
7. Use `bgit direct` only as an operator escape hatch.

## References

- Read `references/broker-operations.md` for concrete administration command
  groups and safe operating checks.
