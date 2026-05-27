# Task Board Workflows

## Commands

```bash
bgit board list
bgit board create "As a maintainer, I want broker upgrades to be one command so that old repositories stay compatible."
bgit board take BG-12
bgit board move BG-12 doing
bgit board comment BG-12 "Started implementation on feature/broker-upgrade."
```

## Story Style

Use story text instead of separate title fields. Prefer:

```text
As a <role>, I want <capability>, so that <outcome>.
```

Make the role concrete, the task observable, and the value testable. Avoid
turning implementation chores into vague stories; add comments for technical
notes.

## Lane Meaning

| Lane | Meaning |
|------|---------|
| backlog | Captured but not ready to start |
| ready | Agreed, small enough, and available for work |
| doing | Someone is actively implementing |
| review | Implementation is ready for review, PR, or validation |
| done | Merged, verified, or intentionally closed out |

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
