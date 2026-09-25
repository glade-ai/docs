# Filing Packet Document Types

## Overview

Each document in the filing packet must be labeled with the correct ECF document type. The document type dropdown in the filing packet lists named options for all commonly filed documents. Selecting the correct type ensures courts can identify each file — courts including FLMB and FLSB reject filings that contain unrecognized filenames.

## Key Behaviors

- Use a named document type whenever one exists in the dropdown. The generic "Other" option is for documents that do not match any named type.

### Common document types

- For **Chapter 7 business-debt cases** where the debtor is claiming exemption from the means test presumption of abuse, upload the B122A-1 Supplement and select **Statement of Debtor's Temporary Exclusion from Presumption of Abuse (B122A-1Supp)** from the document type dropdown. This is supported for all available districts. Filing this document labeled as "Other" causes a submission failure.
- When a court requires individual debtor identification documents, select **PhotoID (Debtor 1)** or **PhotoID (Debtor 2)** for each debtor's photo identification, and **DeBN (Debtor 1)** or **DeBN (Debtor 2)** for each debtor's Declaration of Electronic Notice. The Debtor 1 variant is for the primary debtor; the Debtor 2 variant is for the co-debtor in a joint case.
- **Means Exemption (Form 122A-1Supp)** is also recognized end-to-end across the catalog, validator, and runtime allowlist, so uploads that select this option no longer fail filename validation on the way to PACER.
- Glade also accepts non-canonical filename variants for **Verification of Creditor Matrix** uploads, so files named with run-together or otherwise normalized variants pass the filing packet's filename check instead of being rejected.

### District-specific document types

- For **Western District of Pennsylvania (PAWB)** Chapter 7 cases, **Local Form 1 — Declaration Re: Electronic Filing of Petition, Schedules & Statements** is available in the document type dropdown. This form is submitted through the EDSS portal alongside the SSN Statement — it is not part of the standard ECF filing packet. A Local Form 1 slot appears in the per-district document checklist for PAWB Chapter 7 workflows once the document is labeled and uploaded.
- For **Florida Southern (FLSB)** Chapter 13 cases, **Local Form 67 — Certification of Compliance** is available in the document type dropdown. The form auto-surfaces in the FLSB Chapter 13 required-document checklist, and ad-hoc uploads from the case documents picker are accepted under common filename variants (with or without spaces, hyphens, underscores, or the full form name).
- For **Maryland (MDB)** Chapter 7 cases, **Form 108 — Statement of Intention** is filed as a separate case-open document rather than folded into the consolidated petition. It has its own **Statement of Intent** slot in the district's document checklist, and common filename variants for the form are recognized automatically so the upload lands in that slot instead of falling back to **Other**.
- Additional district-specific document types are available in the dropdown so attorneys filing in these courts can label uploads correctly instead of falling back to **Other**:
  - **Ohio Southern (OHSB)** Chapter 7 — **Statement of Intent** (Statement of Intention for individuals filing under Chapter 7) and **Verification of Creditor Matrix** (OHSB filename variant) are selectable from the document type dropdown.
  - **Washington Eastern (WAEB)** Chapter 7 — **Declaration Regarding Payments (LBR 1007-1)** is selectable from the document type dropdown.
  - **New Mexico (NMB)** Chapter 7 — **Marital Status** is selectable from the document type dropdown.
  - **Louisiana Eastern (LAEB)** Chapter 7 — **Tax Returns** is selectable from the document type dropdown.
  - **Pennsylvania Western (PAWB)** Chapter 7 — `lf29.pdf` (the PAWB filename for the Verification of Creditor Matrix) is now accepted on upload in addition to the canonical name.
- For **Ohio Southern (OHSB)** Chapter 7 joint-debtor filings, **Statement 1015-2 — Joint Debtor Compliance (OHSB)** is available in the document type dropdown for the Joint Debtor Compliance Statement form (Statement 1015-2 with No Prior). Label the uploaded form with this document type so it is recognized at filing time — uploading it as **Other** prevents the OHSB filing engine from picking it up.
- For **Washington Eastern (WAEB)** Chapter 7 cases, three additional installment-and-fee-related document slots are now available in the case's document checklist when the corresponding files are attached: **Form 103A — Application for Individual to Pay Filing Fee in Installments**, **Form 103B — Application to Have the Filing Fee Waived**, and **LBR 1007-1 — Declaration Regarding Payments**. Slots only render when a file is attached, so cases that pay the filing fee in a single transaction continue to show only the standard checklist. Common filename variants for the LBR 1007-1 declaration (with or without spaces, hyphens, or the full form name) are accepted on upload.

### Custom filenames

- When you assign a custom filename to a document being added to PACER, Glade now preserves spaces, hyphens, parentheses, periods, plus signs, apostrophes, and accented letters in the filename. Filenames such as `Pay Advices`, `Tax Return 2024`, and `Photo ID (Debtor 1)` flow through to PACER as typed instead of being collapsed into a single run-on word. Only characters that filesystems or PACER cannot accept (such as path separators and control characters) are removed.
- Filenames that contain only special characters and would resolve to an empty name are rejected at the form before they can be saved, so you see the validation message immediately rather than encountering a runtime error during filing.

### Labels the district does not accept

- **A document type the district does not accept is refused, not quietly dropped.** When you label a document by hand and the filing district's rules do not accept that type for the case, the save fails with an error explaining the problem. Previously the save appeared to succeed while the label was silently cleared, so the document went back to being unlabelled — and the packet was a file short at filing time with nothing on screen to say why. Check any document you labelled and later found unlabelled again; it was most likely refused by the district's rules rather than lost.
- The district check recognises every way a district can accept a document — as its own upload, folded into the case-open bundle, combined with other files, or excluded from the packet under a specific filename. A document type a district genuinely accepts is no longer refused because it happens to be accepted in one of the less common ways.
- Automatic labelling is unchanged. When Glade cannot match a document to a district's slot on its own, it still leaves the document unlabelled rather than guessing at a type, so nothing is filed under a label nobody chose.
- **A form that is built into the petition does not also appear as its own packet row.** Where a district folds a form into the consolidated petition — Form 122A-1 is the common one — that form is no longer labelled as a separate filing document, so it stops appearing in the filing packet as a standalone row alongside the petition that already contains it. This now holds on every case; previously it applied only to some, and on the rest staff had to clear the label on the form by hand before each submission. If your team has been doing that as a routine step before filing, it is no longer needed.

## Related Features

- [Filing Packet](./README.md)
- [Adding documents to the packet](./adding-documents.md)
- [Required documents in the filing packet](./required-documents.md)
- [Packet checks in the pre-filing review](../pre-filing-review/packet-checks.md)
- [South Carolina DeBN elections](../../pacer/south-carolina-debn.md)
