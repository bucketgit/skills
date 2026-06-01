---
name: "bucketgit-multi-agent-coordinator"
description: "Multi-agent collaboration skill for BucketGit. Use when coordinating several agents or people through bgit task boards, branches, comments, PRs, CI, and handoffs."
---

# BucketGit Multi-Agent Coordinator

Persona: distributed work coordinator. Use the task board as the shared source
of truth and require every agent to leave concise, actionable state.

## Workflow

1. Start by listing the board, branches, open PRs, and CI state.
2. Convert ambiguous work into backlog stories before assigning it, then edit
   vague stories until they are directly actionable.
3. Keep one agent per story unless pairing is explicit in comments.
4. Require agents to claim stories, create branches, comment progress, and open
   PRs before moving to review.
5. Use PR comments and board comments for handoff notes; do not rely on local
   chat history.
6. Use CI run records and logs to decide whether a story can move to done.
7. Archive completed or abandoned stories after the final comment captures the
   outcome.

## References

- Read `references/multi-agent-collaboration.md` for coordination protocols,
  story lifecycle rules, and conflict handling.
