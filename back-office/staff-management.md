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
- **Editing team member details**: A team member's name and email address can be updated directly from the staff management interface. Keeping email addresses current ensures the team member retains access to their cases and workflows — changing an email address that is out of sync with the person's actual account can cause their assigned workflows to become inaccessible.
- **Adding a firm billing payment method**: Adding the payment card on file for your firm's own Glade billing is no longer limited to the firm owner. A team member can add a firm billing card without being the owner, and Glade records which team member added each card so there is a clear trail of who set up a payment method.
- **Attorney addresses accept lettered unit numbers**: The Suite/Apt field on an attorney's mailing and physical address accepts letters as well as digits, so `3A`, `B`, and `12-C` save as entered. These fields previously accepted digits only and silently dropped everything else on save — `3A` came back as `3` — which put an incomplete address on anything generated from the attorney's record. Check any attorney whose suite or unit number contains a letter and re-enter it if it was truncated.
- **More than one filing attorney profile per person**: An attorney who files in more than one state can hold a separate filing profile for each — its own mailing and physical address, phone numbers, and bar and licensing details — all recorded against the same team member. Add each profile from the Attorney Information page. The email address on a filing profile is contact information that appears on the filing, not a separate login, so the same address is expected on every profile for that person. Previously only one profile could exist per team member: a second one failed to save, and the workaround was to invent a second email address for the same attorney, which is not necessary.
  - One profile per firm remains the default filing attorney. Marking a new profile as the default clears the flag from the previous one.
  - Deleting a profile removes only that profile and leaves the attorney's others in place. Previously a delete often removed nothing at all.
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

- When a team member is removed, their workflow **ownership** assignments are cleared automatically. A departed member no longer appears as an owner on their workflows and no longer keeps owner-derived access — for example, they are dropped from the group that can view a workflow's invoices. Other manual references to that person (for example, a mention in a note) are not swept up automatically and may need to be updated by hand.
- Organization membership validation prevents adding someone who is already a paying customer, but it does not prevent the reverse (an organization member later becoming a direct paying customer).
- Two filing profiles for the same attorney carry the same name, so a list that asks you to choose a filing attorney can show that name twice. Tell them apart by the state on the profile's mailing address, and confirm you have picked the right one before filing.

## Related Features

- [Case Management](./case-management.md) — team members are assigned as case owners and collaborators.
- [Reporting](./reporting.md) — paralegal and documents reports segment data by workflow role.
- [Settings](./settings.md) — workflow roles and system roles are configured per firm.
