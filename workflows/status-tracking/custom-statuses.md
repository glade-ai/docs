# Custom Statuses

## Overview

In addition to the built-in statuses, your firm can define its own case statuses with a title, icon, and color, and optional behaviors that affect tasks and follow-ups. Any status — custom or built-in — can be archived to remove it from the status picker. This page covers creating custom statuses, their optional behaviors, and archiving statuses.

## Key Behaviors

- **Custom statuses**: Your firm can create custom statuses with a title, icon, and color. Custom statuses also support two optional behaviors:
  - **Archive behavior** — moving a case to this status completes all pending tasks and promotes any related workflows, just like archiving
  - **Disable followups** — suppresses automated reminder emails and messages for cases in this status
- **Archiving statuses**: Any status — including built-in default statuses — can be archived. Archiving a status removes it from the status picker so it cannot be assigned to new cases. When you archive a status that is currently in use, a confirmation prompt shows how many active workflows are using it, so you can make an informed decision before proceeding. See [Settings](../../back-office/settings.md) for the archive/unarchive UI.
- **Archived status visibility**: Cases that are currently assigned an archived status continue to display that status correctly — the label, icon, and color remain visible in workflow lists and on the case. Archived statuses are only hidden from pickers where you select a status; existing cases are not affected.
- **Viewing archived statuses**: Archived statuses are hidden by default on the Custom Statuses settings page. Toggle **Show archived** to reveal them.

## Configuration

- **Custom statuses**: Created and managed per firm. Each status has a unique identifier, display title, icon, color, and optional behavioral flags (archive behavior, disable followups). Any status — custom or built-in default — can be archived from the Custom Statuses settings page.

## Edge Cases & Limitations

- Custom statuses with archive behavior trigger the same task completion logic as the built-in Archived status, but the case retains the custom status rather than switching to Archived.
- Archiving a default status (one that shipped with your firm setup) does not delete it — it is preserved for historical reference but removed from the picker. Default statuses cannot be deleted, only archived.
- The number of active workflows shown in the archive confirmation reflects workflows at that moment; cases may have moved to other statuses by the time you confirm.

## Related Features

- [Status Tracking](./README.md)
- [Case Status](./case-status.md)
- [Workflow Labels](./workflow-labels.md) — labels carry no behavior, unlike custom statuses
- [Settings](../../back-office/settings.md)
