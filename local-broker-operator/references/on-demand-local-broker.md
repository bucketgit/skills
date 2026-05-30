# In-Process Local Broker

## Intended Use

Use local broker mode when a user wants BucketGit broker semantics without a
deployed AWS/GCP broker:

- Local filesystem-backed repo for single-machine or shared-disk use.
- S3-backed repo guarded by local broker authorization and metadata.
- GCS-backed repo guarded by local broker authorization and metadata.
- Local development, demos, offline-ish work, or small trusted collaborations
  where each operator can access the underlying storage.

Do not suggest a long-lived localhost broker. The normal path is a normal
`bgit` command; local broker routing happens in-process.

## URI Shapes

Local broker storage URI examples:

```bash
bgit clone file://app.git
bgit clone s3://app.git --profile work --region eu-west-1
bgit clone gs://app.git --profile work --region europe-west1
```

Interpretation:

- No team segment is used in the URI.
- `core` is the internal default team.
- Profile and region are command options, not URI components.
- For S3, omitted profile defaults to `default`; omitted region defaults to
  `us-east-1`.
- For GCS, omitted profile defaults to `default`; omitted region defaults to
  `us-central1`.
- One physical bucket/path is one repo. Do not multiplex multiple logical repos
  into one bucket.
- `file://` repositories are stored below `~/.bgit/local-broker` or
  `$BGIT_HOME/local-broker`.
- S3/GCS physical bucket names are derived from the cached AWS account ID or GCP
  project ID plus the repo name. The visible repo remains `app.git`.

## Storage Layout

The local broker stores Git data and broker state together:

```text
<repo storage>
  HEAD
  refs/
  objects/
  .bucketgit/
    broker-state/
      v1/
        repo-table-item.json
        refs/<encoded-ref>.json
        locks/<encoded-ref>.json
        tables/...
```

Authoritative state:

- Git objects: normal repo object storage.
- Ref coordination: `.bucketgit/broker-state/v1/refs/`.
- Broker metadata: `.bucketgit/broker-state/v1/`.
- Materialized Git refs: compatibility output, not the coordination source.

## Ref Safeguards

For a local broker ref update:

1. Broker resolves the repository and reads storage-backed broker metadata.
2. Broker applies permission and branch-protection checks.
3. Broker acquires a short storage-backed lease under
   `.bucketgit/broker-state/v1/locks/`.
4. Broker re-reads the authoritative ref record under
   `.bucketgit/broker-state/v1/refs/`.
5. If the authoritative hash differs from the client old hash, reject with a
   stale ref.
6. If valid, write the authoritative ref record.
7. Materialize the normal Git ref file for compatibility.

This means stale materialized refs should cause a retry/reconciliation path, not
silent overwrite of storage-backed broker state.

## Recovery Playbooks

### Push Rejected As Stale Ref

Use normal collaboration recovery:

```bash
bgit fetch
bgit status
bgit pull
bgit push
```

If the user has local commits, inspect the branch graph before retrying:

```bash
bgit log --oneline --decorate --graph --all -20
```

### Storage State Disagrees With Materialized Refs

Do not hand-edit implementation state. Prefer forcing `bgit` to re-read the
storage-backed broker state:

1. Run `bgit ls-remote` or `bgit fetch` to read current remote refs.
2. Inspect `.bucketgit/broker-state/v1/refs/` only as a recovery action.
3. Rebuild normal Git refs from broker-state records only after confirming the
   record hash is valid and the object exists.

For direct object inspection, use the bucket recovery skill and direct mode only
after confirming this is a recovery task.

### Materialized Git Ref Missing Or Wrong

Broker-state ref records are the source of truth. Recovery should rebuild the
normal Git ref from `.bucketgit/broker-state/v1/refs/<encoded-ref>.json` only
after confirming the record has a valid 40-character hash and the object exists.

Do not overwrite broker-state from the materialized ref unless the operator has
explicitly chosen rollback to an older known-good ref.

### Lock Appears Stuck

Locks are short-lived. First retry after the lease window. If a lock remains and
its `expires_at` is in the past, the broker should be allowed to replace it on
the next operation.

Manual lock deletion is a recovery action. Before deleting, record:

- repo URI
- ref
- lock contents
- current broker-state ref hash
- materialized ref hash

### Storage Backend Credentials Fail

For S3-backed local broker repos:

```bash
aws sts get-caller-identity
aws s3api head-bucket --bucket <bucket>
```

For GCS-backed local broker repos:

```bash
gcloud auth list
gcloud storage ls gs://<bucket>
```

Fix cloud credentials first. Do not repair broker metadata when the issue is
provider authentication.

## What Not To Do

- Do not tell users they must keep a local broker server running.
- Do not encode team names, profiles, or regions into local broker storage URIs.
- Do not use `bgit setup` as a prerequisite for `file://` local broker repos.
- Do not use `bgit direct` for ordinary local broker work.
- Do not bypass branch protection or broker ref safeguards with direct writes
  unless explicitly performing recovery with a rollback plan.
