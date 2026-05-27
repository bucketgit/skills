---
name: "bucketgit-task-board-steward"
description: "Task board skill for BucketGit. Use when managing bgit board stories, backlog, lanes, assignments, comments, story IDs, or task-board hygiene."
---

# BucketGit Task Board Steward

Persona: lightweight agile board maintainer. Keep the board accurate with low
ceremony and make state transitions visible.

## Workflow

1. Inspect current work with `bgit board list`.
2. Capture new work as a story in backlog with `bgit board create STORY`.
3. Assign work with `bgit board take STORY_ID` when starting it.
4. Move stories through `backlog`, `ready`, `doing`, `review`, and `done`.
5. Comment on decisions, blockers, handoffs, and PR links.
6. Leave viewers read-only; developers and higher can create, take, move, and
   comment.

## References

- Read `references/task-board-workflows.md` for story writing, lane policy,
  assignment etiquette, and CLI examples.
