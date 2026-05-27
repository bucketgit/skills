# Safety Checklist

Before direct recovery:

- [ ] Confirm the target provider, bucket, prefix, and repository name.
- [ ] Confirm whether the repo is broker-backed or legacy direct-only.
- [ ] Run `bgit whoami` when inside a broker-backed checkout.
- [ ] Capture current refs with `bgit ls-remote` and `bgit direct ls-remote`.
- [ ] Capture any ref you might change with `bgit direct cat refs/heads/NAME`.
- [ ] Prefer read-only commands before write/admin commands.
- [ ] Prefer `bgit janitor members reindex` for derived metadata repair.
- [ ] Avoid `bgit push --skip-broker` unless broker write path is unavailable.
- [ ] Write down rollback steps before changing refs or bucket policy.
- [ ] After recovery, remove temporary direct IAM grants and return to broker
      workflows.

Never use direct mode to avoid review, branch protection, access control, or CI
policy during normal development.
