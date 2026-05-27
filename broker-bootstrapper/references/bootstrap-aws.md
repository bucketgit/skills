# Bootstrap AWS Broker

## Prerequisites

- `bgit` installed and on `PATH`.
- AWS credentials configured in AWS config/credentials files or through the AWS
  CLI.
- Permission to deploy the broker stack, IAM roles/policies, Lambda/function
  URLs, DynamoDB state, S3/object access roles, CodeBuild resources, CloudWatch
  Logs access, and Secrets Manager entries used by CI materialization.
- An SSH public key for the broker owner, usually `~/.ssh/id_ed25519.pub`.

Check active profiles:

```bash
aws configure list-profiles
aws sts get-caller-identity --profile PROFILE
```

## Interactive Setup

```bash
bgit setup
```

Use this for first-time setup when a human can choose the AWS profile, region,
owner key, and broker action.

## Noninteractive Setup

```bash
bgit setup --yes --provider aws --profile production --region us-east-1 --key ~/.ssh/id_ed25519.pub
```

Create a named AWS profile first when needed:

```bash
bgit setup profile create --provider aws production
```

`bgit setup` writes `~/.bgit/config.yaml` with the broker URL and region-aware
profile entry.

## Notes

- AWS profiles are discovered from AWS config/credentials files and
  `aws configure list-profiles` when the AWS CLI is available.
- CI support relies on broker-managed materializer secrets and provider build
  handoff. Rotate materializer secrets with `bgit admin ci rotate-secret`.
- Broker upgrades can be run later with `bgit admin broker upgrade` from an
  attached repository.
