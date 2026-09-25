# Matching Statements to Businesses

## Overview

A profit & loss statement only contributes to Schedule I line 8a once it belongs to a business on the case. Uploading into the business's own folder in the organizer binds it directly; otherwise Glade matches the statement to a business by the name printed on it, and creates a business when the statement names one that is not on the case yet.

## Key Behaviors

### A statement uploaded outside its business's folder

A profit & loss statement only reached Schedule I line 8a if it was uploaded **into the business's own folder** in the organizer. Uploaded anywhere else it read correctly and its lines landed on the case, but it belonged to no business — so every figure that groups by business skipped it and the business income calculation produced nothing, with no error shown anywhere.

- **A statement is now matched to a business by the name printed on it** when there is no folder to place it from. `RIVERA LANDSCAPING, LLC.` on the statement matches a business your team recorded as `Rivera Landscaping, LLC` — capitalization, spacing, and trailing punctuation are ignored.
- **Uploading into the business's folder is still the exact route** and takes precedence. Name matching is the fallback.
- **Matching is exact, not approximate.** `Rivera Landscaping` is not matched to `Rivera Landscaping II` — two businesses a debtor reports separately — because putting one business's income on another's line of a form signed under penalty of perjury is worse than leaving it unattached. A statement that does not match, names no business, or matches two businesses with the same name stays unattached.
- **This applies to existing cases as well as new ones.** Uploading business income data to a case already open binds it and feeds the calculation.
- **Statements already sitting unattached are not repaired automatically.** If a case shows itemized profit & loss data but no business income figures, re-upload the statement or contact support. Many unattached statements are on cases with no business income source at all, which have to have the source added first.

### A statement whose business is not on the case yet

**A statement whose business is not on the case yet creates one.** Where a parsed statement cannot be matched to a business already on the case, Glade creates a business income source named from the name printed on the statement and binds the statement to it, so the figures reach line 8a without the business having to be entered by hand first. It does not guess where the name is ambiguous: a statement that matches several of the case's businesses, or that carries no business name at all, is left unbound for your team to place. This applies to statements read from now on — a statement that is already sitting unbound stays that way until it is placed.

## Edge Cases & Limitations

- A business is created from a statement's printed name only where the match is unambiguous. A statement matching several of the case's businesses, or carrying no business name, stays unbound and contributes nothing to line 8a until your team binds it.
- A profit & loss statement is matched to a business by an exact name after allowing for capitalization, spacing, and punctuation. Two businesses with the same recorded name cannot be told apart and neither is matched; rename one of them so the statement has a single answer to bind to.

## Related Features

- [Business and Rental Income](./README.md)
- [Profit & Loss Statements](./profit-and-loss-statements.md)
- [Schedule I Line 8a](./schedule-i-line-8a.md)
- [Adding Business and Rental Sources](./adding-business-sources.md)
- [Income Organizer](../README.md)
