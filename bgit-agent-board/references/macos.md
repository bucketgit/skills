# macOS Agent Board Setup

## Install bgit

Prefer Homebrew:

```bash
brew tap bucketgit/bgit
brew install bgit
bgit --version
```

If a user has multiple copies, check:

```bash
which bgit
type bgit
```

## Single-Machine Board Repo

```bash
bgit clone file://planning.git
cd planning
bgit board list
```

## AWS-Backed Distributed Board

Install and configure AWS CLI:

```bash
brew install awscli
aws configure
aws sts get-caller-identity
```

Then clone:

```bash
bgit clone s3://planning.git
cd planning
bgit board list
```

Use an explicit profile/region when needed:

```bash
bgit clone s3://planning.git --profile work --region eu-west-1
```

## GCP-Backed Distributed Board

Install and authenticate Google Cloud CLI:

```bash
brew install --cask google-cloud-sdk
gcloud init
gcloud auth application-default login
gcloud auth list
gcloud config get-value project
```

Then clone:

```bash
bgit clone gs://planning.git
cd planning
bgit board list
```

Use an explicit profile/region when needed:

```bash
bgit clone gs://planning.git --profile work --region europe-west1
```
