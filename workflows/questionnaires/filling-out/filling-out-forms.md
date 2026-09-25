# Filling Out Forms

## Overview

When using Glade's native form provider, clients and your team fill out sections and fields through the client portal or dashboard, with changes auto-saved and synced in real time. This page covers how a new questionnaire is pre-filled, how template defaults are recorded, and what happens when several people edit at once.

## Key Behaviors

### Pre-filling a new questionnaire

Initial values can be pre-populated from field mappings tied to the client's workflow or from the inheritance scheme (see [Template Settings](../templates/template-settings.md#inheritance-scheme)). Clients fill out sections and fields through the client portal, with changes auto-saved and synced in real time.

**A lease no longer stops the client questionnaire from pre-filling the Schedules.** On a case where the client recorded a lease but has nothing on the client questionnaire's **Debts & liabilities** list, the Bankruptcy Schedules questionnaire now pre-fills from the client questionnaire as usual. Previously the whole client questionnaire failed to load as a source in that situation, so every Schedules field drawing from it — whether the debtors are filing jointly, marital status, employers, and the rest — came through blank with nothing on screen to explain why, and the answers had to be re-entered by hand. The lease is still carried across as a creditor for Schedule G, and cases that already had entries on Debts & liabilities are unaffected. If your team prepared Schedules on a case with a lease and found the client's answers missing, re-check that case against the client questionnaire.

### Editing at the same time

When two people edit the same questionnaire at the same time — for example, a client and a paralegal, or an attorney working alongside an AI autofill — each person's edits to different fields are preserved. If two edits target the same field, the newer value wins and the older one is discarded silently rather than producing a save error. Edits to other fields in the same save attempt still go through.

For concurrent edits to list and table rows, see [Working With Lists](./working-with-lists.md#concurrent-edits-to-list-rows).

Response history tracks when responses are modified, supporting undo and audit.

### Template defaults

Default values configured in the questionnaire template are saved automatically when the questionnaire is set up, so a displayed default is recorded as a real answer from the start — even if nobody ever opens the section that contains the field. This covers every kind of field the template can carry a default for, not only single-select options, and it covers the cells of list and table rows that already exist as well as top-level fields.

Because the answer is stored up front:

- A field showing a default counts as answered during validation and is not flagged as incomplete. Previously a filer could see the answer on screen while the Petition Check reported the field as blank.
- The default appears on any generated PDF court form, including checkbox selections such as a **No** answer on the Statement of Financial Affairs. Previously those lines printed blank on a sworn document.

Answers already given are never touched — a default is only written where the field has no answer at all. Questionnaires started as a copy of another questionnaire inherit the original's answers and are not re-defaulted.

> TODO: Confirm what happens to fields a *newer template version* introduces on a questionnaire that is upgraded in place — whether their defaults are written at upgrade time or only once the field is touched.

Template defaults are filled in as the last step of setting up a new questionnaire, after any information Glade already holds on the case has been carried across. A default therefore only ever fills a field that has no answer yet — it never replaces something the case record already knows, so a client's real figure is not shadowed by a template placeholder. Because the defaults are in place before anyone opens the form, the duplicate check that runs on a newly created list sees them too.

A field that starts out at its template default — for example a currency field showing $0.00 — is still eligible for autofill the first time the questionnaire loads. Fields such as the applicable median family income on Chapter 7 Form 122A-1 now populate from the client's state and household size on open, instead of sitting at $0.00 with no indication that anything was missing. Values you have typed yourself are never replaced by this initial pass.

A field inside a list can also be given a default **value** in the template, which is filled in automatically each time a new row is added. For example, on bankruptcy Schedule A/B a new property row can default the **% of asset owned by the debtor** to 100% — the common case for individual filers — so your team does not re-enter it on every property. The default applies only to newly-added rows; existing rows keep their values. The seeded value is saved with the row, so it persists after you save, and you can change it before or after saving.

## Edge Cases & Limitations

- When upgrading a questionnaire to a new template version, pre-filled initial values are not re-applied during the upgrade (see [Template Upgrades](../case-data/template-upgrades.md)).

## Related Features

- [Questionnaires](../README.md)
- [Filling Out Questionnaires](./README.md)
- [Field Behaviors](./field-behaviors.md)
- [Working With Lists](./working-with-lists.md)
- [How Autofills Work](../autofills/how-autofills-work.md)
- [Case Data Sync](../case-data/case-data-sync.md)
- [Client Portal](../../../intake/client-portal/README.md)
