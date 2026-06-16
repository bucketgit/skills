# Linux Agent Board Setup

## Install bgit

Download the latest Linux binary for the machine architecture from:

```text
https://github.com/bucketgit/bgit/releases/latest/
```

Use `bgit-linux-amd64` for x86_64/amd64 systems and `bgit-linux-arm64` for
ARM64/aarch64 systems. Install it on `PATH`, for example as
`/usr/local/bin/bgit`, and mark it executable.

After installation:

```bash
bgit --version
which bgit
```

## Single-Machine Board Repo

```bash
bgit clone file://planning.git
cd planning
bgit board list
```

## AWS-Backed Distributed Board

Install AWS CLI v2 using the distribution package if available, or AWS's Linux
installer. Validate credentials before using `s3://`:

```bash
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

Install Google Cloud CLI using the distro package or Google's package
repository. Authenticate both gcloud and application-default credentials:

```bash
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
