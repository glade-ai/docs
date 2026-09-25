# Required Documents in the Filing Packet

## Overview

Some documents are required by a district's rules and must not be dropped from the petition before filing. Which documents a district expects, and whether each is filed inside the petition or as its own file, is configured per district and chapter by Glade.

## Key Behaviors

### Locked required documents

When you prepare a petition, any document the district marks as required is pre-checked and **locked** in the document list — it shows a **Required for filing** note and cannot be unchecked or removed, and range-selection skips over it. This prevents a required document from being left out by accident. For example, Florida Middle District Chapter 7 petitions require the Creditor Matrix and the Verification of Creditor Matrix, so both are locked into the packet. Other pre-checked documents that the district does not mark as required stay freely toggleable, so you can include or exclude them as needed.

**Glade's own petition output is not offered as an input.** The documents Glade compiles for the case — **Petition**, **Petition (Draft)**, **Petition for Signatures (Draft)**, and **Signature Pages** — are not selectable in the Prepare Petition document list. They are what the compile produces, not material to fold into it, and picking one built a petition containing a copy of an earlier petition. How each of these documents is filed is unchanged; only their appearance in the selection list is.

### Per-district configuration

Which documents a district expects, and whether each is filed inside the petition or as its own file, is configured per district and chapter by Glade. **Eastern District of Kentucky** Chapter 7 cases now include **Form 103A** — the application to pay the filing fee in installments — as its own document in the packet. It appears only when the case elects to pay the fee in installments, and not when a fee waiver is requested instead. Previously the form had no slot in the packet for that district, so filers electing installments could not include it. If your district is missing a form your court requires, contact support to have it configured.

Some districts fold a form into the petition itself rather than expecting it as its own file — North Carolina Eastern Chapter 7, for example, builds Form 122A-1 and Form 2030 into the petition. Those forms have no separate slot in the packet, and Glade no longer reports them as missing documents. A compliant filing in one of these districts is no longer held up over a form that is already inside the petition. A form the district does expect as its own file is still flagged when it is genuinely absent, including a form that is both built into the petition and filed separately.

**Florida Middle District Chapter 13** filings are a correction to this. The Certificate of Credit Counseling and Form 121 (Statement About Your Social Security Numbers) are filed as their own separate documents in this district rather than being folded into the petition. They had been configured the wrong way round, so each now has its own slot in the packet and is expected as a separate file.

## Related Features

- [Filing Packet](./README.md)
- [Filing packet document types](./document-types.md)
- [Required documents check](../pre-filing-review/required-documents.md) — how missing required documents are reported before filing.
