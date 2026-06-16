# Local Board Workflows

## Choose Storage

- `file://` is for single-machine planning. Use it for one agent or many agents
  coordinating on the same machine.
- `s3://` is for multi-agent planning across different machines or locations
  when everyone has access to the same AWS account/bucket credentials.
- `gs://` is for multi-agent planning across different machines or locations
  when everyone has access to the same GCP project/bucket credentials.

## Start A Local Planning Repo

Single-machine filesystem-backed:

```bash
bgit clone file://planning.git
cd planning
```

Distributed AWS-backed local broker:

```bash
bgit clone s3://planning.git
cd planning
```

Distributed GCP-backed local broker:

```bash
bgit clone gs://planning.git
cd planning
```

## Inspect Stories

Active board:

```bash
bgit board list
```

Archived board:

```bash
bgit board list --archived
```

## Agentic Planning Loop

1. Capture work as concise stories.
2. Keep only actionable work in `ready`.
3. Agents claim work with `take`.
4. Agents comment with branch, status, blockers, and verification.
5. Move completed work to `done`.
6. Archive completed or abandoned stories after the final outcome comment.

Example:

```bash
bgit board create "As a maintainer, I want smoke tests for local broker clone flows so that regressions are visible."
bgit board move BG-1 ready
bgit board priority BG-1 1
bgit board take BG-1
bgit board comment BG-1 "Working in feature/local-broker-smoke-tests."
bgit board move BG-1 review
bgit board comment BG-1 "Tests pass locally; ready for review."
bgit board move BG-1 done
bgit board archive BG-1
```

## Useful Commands

```bash
bgit board list
bgit board list --archived
bgit board create "Story text"
bgit board edit BG-1 "Updated story text"
bgit board move BG-1 backlog
bgit board move BG-1 ready
bgit board move BG-1 doing
bgit board move BG-1 review
bgit board move BG-1 done
bgit board take BG-1
bgit board assign BG-1 USER
bgit board assign BG-1 unassigned
bgit board priority BG-1 2
bgit board comment BG-1 "Handoff note."
bgit board archive BG-1
bgit board unarchive BG-1
```

## Local Broker Notes

- Local broker repositories do not require `bgit setup`.
- `file://` stores repository data locally and is not suitable for agents on
  different machines unless they share the same filesystem.
- `s3://` uses AWS credentials already available to each machine.
- `gs://` uses Google Cloud credentials already available to each machine.
- Prefer `bgit board list` as the first command in every planning session.
- Do not use direct bucket operations for normal local-board planning.
