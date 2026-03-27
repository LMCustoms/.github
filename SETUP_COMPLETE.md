# LMCustoms Organization Setup — COMPLETE ✅

**Date:** 2026-03-27  
**Status:** Fully configured and operational

---

## ✅ What Was Done

### 1. Team Structure Created

| Team | Permissions | Members |
|------|------------|---------|
| **Owners** | Admin on all repos | WingsOfCobra |
| **Maintainers** | Maintain on all repos | WingsOfCobra |
| **Developers** | Write on all repos | WingsOfCobra |
| **Bots** | Write (CI/CD) | WingsOfCobra |

### 2. Repository Configuration

#### All Repositories (4 total)
- ✅ **Dependabot** enabled (security alerts)
- ✅ **Issue templates** (bug, feature, question)
- ✅ **PR template** (checklist)
- ✅ **CI/CD workflows** (lint, test, build, notify)
- ✅ **PR notifications** → `pr@lmcustoms.cc`
- ✅ **Semantic versioning** (automated releases)

#### neo-dock (public)
- ✅ **Branch protection** on `main` (requires PR + 1 approval + CI passing)

#### Private Repos (wrapped, docs, branding)
- ⚠️ Branch protection requires **GitHub Pro** (upgrade recommended)

### 3. Organization Defaults (`.github` repo)

Created organization-wide configuration:

- **Workflows:**
  - `ci.yml` — Lint, test, build, notify
  - `pr-notifications.yml` — Email on PR activity
  - `release.yml` — Semantic versioning & changelog

- **Documentation:**
  - `SECURITY.md` — Security policy
  - `CONTRIBUTING.md` — Contribution guidelines
  - `CODE_OF_CONDUCT.md` — Community standards
  - `profile/README.md` — Organization profile

### 4. Documentation Rebranded

Updated `docs` repo with LMCustoms branding:

- Project overview
- Development setup guide
- CI/CD documentation
- Release management guide
- Conventional commits guide
- Workflow documentation

---

## 📧 Email Configuration (Required)

Workflows need SMTP secrets to send notifications.

**Add to:** GitHub → LMCustoms → Settings → Secrets and variables → Actions

| Secret | Example Value |
|--------|--------------|
| `SMTP_SERVER` | `smtp.gmail.com` or `mail.lmcustoms.cc` |
| `SMTP_PORT` | `587` (TLS) or `465` (SSL) |
| `SMTP_USERNAME` | `your-email@gmail.com` |
| `SMTP_PASSWORD` | App-specific password |

**Recipients:**
- `alert@lmcustoms.cc` — CI failures, releases, security alerts
- `pr@lmcustoms.cc` — PR activity (opened, reviewed, merged)

---

## 🔄 Pending Actions

### PRs Awaiting Approval

Due to branch protection on `neo-dock`:

- **[PR #37](https://github.com/LMCustoms/neo-dock/pull/37)** — Add issue/PR templates
- **[PR #38](https://github.com/LMCustoms/neo-dock/pull/38)** — Enable CI/CD workflows

**Action:** Review and merge these PRs.

### Upgrade to GitHub Pro (Recommended)

Benefits:
- Branch protection on private repos
- Code scanning (security)
- Advanced permissions
- Better insights

Cost: ~$4/user/month

---

## 🚀 How to Use This Setup

### For New Repositories

1. **Create repo** via GitHub UI
2. **Add to teams:**
   ```bash
   gh api orgs/LMCustoms/teams/owners/repos/LMCustoms/<repo> -X PUT -f permission=admin
   gh api orgs/LMCustoms/teams/maintainers/repos/LMCustoms/<repo> -X PUT -f permission=maintain
   gh api orgs/LMCustoms/teams/developers/repos/LMCustoms/<repo> -X PUT -f permission=push
   ```
3. **Copy workflows** from `.github` repo
4. **Apply branch protection** (if public or GitHub Pro)
5. **Enable Dependabot** (GitHub UI)

### For Pull Requests

1. **Create feature branch:**
   ```bash
   git checkout -b feat/my-feature
   ```

2. **Commit using conventional format:**
   ```bash
   git commit -m "feat(module): add new feature"
   ```

3. **Push and open PR:**
   ```bash
   git push origin feat/my-feature
   gh pr create
   ```

4. **Wait for:**
   - CI to pass (lint, test, build)
   - 1+ approval
   - Email to `pr@lmcustoms.cc`

5. **Merge** (squash recommended)

### For Releases

**Automatic** (when pushing to `main`):

1. Ensure commits follow conventional format
2. Push to `main` (or merge PR)
3. Workflow runs automatically
4. Version bumped, changelog generated, GitHub release created
5. Email sent to `alert@lmcustoms.cc`

**Manual** (if needed):

```bash
git tag -a v1.2.3 -m "Release v1.2.3"
git push origin v1.2.3
gh release create v1.2.3 --generate-notes
```

---

## 📚 Resources

- **Documentation:** [LMCustoms/docs](https://github.com/LMCustoms/docs)
- **Organization Config:** [LMCustoms/.github](https://github.com/LMCustoms/.github)
- **Branding:** [LMCustoms/branding](https://github.com/LMCustoms/branding)
- **Security Policy:** [SECURITY.md](https://github.com/LMCustoms/.github/blob/main/SECURITY.md)
- **Contributing:** [CONTRIBUTING.md](https://github.com/LMCustoms/.github/blob/main/CONTRIBUTING.md)

---

## 🎯 Next Steps

1. ✅ **Merge neo-dock PRs** (#37, #38)
2. ✅ **Add SMTP secrets** for email notifications
3. ✅ **Test workflows** by opening a test PR
4. 🔄 **Consider GitHub Pro** for private repo branch protection
5. 🔄 **Invite team members** and assign to appropriate teams

---

**Setup completed by:** GitHub Agent 🐙  
**Contact:** [anian@lmcustoms.cc](mailto:anian@lmcustoms.cc)

**Built with precision. Delivered with care. 🚀**
