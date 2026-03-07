# Glade MCP Server

## Overview

The Glade MCP Server connects AI assistants — such as Claude — to a firm's Glade data through the Model Context Protocol (MCP). It provides read-only access to customers, cases, invoices, payment plans, tasks, team members, and organizational data. Firms authenticate through their standard Glade login, and all data access is scoped to what the authenticated user is authorized to see.

## Key Behaviors

The MCP server acts as a bridge between MCP-compatible AI assistants and the Glade platform. It exposes 28 read-only tools that AI assistants can call to query firm data. All queries respect the same access controls as the Glade app — users only see data they have permission to access. No data can be created, modified, or deleted through the MCP server.

### Supported AI clients

- **Claude Code** (command-line tool) — auto-discovers the server and prompts for login.
- **Claude.ai** (web) — connect via Settings > Connectors > Add custom connector.
- Any MCP-compatible client that supports OAuth 2.1 or bearer token authentication.

### Available data categories

| Category | What you can query |
|----------|--------------------|
| **Customers** | Customer list, contact details, verification status, communication preferences |
| **Cases & Workflows** | Open and closed cases, case data fields (parties, attorneys, billing, case IDs), workflow steps and progress, collaborators |
| **Tasks** | Pending and completed tasks, assignments, task details, filtering by workflow or assignee |
| **Invoices** | Invoice list with status filtering, line items, payment history, date range queries |
| **Payment Plans** | Active and completed plans, installment schedules, payment method details |
| **Team Members** | Team roster, roles (admin, case worker, finance) |
| **Organizations** | Organization details, member lists, member permissions |
| **Agencies** | Agency details, membership |

### How authentication works

When connecting for the first time, the AI client prompts the user to log in through Glade's standard login page. After login, the server issues a secure token that the AI client uses for subsequent requests. The token identifies who the user is and what data they can access. All data queries are scoped to the authenticated user's permissions — there is no way to access another firm's data.

### Example use cases

- "Show me all unpaid invoices" — the AI queries the invoice list filtered by status.
- "What's the status of the Jones case?" — the AI retrieves case data and workflow progress.
- "List pending tasks assigned to Sarah" — the AI queries tasks filtered by assignee and completion status.
- "How many active payment plans do we have?" — the AI lists payment plans filtered by status.
- "Who are my team members?" — the AI retrieves the team roster with roles.

### How queries work

The AI assistant translates natural language questions into structured data queries. Results are returned in pages (default 20 items, up to 100 per page) for large datasets. The AI can combine multiple queries to answer complex questions (e.g., finding a customer's cases, then their invoices). All queries are read-only and cannot change any data.

### Case data and conflict detection

Case data fields follow a structured schema (primary party, secondary party, attorney information, billing details, case identifiers). When multiple sources provide different values for the same field (e.g., a form submission and a manual entry disagree on an address), the system flags the conflict. The AI can surface these conflicts to help staff resolve discrepancies.

### Security

- Read-only access — no risk of accidental data changes.
- Per-user data isolation — each user only sees data from firms they belong to.
- All connections encrypted (HTTPS).
- Login credentials are never shared with the AI assistant.
- All access is logged for auditing.
- Supports token rotation for security best practices.

## Configuration

| Setting | Description |
|---------|-------------|
| MCP server URL | `https://mcp.prod.glade.ai/mcp` (production) or `https://mcp.staging.glade.ai/mcp` (staging) |
| Authentication | Standard Glade login — no separate credentials needed |
| Data scope | Determined by the authenticated user's existing Glade permissions |

To connect in Claude Code: add the server URL and authenticate when prompted.

To connect in Claude.ai: go to Settings > Connectors > Add custom connector and enter the server URL.

## Edge Cases & Limitations

- **Read-only** — the MCP server cannot create, update, or delete any data. All changes must be made through the Glade app.
- **Pagination required** — large result sets are returned in pages (up to 100 items per page). The AI assistant handles pagination automatically, but very large queries may require multiple requests.
- **No full-text search** — queries filter by structured fields (status, date range, assignee) rather than free-text search across all content.
- **Token expiration** — authentication tokens expire after 60 days. The AI client handles re-authentication automatically when needed.
- **Conflict visibility** — the server can surface data conflicts (when multiple sources disagree) but cannot resolve them. Staff must resolve conflicts in the Glade app.
- **Calendar provider required for some data** — some case data fields depend on external integrations being configured.
- **No file or document access** — the MCP server provides structured data only; it does not serve document files, PDFs, or attachments.

## Related Features

- [Invoices](../payments/invoices.md)
- [Payment Plans](../payments/payment-plans.md)
- [Scheduling](../appointments/scheduling.md)
