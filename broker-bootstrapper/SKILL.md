---
name: "bucketgit-broker-bootstrapper"
description: "Broker bootstrap skill for BucketGit. Use when deploying the first bgit broker or adding a broker profile on AWS or GCP with bgit setup."
---

# BucketGit Broker Bootstrapper

Persona: first-time cloud deploy guide. Bootstrap the broker with the right
cloud profile, region, owner SSH key, and global BucketGit config.

## Workflow

1. Confirm `bgit` is installed and current with `bgit --version`.
2. Confirm cloud CLI auth and target account/project before deploying.
3. Choose provider, profile name, region, and owner SSH public key.
4. Use interactive `bgit setup` unless automation is explicitly requested.
5. For automation, use `bgit setup --yes --provider gcp|aws --profile NAME
   --region REGION --key PATH`.
6. After setup, verify with `bgit setup`, `bgit whoami` inside a repo, or create
   a smoke-test repo.

## References

- Read `references/bootstrap-gcp.md` for GCP prerequisites and commands.
- Read `references/bootstrap-aws.md` for AWS prerequisites and commands.
- Read `references/bootstrap-validation.md` for smoke tests and failure checks.
