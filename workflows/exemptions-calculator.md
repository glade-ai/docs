# Exemptions Calculator

## Overview

The Exemptions Calculator is a panel available in bankruptcy cases that helps attorneys analyze how claimed exemptions apply to a client's assets. It aggregates properties and exemptions from the case's schedules and shows at a glance which assets are fully exempt, partially exempt, or over-limit — along with the applicable statutes.

## Key Behaviors

- The Exemptions Calculator panel opens while viewing Schedule A/B, Schedule C, or the Master Creditor List. It provides a summary alongside the schedule so you can review exemption coverage without leaving the form.
- A top-level **Exemptions Summary** card shows the total exempted value and the total non-exempt value across all assets.
- The amount available to exempt for each asset is the debtor's **net equity** — the asset's value minus any secured liens against it — not its gross value. Liens are taken from the secured creditors selected for that property on the Master Creditor List, and every creditor secured by the property is summed and subtracted. A property can have multiple liens attached, and the total of all selected liens is used. If no creditors have been selected for a property, the calculator falls back to the single lien amount entered directly on the property. For example, a vehicle worth $3,000 with a $1,000 lien shows $2,000 of equity to exempt, not $3,000. When the secured liens exceed the asset's value, the equity to exempt is $0 (it does not go negative). A creditor whose claim amount is unknown or blank contributes nothing to the lien total.
- Two tabs organize the data in different ways:
  - **By Property** — Groups assets by category in collapsible cards. Each card shows the property name in bold, any liens indented beneath it, and the exemptions claimed against that property displayed as styled pills with the statute citation. Use **Expand All** or **Collapse All** to open or close all category cards at once.
  - **By Exemption** — Groups exemptions by statute. Each exemption card shows the statute as a subheading, the claimed amount, and the properties it applies to, indented beneath. Use **Expand All** or **Collapse All** to open or close all exemption cards at once.
- Status banners show the utilization state for each exemption:
  - **Purple banner** — Remaining capacity is available under this exemption.
  - **Green banner** — The exemption is fully utilized (claimed amount equals the statutory limit).
  - **Warning banner** — The claimed amount exceeds the statutory limit.
- Non-exempt rows are highlighted in red with bold text so over-limit items stand out.
- A **Only show non-exempt** toggle filters both tabs to display only properties or exemptions with a non-exempt balance, letting you focus on items that need attention.
- When viewing Schedule A/B, property names are clickable links that navigate to the property's detail view. Property links are not shown when viewing from Schedule C.
- **Totals update as you type.** Editing an exemption amount on the Exemptions List, or a property value on the Master Property List, recalculates the summary on each keystroke. Previously the figures only moved once you clicked or tabbed out of the field, so the totals read $0 while an amount was being entered — a common source of confusion when learning the calculator. Any autofill notice on the field stays visible while you type.
- Live recalculation does not save anything. The calculator modal still requires an explicit submit to record your changes.

## Configuration

The Exemptions Calculator pulls data from the case's scheduled assets and claimed exemptions. No separate configuration is required — it reflects whatever has been entered in the relevant schedules.

## Edge Cases & Limitations

- The calculator reflects the current state of the schedules. If schedules are incomplete or have not been submitted, the totals may be partial.
- Statute citations are displayed as entered in the exemption data. If a statute citation is missing or malformed, the pill still appears but may show an incomplete citation.

## Related Features

- [Questionnaires](./questionnaires.md)
- [Document Collection](./document-collection.md)
