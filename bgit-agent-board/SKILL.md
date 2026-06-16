---
name: "bgit-agent-board"
description: "Use for agent planning and coordination with BucketGit task boards backed by file:// for same-machine agents, s3:// for distributed AWS-backed agents, or gs:// for distributed GCP-backed agents, with OS-specific setup for macOS, Linux, and Windows."
---

# BucketGit Agent Board

Persona: agent-board coordinator. Use the BucketGit board as the source of
truth for single-machine or distributed agent planning without deploying a cloud
broker service.

## Scope

Use this skill only for local development or local-broker repositories:

```bash
bgit clone file://repo-name.git
bgit clone s3://repo-name.git
bgit clone gs://repo-name.git
```

- Use `file://` for single-machine planning, whether one agent or multiple
  agents are working on that same machine.
- Use `s3://` for multi-agent planning across different machines/locations when
  collaborators share AWS bucket access.
- Use `gs://` for multi-agent planning across different machines/locations when
  collaborators share GCP bucket access.

Assume `s3://` uses already configured AWS credentials and `gs://` uses already
authenticated Google Cloud credentials. Do not use this skill for managed cloud
brokers, public hosted brokers, or non-board bgit administration.

## Workflow

1. Ensure `bgit` is installed for the current OS.
2. For `s3://`, ensure AWS CLI credentials work before cloning.
3. For `gs://`, ensure `gcloud` authentication works before cloning.
4. Clone or initialize the local-broker repository.
5. Use `bgit board list` to inspect active stories.
6. Create concise stories for planned work with `bgit board create`.
7. Move ready work through `backlog`, `ready`, `doing`, `review`, and `done`.
8. Use `bgit board take`, `assign`, `comment`, and `priority` to coordinate
   agents.
9. Archive finished stories when the active board gets noisy.

## References

- Read `references/macos.md` for macOS install and credential setup.
- Read `references/linux.md` for Linux install and credential setup.
- Read `references/windows.md` for Windows install and credential setup.
- Read `references/local-board-workflows.md` for board commands, planning
  patterns, and agent handoff conventions.
