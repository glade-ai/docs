# Income Calculation Modes

## Overview

Each employment income source (such as a paystub) in the Income Organizer can be set to one of several calculation modes, which decide how the monthly Schedule I figure is derived from the client's paystubs. The mode is set per source from the organizer header, and your firm can choose the mode new sources start with.

## Key Behaviors

Each income source (such as a paystub) can be set to one of these calculation modes:

- **Per-paycheck mode**: income amounts are taken directly from individual pay period values.
- **YTD (year-to-date) mode**: monthly amounts are derived by dividing the year-to-date totals by the number of pay periods elapsed. Use this mode when per-period figures are unavailable or less accurate than the running YTD totals.
- **YTD period method**: estimates average monthly income by comparing the year-to-date totals on the paystubs that bracket a chosen six-month period, then dividing the bracketed gross by six. You pick a **filing (test) month**, and Glade treats the six full months before that month as the period to measure. Use this mode to base the figure on a defined window rather than on the full running year-to-date total.
- **Latest paystub**: bases Schedule I on the current-period figures from one representative paystub, scaled up to a monthly amount using the client's pay frequency. Use this mode when a single recent paystub reflects the client's income better than an average across all stubs or a running year-to-date total — for example after a raise or a change of job.

A Schedule I calculation mode does not change the means test's Current Monthly Income — see [Means Test](./means-test.md).

### Latest Paystub Mode

Latest paystub mode is offered first in the list of calculation methods on an employment income source.

- Glade uses the current-period column of the paystub — gross earnings and every deduction — and converts each figure to a monthly amount from the pay frequency you select. A client paid every two weeks has each current-period figure multiplied by 26 and divided by 12.
- By default the most recent paystub on the case is used. Because the latest stub is sometimes unrepresentative — a short first week, a bonus period, an unpaid absence — you can choose a different paystub as the source instead. A paystub you pick explicitly is eligible even if it carries no date.
- **Pay frequency is required.** Until you select one, no figure is calculated and **Apply** stays disabled. Glade does not assume a frequency.
- A monthly preview shows the resulting figure before you apply it, so you can sanity-check it against the paystub.
- **The means test is not affected.** The Chapter 7 means test always uses the standard six-month calculation, whichever Schedule I mode the source is set to.
- **Existing income sources are not changed.** A source that was already configured keeps the calculation method it was set to. Latest paystub applies to sources you set it on and to new sources created after the firm default is set.

### Firm Default Calculation Method

Your firm can set the calculation method that new employment income sources start with, under **Petition Settings**. New sources are created with that method; existing sources are untouched. The in-organizer checkbox for setting the firm default from the calculator you are working in is still available.

### Where to Set the Calculation Mode

The calculation mode is set from an **Income calculation** action in the income organizer header, available while table view is open. It was previously a small **Calculation:** button tucked inside the Employer cell of each row, which meant opening table view and then finding the right row for something that is set on most cases.

- The header action names the mode currently in effect — for example **Calculation: All Paystubs** or **Calculation: YTD**. When the case's employment sources are set to different modes, it reads **Calculation: Mixed**.
- If the case has more than one employment income source, opening the action asks which source you are setting before showing the settings. With a single employment source it opens straight onto that source's settings.
- Changes are applied with **Apply Changes**, as before. If you switch to a different income source with unapplied changes, Glade asks whether to discard them — declining leaves you on the source you were editing.
- Only employment income sources are listed. Non-employment income (Social Security, rental income, and similar) does not use these modes and is not offered.

### Period Method Preview

When you choose the YTD period method, a preview shows how the figure is built before you apply it: the filing month you selected, the six-month period that falls before it, how many paystubs were used as the start and end anchors, the breakdown rows that make up the calculation, and the resulting monthly gross. The filing month defaults to the month after the latest paystub that carries year-to-date data, and you can change it.

If you also apply the period method to the means test, a warning banner flags it as a non-standard calculation method so you can confirm it against the case's requirements before relying on it.

## Configuration

| Setting | Description |
|---------|-------------|
| Calculation mode | Per-paycheck, YTD, YTD period method, or latest paystub, set per employment income source from the **Income calculation** action in the organizer header (table view) |
| Default calculation mode for new sources | Set firm-wide under Petition Settings. Applies to employment income sources created afterwards; existing sources keep their own setting |
| Filing (test) month | For the YTD period method, sets the month whose preceding six full months form the period being measured |
| Source paystub | For latest paystub mode, which paystub the current-period figures are read from. Defaults to the most recent stub on the case |
| Pay frequency | Used to convert YTD amounts to monthly figures (e.g., weekly = 52 periods/year) |

## Edge Cases & Limitations

- If a paystub does not include YTD overtime data, overtime shows as $0 in YTD mode — no error is shown. This is expected for clients without overtime.
- YTD calculations depend on accurate pay period counts. If the number of pay periods elapsed is incorrect, monthly figures will be off proportionally.
- Latest paystub mode produces no figure at all when the pay frequency is missing, rather than assuming one. Select the frequency to calculate.
- Latest paystub mode affects Schedule I only. It is not available for the means test, which always uses the standard six-month calculation.
- Income sources configured before latest paystub mode existed continue to use the method they were set to. They are not migrated automatically.
- The YTD period method needs paystubs whose year-to-date sections bracket the chosen period. If there aren't enough anchoring paystubs, the method can't be applied and you'll be prompted to upload paystubs that bracket the window. The method always divides the bracketed gross by six months. Periods that cross a calendar-year boundary, and a July filing month, are handled as special cases.
- **A July filing month is measured against the end of June.** The six-month window for a July filing is January through June, and because year-to-date figures have not reset by then, the whole window can be read off a single paystub. Glade uses the last June paystub's year-to-date gross for this. Where there is no June paystub to read, it works back from the latest July stub by removing **every** July pay period from the year-to-date figure. Previously only one July pay period was removed, so on a case with more than one July paystub — biweekly pay, most often — the earlier July paychecks stayed inside the January-to-June total and the monthly gross on Schedule I came out too high. Organizers calculated before this was corrected keep the figures they were given; re-run the calculation on an affected July source to pick up the corrected figure.

## Related Features

- [Income Organizer](./README.md)
- [Schedule I](./schedule-i.md)
- [Means Test](./means-test.md)
- [Paystub Extraction](./paystub-extraction.md)
