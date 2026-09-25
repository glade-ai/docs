# Credit Counseling Checks

## Overview

The pre-filing review checks whether a debtor's credit counseling briefing is recent enough to satisfy § 109(h). Credit counseling recency was held back from the first release of the review and has since been switched on — see [Certificate recency before filing](../../abacus-credit-counseling.md) for what it reports.

## Key Behaviors

- Recency findings state the **date the briefing was completed** and the **date the certificate remains valid through**, rather than only reporting pass or fail. This makes it possible to see how much time is left on a certificate, and to audit afterwards which date the check was actually assessing.
- Findings also record **which date was used** — the date printed on the certificate, or the date the certificate reached Glade. The two can be months apart when a briefing was completed with a provider outside Glade and the certificate attached later.
- **The credit counseling certificate's own row in the packet is flagged when a check about it fails.** Previously only the petition document could show a "Needs attention" marker, so a blocking credit counseling finding left the certificate row looking fine and the problem had to be found in the review results.
- The credit counseling completion date is not part of the [required fields check](./required-fields.md); a missing date on the questionnaire no longer stops a filing, and recency is assessed here instead.

## Related Features

- [Pre-filing Review](./README.md)
- [Certificate recency before filing](../../abacus-credit-counseling.md)
- [Evergreen credit counseling](../../evergreen-credit-counseling.md)
- [Packet checks](./packet-checks.md) — two credit counseling certificates on one slot.
