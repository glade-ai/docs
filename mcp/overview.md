# Glade MCP Server

## Overview

The Glade MCP Server connects AI assistants to your firm's Glade data through the [Model Context Protocol](https://modelcontextprotocol.io/) (MCP). It provides read-only access to your customers, cases, invoices, payment plans, tasks, team members, and more. You authenticate with your standard Glade login, and all data access is scoped to what you're authorized to see — the same permissions as the Glade app.

## Key Behaviors

### What is MCP?

MCP is an open protocol that lets AI assistants connect to external data sources. Instead of copying data into a chat, the AI can query your Glade account directly — asking structured questions like "show me unpaid invoices" or "what tasks are assigned to Sarah" and getting real answers from your live data.

### Supported AI clients

The Glade MCP server works with any MCP-compatible AI client, including:

- **Claude Desktop** — connect via Settings > Integrations > Add custom integration.
- **Claude Code** (command-line tool) — auto-discovers the server and prompts for login.
- **Claude.ai** (web) — connect via Settings > Connectors > Add custom connector.
- Other MCP-compatible clients that support OAuth 2.1 or bearer token authentication.

### What you can access

| Category | What you can query |
|----------|--------------------|
| **Customers** | Customer list, contact details, verification status, communication preferences |
| **Cases & Workflows** | Open and closed cases, case data fields (parties, attorneys, billing, case IDs), workflow steps and progress, collaborators |
| **Workflow Templates** | Available workflow templates, their steps, and data collection fields |
| **Tasks** | Pending and completed tasks, assignments, task details, filtering by workflow or assignee |
| **Invoices** | Invoice list with status filtering, line items, payment history, date range queries |
| **Payments** | Payment records with status, fees, and related metadata |
| **Payment Plans** | Active and completed plans, installment schedules, payment method details |
| **Task Efficiency** | Individual task timing metrics, aggregate statistics by workflow and task type, AI-generated efficiency reports |
| **Team Members** | Team roster and roles |
| **Organizations** | Organization details, member lists, member permissions |
| **Agencies** | Agency details and membership |
| **Documentation** | Browse, read, and search Glade's product documentation by topic |

### How authentication works

When connecting for the first time, the AI client prompts you to log in through Glade's standard login page. After login, the server issues a secure token that the AI client uses for subsequent requests. The token identifies who you are and what data you can access. All data queries are scoped to your permissions — there is no way to access another firm's data.

### Example questions you can ask

- "Show me all unpaid invoices" — queries invoices filtered by status.
- "What's the status of the Jones case?" — retrieves case data and workflow progress.
- "List pending tasks assigned to Sarah" — queries tasks filtered by assignee and completion status.
- "How many active payment plans do we have?" — lists payment plans filtered by status.
- "Who are my team members and what are their roles?" — retrieves the team roster.
- "How efficient are we at completing intake tasks?" — pulls task efficiency metrics.
- "How do online payments work in Glade?" — searches the product documentation.

### How queries work

The AI assistant translates your natural language questions into structured data queries. Results are returned in pages (default 20 items, up to 100 per page) for large datasets. The AI can combine multiple queries to answer complex questions — for example, finding a customer's cases, then pulling their invoices. All queries are read-only and cannot change any data.

### Getting started

The AI assistant uses a "start here" tool called `persons_me` to understand who you are and what firms you belong to. From there, it navigates to the specific data you're asking about. You don't need to know the tool names — just ask questions in plain language and the AI figures out which tools to call.

### Case data and conflict detection

Case data fields follow a structured schema covering primary and secondary parties, attorney information, billing details, and case identifiers. When multiple sources provide different values for the same field (e.g., a form submission and a manual entry disagree on an address), the system flags the conflict. The AI can surface these conflicts to help you resolve discrepancies.

### Security

- **Read-only access** — no risk of accidental data changes.
- **Per-user data isolation** — you only see data from firms you belong to.
- **All connections encrypted** (HTTPS).
- **Login credentials are never shared** with the AI assistant.
- **All access is logged** for auditing.
- **Token rotation** supported for security best practices.

## Configuration

| Setting | Description |
|---------|-------------|
| MCP server URL | `https://mcp.prod.glade.ai/mcp` (production) or `https://mcp.staging.glade.ai/mcp` (staging) |
| Authentication | Standard Glade login — no separate credentials needed |
| Data scope | Determined by your existing Glade permissions |

**Claude Desktop**: Go to Settings > Integrations > Add custom integration and enter the server URL.

**Claude Code**: Add the server URL to your MCP configuration and authenticate when prompted.

**Claude.ai**: Go to Settings > Connectors > Add custom connector and enter the server URL.

## Edge Cases & Limitations

- **Read-only** — the MCP server cannot create, update, or delete any data. All changes must be made through the Glade app.
- **Pagination** — large result sets are returned in pages (up to 100 items per page). The AI assistant handles pagination automatically, but very large queries may require multiple requests.
- **No full-text search on operational data** — queries on customers, cases, invoices, etc. filter by structured fields (status, date range, assignee) rather than free-text search. Documentation search does support keyword matching.
- **Token expiration** — authentication tokens expire after 60 days. The AI client handles re-authentication automatically when needed.
- **Conflict visibility** — the server can surface data conflicts (when multiple sources disagree) but cannot resolve them. Resolve conflicts in the Glade app.
- **No file or document access** — the MCP server provides structured data and product documentation. It does not serve uploaded files, PDFs, or attachments.

## Related Features

- [Tools Reference](tools-reference.md)
- [Invoices](../payments/invoices.md)
- [Payment Plans](../payments/payment-plans.md)
