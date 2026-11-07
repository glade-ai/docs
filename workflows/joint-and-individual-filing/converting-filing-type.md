# Converting Between Joint and Individual Filing

## Overview

Staff can convert a case from individual to joint filing, or from joint to individual, from the workflow's settings. The case stays where it is: it is not archived and recreated as it is with a [workflow switch](../workflow-switch.md), and it stays on the same workflow. Converting to joint adds the spouse to the case; converting to individual removes them and clears Debtor 2.

## Key Behaviors

- **Run from the workflow's settings** with **Convert to joint** or **Convert to individual**, whichever applies to the case. Before you confirm, a dialog shows what the conversion will change and any warnings.
- **The case's filing type changes in place.** The workflow's joint or individual selection — for example, Chapter 7 joint or Chapter 7 individual — is switched to the other option on the same workflow.
- **The change is recorded in the case's activity history.**
- **If any part of the conversion fails, the whole conversion is undone**, so the case is not left half converted.

### Converting to joint

- **You identify the spouse.** The spouse is matched to an existing person by email, or added as a new one, and connected to your firm.
- **The spouse gets access to the case and is sent an invite.**
- **Debtor 2 is filled in** on the case record from the spouse's details, and the household's marital status is set to married unless it already says married or you choose a different value in the dialog.
- **The schedules questionnaire follows.** "Are you filing jointly?" becomes Yes, the household is marked married, and Debtor 2's answers are filled from the case record. Submitted schedules questionnaires are updated too.
- Other in-progress questionnaires on the case receive the new Debtor 2 details through case data sync.

### Converting to individual

- **The spouse is removed from the case.** Their access through the case ends. Their contact record at your firm, and any access someone added for them by hand, are kept.
- **Debtor 2 is cleared** on the case record, including Debtor 2's other names (AKAs). The household's marital status changes only if you choose a value in the dialog.
- **The schedules questionnaire follows.** "Are you filing jointly?" becomes No and every Debtor 2 answer is cleared, including on submitted questionnaires. Rows in Debtor 2's own lists are removed.
- Other questionnaires on the case keep their answers.

### What is not changed

The conversion does not change:

- workflow steps that have already run;
- questionnaires and document requests already sent;
- income organizers;
- credit reports and credit counseling;
- retainers.

The dialog warns about this. Review these items on the case and update them by hand where the change of filing type affects them.

## Edge Cases & Limitations

A conversion cannot run when:

- the case has been filed;
- the workflow has no joint/individual selection, the selection is ambiguous, or the workflow has no matching option to switch to;
- the workflow is not set up for a spouse — use a [workflow switch](../workflow-switch.md) to move the case to a workflow that is;
- the spouse cannot be identified unambiguously, or is the same person as the primary debtor;
- another conversion or a [debtor swap](./swapping-debtors.md) is already in progress on the case;
- the schedules questionnaire cannot be updated — for example, while it is being upgraded to a new template version.

Other limitations:

- **Debtor 2's answers are cleared, not struck.** On an amended schedule, converting to individual removes Debtor 2's answers from the forms rather than printing them as removed, even if they were struck first. See [Amendment Marks](../questionnaires/petition/amendment-marks.md).
- If the case changes between opening the dialog and confirming, the conversion is refused and has to be reviewed again.

> TODO: Confirm exactly where in the workflow's settings the conversion is offered, and whether the spouse's details are entered in the dialog or picked from existing contacts.

## Related Features

- [Joint and Individual Filing](./README.md)
- [Swapping Debtors](./swapping-debtors.md)
- [Workflow Switch](../workflow-switch.md)
- [Case Data Sync](../questionnaires/case-data/case-data-sync.md)
- [Amendment Marks](../questionnaires/petition/amendment-marks.md)
