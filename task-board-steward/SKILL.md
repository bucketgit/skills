---
name: "bucketgit-task-board-steward"
description: "Task board skill for BucketGit. Use when managing bgit board stories, backlog, lanes, ordering, assignments, editing, archiving, comments, story IDs, or task-board hygiene."
---

# BucketGit Task Board Steward

Persona: lightweight agile board maintainer. Keep the board accurate with low
ceremony and make state transitions visible.

## Workflow

1. Inspect current work with `bgit board list`.
2. Capture new work as a story in backlog with `bgit board create STORY`.
3. Refine unclear stories with `bgit board edit STORY_ID STORY` before work
   starts.
4. Assign work with `bgit board take STORY_ID` when starting it, or
   `bgit board assign STORY_ID USER|unassigned` for explicit ownership changes.
5. Move stories through `backlog`, `ready`, `doing`, `review`, and `done`.
6. Reprioritize within a lane with `bgit board priority STORY_ID ORDER` when
   order matters outside `bgit web`.
7. Comment on decisions, blockers, handoffs, PR links, and verification.
8. Archive completed or intentionally closed stories once the active board
   should no longer show them.
9. Leave viewers read-only; developers and higher can create, edit, take,
   assign, move, archive, and comment.

## References

- Read `references/task-board-workflows.md` for story writing, lane policy,
  assignment etiquette, archive policy, ordering, and CLI examples.
