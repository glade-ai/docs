# Glade AI Checks on Tax Returns

## Overview

When a client uploads a federal tax return (a Form 1040 packet), Glade AI reads it and raises findings for your team to review, the same way it already checks other uploaded document types. Tax returns often reveal information a client did not mention, such as a side business, a rental property, or a retirement withdrawal, so these findings help attorneys and paralegals catch issues before the petition is filed.

## Key Behaviors

- **Tax returns get Glade AI findings.** An uploaded document that Glade recognizes as a Form 1040 tax return is checked page by page, and anything worth a closer look is raised as a finding on the document. Before this, tax returns were recognized but never checked.
- **What the check looks for.** Findings cover, among other things:
  - a return that does not appear to belong to the debtor;
  - a filing status that does not fit the case, such as a single or head-of-household return on a joint case;
  - a married client filing bankruptcy alone, with a prompt to collect the spouse's pay information;
  - the tax year on the return, and whether a newer return should be available;
  - an unsigned or draft copy of the return;
  - schedules that appear to be missing from the return;
  - Schedule C or F businesses, including a business that reports a loss with no income, which may have been set up by a tax preparer rather than being a real business;
  - Schedule E rental income and K-1s;
  - asset sales, digital assets, and retirement distributions;
  - interest and dividend payers, other income, and employers;
  - a refund or balance due, and the account a refund is deposited to;
  - signs of home ownership, dependents, and estimated or household payments.
- **IRS transcripts are handled differently.** An IRS account or return transcript shows only the first letters of each name, so a shortened name that matches the start of the debtor's first and last name is treated as the debtor. Transcripts never include schedules, so the missing-schedule check is skipped for them. Before this adjustment, transcripts were often flagged by mistake as belonging to someone else or as missing schedules.
- **Partial uploads are not flagged for missing schedules.** Glade AI knows the full page count of each upload, so it does not report a schedule as missing just because it is checking only part of a long document.
- **Tax return findings appear with the other document checks.** Open **Check work** and look at the document's **Glade AI findings**. The check runs for every firm, and your team cannot turn it off. If you don't see tax return findings on a return, contact Glade support.

## Edge Cases & Limitations

- The check reads the return on its own. It does not compare the return with the rest of the case, so it does not, for example, point out that a Schedule C business is missing from the questionnaire. Your team still needs to compare the return against the client's answers.
- Findings are suggestions for review, not conclusions. Review each one before acting on it.

## Related Features

- [Uploading and Reviewing Documents](./uploading-and-reviewing.md)
- [Automatic Data Extraction](./data-extraction.md)
- [Income Documents](./income-documents.md)
- [Document Collection](./README.md)
