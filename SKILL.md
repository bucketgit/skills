---
name: "bucketgit-skills"
description: "BucketGit skill pack for agents using bgit repositories, broker administration, task boards, pull requests, CI/CD, and multi-agent collaboration. Use when working with BucketGit/bgit workflows from ordinary repository creation through broker operations."
version: 0.1.0
author: BucketGit
license: MIT
tags:
  - bucketgit
  - bgit
  - git
  - broker
  - collaboration
agents:
  - codex-cli
  - claude-code
---

# BucketGit Skills

Scenario skills for using `bgit` safely and effectively. Load only the skill
that matches the current task.

## Skills Overview

| Skill | Folder | Persona | Use When |
|-------|--------|---------|----------|
| Installer | `installer/` | Cross-platform setup helper | Installing or updating the `bgit` binary on macOS, Linux, or Windows |
| Broker Bootstrapper | `broker-bootstrapper/` | First-time cloud deploy guide | Bootstrapping a BucketGit broker on AWS or GCP |
| Repository Starter | `repo-starter/` | Practical repo onboarding guide | Creating, attaching, cloning, or checking a BucketGit repository |
| Broker Administrator | `broker-administrator/` | Cloud-aware broker operator | Managing brokers, teams, users, keys, access, protection, and upgrades |
| Bucket Recovery Operator | `bucket-recovery-operator/` | Low-level recovery specialist | Inspecting or repairing direct bucket/object-storage repository state |
| Task Board Steward | `task-board-steward/` | Agile board maintainer | Creating, triaging, assigning, moving, and commenting on task-board stories |
| Multi-Agent Coordinator | `multi-agent-coordinator/` | Distributed work coordinator | Coordinating multiple agents through backlog, lanes, comments, branches, PRs, and CI |
| PR And CI Operator | `pr-ci-operator/` | Release-minded reviewer | Creating/reviewing PRs, checking diffs, mergeability, CI status, and build logs |

## Rules

- Prefer broker-backed workflows. Use `bgit direct` only for recovery, repair,
  migration, or low-level inspection.
- Treat broker metadata as authoritative for users, roles, task-board stories,
  pull requests, issues, branch protection, and CI run records.
- Before changing access, refs, or broker infrastructure, identify the current
  broker, repo, user, role, and capabilities with `bgit whoami`.
- Do not bypass branch protection. Use task-board comments, PRs, review state,
  and CI records to leave a clear collaboration trail.

## References

- Read `references/scenario-routing.md` when deciding which scenario skill to
  load or when a task spans multiple BucketGit workflows.
