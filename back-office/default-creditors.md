# Default Creditors

## Overview

Default creditors are a Petition Settings option that adds a fixed set of creditors to every new bankruptcy case your firm opens. A firm that lists the same creditors on most of its cases — a state department of revenue or the IRS as a priority tax creditor, for example — picks them once from its creditor directory instead of adding them to each case by hand. Firm admins and staff who manage petition settings configure the list; preparers see the creditors already on the case's creditor list when they start work.

## Key Behaviors

- **Creditors come from your firm's own creditor directory.** Open **Add creditor** in the **Default creditors** section of Petition Settings and search by creditor name. The search runs against your firm's directory and loads more results as you scroll. A creditor already in the list is not offered again.
- **Each creditor has an account type.** The account type decides which schedule the creditor usually lands on. The choices are grouped by schedule: Schedule E priority types first, then Schedule D, Schedule F, and Schedule G. A newly added creditor starts as **Tax**; change it if that is not right.
- **Each row shows the creditor's name and address**, the account type, and a remove button.
- **Every new bankruptcy case starts with the list.** When a bankruptcy case is created, each configured creditor is added to the case's creditor list (the Master Creditor List) with the chosen account type, a $0 balance, and marked as open. Preparers fill in the amounts and details as they work the case.
- **Saving works like the rest of Petition Settings.** Changes to the list are kept only when you click **Save changes**, together with the other settings on the page. The order of the list is kept.
- **Save errors explain what is wrong.** If a save is refused, the message shows the reason — for example, a duplicate creditor or a creditor that is no longer in your directory — instead of a generic error.

## Configuration

- **Where:** Account → Petition Settings → **Default creditors**.
- **Limit:** Up to 50 creditors. **Add creditor** turns off once the list reaches 50.
- **Account type:** One per creditor, chosen from the same account types used on a case's creditors.
- An empty list adds no creditors to new cases.

## Edge Cases & Limitations

- **Only new cases are affected.** Changing the list does not add, remove, or update creditors on cases that already exist.
- **Bankruptcy cases only.** Other case types do not receive default creditors.
- **A creditor removed from the directory stays in the list until you remove it.** It shows as **Deleted from directory** with only a remove button, and it is skipped when new cases are created. You can keep saving your other petition settings while it is there, but to change the default creditor list you must remove that entry first — an inline message asks you to.
- **The section is being rolled out gradually** and may not appear on your firm's Petition Settings page yet.

> TODO: Confirm which bankruptcy cases receive default creditors — seeding currently applies only to cases whose creditors are kept on the case record, and it is not yet clear whether that covers every new bankruptcy case.

## Related Features

- [Settings — Petition Settings](./settings.md#petition-settings)
- [Importing creditors from a credit report](../intake/credit-reports/importing-creditors.md)
- [Case data sync](../workflows/questionnaires/case-data/case-data-sync.md)
