# MCP Tools Reference

## Overview

The Glade MCP Server provides tools across multiple categories, including profile, customers, cases, workflows, tasks, invoices, payments, payment plans, task efficiency, team members, organizations, agencies, court notices, dockets, custom reports, and documentation. Most are read-only; a small set of actions that change data is being introduced separately — see [Write actions](#write-actions). You don't need to call these tools directly — your AI assistant selects the right ones based on your questions. This reference is useful if you want to understand exactly what data is available or troubleshoot why a question isn't returning the results you expect.

## Key Behaviors

All tools share these behaviors:

- **Permission-scoped** — results are limited to what you have access to in Glade, and an action you could not perform in the app cannot be performed through the assistant either.
- **Paginated** — list tools return results in pages (default 20, max 100 per page).
- **Read by default** — every tool listed below is read-only unless it appears under [Write actions](#write-actions).

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
| `customers_list` | Lists customers for a firm. Can be narrowed by a search term matching name, email, phone, contact phone, date of birth, or the last four digits of a Social Security number. Paginated. |
| `customers_get` | Gets a customer's full profile including contact info and preferences. |

### Cases & Workflows

| Tool | What it does |
|------|-------------|
| `user_workflows_list` | Lists cases for a firm. Filter by status, assignee, last activity date, or workflow template, or narrow by a search term matching the client's name or email, the case number, or the name or email of another person on the case. Paginated. |
| `user_workflows_get` | Gets full case details including steps, data fields, collaborators, owners, and task summary. |
| `case_data_schema_get` | Gets the global schema defining all structured case data fields (parties, attorneys, billing, IDs). |
| `case_data_list` | Gets all resolved data for a specific case, including provenance and conflict status. |

**Finding one client or one case by name.** Both list tools accept a search term, so the assistant can answer "what's the status of Maria Alvarez's case" with a single lookup. Previously neither could filter by name, so the only way to find one client was to page through the firm's whole list — hundreds of requests on a large firm, and slow enough that broad questions often stalled or gave up before producing an answer. If your assistant has struggled to find a specific client or case by name, retry those questions.

- Searching cases also matches other people on the case, so a case can be found by a spouse's or co-debtor's name as well as the primary client's.
- Case numbers are matched as a whole value rather than word by word, so a case number never matches a different case that happens to share a fragment of it.

In addition to the tools above, the assistant can read the case's **internal team message thread** — the firm-side discussion attached to the workflow, separate from the client-facing inbox conversation. Messages include their attachments (id, type, reference, and title). When a message has a document attachment, the assistant can fetch a short-lived signed download URL for the document. Cases that don't have an internal thread return an empty list.

> TODO: confirm the exact tool names exposed for `GET /user-workflows/:id/messages` and `GET /user-workflows/:id/attachments/:id/download` once they appear in the MCP tool registry.

### Form Requests (Intake Form Answers)

| Tool | What it does |
|------|-------------|
| `form_requests_list` | Lists intake form requests for a firm, optionally narrowed to a single case. Each entry includes the client's submitted answers as plain question-and-answer pairs. Paginated. |
| `form_requests_get` | Gets a single form request with its full set of submitted answers as question-and-answer pairs. |

These tools let the assistant read and summarize what a client entered on an intake form — for both the firm's intake forms and Glade questionnaires — so you can ask questions like "what did this client say about their assets?" without opening the case in the Glade app. The answers are returned with their question labels, so the assistant doesn't need to guess what each value means.

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

### eFiling

These tools let a firm run its own review over a case before it is filed — its own AI assistant, its own criteria — using the same information the eFiling packet screen shows.

| Tool | What it does |
|------|-------------|
| eFiling packet — get | Returns a case's whole filing packet in one read: the district resolved for the case, every document slot that district requires with the file currently occupying it, whether the packet is ready to send to PACER, and the pre-filing review's findings. Use this for "is this case ready to file" questions — the alternative is assembling the district, the documents, and the review from separate reads and hoping they describe the same moment. |
| eFiling district — get | Returns the district resolved for a case, including its filing method and any filing notes. |
| Filing review — get | Returns the most recent pre-filing review for a case with its findings, including which findings an attorney has signed off on and which have been dismissed. Paginated. |

> TODO: Confirm the registered MCP tool names for the three eFiling tools once the matching `glade-mcp-server` companion is settled.

### Court Notices

| Tool | What it does |
|------|-------------|
| Court notices — list | Lists PACER court notices for a firm. Paginated. Filterable by case, workflow, notice type, and date range, so the assistant can answer questions like "what motions were filed last week on case X" without having to scan unrelated docket activity. Asking about one workflow returns the notices for the whole matter — see below. |
| Court notices — get | Returns the full content of a single court notice, including its body text and the IDs of any attachments. |
| Court notice attachment — download | Returns a short-lived signed URL for a specific attachment on a court notice so the document can be retrieved. Non-document attachments return a null URL. |

**Court notices cover the whole matter, not one workflow.** A matter often carries several workflows — a retainer alongside a filing workflow, or a new one created when a case converts chapter — and court notices are attached to whichever workflow the case was filed under. Asking the assistant about a case returns its notices regardless of which workflow you name, so a question asked against the retainer no longer comes back empty on a case with an active docket.

Notices from a different matter are never included. Only workflows belonging to the same case are considered.

### Dockets

| Tool | What it does |
|------|-------------|
| Docket — get | Returns the cached PACER docket for a case by case number, including the header information and every docket entry. Use this for questions about the complete historical record on a case rather than for recent activity (which Court Notices covers). |

> TODO: Confirm the registered MCP tool names for the four endpoints above once the matching `glade-mcp-server` companion is settled (court notices list, court notices get, court notice attachment download, docket get).

### Inbox Conversations

The assistant can read messages on inbox conversations between the firm and a client. Message responses include any attachments on the message (id, type, reference, and title). When a message has a document attachment, the assistant can fetch a short-lived signed download URL for the document. Non-document attachments return a null URL.

> TODO: confirm the exact tool name exposed for `GET /conversations/:id/attachments/:id/download` once it appears in the MCP tool registry.

### Custom Reports

The saved Custom Reports your firm builds under **Workflow Reports → Custom Reports** can be read and managed through the assistant. A report the assistant creates is a real saved report — it appears on the firm's dashboard alongside the ones your team built by hand, and can be opened, edited, and exported there.

| Tool | What it does |
|------|-------------|
| Custom reports — list | Lists the firm's saved custom reports. Searchable by name, and filterable by who created the report. Paginated. |
| Custom reports — get | Returns one saved report with the data it covers, its columns, its filters, and its sort order. |

Creating, editing, duplicating, and deleting a saved report are write actions — see below.

> TODO: Confirm the registered MCP tool names for the custom report tools once the matching `glade-mcp-server` companion is settled.

### Write actions

Alongside the read tools, a set of actions can change data. These cover the support requests the assistant could previously only describe rather than carry out.

| Area | What the assistant can do |
|------|--------------------------|
| **Bookings** | Cancel a consultation, or reschedule it to a new time and optionally a different team member. |
| **Clients and contacts** | Correct a client's, spouse's, or contact's name, email address, or phone number. |
| **Team** | Invite a team member, and correct a team member's role — including the case where a member has no role recorded and the firm cannot add anyone new until it is fixed. |
| **Invoices and payments** | Void an invoice, refund a payment in full or in part, and remove processing fees from an invoice. |
| **Cases** | Resend a client's portal invitation, re-run a workflow step that did not fire, and re-run AI extraction on a document that was read incorrectly. |
| **Custom reports** | Create, edit, duplicate, and delete a saved custom report. |

How these are guarded:

- **Write actions are off unless your firm has them switched on.** Where they are not enabled, the assistant answers as it does today — it explains what to change and leaves the change to you.
- **Your own permissions still apply.** Inviting a team member or changing a role requires the same team-management permission the app requires; without it the action is refused. Every action is scoped to your firm, and an action aimed at another firm's record is refused as not found.
- **Sensitive client fields are deliberately out of reach.** Date of birth, Social Security number, and address cannot be changed through the assistant — only name, email, and phone.
- **A portal invitation always goes to the case's own client.** The recipient is taken from the case rather than supplied in the request, so an invitation cannot be redirected to someone else.
- **Money actions are confirmed before they run.** The assistant confirms a void or a refund with you first, and each one is recorded in an audit trail identifying who asked for it.

> TODO: Confirm which write actions are available to firms today and how a firm has them enabled. The actions are being switched on in batches, so a firm may have some and not others.

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
- **Payment plan listings honor the page size.** `payment_plans_list` previously ignored it and returned every payment plan on the firm in a single response, which made bulk financial questions slow to answer and, for firms with many plans, time out before returning anything. If your assistant has been failing or stalling on broad payment plan questions, retry them.
- **Out-of-range page sizes are adjusted rather than rejected.** On the invoice, payment, and payment plan listings, a page size above 100 is reduced to 100 and a page size below 1 is raised to 1, instead of returning an error.
- **Review counts cover the whole review, not the page you asked for.** On the filing review, the tallies are counted across every finding in the run even when the findings themselves come back a page at a time, so a count never under-reports because the review spans more than one page. Blocking failures are counted two ways: the total, and how many are still unresolved. An attorney signing off on a finding clears the gate for filing but does not change what the review reports.
- **A packet is still readable where pre-filing review is switched off**, and comes back with no review attached. That is a different answer from a review that is switched on but has never been run, and the two stay distinguishable — so "not configured" is never mistaken for "reviewed and clean".
- **Case data is not exposed over MCP.** The eFiling tools cover the packet, the district, and the review; the case's creditor and property records are not available to the assistant, so a review it runs works from the filing packet rather than from the underlying case data.
- **Listing one person's tasks now works.** Asking for the tasks assigned to a specific team member used to fail outright, leaving the assistant with nothing but an unfiltered list of every task at the firm. If your assistant has been unable to answer "what is Sarah working on", retry it.
- **Write actions are limited to the list above**, and only where your firm has them enabled. For anything else, the assistant will tell you the change needs to be made in the Glade app.
- **Creating a report does not run it.** The assistant saves a custom report to your firm's dashboard with the columns and filters you described; open it in Glade to read the rows or export them.

## Related Features

- [MCP Overview](overview.md)
