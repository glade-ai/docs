# Template Upgrades

## Overview

When your firm publishes a new version of a questionnaire template, questionnaires already in progress can be moved onto it. This page covers release notes on a published version, the upgrade prompt, defaults on new fields, and what an upgrade does — and does not do — to answers, case data, and case data sync.

## Key Behaviors

### Release Notes on a Questionnaire Update

Every published version of a questionnaire template carries release notes describing what changed.

- **Publishing requires a note.** A template version cannot be published with a blank release note, or one made up only of spaces.
- **Updating is offered only on an in-progress form request.** The **New version available → Update now** button in the form request header, and the **Update to current version** menu item, appear only while the form request is **in progress**. They no longer appear once it has been submitted for review, completed, or skipped, and an update attempted on such a form request is refused with the message "Only an in-progress form request can be updated to the latest version. Reopen it first." To update a submitted form request, reopen it first, then update it (see [Re-opening and Re-syncing](./reopening-and-resync.md#re-opening)). Previously a form request submitted for review could still be updated, which reopened its questionnaire for editing while the form request continued to read as submitted.
- **Update now shows what changed.** When an in-progress questionnaire has a newer template version, choosing **Update now** starts the update and opens a notice showing the current published version and its release notes. Choose **Okay** to dismiss it. If the version details cannot be loaded, the notice offers a retry.

### Outdated Template Upgrade Prompt

If you try to save responses on a questionnaire whose template version is no longer accepting changes, a modal appears explaining that the template has been updated. The modal includes an **Upgrade Questionnaire** button that moves the questionnaire onto the current template version and reloads it so you can continue editing. Until you upgrade, saves on the old version are blocked. The **Upgrade Questionnaire** button follows the same rule as **Update now**: on a form request that is not in progress, it shows the "Reopen it first" message instead of upgrading.

### Which Answers Carry Over to the New Version

An upgrade copies each answer to the matching field on the new template version. An answer carries over only if the field kept the same shape:

- **The field is still a list or table, or still not one.** A field that changed from a single field into a list or table, or the other way round, does not keep its answer.
- **The field sits in the same list or table as before**, or is still outside any list or table. Moving a field into or out of an explanation group is a layout change and does not affect matching.

When a field's type changed, the answer carries over only for simple conversions:

- Number to text.
- Number, or text that holds a number, to currency.
- Currency to number, unless the amount was marked unknown or overridden with text.
- Single-select to multi-select, or multi-select to single-select when only one choice was selected.
- Text to number, as before.

For any other change, the answer is dropped rather than stored in a form the new field cannot read. Answers inside a dropped list or table, and documents uploaded to it, are dropped with it.

- **Questionnaires stuck on failed upgrades now upgrade.** A field whose shape had changed between versions could make every later upgrade of a questionnaire fail. Those questionnaires now upgrade normally.
- **A deleted field's answers no longer move into an unrelated new field.** Fields and sections added in the template editor now get identifiers that are never reused. Previously, a new field added after a deletion could be matched to the deleted field on upgrade and receive its answers.

### Upgrading a Questionnaire and Case Data

Upgrading a questionnaire to a newer template version does not remove case data that the questionnaire does not cover.

- Property, creditors, and other case entities that came from elsewhere — a sibling questionnaire, a credit report import, your team entering them directly — survive the upgrade.
- Case entities are only cleared out during an upgrade when the questionnaire being upgraded is the bankruptcy schedules questionnaire *and* it is actively syncing with case data. That is the only case where the form genuinely owns those lists.
- Previously, upgrading any questionnaire cleared every live asset and creditor that the new version did not contain. Upgrading a form with no property list, for example, could wipe all of the case's property. If a case lost case-data entries after a questionnaire upgrade, restore them from the removed-items view (see [Deleting and Restoring Case Data Entities](./case-data-sync.md#deleting-and-restoring-case-data-entities)).

### Case data sync after an upgrade

**An upgrade does not switch case data sync back on for a questionnaire that had it switched off.** Submitting a questionnaire stops it syncing, deliberately, so that a form the client has already handed in cannot go on overwriting the case record — or be overwritten itself. Until this correction, an upgrade re-enabled syncing on any questionnaire that was not marked *completed*, and a questionnaire sitting in **submitted for review** is not completed. Because the schedules template is republished often and questionnaires upgrade when they are opened, a client questionnaire that had been submitted weeks earlier could quietly become an authoritative source again and push its stale answers back over schedules an attorney had prepared since.

- Syncing is now re-enabled by an upgrade only where the questionnaire is still **in progress** and has never synced — the case the re-enabling was written for, where a template gains its first case data connections.
- A questionnaire whose syncing was switched off deliberately, whether by submission or by your team, stays switched off through an upgrade. Turn it back on from the questionnaire itself when you want it (see [Re-opening and Re-syncing](./reopening-and-resync.md#re-opening)).
- This stops further overwrites; it does not undo any that already happened. If prepared schedules on a case were replaced with older client answers, the replaced values need correcting on the case.

### An upgrade no longer empties a prepared list

An upgrade reads a list as it stood before the upgrade, which is settled and complete. It does not read the freshly-copied list back before that copy has finished being written, which would look empty and treat the case's creditors and assets as though they had been deleted.

Two safeguards sit behind that, so a bad read can no longer take a list with it:

- If the upgrade reads back an empty list while it is about to remove entries, it stops and removes nothing.
- If it would remove ten or more entries and more than half of what it looked at, it stops and removes nothing.

In either case the upgrade still completes and the questionnaire is usable — only the removals are skipped. If creditors or assets are missing after an upgrade, contact support with the case rather than re-entering them, so the rows can be restored with their deduplication and ordering.

### New fields get their template defaults

When an upgrade moves a questionnaire onto a version that adds fields, list columns, or table columns with a template default, those new fields are filled with their defaults. This works the same way as when a questionnaire is first created.

- **Case data comes first.** Defaults are applied after the upgraded questionnaire has been filled from case data. A field case data already has a value for keeps that value. The default only fills a field that is still empty.
- **A default on a field connected to case data reaches the case record**, where it ranks below real data. Previously only some upgrades applied defaults, and on those a connected field's default never reached the case record.
- If filling the questionnaire from case data fails during the upgrade, defaults are not applied, so they cannot overwrite fields case data would have filled.

### Household details on an upgrade

**Household details now reach the case record on an upgrade.** Dependents and marital status were only written to the case record when a questionnaire was *completed*. **Update now** upgrades a questionnaire that is still in progress and never completes it, so an attorney upgrading a live case saw a blank Household section even though the answers were sitting on the form.

- **Dependents are copied onto the Household panel when the case has none.** Dependents already on the case are left exactly as they are, whatever they came from, and the rest of the case record is not resynced — only the dependents are seeded.
- **The client's marital status is written across too**, so the Household panel shows whether the client is married and living together or married and separated without waiting for the filer to finish the form. Only these married answers are carried across this way.
- Seeding is skipped when case data sync is switched off for the questionnaire, when the case already has dependents, or when Schedule I has no usable rows to read.
- **In-progress cases pick this up on their next upgrade** — whether through **Update now** or any other template-version upgrade. A case that was upgraded before this took effect can be upgraded a second time to fill the details in, or the field can be re-saved on the form.
- A case that was completed and never upgraded still needs the separate repair for completed schedules. Contact support with the case rather than re-entering the household by hand.

## Edge Cases & Limitations

- If a form request is submitted at the same moment someone updates it, or its status and its questionnaire's status disagree, the update is refused with a message that the questionnaire has been submitted and to contact support. Reopening does not help in that case, because the form request already reads as in progress. Previously this showed a generic error.
- When upgrading a questionnaire to a new template version, responses are copied from the old instance. Pre-filled initial values are not re-applied during the upgrade. Fields the new version adds do get their template defaults — see [New fields get their template defaults](#new-fields-get-their-template-defaults).
- An answer dropped because its field changed shape or type is not restored by a later upgrade. Re-enter it on the new field.
- A new field added before field identifiers stopped being reused may already hold answers carried over from a deleted field on an earlier upgrade. Those answers are not removed automatically.
- An upgrade seeds dependents only when the case has none. A case whose dependents are partly entered — one of three on the case record — is left alone rather than topped up, so the remaining dependents have to be added by hand.
- Marital status is carried across on upgrade only for the married answers. A client recorded as not married does not have that written to the case record this way.
- Upgrading the questionnaire to a newer template version does not reconnect a questionnaire you disabled by hand.
- Itemized rows on Schedule A/B Part 3 appear only on cases whose schedules questionnaire is on the current template — see [Schedule A/B Property](../schedules/property.md#personal-property-on-schedule-ab-part-3).

## Related Features

- [Questionnaires](../README.md)
- [Case Data](./README.md)
- [Case Data Sync](./case-data-sync.md)
- [Re-opening and Re-syncing](./reopening-and-resync.md)
- [Template Settings](../templates/template-settings.md)
