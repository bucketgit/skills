# Scenario Routing

Load the smallest skill that covers the task:

| User Intent | Load |
|-------------|------|
| "Install bgit", "update bgit", "Homebrew", "Linux binary", "Windows install" | `installer/SKILL.md` |
| "First broker", "deploy broker", "bootstrap AWS", "bootstrap GCP", "setup cloud account" | `broker-bootstrapper/SKILL.md` |
| "Local broker", "in-process broker", "clone s3://", "clone gs://", "clone file://", "local broker recovery" | `local-broker-operator/SKILL.md` |
| "Create a repo", "init", "clone", "push failed", "who am I?" | `repo-starter/SKILL.md` |
| "Upgrade broker", "grant access", "teams", "keys", "protection" | `broker-administrator/SKILL.md` |
| "Direct bucket", "recovery", "repair refs", "stale ref", "bucket IAM", "janitor" | `bucket-recovery-operator/SKILL.md` |
| "Create story", "edit story", "move card", "reorder", "assign", "archive", "comment", "board hygiene" | `task-board-steward/SKILL.md` |
| "Coordinate agents", "split backlog", "handoff", "parallel work" | `multi-agent-coordinator/SKILL.md` |
| "Create PR", "review diff", "merge", "CI logs", "build failed" | `pr-ci-operator/SKILL.md` |

For broad tasks, compose skills in this order:

1. `installer` if `bgit` is missing or version-sensitive.
2. `broker-bootstrapper` if no broker exists yet.
3. `local-broker-operator` if the repository is local-broker-backed or uses
   `s3://`, `gs://`, or `file://` local broker flows.
4. `repo-starter` to establish the repository and identity.
5. `task-board-steward` or `multi-agent-coordinator` to define work.
6. `pr-ci-operator` to review, validate, and merge.
7. `broker-administrator` only when permissions, broker deployment, or repo
   policy must change.
8. `bucket-recovery-operator` only for direct bucket recovery, migration, or
   repair work that intentionally bypasses normal broker workflows.

Avoid loading broker administration context for routine story, PR, or local
worktree tasks.
