# Staff Management

## Overview

Staff management controls who has access to your firm's back office and what they can do. The system has two layers: **team members** who are staff on your firm's account with platform-level roles, and **organizations** that represent client-side groups (e.g., a client company) with their own member permissions.

## Key Behaviors

- **Team members** are people linked to your firm with a system role and an optional workflow role.
- **System roles** control platform-level permissions. There are three role types:
  - **Admin** — full access to all back-office features
  - **Case Worker** — access to case management features but not team or finance settings
  - **Finance** — access to financial and billing features
- The firm owner automatically has full permissions regardless of assigned role.
- **Workflow roles** are custom roles your firm defines (e.g., "Paralegal", "Documents Team", "Intake Lead"). They are used to:
  - Segment team members in reports (e.g., the paralegal report filters by the "Paralegal" role)
  - Set a default assignment role for each team member so they are automatically assigned the right role on new cases
  - Control which team members appear in specific report views
- **Case ownership**: You can assign one or more team members to a case. Each owner can have specific workflow roles on that case (e.g., one person might be the Paralegal on case A but Intake Lead on case B).
- **Organizations** belong to your firm and represent client-side groups. Each organization has an owner and members. Organization members have granular permissions:
  - Assign team members to cases
  - Invite other collaborators
  - Receive customer notifications
  - Initiate new workflows
  - Make payments
  - Be automatically invited to all cases
- When you add someone as an organization member, the system creates their account if they do not already have one. A person who is already a paying customer of your firm cannot be added as an organization member.

## Configuration

- **System roles**: Three built-in role types (Admin, Case Worker, Finance), each granting different permissions.
- **Workflow roles**: Created by your firm with a name and display rank. The rank controls the order roles appear in lists and reports.
- **Organization member permissions**: Set individually per member when they are added to the organization.

## Edge Cases & Limitations

- If a team member is removed, their existing case assignments are not automatically removed. Those assignments persist until manually updated.
- Organization membership validation prevents adding someone who is already a paying customer, but it does not prevent the reverse (an organization member later becoming a direct paying customer).

## Related Features

- [Case Management](./case-management.md) — team members are assigned as case owners and collaborators.
- [Reporting](./reporting.md) — paralegal and documents reports segment data by workflow role.
- [Settings](./settings.md) — workflow roles and system roles are configured per firm.
