# casc-renovate-preset-polarion-docker

**Renovate configuration preset for Polarion Docker repositories on GitHub**

Dependency management for Dockerfiles, Docker Compose, Python (uv/pep621), pre-commit hooks, and GitHub Actions with smart automerge and security-first defaults.

---

## Quick Start

Add this to your repository's `renovate.json`:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": [
    "github>SchweizerischeBundesbahnen/casc-renovate-preset-polarion-docker"
  ]
}
```

That's it! Renovate will now:
- Automatically update dependencies across supported ecosystems
- Auto-merge safe updates after a 3-day stabilization period
- Alert on security vulnerabilities with priority PRs
- Maintain lock files weekly

---

## Supported Ecosystems

| Ecosystem | Manager | Auto-Update |
|-----------|---------|-------------|
| **Dockerfile** | dockerfile | Minor/patch (3-day wait) |
| **Docker Compose** | docker-compose | Minor/patch (3-day wait) |
| **Python** | pep621 (uv/pyproject.toml) | Minor/patch (3-day wait) |
| **Pre-commit** | pre-commit | All updates incl. major |
| **GitHub Actions** | github-actions | All updates incl. major |

---

## Automerge Strategy

| Update Type | Automerged? | Stabilization | Notes |
|-------------|-------------|---------------|-------|
| Minor/patch | ✅ Yes | 3 days | Requires CI to pass |
| Major | ❌ No | — | Manual review required |
| GitHub Actions (any incl. major) | ✅ Yes | 3 days | Requires CI to pass |
| Pre-commit hooks (any incl. major) | ✅ Yes | 3 days | ignoreTests: true |
| Python version (major/minor) | ❌ No | — | Manual review required |
| Security vulnerabilities | ❌ No | 0 days | Labeled `security`, priority queue |
| Lock file maintenance | ✅ Yes | — | Monday 4am |

**Branch-based automerge** — silent merges when tests pass, using GitHub's native auto-merge.

**3-day stabilization** — enforced strictly via `internalChecksFilter: strict`. Allows time for the community to discover issues before automerge.

---

## Security

- **OSV vulnerability alerts** enabled
- **No waiting period** for security fixes (`minimumReleaseAge: 0 days`)
- **Priority queue** — security PRs use `prPriority: 99` to jump Renovate's rate limit queue
- **Manual review** required for all security updates (no automerge)
- All vulnerability PRs labeled `security`

---

## Developer Setup

### Prerequisites

- jq (for JSON validation)
- pre-commit

### Validation

```bash
# JSON syntax check
jq empty default.json

# Run all pre-commit hooks
pre-commit run --all-files
```

---

## Deployment

Changes to `default.json` are **live immediately** when merged to `main`. All consuming repositories receive updates on the next Renovate run — there is no staging environment.

---

## Support

For issues or questions, open an issue in this repository.