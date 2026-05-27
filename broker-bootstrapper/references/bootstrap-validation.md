# Bootstrap Validation

## Verify Config

```bash
bgit setup
bgit repos
```

Inspect `~/.bgit/config.yaml` only when needed to confirm profile, region, and
broker URL.

## Smoke-Test Repository

```bash
bgit admin repo create --team core smoke-test
mkdir smoke-test
cd smoke-test
bgit init --noninteractive --repo smoke-test --profile PROFILE.REGION --team core
printf 'hello\n' > README.md
bgit add README.md
bgit commit -m "Initial commit"
bgit push
bgit whoami
```

Expected:

- `bgit push` succeeds through broker object capabilities and CAS ref update.
- `bgit whoami` shows broker URL, repo, owner/admin identity, broker version,
  and capabilities.

## Common Failures

- `broker is incompatible with this bgit version`: run `bgit admin broker upgrade`
  from a repository attached to that broker.
- `broker admin SSH signature required`: ensure the owner key was imported and
  the private key is available through `ssh-agent`, `BGIT_SSH_KEY`, or
  `--identity`.
- `role: none`: grant repository or team access for the current broker user.
- Cloud deploy permission errors: fix cloud IAM first; broker deployment usually
  requires broad account/project administration rights.
