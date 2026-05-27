# Bootstrap GCP Broker

## Prerequisites

- `bgit` installed and on `PATH`.
- `gcloud` installed.
- Authenticated GCP account with permission to enable APIs, create or update
  Cloud Run functions, manage Firestore, manage Cloud Storage, manage IAM
  bindings, and manage Secret Manager secrets used by CI materialization.
- An SSH public key for the broker owner, usually `~/.ssh/id_ed25519.pub`.

Check active account and project:

```bash
gcloud auth list
gcloud config list
gcloud projects describe PROJECT_ID
```

## Interactive Setup

```bash
bgit setup
```

Use this for first-time setup when a human can choose the GCP configuration,
region, owner key, and broker action.

## Noninteractive Setup

```bash
bgit setup --yes --provider gcp --profile work --region europe-west1 --key ~/.ssh/id_ed25519.pub
```

Create a named GCP profile first when needed:

```bash
bgit setup profile create --provider gcp work
```

`bgit setup` writes `~/.bgit/config.yaml` with the broker URL and region-aware
profile entry.

## Notes

- GCP profiles are discovered from `gcloud` configurations.
- The setup flow enables required APIs when allowed.
- Broker upgrades use the same setup/provisioning machinery and can be run later
  with `bgit admin broker upgrade` from an attached repository.
