# Case Data Sync

## Overview

Some questionnaire fields and lists are linked to the case record — they display a value pulled from the case record rather than a standalone response, and edits flow back to it. This page covers how synced fields and entity-bound lists behave, turning sync off for one questionnaire, deleting and restoring case record entities, and how data reaches the schedules from other sources.

## Key Behaviors

### Case Data Sync Fields

Some questionnaire fields are linked to case data — they display a value pulled from the case record rather than a standalone response. These fields show the synced value by default.

When you edit a case data sync field, the updated value saves automatically and syncs to the case record immediately — no extra confirmation step is required.

Fields that sit inside a table underneath an explanation heading receive synced values like any other. Schedule I line 8 is the common example: those business and rental income lines are nested this way, and values sent from the Income Organizer were being skipped, so the lines stayed at $0.00 with nothing to indicate a figure had been missed. They fill on the next sync. If your team has been re-typing Schedule I line 8 figures by hand, re-sync the case and the lines should populate on their own.

### Turning sync off for one questionnaire

You can stop a single questionnaire from syncing with case data without waiting for an out-of-sync banner to offer it. On an in-progress Glade questionnaire, the same three-dot menu that holds the questionnaire's other actions offers:

- **Disable case data sync** while the questionnaire is syncing. You are asked to confirm, and syncing stops for that questionnaire only. Answers already on the form are left exactly as they are.
- **Re-enable case data sync** while syncing is off. Choosing it only turns syncing back on — no answer is replaced, and there is nothing to review first. Use this when a questionnaire's edits have stopped carrying over to the rest of the case.

A disable you make from the menu is remembered through submission. Submitting a questionnaire turns syncing off, and re-opening one normally turns it back on again when the case data behind it has not changed — so a questionnaire you had deliberately disconnected used to reconnect itself the moment someone submitted and re-opened it. It now stays disconnected until you turn syncing back on yourself.

- Turning syncing back on — from the menu, or from the out-of-sync banner — clears the manual disable. From then on, submitting and re-opening reconnects the questionnaire automatically again, as it does for any other questionnaire.
- **Re-enable is not offered in the menu while the out-of-sync banner is showing.** Use the banner's own action in that case, so you see which values case data would change before anything is replaced. See [Reviewing changes before you sync](./reopening-and-resync.md#reviewing-changes-before-you-sync).
- Upgrading the questionnaire to a newer template version does not reconnect a questionnaire you disabled by hand.

### Entity-Bound List Fields

Some list and table fields are linked directly to case entities such as creditors or assets. When a questionnaire has this binding configured, adding, editing, or removing rows in those lists updates the corresponding case entities.

- When a firm team member removes a row from an entity-bound list, the corresponding entity (creditor or asset) is deleted from the case record immediately.
- When a client removes a row, the deletion is held for team review rather than applied immediately. A team member must approve the change before the entity is removed from the case record.
- Writes (adding and editing rows) follow the same case data sync behavior as other synced fields.

### Blank Rows Are Not Written to the Case Record

An empty row left behind in a questionnaire list — a creditor row someone started and abandoned, a blank property row — is not written to the case record. Only rows with at least one field filled in create a creditor, asset, or other case entity.

- A blank row alongside filled rows is skipped; its filled siblings are still saved as normal.
- A partly-filled row is kept. Only rows where every field is empty (or contains nothing but spaces) are dropped.
- Nameless entries created before this took effect are cleaned up the next time the questionnaire syncs — they are treated as no longer present and removed from the case record.

Blank creditor rows previously became nameless creditors on the case, which then spread into the schedules and could leave them unusable until someone cleaned the case record up by hand.

### Deleting and Restoring Case Data Entities

Case records hold entities such as creditors and assets that feed synced questionnaire lists. When an entity is deleted from the case record, it is removed from live lists, entity counts, and any synced questionnaires — but it is not erased. The deletion is recorded so your team can review what was removed and undo it.

- Each deletion is kept with who deleted it and when, and is retained as history rather than silently discarded. Restoring an entity is recorded the same way.
- Deleted entities appear in a removed-items view. Restoring an entity returns it to the case record and re-creates its corresponding questionnaire row with the values it had.
- Deleting entities from the case record keeps synced questionnaire lists in step: the matching rows are removed, and the remaining rows in a sync-enabled list continue to show their values. Previously, deleting case-data entities could leave blank rows where the deleted items used to be in lists such as "Your Property"; those rows now display correctly, and the deleted items still appear under Removed Items.
- **Removal history on a removed item.** Opening an item in the removed-items view shows every time it was removed or restored, oldest first, with who did it and when. An item that was removed, restored, and removed again shows all three events rather than only the most recent one — so on an amended schedule your team can explain why an asset or creditor is no longer on the petition. Removals Glade carries out on its own, such as a credit report resync, a questionnaire resync, or duplicate cleanup, are recorded with no person named against them.

### Importing List Data from Another Questionnaire

**The one-off import actions have been removed.** The questionnaire's overflow menu no longer offers **Import from credit report**, **Import case data**, or **Import from client questionnaire**, and the master and client creditor lists no longer carry an **Import** dropdown.

These actions copied a whole list over the top of the answers already on the form, which is how a schedule an attorney had prepared could revert to older client-supplied data in a single click. The credit report import had additionally stopped working — it reported that no creditors had been imported even on cases whose credit report held them. Case data sync is now the one route by which a credit report, a client questionnaire, or the case record reaches the schedules — it applies changes as they happen and lets you review them first, rather than replacing a list wholesale. See [Case Data Sync Fields](#case-data-sync-fields) and [Reviewing changes before you sync](./reopening-and-resync.md#reviewing-changes-before-you-sync).

- **Run Deduplicator** is unchanged and still sits on both creditor lists.
- **Pay organizer and income organizer imports are unaffected.** **Import data from pay organizer** still appears on a case that has a pay organizer, and the Means Test section keeps **Import Data from Income Organizer**. Pay organizers are not yet carried by case data sync, so those two are still how income figures reach the schedules. See [Schedule I and Income](../schedules/income.md#importing-income-organizer-figures).

Lists that are pre-filled automatically from another questionnaire on the same case continue to work as before. The copied rows stay linked to the same case record entity as their source rows, so pre-filled assets, creditors, and other list items update the existing entity in case data instead of creating a duplicate, and they keep their positions and values when the page refreshes.

### Schedules When a Case Switches Chapter

When a Chapter 7 or Chapter 13 case is switched to a different workflow, the client keeps working in the schedules questionnaire they already filled in. That questionnaire, with its saved answers, moves to the new workflow, and the empty schedules questionnaire the new workflow would otherwise create is removed. Messages that pointed at the new, empty questionnaire point at the preserved one instead.

Previously the new workflow could show an empty schedules questionnaire after a switch, while the client's earlier answers stayed behind on the archived workflow.

## Edge Cases & Limitations

- Case data sync only writes to questionnaires that are still in progress. Once a questionnaire is submitted, submitted for review, snapshotted, or otherwise past the in-progress stage, incoming case data updates no longer modify its responses — completed work is preserved as it was at submission. Add or edit data on an in-progress questionnaire to apply new values from the case record. Re-opening a submitted questionnaire also resumes syncing when case data has not changed since it was last synced; if case data has changed, syncing stays off until you choose **Get back in sync** (see [Re-opening and Re-syncing](./reopening-and-resync.md)).
- When more than one questionnaire on the same case can sync case data — for example, the client questionnaire and the schedules questionnaire — each one syncs independently. Starting or initiating a second questionnaire does not turn off syncing on another that is still in progress: both keep syncing while open. A questionnaire stops syncing only when it is itself submitted, not when a sibling questionnaire is created.

## Related Features

- [Questionnaires](../README.md)
- [Case Data](./README.md)
- [Re-opening and Re-syncing](./reopening-and-resync.md)
- [Template Upgrades](./template-upgrades.md)
- [Autofill Status Indicators](../autofills/status-indicators.md)
- [Working With Lists](../filling-out/working-with-lists.md)
- [Workflow Switch](../../workflow-switch.md)
- [Case Management](../../../back-office/case-management.md)
