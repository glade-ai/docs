# Staff Management

## Overview

Staff management controls who has access to a creator's back office and what they can do. The system has two layers: **team members** who are staff on the creator's account with platform-level roles, and **organizations** that represent client-side groups (e.g., a law firm's client company) with their own member permissions.

## Key Behaviors

- **Team members** (`TeamMember`) link a `Person` to a `Creator` with a system role (`Roles`) and an optional workflow role (`WorkflowRoles`).
- System roles (`Roles`) control platform-level permissions via boolean flags: `admin`, `manageTeam`, and `finance`. The `role` field is an enum of `admin`, `caseWorker`, or `finance`.
- The creator owner (the `Person` whose `personId` matches the `Creator.personId`) implicitly has full permissions. The platform super-admin (`NOODLE_CREATOR_PERSON_ID`) also bypasses role checks.
- Permission checks use `creatorTeamService.checkTeamRole()`, which resolves the team member's role and evaluates the requested permission (`admin`, `manageTeam`, or `finance`). If the person is the creator owner or the platform super-admin, the check passes regardless of role.
- Permission checks for creator access use `creatorService.userHasPermissionForCreator()`, which verifies a person is either the owner or a team member.
- **Workflow roles** (`WorkflowRoles`) are creator-defined named roles with a rank for ordering (e.g., "Paralegal", "Documents Team", "Intake Lead"). Each team member can have a `defaultWorkflowRoleId` that determines their default assignment role.
- **Case ownership** is managed through `UserWorkflowOwner`, which links a person to a case. Owners can optionally have `workflowRoles` (stored as a JSONB string array) specific to that case assignment.
- Workflow reports use workflow roles to segment team members: the paralegal report filters owners by the "Paralegal" role, and the documents report filters by "Paralegal" and "Documents Team" roles.
- **Organizations** (`Organization`) belong to a creator and have an owner (`Person`) and members (`OrganizationMember`). Organization members have granular permissions: `canAssign`, `canInviteCollaborators`, `canReceiveCustomerNotifications`, `canInitiateWorkflows`, `canMakePayments`, and `inviteToAllCases`.
- Adding an organization member finds or creates a `Person` record and sets up customer relationships. A person who is already a paying customer of the creator cannot be invited as an organization member.

## Configuration

- **System roles**: Created as `Roles` entities. The three role types (`admin`, `caseWorker`, `finance`) each grant different permission flags.
- **Workflow roles**: Created per creator as `WorkflowRoles` entities with a name and rank. The rank field controls display ordering.
- **Organization member permissions**: Set individually per member when they are added to the organization.

## Edge Cases & Limitations

- The `Roles` entity stores permissions as individual boolean columns (`admin`, `manageTeam`, `finance`) alongside a `role` enum. This means the enum value and the boolean flags could theoretically diverge if set inconsistently.
- Workflow roles are not enforced at the entity level for case ownership — `UserWorkflowOwner.workflowRoles` is a free-form JSONB array. Reports rely on joining back to `TeamMember` and `WorkflowRoles` to determine a person's role.
- There is no cascading removal of case ownership when a team member is deleted. Orphaned `UserWorkflowOwner` records may persist.
- Organization membership validation prevents adding someone who is already a paying customer, but it does not prevent the reverse (an org member later becoming a direct paying customer).

## Related Features

- [Case Management](./case-management.md) — team members are assigned as case owners and collaborators.
- [Reporting](./reporting.md) — paralegal and documents reports segment data by workflow role.
- [Settings](./settings.md) — workflow roles and system roles are configured per creator.
