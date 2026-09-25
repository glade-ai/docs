# Workflow Bookings and Access

## Overview

Appointments can be created automatically as steps within a workflow, and booking events can drive later workflow steps. This doc covers how workflow bookings behave, the email sent when a team member is assigned a Schedule Appointment task, and who can view and manage a booking.

## Key Behaviors

### Workflow integration

- Appointments can be created automatically as steps within a workflow.
- Workflow-generated bookings can be assigned to specific team members based on workflow rules.
- Access permissions are automatically granted to workflow participants.
- Booking events (created, rescheduled, canceled) can trigger subsequent workflow steps.
- When a workflow creates a booking task for a client, the task title includes the appointment type name — for example, "Schedule Appointment: Initial Consultation". This helps clients identify which service they are being asked to schedule when multiple appointment types exist.

### Email when a team member is assigned a Schedule Appointment task

When a team member is newly assigned to a **Schedule Appointment** task on a case, they receive an email telling them so, with a link to the case. Reassigning the task now reaches the new assignee — previously nothing was sent, and a task could sit with someone who had no idea it was theirs.

- **Only the people newly added get the email.** Bookings re-check their assignees whenever they are created, rescheduled, skipped, canceled, or unscheduled, and when collaborators change. Someone who was already on the task is not emailed again each time one of those happens.
- **You are not emailed about your own action.** Assigning the task to yourself sends nothing.
- **This covers the Schedule Appointment task only.** Other task types — responding to a discussion, reviewing a document request, and the rest — do not send an assignment email. A task asking a client to pick from your availability is also excluded, because the case owners already receive their own notification for it.
- No setting is involved: the email is on for every firm.

### Permissions and access

- Firm users always have full access to manage bookings.
- Clients can view and manage their own bookings.
- Additional collaborators can be granted access to specific bookings.
- Workflow participants automatically receive appropriate access.
- **Workflow bookings require explicit assignment**: When a booking is created as a step in a workflow, only people who are explicitly assigned to that booking (or who are members of the firm) can view, reschedule, or cancel it. A client being the subject of the booking is not enough on its own — for example, a signing or notarization booking that is only assigned to firm staff is hidden from the client's upcoming bookings list and the client cannot reschedule it. Add the client as an assignee on the booking if they should be able to manage it themselves.

## Related Features

- [Scheduling](./README.md)
- [Team Member Assignment](./team-assignment.md)
- [Booking Lifecycle](./booking-lifecycle.md)
