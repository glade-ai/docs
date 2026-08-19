# Signature Pages

## Overview

Petition documents Glade generates carry signature pages for the debtor and the attorney. Once a page has been signed, it is uploaded back to the case and Glade merges the executed page into the correct form, so the form goes to the court with the real signature in place rather than the blank page. This page covers how an uploaded executed page is matched to its form and what happens when it cannot be matched.

For how signature pages are laid out in the documents Glade generates, see [Petition Settings](../back-office/settings.md#petition-settings).

## Key Behaviors

### How an uploaded page is matched to its form

Glade identifies an executed signature page by reading the **footer** of the uploaded page — the form's identity and its page number, printed along the bottom edge — and merges it into the form that footer names.

- Official bankruptcy forms are identified by the official form number in the footer, for example `Official Form 108`.
- **Named local forms without an official form number** are also recognized. Some forms are court-specific or produced by Glade and carry a name in the footer instead of an official form number. The **Verification of Creditor Matrix** is recognized this way.
- When a page's body text mentions a different form than its footer does, the footer wins. A signed Form 108 page whose body cites Form 106G is identified as Form 108. Previously the first form reference anywhere on the page was used, so a page like this was matched to the wrong form and the merge failed with a message that no matching signature page could be found in the selected form — even though the correct page had been uploaded.

### Merging a whole signed packet from one scan

Firms commonly print the signature packet, sign every page by hand, and scan the lot back as a single multi-page PDF. That scan can be merged in one action, rather than being split into one file per form first.

- Glade reads the scan once, identifies each page by its footer as described above, matches the pages to the signature pages the case expects, and applies every successful match together in a single update to the petition.
- The result reports what happened to each form, and names any expected signature page that no page in the scan matched — so a page the scanner missed, or one signed in the wrong place, is called out rather than passing unnoticed.
- Matched pages are replaced. Expected forms with no match are left as they were and can be handled with a follow-up upload; nothing is filed with a blank page in place of a match that failed.
- Merging one file into one form still works exactly as before, for teams that prefer to handle pages individually.

Previously merge accepted one file for one form at a time, so a firm that scanned the executed packet as a single PDF had to split it up before any of it could be merged.

### When a page cannot be matched

If Glade cannot read a form identity from the footer, the upload is held for review rather than merged, with a message that the form footer could not be read. The document is still stored on the case; nothing is lost.

This is what used to happen on every upload of a form with no official form number, which made those forms impossible to complete through signature page merge and blocked filing on the cases that needed them.

## Configuration

There is no per-firm configuration for how executed pages are matched. Recognition of named local forms is maintained by Glade — contact support to have a form your court requires added.

Merging a multi-page executed scan in one action depends on signature-page merge being switched on for your firm. Contact support if it is not available on your cases.

> TODO: Confirm where a multi-page executed scan is uploaded from in the app, and how the per-form results and the list of unmatched forms are presented, so those steps can be documented here.

## Edge Cases & Limitations

- Recognition of named local forms works from a maintained list, not from a general rule, so that a page cannot be merged into the wrong form by accident. A named local form that is not yet on the list is held for review. Other forms known to have this shape — including the Central District of California's F 1007-1 and the Western District of Pennsylvania's LF-29 — are not yet recognized.
- Matching depends on the footer surviving scanning and printing. A page scanned so that the footer is cut off, illegible, or missing cannot be matched.

> TODO: Confirm where an executed signature page is uploaded from, and where a page held for review appears for the team to resolve, so those steps can be documented here.

## Related Features

- [Questionnaires](./questionnaires.md) — the petition forms and draft packet that signature pages belong to.
- [Document Collection](./document-collection.md) — how uploaded files are requested and reviewed.
- [Back Office Settings](../back-office/settings.md#petition-settings) — how signature pages are laid out in generated petitions.
