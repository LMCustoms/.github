# LMCustoms Organization Configuration

This repository contains organization-wide defaults, workflows, and documentation for all LMCustoms repositories.

## 📂 Structure

```
.github/
├── workflows/           # Reusable GitHub Actions workflows
│   ├── ci.yml          # Lint, test, build pipeline
│   ├── pr-notifications.yml  # Email notifications for PRs
│   └── release.yml     # Semantic versioning & releases
├── profile/
│   └── README.md       # Organization profile (appears on org page)
├── SECURITY.md         # Security policy
├── CONTRIBUTING.md     # Contribution guidelines
└── CODE_OF_CONDUCT.md  # Community standards
```

## 🔧 Workflows

### CI Pipeline (`ci.yml`)

Automatically runs on PRs and pushes to `main`/`develop`:

- **Lint** — Code style checks
- **Test** — Run test suites
- **Build** — Compile/bundle projects
- **Notify** — Send results to `alert@lmcustoms.cc`

Supports: Node.js, Rust, Python projects.

### PR Notifications (`pr-notifications.yml`)

Sends email to `pr@lmcustoms.cc` when:
- PR opened/reopened/closed
- Review requested
- Review submitted

### Release Workflow (`release.yml`)

Semantic versioning based on [Conventional Commits](https://www.conventionalcommits.org/):

- `feat:` → Minor version bump
- `fix:` → Patch version bump
- `BREAKING CHANGE:` → Major version bump

Automatically:
- Tags releases
- Generates changelogs
- Creates GitHub releases
- Notifies `alert@lmcustoms.cc`

## 📧 Email Setup

Workflows require SMTP secrets:

```
SMTP_SERVER
SMTP_PORT
SMTP_USERNAME
SMTP_PASSWORD
```

Add these to **Organization Secrets** (Settings → Secrets and variables → Actions).

## 🎯 Team Structure

| Team | Permissions | Purpose |
|------|------------|---------|
| **Owners** | Admin | Full control |
| **Maintainers** | Maintain | Merge PRs, manage releases |
| **Developers** | Write | Push branches, open PRs |
| **Bots** | Write | CI/CD automation |

## 🔒 Branch Protection

All repos enforce:
- ✅ Require PR before merge
- ✅ Require 1+ approval
- ✅ Require CI passing
- ❌ No force push
- ❌ No branch deletion
- ✅ Require conversation resolution

## 📋 Repository Defaults

New repos automatically inherit:
- Issue templates (bug, feature, question)
- PR template (checklist)
- Security policy
- Contributing guide
- Code of Conduct

## 🚀 Creating New Repos

1. Create repo via GitHub
2. Enable **Dependabot** alerts
3. Add repo to teams (Owners=admin, Maintainers=maintain, Developers=write)
4. Apply branch protection to `main`
5. Push initial commit following conventional commits

Workflows will automatically activate on first PR/push.

## 📖 Documentation

See `docs` repo for comprehensive project documentation.

---

**© 2026 LMCustoms. All rights reserved.**
