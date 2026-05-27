# PR And CI Workflows

## Pull Requests

```bash
bgit pr create --title "Add docs" --body "Adds onboarding docs." --source feature/docs --target main
bgit pr list
bgit pr view 1
bgit pr diff 1
bgit pr comment 1 "Reviewed CLI behavior and docs."
bgit pr approve 1 "Looks good."
bgit pr merge 1 --delete-branch
```

Use `bgit pr reject ID COMMENT` for blocking review feedback and
`bgit pr close ID` for abandoned work.

## Mergeability

Before merge:

```bash
bgit pr view ID
bgit pr diff ID
bgit ci list
```

Confirm the target branch, source branch, diff, review state, and CI result.
If the broker reports conflicts or non-mergeable state, keep the PR open and
ask the author to rebase, merge target, or resolve conflicts on the source
branch.

## CI Runs

```bash
bgit ci list
bgit ci run --ref feature/docs
bgit ci run --ref feature/docs --config cloudbuild.yaml --provider gcp
bgit ci run --ref feature/docs --config buildspec.yaml --provider aws
bgit ci view 4
bgit ci logs 4
bgit ci watch 4
```

The broker verifies repository state before handing off to provider CI. CI
configuration should come from committed files such as `cloudbuild.yaml` for GCP
or `buildspec.yaml` for AWS.

## Failure Triage

- If a run is queued for too long, check provider permissions and materializer
  logs.
- If logs are unavailable, verify the broker stack has the CI log/read
  capabilities for the provider.
- If token errors occur, rotate with `bgit admin ci rotate-secret` and rerun.
- If the build used an unexpected config file, inspect the committed ref and
  the `--config` value used for the run.
