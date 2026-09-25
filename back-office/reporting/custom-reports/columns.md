# Custom Report Columns

## Overview

A custom report is built from the columns your firm chooses. This doc covers columns whose behavior needs explaining: court notice type, case number, client address, and reaffirmation agreement.

## Key Behaviors

### Court notice type

- The **Court notice type** column reflects the filter you have applied. When you filter the report to specific court notice types, the column shows only those types for each case — previously it listed every notice type on the case regardless of the filter, so a filtered report showed rows whose column contradicted the filter above it.
- Each type in the **Court notice type** column is clickable and opens the matching notice in a panel. Where a case has more than one notice of the same type, the link opens the most recent one.

### Case number

- The **Case number** column answers the same question the case-number filter asked. Ordinarily a case with no number of its own borrows one from another workflow in the same case group, so the column is rarely blank. When you filter a report to cases **without** a case number, that borrowing is switched off and the column shows each row's own value — which, for every row the filter returned, is empty.
  - Previously a report such as *Time Sensitive — Without a Case #* could list a case with a case number printed beside it, so the report looked broken even though the filter had returned the right rows. If your firm stopped trusting a "without a case number" report, try it again.
  - Reports that do not use that filter are unchanged: the column still fills in a number from a related workflow where the case has one.

### Client address

- The **Client address** column reads the client's address from case data — the same address shown on the case's own case-data panel, written there by questionnaire sync, credit report pulls, and document extraction. The column was previously blank for most cases because it read an older location that almost nothing writes to any more; more than 10,000 cases across 51 firms had an address on file and an empty cell.
  - Each part of the address resolves on its own, so a case with a street but no ZIP still shows the street.
  - An address that exists only on the client record in the Clients panel, and was never written to case data, shows as blank. If a case shows an address on screen but not in the report, that is the reason — contact Glade support if you need those addresses brought across.
  - The column is for display. Sorting or filtering the report by client address is not available.

### Reaffirmation agreement

- **Reaffirmation agreement**: A column and a matching filter report whether a case intends to reaffirm any debt. A case counts as reaffirming when at least one creditor on the bankruptcy schedules questionnaire's creditor list answers the statement-of-intention question — "What do you intend to do with the property that secures the debt?" — with **Retain the property and enter into a Reaffirmation Agreement**. One qualifying creditor is enough for the whole case.
  - Only creditors listed on **Schedule D** are considered. The same intention question is asked on every creditor row, and rows on Schedules E/F/G carry a default answer that does not indicate an intention about secured property, so counting them would report cases as answered when nothing was decided.
  - Creditor rows excluded from the petition are ignored.
  - The filter offers reaffirming and non-reaffirming selections plus a **not answered** selection. A case whose bankruptcy schedules questionnaire has not been filled in — a consultation or a turned-down matter, for example — has no answer to give and falls under **not answered** rather than under "no".
  - The lease-assumption question on the same form ("Will the lease be assumed?") is **not** available as a column or filter.

## Configuration

- **Reaffirmation agreement**: Nothing to configure. The answer is read from the bankruptcy schedules questionnaire and updates as the questionnaire is filled in.

## Edge Cases & Limitations

- The **Client address** column is blank for a case whose address was never written to case data, including cases whose address is held only on the client record. It cannot be sorted or filtered on.
- The **Reaffirmation agreement** column reports what the schedules questionnaire says, not what was ultimately filed. A reaffirmation agreement decided outside the questionnaire, or changed after the petition went out, is not reflected until the questionnaire is updated.
- Cases with no bankruptcy schedules questionnaire are reported as **not answered** on the reaffirmation column. This is the expected result for consultations and non-bankruptcy matters, and it is distinct from a case that answered "no".

## Related Features

- [Custom Reports](./README.md)
- [Filters](./filters.md)
- [Time from Retainer to Filing](./retainer-to-filing.md) — first retainer signed and days to filing columns
- [Court Notices Report](../court-notices-report.md)
