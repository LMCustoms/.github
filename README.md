# LMCustoms Organization Configuration

This repository contains organization-wide defaults, reusable workflows, and documentation for all LMCustoms repositories.

## Structure

```
.github/
├── workflows/                    # Reusable GitHub Actions workflows
│   ├── ci-node.yml              # Node.js CI (lint, typecheck, test, build)
│   ├── docker-build-push.yml    # Docker build & push to GHCR
│   ├── deploy-ssh.yml           # Deploy via SSH
│   ├── pr-notifications.yml     # Email notifications for PRs
│   ├── release-semantic.yml     # Semantic versioning & releases
│   └── security-audit.yml       # Dependency vulnerability scanning
├── profile/
│   └── README.md                # Organization profile (appears on org page)
├── SECURITY.md
├── CONTRIBUTING.md
└── CODE_OF_CONDUCT.md
```

## Reusable Workflows

All workflows use `workflow_call` and are called from individual repos like:

```yaml
jobs:
  ci:
    uses: LMCustoms/.github/.github/workflows/ci-node.yml@main
    with:
      node-version: "22"
```

### `ci-node.yml` — Node.js CI

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `node-version` | string | `"20"` | Node.js version |
| `package-manager` | string | `"npm"` | `npm`, `pnpm`, or `yarn` |
| `working-directory` | string | `"."` | Path to package root |
| `run-lint` | boolean | `true` | Run lint step |
| `run-typecheck` | boolean | `false` | Run typecheck step |
| `run-test` | boolean | `true` | Run test step |
| `run-build` | boolean | `true` | Run build step |

### `docker-build-push.yml` — Docker Build & Push

Builds and pushes to GitHub Container Registry with automatic tagging (SHA, branch, semver, latest).

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `image-name` | string | *required* | Image name (e.g. `lmcustoms/my-app`) |
| `context` | string | `"."` | Docker build context |
| `dockerfile` | string | `"Dockerfile"` | Path to Dockerfile |
| `push` | boolean | `true` | Push after building |

### `deploy-ssh.yml` — Deploy via SSH

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `script` | string | *required* | Shell commands to run on the server |

Requires secrets: `DEPLOY_HOST`, `DEPLOY_USER`, `DEPLOY_SSH_KEY`

### `pr-notifications.yml` — PR Email Notifications

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `to` | string | `"pr@lmcustoms.cc"` | Recipient email |

Requires secrets: `SMTP_SERVER`, `SMTP_PORT`, `SMTP_USERNAME`, `SMTP_PASSWORD`

### `release-semantic.yml` — Semantic Release

Conventional Commits-based versioning: `feat:` = minor, `fix:` = patch, `BREAKING CHANGE:` = major.
Generates changelogs, GitHub releases, and optional email notifications.

Repos can override by providing their own `.releaserc.json` or `release.config.js`.

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `node-version` | string | `"20"` | Node.js version |
| `notify` | boolean | `true` | Send email on release |

### `security-audit.yml` — Dependency Audit

Runs weekly (Monday 08:00 UTC) and on-demand via `workflow_call`.

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `package-manager` | string | `"npm"` | `npm`, `pnpm`, or `yarn` |
| `node-version` | string | `"20"` | Node.js version |
| `audit-level` | string | `"high"` | Minimum severity to fail |

## Secrets

### SMTP (org-level)

Required for PR notifications and release emails:

```
SMTP_SERVER
SMTP_PORT
SMTP_USERNAME
SMTP_PASSWORD
```

### Deployment (per-repo)

Required for SSH deployments:

```
DEPLOY_HOST
DEPLOY_USER
DEPLOY_SSH_KEY
```

Add org-wide secrets at **Settings > Secrets and variables > Actions**.

## Adding Workflows to a New Repo

Create thin caller workflows in your repo's `.github/workflows/`:

```yaml
# .github/workflows/ci.yml
name: CI
on:
  pull_request:
  push:
    branches: [main]

jobs:
  ci:
    uses: LMCustoms/.github/.github/workflows/ci-node.yml@main
    with:
      node-version: "22"
      run-typecheck: true
```

Use `secrets: inherit` to pass org-level secrets:

```yaml
jobs:
  notify:
    uses: LMCustoms/.github/.github/workflows/pr-notifications.yml@main
    secrets: inherit
```

## Team Structure

| Team | Permissions | Purpose |
|------|------------|---------|
| **Owners** | Admin | Full control |
| **Maintainers** | Maintain | Merge PRs, manage releases |
| **Developers** | Write | Push branches, open PRs |
| **Bots** | Write | CI/CD automation |

## Branch Protection

All repos enforce:
- Require PR before merge
- Require 1+ approval
- Require CI passing
- No force push
- No branch deletion
- Require conversation resolution

---

**LMCustoms 2026**
