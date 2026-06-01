# Multi-Agent Collaboration

## Initial Sync

```bash
bgit board list
bgit pr list
bgit ci list
bgit branch
bgit status
```

The coordinator should summarize:

- Stories available in backlog or ready.
- Stories already owned.
- PRs awaiting review.
- CI failures blocking done.
- Branches that may conflict.

## Assignment Protocol

1. Create a story if the work is not already represented.
2. Edit the story if the role, task, or outcome is unclear.
3. Move it to `ready` once scope is clear.
4. The implementing agent runs `bgit board take STORY_ID`.
5. The implementing agent comments with the branch name.
6. The coordinator avoids assigning overlapping files to multiple agents unless
   the dependency is intentional.

Example:

```bash
bgit board create "As a repo admin, I want direct user assignment in setup so that broker users can be granted repo access without invites."
bgit board edit BG-21 "As a repo admin, I want direct user assignment in setup so that existing broker users can receive repo access without invite round-trips."
bgit board move BG-21 ready
bgit board take BG-21
bgit board comment BG-21 "Working on feature/direct-user-assignment."
```

## Transition Protocol

| Transition | Required Evidence |
|------------|-------------------|
| backlog -> ready | Story is understandable and not blocked |
| ready -> doing | Agent has claimed it and named a branch |
| doing -> review | PR exists, diff is reviewable, tests were run or limitation is documented |
| review -> done | PR merged or accepted, CI state understood, follow-ups captured |

## PR And CI Protocol

```bash
bgit pr create --title "Direct repo user assignment" --source feature/direct-user-assignment --target main
bgit pr diff 12
bgit ci run --ref feature/direct-user-assignment
bgit ci watch 5
bgit board comment BG-21 "PR #12, CI #5 passing."
bgit board move BG-21 done
bgit board archive BG-21
```

## Conflict Handling

- If two agents claim overlapping work, pause one story in `ready` or reassign it.
- If CI fails, keep the story in `review` and comment with the failing run ID.
- If scope grows, split a new backlog story rather than expanding the active one
  silently.
- If an agent stops, reassign or unassign the story and comment with the last
  known branch and blocker.
- If completed or abandoned work clutters the active board, archive it only
  after a final outcome comment.
- If edit, archive, or board ordering fails with an unknown endpoint, the broker
  needs `bgit admin broker upgrade`; continue with existing lane order until it
  is upgraded.
