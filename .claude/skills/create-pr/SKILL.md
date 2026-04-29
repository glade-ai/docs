---
name: create-pr
description: Use when creating a pull request — covers gh pr create command, release labels, draft PRs, and PR description format
sync: true
---

## Creating Pull Requests

### Command

```bash
gh pr create --draft --title "..." --body "..." --label release-minor
```

Always create as `--draft`. The author promotes to ready when it's ready for review.

### Release label (required, default: release-minor)

Exactly one release label is required — CI will fail without it.

| Label | When to use |
|---|---|
| `release-patch` | Bug fixes, documentation, minor improvements, refactoring — no new functionality |
| `release-minor` | New features, endpoints, components, non-breaking enhancements — **default** |
| `release-major` | Breaking changes that affect API consumers or existing functionality |

When in doubt, use `release-minor`. It's easier to downgrade than explain why a feature was a patch.

### PR description

The body must answer **why** — what problem does this solve, what decision was made, why this approach? Avoid descriptions that just restate the title or list changed files.

Good structure:
1. **Why** — the problem or motivation
2. **What** — what was done (brief)
3. **How to verify** — what you tested or how a reviewer can check it

### Example

```bash
gh pr create \
  --draft \
  --title "feat: add retry logic for QB sync failures" \
  --body "$(cat <<'EOF'
QB sync failures were silently dropped when the token expired mid-sync, causing invoices to fall out of sync with no alert.

Added `withQbSyncRetry` wrapper that retries on 429/5xx with exponential backoff and captures to Sentry on final failure.

Tested against an expired token in staging — confirmed retry fires twice then succeeds on token refresh.
EOF
)" \
  --label release-minor
```

### Promoting from draft

Once the PR is ready for review, promote it:

```bash
gh pr ready
```
