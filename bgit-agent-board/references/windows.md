# Windows Agent Board Setup

Use PowerShell unless the user is explicitly working in WSL.

## Install bgit

Install the Windows release binary and ensure its directory is on `PATH`.
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
