# Broker Operations

## Broker And Repo Inventory

```bash
bgit whoami
bgit admin repo list
bgit admin repo info
bgit repos
```

Check broker version and capabilities before diagnosing permission failures.
Older brokers may lack v2 request signatures, constrained object capabilities,
CI endpoints, or repository user-grant listing.

## Upgrade And Bootstrap

```bash
bgit admin broker upgrade
bgit admin broker owner-bootstrap reset
```

Use owner-bootstrap reset only when re-establishing owner onboarding. The broker
stores a bootstrap token hash, not a readable token.

## Broker Users

```bash
bgit admin broker-users list
bgit admin broker-users upsert ada --role user --key ~/.ssh/ada.pub
bgit admin broker-users upsert ada --role admin --key "ssh-ed25519 ..."
bgit admin broker-users upsert ada --role user --suspended true
bgit admin broker-users delete ada
```

Broker users have stable identities and SSH keys. Repository access is still
controlled through team membership, team-to-repo grants, direct repo grants, or
legacy invite flows.

## Teams

```bash
bgit admin teams list
bgit admin teams create platform
bgit admin teams member add TEAM ada --role developer
bgit admin teams member remove TEAM ada
bgit admin teams repo list
bgit admin teams repo add TEAM developer
bgit admin teams repo remove TEAM
```

Prefer teams for normal project membership. Grant the least role that supports
the workflow: viewer reads, developer pushes and edits work items, admin manages
repo settings.

## Repositories

```bash
bgit admin repo create --team platform app
bgit admin repo visibility public
bgit admin repo visibility private
bgit admin repo readonly on
bgit admin repo readonly off
bgit admin repo issues on
bgit admin repo issues off
bgit admin repo rename new-name
bgit admin repo delete --yes
```

Repo delete is destructive. Confirm the broker, team, and logical repo name
before running it.

## Keys And Invites

```bash
bgit admin keys list
bgit admin keys add --user ada --role developer --key ~/.ssh/ada.pub
bgit admin keys import-github octocat --role read
bgit admin keys suspend KEY_OR_FINGERPRINT
bgit admin keys remove KEY_OR_FINGERPRINT
```

Use invite commands only when the flow requires explicit acceptance:

```bash
bgit admin invite-user --broker URL --team TEAM --user ada --role developer app
bgit admin accept-invite CODE
bgit admin cancel-invite --broker URL --team TEAM --user ada app
```

## Protection And CI Secrets

```bash
bgit admin protect add main
bgit admin protect list
bgit admin protect remove main
bgit admin ci rotate-secret
```

Protected branches should be updated through PR merge paths. CI materializer
secrets are managed by the broker stack and rotated through the admin command.
