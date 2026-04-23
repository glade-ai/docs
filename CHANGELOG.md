# Changelog

Documentation changes are tracked here. Each entry corresponds to a pull request raised by the daily update hook or a manual edit.

## Format

Entries are added automatically when a PR is merged. Each entry has:
- **Heading:** `## YYYY-MM-DD HH:MM · [PR #N](url)` (merge datetime and link to the PR).
- **Body:** The content from the PR description between `<!-- changelog -->` and `<!-- /changelog -->`, or "no details available" if the block was missing or empty.

Use one sub-section per domain/feature inside the changelog block (e.g. `### domain/feature` plus bullets). See CONTRIBUTING.md and AGENTS.md for how to add the block when opening a PR.

```
## YYYY-MM-DD HH:MM · [PR #N](https://github.com/owner/repo/pull/N)

### <domain>/<feature>
- What changed and why
```

---
## 2026-04-23 05:58:03-04:00 · [PR #105](https://github.com/glade-ai/docs/pull/105)

no details available

## 2026-04-16 18:47:17-04:00 · [PR #99](https://github.com/glade-ai/docs/pull/99)

### appointments/scheduling
- Updated client booking flow: free-session booking button now reads "Book a call" (was "Book for free")
- Added documentation for unscheduling: team members can clear a scheduled booking's time, returning it to pending status for client re-selection, with calendar event removal and client notification
- Added documentation for rescheduling canceled/completed bookings: team members can assign a new time, recreating calendar events, reminders, and email notifications

## 2026-04-16 12:53:05-04:00 · [PR #100](https://github.com/glade-ai/docs/pull/100)

### integrations/efiling
- Added documentation for the Contact Support button that appears on non-retryable e-filing errors: sends a pre-filled message to the support conversation and opens the chat
- Added edge case note: the button only appears for non-retryable errors and gracefully degrades when no support conversation exists

## 2026-04-10 11:16:08-04:00 · [PR #90](https://github.com/glade-ai/docs/pull/90)

no details available

## 2026-04-10 11:15:18-04:00 · [PR #87](https://github.com/glade-ai/docs/pull/87)

no details available

## 2026-04-08 13:56:56-04:00 · [PR #86](https://github.com/glade-ai/docs/pull/86)

no details available

## 2026-04-07 11:40:44-04:00 · [PR #81](https://github.com/glade-ai/docs/pull/81)

no details available

## 2026-03-08 17:52:22-07:00 · [PR #11](https://github.com/glade-ai/docs/pull/11)

### (infra)
- Add `.github/workflows/changelog-on-merge.yml`: **changelog-on-merge** job runs on push to `main` when the push includes merge commits; loops over each merged PR, extracts content between `<!-- changelog -->` and `<!-- /changelog -->` from the PR body (or uses "no details available"), inserts one section per PR after `---` in CHANGELOG (datetime, PR link, content). Idempotency: skip if PR already in CHANGELOG.
- **changelog-pr-check** job runs on `pull_request` for `**/*.md`: requires both `<!-- changelog -->` and `<!-- /changelog -->` with non-empty content between them.
- Update CHANGELOG.md Format section to describe the new entry shape.
- Update AGENTS.md and CONTRIBUTING.md: changelog block with one sub-section per domain/feature, both tags required.

## 2026-03-06

### payments/invoices
- Replaced placeholder with comprehensive invoice documentation covering the full invoice lifecycle, payment methods, templates, payment plans, processing fees, PDF generation, notifications, permissions, versioning, QuickBooks integration, and trust accounting.

### (initial)
- Initial scaffolding: six domain folders with placeholder feature files.
