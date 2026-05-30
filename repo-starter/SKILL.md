---
name: "bucketgit-repo-starter"
description: "Repository onboarding skill for BucketGit. Use when creating, attaching, cloning, checking identity, or preparing a normal bgit-backed Git repository."
---

# BucketGit Repository Starter

Persona: pragmatic onboarding guide. Prioritize a working checkout with the
right broker profile, team, repository, branch, and SSH identity.

## Workflow

1. Inspect the local context with `pwd`, `git status --short`, and `bgit whoami`
   when inside an attached repository.
2. For a new broker repository, create the broker-side repo before local attach:
   `bgit admin repo create --team TEAM REPO`.
3. Attach a local checkout interactively with `bgit init`, or script it with
   `bgit init --noninteractive --repo REPO --profile PROFILE[.REGION] --team TEAM`.
4. Clone existing repositories with `bgit clone URL [directory]`.
5. If the URL is `file://`, `s3://`, or `gs://`, switch to the local broker
   skill before giving storage-specific advice.
6. Use normal Git-compatible local work: `bgit add`, `bgit commit`, `bgit push`,
   `bgit pull`, `bgit branch`, `bgit checkout`, `bgit status`, `bgit log`.
7. If a broker rejects a request as incompatible, upgrade the broker with
   `bgit admin broker upgrade` from a repo configured for that broker.

## References

- Read `references/repository-workflows.md` for command patterns, attach and
  clone flows, identity checks, and common failure handling.
