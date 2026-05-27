# Direct Mode

Direct mode is the low-level object-storage and cloud IAM escape hatch:

```bash
bgit direct help
bgit direct clone gs://bucket/prefix.git [directory]
bgit direct clone s3://bucket/prefix.git [directory]
bgit direct origin gs://bucket/prefix.git
bgit direct remote add origin s3://bucket/prefix.git
bgit direct fetch
bgit direct pull
bgit direct push
bgit direct ls-remote
bgit direct ls
bgit direct cat
bgit direct show
bgit direct log
bgit direct put
bgit direct admin grant-read|grant-write|grant-admin IDENTITY
```

Normal BucketGit workflows should use `setup`, `init`, native Git transport,
`bgit admin`, PRs, and broker capabilities. Direct mode intentionally bypasses
the broker control plane.

## Configure A Direct Origin

```bash
bgit direct origin gs://my-bucket/repositories/app.git
bgit direct origin s3://my-bucket/repositories/app.git --profile aws-profile
```

Git remote syntax is also available:

```bash
bgit direct remote add origin gs://bucket/prefix.git
bgit direct remote set-url origin s3://bucket/prefix.git
```

## Inspect Repository State

List refs:

```bash
bgit direct ls-remote
bgit direct ls-remote --heads
bgit direct ls-remote --tags
```

List and read bucket paths:

```bash
bgit --bucket my-bucket --prefix repositories/app.git direct ls refs/
bgit --bucket my-bucket --prefix repositories/app.git direct cat refs/heads/main
bgit --bucket my-bucket --prefix repositories/app.git direct ls objects/
```

Inspect Git data:

```bash
bgit direct show HEAD
bgit direct log --oneline
```

## Cloud IAM Recovery

```bash
bgit direct admin grant-read user:dev@example.com
bgit direct admin grant-write serviceAccount:ci@project.iam.gserviceaccount.com
bgit direct admin grant-admin arn:aws:iam::123456789012:role/Admin
```

Use cloud IAM recovery when broker administration is unavailable or physical
bucket access must be restored. Prefer short-lived or tightly scoped identities
where the cloud platform supports it.
