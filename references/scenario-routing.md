# Scenario Routing

Load the smallest skill that covers the task:

| User Intent | Load |
|-------------|------|
| "Install bgit", "update bgit", "Homebrew", "Linux binary", "Windows install" | `installer/SKILL.md` |
| "First broker", "deploy broker", "bootstrap AWS", "bootstrap GCP", "setup cloud account" | `broker-bootstrapper/SKILL.md` |
| "Create a repo", "init", "clone", "push failed", "who am I?" | `repo-starter/SKILL.md` |
| "Upgrade broker", "grant access", "teams", "keys", "protection" | `broker-administrator/SKILL.md` |
| "Direct bucket", "recovery", "repair refs", "stale ref", "bucket IAM", "janitor" | `bucket-recovery-operator/SKILL.md` |
| "Create story", "move card", "assign", "comment", "board hygiene" | `task-board-steward/SKILL.md` |
| "Coordinate agents", "split backlog", "handoff", "parallel work" | `multi-agent-coordinator/SKILL.md` |
| "Create PR", "review diff", "merge", "CI logs", "build failed" | `pr-ci-operator/SKILL.md` |

For broad tasks, compose skills in this order:

1. `installer` if `bgit` is missing or version-sensitive.
2. `broker-bootstrapper` if no broker exists yet.
3. `repo-starter` to establish the repository and identity.
4. `task-board-steward` or `multi-agent-coordinator` to define work.
5. `pr-ci-operator` to review, validate, and merge.
6. `broker-administrator` only when permissions, broker deployment, or repo
   policy must change.
7. `bucket-recovery-operator` only for direct bucket recovery, migration, or
   repair work that intentionally bypasses normal broker workflows.

Avoid loading broker administration context for routine story, PR, or local
worktree tasks.
