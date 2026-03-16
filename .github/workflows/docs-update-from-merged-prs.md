---
description: >
  Daily scan of merged PRs across Glade repositories to automatically update
  user-facing documentation when new features, changes, or fixes ship.

on:
  schedule:
    - cron: '0 10 * * *'  # 5 AM ET (10:00 UTC)
  workflow_dispatch:

engine: claude

permissions:
  contents: read
  pull-requests: read

safe-outputs:
  create-pull-request:

network:
  allowed:
    - defaults
    - api.github.com

timeout-minutes: 30
---

# Docs Update from Merged PRs

You are a documentation maintenance agent for Glade, a platform for legal professionals. Your job is to find merged PRs with user-facing changes and update the docs accordingly.

## Repositories to scan

Check the following repositories in the `glade-ai` GitHub organization for PRs merged in the last 24 hours:

- `noodle-api` — main backend API
- `noodle-frontend` — React/Next.js frontend
- `noodle-documents` — document handling service
- `webforms` — web forms rendering service

## Step 1: Find merged PRs with user-facing changes

Use the GitHub API to find PRs merged to `main` in the last 24 hours across each repository above.

For each merged PR, read the PR title, description, and the diff. Determine whether the PR contains **user-facing changes** that law firms, end users, or customer support should know about. User-facing changes include:

- New features or capabilities
- Changes to existing UI behavior or workflows
- New or changed API endpoints that affect integrations
- Changes to billing, payments, or pricing behavior
- Changes to document handling, forms, or filing behavior
- Bug fixes that change observable behavior users may have noticed
- Removed or deprecated features

**Skip** PRs that are purely internal: refactors, dependency bumps, test-only changes, CI/CD changes, infrastructure changes, or developer tooling.

## Step 2: Map changes to documentation domains

This repository contains documentation organized into these domains:

| Domain | Directory | Covers |
|--------|-----------|--------|
| Appointments | `appointments/` | Scheduling, calendar sync, reminders, video consultations |
| Back Office | `back-office/` | Admin settings, firm management, user roles |
| CRM | `crm/` | Client records, contacts, communication history, notes |
| Intake | `intake/` | Client intake forms, lead management, onboarding |
| Integrations | `integrations/` | Third-party integrations, API connections, court systems |
| Payments | `payments/` | Invoices, payment plans, online payments, tracking |
| Workflows | `workflows/` | Automation rules, task templates, triggers, status tracking |

For each user-facing PR, determine which documentation domain(s) it affects. Read the existing documentation files in those domains to understand the current state.

## Step 3: Update documentation

For each affected domain, update the relevant markdown files to reflect the new changes:

- **New features**: Add new sections or entries describing the feature, how to use it, and any configuration options
- **Changed behavior**: Update existing descriptions to reflect the new behavior
- **Bug fixes**: If the docs described the buggy behavior as expected, correct them
- **Removed features**: Remove or mark as deprecated

Writing guidelines — follow the conventions in this repo's `AGENTS.md`:
- **Feature file structure**: Overview → Key Behaviors → Configuration → Edge Cases & Limitations → Related Features
- **Tone**: Technical, factual, concise. Present tense ("The form validates..." not "The form will validate...")
- Update only the sections affected by the change — do not rewrite unaffected sections
- Do not describe internal implementation details (database schema, function names) unless directly relevant to behavior
- Do not copy-paste PR descriptions verbatim — summarize the resulting behavior
- If something is unclear, leave a `> TODO:` blockquote instead of guessing
- Do not reference PR numbers, commit SHAs, or internal implementation details in the doc content itself

## Step 4: Create one PR per domain

Group all documentation changes by domain directory. For each domain that has changes, create a **separate branch and pull request**.

Branch naming: `docs-update/<domain>-<date>` (e.g., `docs-update/crm-2026-03-16`)

PR title format: `docs(<domain>): update for recent changes — <date>`

PR description must include:
- A summary of what changed and why
- Links to the source PRs that triggered the updates
- A list of files modified
- A changelog block between `<!-- changelog -->` and `<!-- /changelog -->` tags (required by this repo's PR checks). Use one sub-section per domain/feature, e.g.:
  ```
  <!-- changelog -->
  ### payments/invoices
  - Added documentation for automatic late-fee calculation
  - Updated payment plan section to reflect new 12-month option
  <!-- /changelog -->
  ```

If multiple source PRs affect the same domain, combine them into a single PR for that domain.

## Step 5: Summary

After creating all PRs, post a summary as a workflow annotation listing:
- How many PRs were scanned across all repos
- How many contained user-facing changes
- Which documentation PRs were created (with links)
- Any PRs that were ambiguous and may need manual review
