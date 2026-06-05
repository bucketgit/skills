# Task Board Workflows

## Commands

```bash
bgit board list
bgit board create "As a maintainer, I want broker upgrades to be one command so that old repositories stay compatible."
bgit board edit BG-12 "As a maintainer, I want broker upgrades to be one command so that old repositories can adopt new broker features safely."
bgit board take BG-12
bgit board assign BG-12 ada
bgit board move BG-12 doing
bgit board priority BG-12 1
bgit board comment BG-12 "Started implementation on feature/broker-upgrade."
bgit board archive BG-12
bgit board list --archived
```

## Story Style

Use story text instead of separate title fields. Prefer:

```text
As a <role>, I want <capability>, so that <outcome>.
```

Make the role concrete, the task observable, and the value testable. Avoid
turning implementation chores into vague stories; add comments for technical
notes. If the story text is wrong or too vague, edit it directly before
implementation rather than correcting it only in comments.

## Lane Meaning

| Lane | Meaning |
|------|---------|
| backlog | Captured but not ready to start |
| ready | Agreed, small enough, and available for work |
| doing | Someone is actively implementing |
| review | Implementation is ready for review, PR, or validation |
| done | Merged, verified, or intentionally closed out |

Use ordering within a lane to communicate priority. In `bgit web`, drag cards
within the same lane to reorder them. From the CLI, use:

```bash
bgit board priority BG-12 3
bgit board priority BG-12 1 --lane ready
```

Setting a story to priority `3` shifts the existing story at `3` and every story
after it down by one. The broker then normalizes the lane to dense `1..N`
positions, so do not manually reassign every story to close gaps or make room.
Older brokers that do not support ordering may keep the previous order and
surface an upgrade warning; do not encode priority into story text as a
workaround.

Use the story detail view in `bgit web` for the activity history when auditing
who edited, moved, assigned, commented on, archived, or unarchived a story.

## Assignment Etiquette

- Only unassigned stories are "taken".
- Reassignment should be explicit and visible.
- Use `Unassigned` when work is no longer owned.
- Comment when ownership changes because of a blocker or handoff.

## Review Linkage

When work moves to review, comment with the PR number or branch:

```bash
bgit board move BG-12 review
bgit board comment BG-12 "PR #7 opened from feature/broker-upgrade."
```

Move to done only after merge and verification.

## Archive Policy

Archive stories when they are no longer useful on the active board:

- Done work after merge/verification and any follow-up stories have been
  captured.
- Superseded stories after the replacement story is linked in a comment.
- Intentionally abandoned work after the reason is recorded.

Use archived stories as history, not as active backlog. Inspect them with:

```bash
bgit board list --archived
```

In `bgit web`, use the Archived tab inside the Task board to browse archived
stories without loading them into the active lanes.

Restore an archived story only when it becomes active work again:

```bash
bgit board unarchive BG-12
bgit board move BG-12 ready
```

If archive, edit, priority, or ordering operations report an unknown broker
endpoint, keep the board state as-is and tell the operator to run
`bgit admin broker upgrade`.
