# Exemptions Calculator

## Overview

The Exemptions Calculator is a panel available in bankruptcy cases that helps attorneys analyze how claimed exemptions apply to a client's assets. It aggregates properties and exemptions from the case's schedules and shows at a glance which assets are fully exempt, partially exempt, or over-limit — along with the applicable statutes.

## Key Behaviors

- The Exemptions Calculator panel opens while viewing Schedule A/B, Schedule C, or the Master Creditor List. It provides a summary alongside the schedule so you can review exemption coverage without leaving the form.
- A top-level **Exemptions Summary** card shows the total exempted value and the total non-exempt value across all assets.
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

## Configuration

The Exemptions Calculator pulls data from the case's scheduled assets and claimed exemptions. No separate configuration is required — it reflects whatever has been entered in the relevant schedules.

## Edge Cases & Limitations

- The calculator reflects the current state of the schedules. If schedules are incomplete or have not been submitted, the totals may be partial.
- Statute citations are displayed as entered in the exemption data. If a statute citation is missing or malformed, the pill still appears but may show an incomplete citation.

## Related Features

- [Questionnaires](./questionnaires.md)
- [Document Collection](./document-collection.md)
