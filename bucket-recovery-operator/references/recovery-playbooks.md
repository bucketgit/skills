# Recovery Playbooks

## Broker Is Down But Bucket Is Healthy

Goal: inspect or recover repository content without changing broker metadata.

```bash
bgit direct clone gs://bucket/prefix.git recovered-repo
bgit direct clone s3://bucket/prefix.git recovered-repo
cd recovered-repo
bgit direct ls-remote
bgit log --oneline --decorate -20
```

If users only need read access during outage, grant direct read access
temporarily and remove it after broker service is restored.

## Stale Ref Or Rejected Push

Goal: understand remote ref state before retrying or repairing.

```bash
bgit ls-remote
bgit direct ls-remote
bgit direct cat refs/heads/BRANCH
bgit rev-parse BRANCH
bgit rev-parse origin/BRANCH
```

If broker and direct refs disagree, identify the authoritative state:

- Broker ref state should normally win for broker-backed repos.
- Direct bucket refs may be stale if a previous direct write bypassed broker CAS.
- Do not force-push or direct-push until the expected old and new hashes are
  written down.

## Missing Or Broken Bucket Access

Goal: restore enough cloud access to inspect or repair.

```bash
bgit direct admin grant-read IDENTITY
bgit direct admin grant-write IDENTITY
bgit direct admin grant-admin IDENTITY
```

Examples:

```bash
bgit direct admin grant-read user:dev@example.com
bgit direct admin grant-write serviceAccount:ci@project.iam.gserviceaccount.com
bgit direct admin grant-admin arn:aws:iam::123456789012:role/Admin
```

After recovery, return routine users to broker-managed access.

## Broker Membership Index Looks Wrong

Goal: rebuild derived broker metadata from authoritative repo/team state.

```bash
bgit janitor members reindex
```

Use this when `bgit repos`, setup repository listings, or web access lists look
stale but underlying repo/team grants are correct.

## Migration Or Direct Import

Goal: move data while preserving normal Git object layout.

```bash
bgit direct clone gs://old-bucket/repositories/app.git app-migration
cd app-migration
bgit direct origin s3://new-bucket/repositories/app.git
bgit direct push --tags
bgit direct push HEAD:refs/heads/main
```

After migration, attach or create broker metadata through normal setup/admin
commands rather than editing broker state by hand.

## Emergency Direct Push

Use only when broker write path is unavailable and the operator accepts that
branch protection, PR merge policy, and broker CAS are bypassed:

```bash
bgit push --skip-broker HEAD:refs/heads/main
```

Before doing this, capture:

- Current direct remote ref.
- Local commit to publish.
- Reason broker path cannot be used.
- Follow-up action to reconcile broker metadata after recovery.
