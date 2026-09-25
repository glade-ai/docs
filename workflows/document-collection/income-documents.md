# Income Documents

## Overview

Document requests of the "income data" type collect paystubs and other income documents in a structured form. Glade uses AI to extract income data from each upload, and your team chooses how the extracted paystubs are turned into the monthly income figures used in documents like Schedule I and the means test. This page covers income document requests, AI processing of income rows, and the income calculation modes.

## Key Behaviors

- **Income data document requests**: The "income data" document request type is used for structured income data collection. Income data files can track metadata including income source, pay frequency, start/end dates, and monthly dollar values.
- **Income organizer AI processing**: When a paystub or income document is uploaded, AI automatically extracts the income data. While processing is underway, a loading indicator appears on the row. The uploaded file name is clickable even during processing — you can view the original document without waiting for AI to finish. Once AI completes, the loading indicator clears and extracted data appears. An **Edit** button is available on all income rows once processing is complete, whether the data was entered manually or extracted by AI. The Edit button is only hidden while AI is actively processing a row. If extraction fails — including when a follow-up retry is also interrupted — any income data already on the row is preserved. Earlier entries are not overwritten with empty values when the extractor cannot complete, so re-running AI on the row picks up where the previous attempt left off.

## Configuration

- **Income calculation mode** (employment income): When a client uploads multiple paystubs for employment income, your team can choose how Glade calculates the monthly income figures used in documents like Schedule I:
  - **All paystubs** (default): sums all selected paystubs and averages them across the unique months represented.
  - **Single paystub YTD**: uses the year-to-date totals from one paystub divided by the number of months elapsed in the year. This is useful when only one recent paystub is available or when YTD figures are more accurate than averaging multiple pay periods.
  - **YTD period method**: estimates the monthly figure by comparing the year-to-date totals on the paystubs that bracket a chosen six-month period and dividing the bracketed gross by six. You select a filing (test) month, and the six full months before it form the period being measured. A preview shows the selected month, the period, the anchoring paystubs, and the resulting monthly gross before you apply it. See [Income Organizer](../income-organizer/README.md) for details.
- **Switching modes**: To switch modes, open **Income calculation** in the income organizer header while table view is open, and pick the employment source you are setting if the case has more than one. This control used to sit next to the employer row itself. When using YTD mode, you select which paystub provides the YTD figures, and choose whether to auto-detect months elapsed from the paystub date or set the number manually. A preview of the resulting Schedule I contributions is shown before you apply changes. The preview shows regular wages and overtime as separate line items, with a Gross Income total, so you can verify the breakdown before confirming.
- **Apply YTD to means test**: When YTD mode is active for an employer, you can also apply the same YTD figures to the means test calculation instead of using the standard 6-month window. Toggle this option on within the YTD settings for that employer. When enabled, Glade uses the YTD gross pay divided by months elapsed to populate the means test income line for that employer. Other employers not set to YTD mode continue to use the standard calculation.

## Edge Cases & Limitations

- The Edit button on an income row is hidden while AI is actively processing that row.
- Apply YTD to means test only affects employers set to YTD mode; other employers continue to use the standard calculation.

## Related Features

- [Document Collection](./README.md)
- [Automatic Data Extraction](./data-extraction.md)
- [Income Organizer](../income-organizer/README.md)
