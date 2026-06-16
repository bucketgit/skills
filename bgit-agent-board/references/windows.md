# Windows Agent Board Setup

Use PowerShell unless the user is explicitly working in WSL.

## Install bgit

Download the latest Windows binary for the machine architecture from:

```text
https://github.com/bucketgit/bgit/releases/latest/
```

Use `bgit-windows-amd64.exe` for x86_64/amd64 systems and
`bgit-windows-arm64.exe` for ARM64 systems. Rename it to `bgit.exe` if needed
and ensure its directory is on `PATH`.

Validate:

```powershell
bgit --version
where.exe bgit
```

If using WSL, follow the Linux reference inside the WSL distribution instead.

## Single-Machine Board Repo

```powershell
bgit clone file://planning.git
cd planning
bgit board list
```

## AWS-Backed Distributed Board

Install AWS CLI v2 for Windows, then configure credentials:

```powershell
aws configure
aws sts get-caller-identity
```

Then clone:

```powershell
bgit clone s3://planning.git
cd planning
bgit board list
```

Use an explicit profile/region when needed:

```powershell
bgit clone s3://planning.git --profile work --region eu-west-1
```

## GCP-Backed Distributed Board

Install Google Cloud CLI for Windows, then authenticate:

```powershell
gcloud init
gcloud auth application-default login
gcloud auth list
gcloud config get-value project
```

Then clone:

```powershell
bgit clone gs://planning.git
cd planning
bgit board list
```

Use an explicit profile/region when needed:

```powershell
bgit clone gs://planning.git --profile work --region europe-west1
```
