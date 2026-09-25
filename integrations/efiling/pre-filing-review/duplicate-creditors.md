# Duplicate Creditors

## Overview

This check reads the creditor mailing matrix the case is about to file and flags creditors that look like the same party listed twice. It is an advisory check and never changes the creditor list.

## Key Behaviors

It catches the kinds of near-duplicate that exact matching cannot:

- Typos and abbreviations in a creditor's name.
- The same address written with a nine-digit ZIP on one entry and a five-digit ZIP on another.
- A creditor named two different ways that mean the same company — for example a bank's trading name alongside its full legal name.
- The same creditor listed at two different addresses, raised so someone can decide which address is correct.

**It never merges anything.** The check reports what it found and leaves the decision to the attorney. Dropping a creditor that turns out to be genuinely separate is a notice problem, so no entry is removed from the matrix on the strength of this check.

- It is **advisory** — it does not gate submission, and it can be dismissed like the other advisory findings.
- Creditors that share a mailing address without sharing a name — several creditors using the same lockbox or P.O. box, for example — are not reported as duplicates. That is a normal arrangement, not a mistake.
- The check reads matrices in the different layouts districts use, including multi-column layouts.
- It runs as part of the case's first pre-filing review and on any review you run by hand. Rebuild the matrix and run the review again after correcting the creditor list.

Straightforward duplicates — the same creditor at the same address, differing only in ZIP format, capitalization, or punctuation — are already collapsed when the matrix is built and never reach this check. See [Questionnaires](../../../workflows/questionnaires/README.md) for how the matrix is assembled.

## Edge Cases & Limitations

- The duplicate-creditor check needs the case's creditor matrix to have been generated. Where there is no matrix to read, it reports as unresolved rather than passing, and no creditors are examined.
- The duplicate-creditor check reports judgment calls for a person to settle. It does not correct the creditor list, and a finding it raises is not by itself evidence that two creditors are the same party.

## Related Features

- [Pre-filing Review](./README.md)
- [Case upload files](../../pacer/case-upload-files.md) — when the Creditor Matrix is built.
- [Questionnaires](../../../workflows/questionnaires/README.md)
