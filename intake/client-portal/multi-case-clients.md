# Multi-Case Clients

## Overview

When a client has more than one active case with your firm, the client portal adds a case sidebar, search, and automatic routing to their first case. Historical matters imported from MyCase are hidden from clients so they see only the case your firm is actually working.

## Key Behaviors

### Sidebar, search, and redirect

When a client has more than one active case with your firm, the portal adapts:

- **Sidebar** — a left-hand sidebar appears once the client has two or more active visible cases. Archived, canceled, and closed cases are excluded; cases linked into a chain (for example a refile) collapse to a single most-recent representative.
- **Search** — once the client has more than three cases, the sidebar adds a search input. Search matches both the chain representative and any linked member cases, so searching for any case in a chain finds it.
- **Auto-redirect** — for clients with two or more active cases, opening the home URL routes straight to the first case's representative. The exception is when the URL carries an activity deep link (with a specific case and comment) — the portal honors that deep link and shows the home with the targeted case opened.

### Matters imported from MyCase

Firms that moved to Glade from MyCase carry their history across as imported matters. These are historical records, not work in progress, and they no longer appear to clients.

- **An imported matter is hidden from the client portal**, so a client sees only the case your firm is actually working. Previously the import sat beside the live case, and clients and staff alike kept opening the wrong one.
- A client cannot reach an imported matter by link either. A direct link to one is refused rather than opening it.
- **Your team still sees imported matters in full** on the firm's case tracker, and can filter to them specifically.
- Nothing is deleted or changed by this — the imported record is intact, and only who can see it has changed.

## Edge Cases & Limitations

- Hiding imported MyCase matters covers the client portal and the contact page. A client who bookmarked an imported matter finds the link no longer opens; point them to their live case.
- Only matters carrying the MyCase import status are hidden. A matter migrated some other way, or one re-opened as live work, is treated as an ordinary case and remains visible to the client.

## Related Features

- [Client Portal](./README.md)
- [Portal Home Page](./home-page.md)
- [Case Management](../../back-office/case-management.md)
