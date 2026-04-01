# Inbox

## Overview

The inbox is a notification center inside the back office where your firm receives activity updates. Notifications appear for events such as filing status changes, client actions, document submissions, and other case activity. From the inbox, team members can quickly navigate to the relevant case or resource and manage their notifications.

## Key Behaviors

### Receiving Notifications

- Notifications appear in the inbox automatically as events occur — no refresh is needed.
- Each notification includes a summary of the event and a link to the relevant case or resource. Clicking a notification takes you directly to the associated view (for example, clicking a court filing notification opens the Case Status tab for that case).
- Notifications have a read/unread state. Unread notifications are visually distinguished.
- Notifications can be dismissed to remove them from your inbox view.

### Bulk Actions

You can act on multiple notifications at once:

- **Select individual items**: Check the checkbox on any notification to select it.
- **Shift-click range selection**: Click one notification, then shift-click another to select all notifications between them.
- **Select all**: Use the select-all control to select every notification on the current page.
- **Bulk mark as read**: After selecting one or more notifications, use the bulk mark-as-read action to mark them all as read at once. The change reflects immediately without a page reload.
- **Bulk dismiss**: After selecting one or more notifications, use the bulk dismiss action to remove all selected notifications from your inbox view at once. The page automatically backfills with additional notifications if more are available, so the inbox stays populated.

### Managing Individual Notifications

- Each notification has a three-dot menu with options to mark it as read or dismiss it individually.
- Dismissed notifications are removed from the inbox view. They are not permanently deleted — Glade retains them for internal record-keeping.

## Configuration

Notification preferences (such as which events generate notifications and how they are delivered) are configured in firm settings and individual workflow template settings.

## Edge Cases & Limitations

- Bulk dismiss removes selected notifications immediately from the view. If you're on the last page of notifications and dismiss all of them, the inbox backfills automatically or shows an empty state.
- Select-all selects notifications on the current page only, not across all pages.

## Related Features

- [eFiling](../integrations/efiling.md) — filing status updates generate inbox notifications with direct links to the Case Status tab.
- [Case Management](./case-management.md) — many inbox notifications link directly to case views.
