# Repository Workflows

## Create And Attach

Use this path when a broker repository does not exist yet:

```bash
bgit admin repo create --team core app
mkdir app
cd app
bgit init --noninteractive --repo app --profile work.europe-west1 --team core
```

Interactive attach:

```bash
bgit init
```

`bgit init` prompts for the broker profile, team, and existing repository. A
fresh greenfield flow should select the team first and then the repository.

## Clone

For local broker storage URIs, use the local broker skill:

```bash
bgit clone file://app.git
bgit clone s3://app.git --profile work --region eu-west-1
bgit clone gs://app.git --profile work --region europe-west1
```

Flat broker URLs use the default `core` team:

```bash
bgit clone https://broker.example.com/app.git ./app
```

Team-qualified forms:

```bash
bgit clone https://broker.example.com/core/app.git ./app
bgit clone https://broker.example.com/core/app/app.git ./app
```

## Identity And Health

```bash
bgit whoami
bgit repos mine
bgit status
```

`bgit whoami` should show broker URL, repo, user, role, key fingerprint, broker
version, and capabilities. If role is `none`, fix repository/team grants before
attempting writes.

## Push/Pull

```bash
bgit pull
bgit push
```

`bgit pull` should operate on the current checked-out branch when no branch is
provided. Pushes use broker compare-and-swap ref updates and signed object
capabilities. If an older broker rejects v2 signatures, upgrade it before
retrying.

## Direct Mode

Use `bgit direct` only for low-level recovery and inspection. It is not the
normal path for repository collaboration.
