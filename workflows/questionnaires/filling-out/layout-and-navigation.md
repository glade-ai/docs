# Layout and Navigation

## Overview

The questionnaire screen combines the form itself with a resource panel, a Source Data menu, and table views, and it adapts for clients on mobile devices. This page covers how those parts of the screen behave, including very large questionnaires.

## Key Behaviors

### Resource Panel

The resource panel appears on the right side of the form and displays supplementary information and tools while you work — including autofill explanations, tutorial videos, reference data, and the Exemptions Calculator. All such content opens in the panel rather than as a separate popup dialog.

The panel scrolls independently of the questionnaire content. Scrolling through the form does not move the resource panel, and scrolling the panel does not move the form.

### Source Data Access

While filling out certain forms (for example, Bankruptcy Schedules), a **Source Data** dropdown lets you reference related data without leaving the form. For bankruptcy workflows that include an Income Organizer, an **Income Organizer** option appears in the dropdown — clicking it opens the Income Organizer in a new tab with the table view already expanded, so you can review income figures alongside the schedules form. The option only appears when the workflow has an associated Income Organizer.

### Working in the Schedule Builder's Tables and Date Fields

A set of layout problems in the Schedule Builder — things covering other things as you scrolled — have been corrected. They were side effects of making the page itself the scrolling surface so that the buttons at the bottom of a long form could be reached; that scrolling behavior is unchanged.

- **A date field's calendar opens in full.** Picking a gift date on the Statement of Financial Affairs, or a signature date, no longer means scrolling around to find a calendar that has been cut off at the edge of the form.
- **A table's filter row, header, and footer stay pinned only inside the table itself.** On Schedule F and Schedule D they could pin over the rows you were reading, so **Show Fillable PDFs**, **Show External Data**, **Source Data**, and the linked-field badges sat on top of the data instead of scrolling away with the page.
- **The full screen table view is not covered by the form's own controls.** Entering full screen and scrolling now shows only the table.
- **The field resource panel no longer pins itself to the page** as you scroll past it.
- **The checkbox column reads clearly while you scroll sideways.** It stays in place as the table scrolls under it and now has a solid background, rather than letting the rows passing behind show through it.

### Very Large Questionnaires

Questionnaires with hundreds of list rows stay responsive while you work in them. On the largest bankruptcy schedules — a master property or creditor list running to several hundred rows — the form could previously stall long enough that the browser offered to close the page, most often while autofilled and calculated values were being recalculated after an edit. Editing, saving, and moving between sections on those forms now proceed without that pause.

Nothing about how answers are recorded changed, and there is no setting to adjust — only how quickly the form keeps up with you.

### Mobile Experience

Clients filling out questionnaires on a mobile device see a redesigned navigation built for smaller screens:

- A **bottom navigation bar** provides four tabs:
  - **Overview** — shows the questionnaire's overall completion status
  - **Sections** — lists all sections so you can jump directly to any part of the form; includes filtering to narrow by section or progress
  - **Workflow** — shows the client's broader workflow timeline and step progress
  - **Help** — provides access to help resources and tutorials
- A **persistent action bar** at the bottom of each section keeps the save and continue button visible as you scroll, so you never need to scroll back to the top to advance.
- A **close affordance** lets clients dismiss the questionnaire and return to it later without losing progress.
- Clients can switch between questionnaires assigned to the same workflow directly from the mobile navigation, without returning to the home screen.

The mobile layout is only visible to clients accessing the questionnaire on a mobile device. Attorneys and firm staff viewing the same questionnaire on desktop see the standard layout.

## Related Features

- [Questionnaires](../README.md)
- [Filling Out Questionnaires](./README.md)
- [Printing a Questionnaire](./printing.md)
- [Exemptions Calculator](../schedules/exemptions-calculator.md)
- [Chapter 13 Plan Calculator](../schedules/chapter-13-plan-calculator.md)
- [Income Organizer](../../income-organizer/README.md)
- [Client Portal](../../../intake/client-portal/README.md)
