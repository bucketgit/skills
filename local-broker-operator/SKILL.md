---
name: "bucketgit-local-broker-operator"
description: "Local broker skill for BucketGit. Use when working with bgit in-process local brokers, local filesystem repositories, s3:// or gs:// local-broker-backed repositories, storage-backed broker metadata, ref safeguards, URI/profile selection, and recovery scenarios."
---

# BucketGit Local Broker Operator

Persona: local-first repository operator. Keep the workflow transparent: use
the in-process local broker path built into `bgit`, avoid localhost server
assumptions, and treat storage-backed broker state as authoritative.

## Operating Model

- Prefer `bgit clone file://repo.git`, `bgit clone s3://repo.git`, or
  `bgit clone gs://repo.git`. The local broker is internal to the command; no
  separate local HTTP broker should be started.
- Do not add team names to local broker storage URIs. The local broker uses the
  default `core` team internally.
- Select AWS/GCP credentials with `--profile` and `--region`; do not encode
  profile or region into the URI host/name. If omitted, defaults are
  `default/us-east-1` for S3 and `default/us-central1` for GCS.
- Treat `.bucketgit/broker-state/v1/` in the repo storage as authoritative for
  broker metadata and local ref safeguards.
- Physical cloud bucket names are derived from the cached AWS account ID or GCP
  project ID plus the repo name; the visible logical repo remains `repo.git`.

## Workflow

1. Identify whether the task is local broker work: storage URI clone, local
   broker-backed repo, storage-backed ref conflict, or local broker recovery.
2. Check the current repo state with `bgit whoami`, `bgit status`, and
   `bgit ls-remote` when inside a checkout.
3. For new repos, use `bgit clone file://repo.git`, `bgit clone s3://repo.git`,
   or `bgit clone gs://repo.git`; avoid instructing the user to run setup or a
   persistent broker for local broker work.
4. For push/fetch conflicts, prefer normal Git-style recovery:
   `bgit fetch`, `bgit pull`, inspect, then retry.
5. For suspected state drift, inspect storage-backed broker state rather than
   editing local implementation files.
6. For repair, preserve the old state first and only rebuild materialized Git
   refs from broker-state records when the broker-state record is coherent.

## References

- Read `references/on-demand-local-broker.md` for command patterns, URI
  interpretation, storage layout, ref-safeguard behavior, and recovery
  playbooks.
