# MCP Tools Reference

## Overview

The Glade MCP Server provides 39 read-only tools organized into categories. You don't need to call these tools directly — your AI assistant selects the right ones based on your questions. This reference is useful if you want to understand exactly what data is available or troubleshoot why a question isn't returning the results you expect.

## Key Behaviors

All tools share these behaviors:

- **Read-only** — no tool can create, modify, or delete data.
- **Permission-scoped** — results are limited to what you have access to in Glade.
- **Paginated** — list tools return results in pages (default 20, max 100 per page).

### Getting started

The AI assistant typically begins with `persons_me` to identify who you are and which firms (creators) you belong to. Most other tools require a creator ID, which comes from this first step.

## Tools by Category

### Your Profile

| Tool | What it does |
|------|-------------|
| `persons_me` | Returns your profile and all your relationships — which creators (firms) you belong to, your teams, organizations, and agencies. This is the starting point for most queries. |

### Creators (Firms)

| Tool | What it does |
|------|-------------|
| `creators_list` | Lists the creators (firms/teams) you belong to. |
| `creators_get` | Gets details for a specific creator. |

### Customers

| Tool | What it does |
|------|-------------|
| `customers_list` | Lists customers for a firm. Paginated. |
| `customers_get` | Gets a customer's full profile including contact info and preferences. |

### Cases & Workflows

| Tool | What it does |
|------|-------------|
| `user_workflows_list` | Lists cases for a firm. Filter by status, assignee, last activity date, or workflow template. |
| `user_workflows_get` | Gets full case details including steps, data fields, collaborators, owners, and task summary. |
| `case_data_schema_get` | Gets the global schema defining all structured case data fields (parties, attorneys, billing, IDs). |
| `case_data_list` | Gets all resolved data for a specific case, including provenance and conflict status. |

### Workflow Templates

| Tool | What it does |
|------|-------------|
| `workflows_list` | Lists available workflow templates. Filter by state (current, draft, stale), type, or enabled status. |
| `workflows_get` | Gets a workflow template's full structure — its steps and data collection fields. |

### Tasks

| Tool | What it does |
|------|-------------|
| `tasks_list` | Lists tasks for a firm. Filter by workflow, assignee, completion status, or action type. |
| `tasks_get` | Gets full task details including data payload and assignees. |

### Invoices

| Tool | What it does |
|------|-------------|
| `invoices_list` | Lists invoices for a firm. Filter by status, customer, or date range. |
| `invoices_get` | Gets full invoice details including line items and payment history. |

### Payments

| Tool | What it does |
|------|-------------|
| `payments_list` | Lists payments for a firm. Filter by status, customer, or date range. |
| `payments_get` | Gets full payment details including fees and related metadata. |

### Payment Plans

| Tool | What it does |
|------|-------------|
| `payment_plans_list` | Lists payment plans for a firm. Filter by status or date range. |
| `payment_plans_get` | Gets full payment plan details including installment schedule and payment method. |

### Task Efficiency

| Tool | What it does |
|------|-------------|
| `task_efficiencies_list` | Lists individual task efficiency records. Filter by workflow, type, completion status, or date range. |
| `task_efficiencies_get` | Gets a specific task efficiency record with timing and reopen metrics. |
| `task_efficiency_aggregate_list` | Gets aggregate efficiency metrics grouped by workflow template and task type — completion rates and time-to-completion statistics. |
| `task_efficiency_reports_list` | Lists AI-generated task efficiency reports. Filter by date range. |
| `task_efficiency_reports_get` | Gets a specific AI-generated efficiency report with full content. |

### Team Members

| Tool | What it does |
|------|-------------|
| `team_members_list` | Lists team members for a firm with their roles. |
| `team_members_get` | Gets a specific team member's profile and role. |

### Organizations

| Tool | What it does |
|------|-------------|
| `organizations_list` | Lists organizations for a firm. |
| `organizations_get` | Gets organization details. |
| `organization_members_list` | Lists members of an organization with their permissions. |
| `organization_members_get` | Gets a specific organization member's details and permissions. |

### Agencies

| Tool | What it does |
|------|-------------|
| `agencies_list` | Lists agencies you belong to (as owner or member). |
| `agencies_get` | Gets agency details. |
| `agency_members_list` | Lists members of an agency. |
| `agency_members_get` | Gets a specific agency member's details. |

### Documentation

| Tool | What it does |
|------|-------------|
| `docs_list` | Lists available product documentation, optionally filtered by domain (e.g., payments, intake, crm). Returns titles and paths without full content. |
| `docs_get` | Gets the full content of a specific documentation page by its path (e.g., `payments/invoices`). |
| `docs_search` | Searches documentation by keyword across titles and content. Use when you're not sure where to look. |

## Edge Cases & Limitations

- **Creator ID required** — most tools require a creator ID. The AI gets this automatically from `persons_me`, but if you belong to multiple firms, you may need to specify which one.
- **Date filters use ISO 8601** — date parameters expect ISO 8601 format (e.g., `2025-01-15T00:00:00Z`). The AI handles this conversion from natural language.
- **Pagination** — list tools default to 20 results per page with a maximum of 100. For very large datasets, the AI may need to make multiple requests.
- **No write operations** — if you ask the AI to change something, it will tell you the change needs to be made in the Glade app.

## Related Features

- [MCP Overview](overview.md)
