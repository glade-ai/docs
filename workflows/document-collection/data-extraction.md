# Automatic Data Extraction

## Overview

When certain documents are uploaded to a document request, Glade reads them and applies the details to the case record — creditors, assets, and debtor information. Extracted values are assistive: they fill in empty fields and are held for review when they disagree with information someone has already confirmed. This page covers which document types are read, what is extracted from each, and how conflicts are handled. Income documents are covered separately in [Income Documents](./income-documents.md).

## Key Behaviors

- When an uploaded document feeds automatic data extraction, its data is applied to the case no matter who uploaded it — the client, a spouse or other party on a joint case, firm staff or a paralegal, or a workflow collaborator. Previously, extracted data was dropped whenever the uploader was not the case's primary client; now any authorized uploader's document contributes its extracted data.

### Mortgage statements

When a mortgage statement is uploaded, Glade detects the document type and extracts loan details into the matching creditor record — the servicer brand, loan account number, loan type, origination date, and the servicer's remittance address. Statements that share an account number are recognized as the same loan, so consecutive monthly statements update one creditor entry instead of creating duplicates. Statements with no readable account number are kept separate to avoid merging unrelated loans from the same servicer. Beyond the servicer creditor, Glade also records the mortgaged property itself as a real-estate asset, capturing the property address. It does not fill in the property's value — a mortgage statement shows the balance owed on the loan, not what the property is worth, so that figure is entered separately. Repeat statements for the same property are recognized by the property address and update the one real-estate asset instead of adding another. Extracted values are assistive — any value a team member or client has entered manually for the same field takes precedence over the AI-extracted value.

### Social Security cards

When a Social Security card is uploaded, Glade reads the holder's legal name and nine-digit Social Security number and writes them to the matching debtor's record. The details are applied to the debtor the document request is assigned to — so on a joint case, the request assigned to the primary debtor fills the primary filer's name and SSN, and the request assigned to the co-debtor fills the co-filer's, regardless of who performed the upload (the attorney often uploads on the client's behalf). If Glade cannot determine which debtor the card belongs to, it applies none of the details rather than risk overwriting the wrong filer — enter that filer's name and SSN manually in that case. The Social Security number is saved in the standard XXX-XX-XXXX format, and a number that cannot be read clearly or is not a valid Social Security number is left off rather than guessed. Only the physical card is read — Social Security award or benefit letters and 1099 forms are not treated as cards. Extracted values are assistive: a value a team member or client has already entered takes precedence.

### Identity documents (currently turned off)

Automatic extraction from driver's licenses and passports is paused. Uploaded licenses and passports are still accepted and stored on the case, but Glade no longer reads the filer's name, date of birth, or address from them — enter those details manually. The feature is paused because an uploaded ID carries no signal about which debtor it belongs to, so on a joint case a co-filer's license or passport could overwrite the primary filer's details. It will return once Glade can confirm which debtor each ID belongs to before applying the data.

### Vehicle documents

When a vehicle title, insurance card, or vehicle history report is uploaded, Glade extracts the vehicle's year, make, model, and VIN — plus the odometer reading from a title — into the matching asset record. A title, insurance card, history report, and registration for the same vehicle are recognized by their VIN and merge into a single asset entry instead of creating duplicates. If a client has already added a vehicle to their property list but not yet filled in its details, an uploaded vehicle document fills in that existing entry rather than creating a second one — so an empty vehicle a client added by hand and the document they upload for it end up as one record. History reports distinguish current details from past ones, so a prior owner or plate does not overwrite the current record.

### Investment account statements

When an investment account statement — such as a brokerage, retirement, or fund-company statement — is uploaded, Glade detects the document type and records the account as an asset on the case. It captures the financial institution, the account number, the account's total value, and how the account is owned (individual or joint), and writes them to the matching asset record. When a single document describes more than one account — for example, a positions screen that lists both a brokerage account and a 401(k), or a statement covering both checking and savings — each account is recorded as its own asset, instead of only the first being captured and the rest dropped. Sub-balances that belong to one plan (such as the Roth and employer-deferral buckets within a single 403(b)) are combined into one entry at the plan's total, while genuinely separate accounts are kept as separate assets. Repeat statements for the same account are recognized by their account number and update one asset entry instead of creating duplicates; statements with no readable account number are kept separate so unrelated accounts are not merged. Extracted values are assistive — a value already entered by a team member or client takes precedence.

### Conflicting extracted values held for review

When a value read from an uploaded document disagrees with a value already on the case record, the change is held for your team to review rather than overwriting the existing value automatically. Values that match, or that fill a field for the first time, are applied directly. The blank starter entries a case begins with — the empty placeholder rows created when the case is first set up — count as empty, not as a confirmed answer. A document-extracted value that fills one of these blank placeholders is applied directly and becomes the current value, and it is not flagged as a conflict against the placeholder it replaced. Only once a real value has been entered or confirmed — by your team, a questionnaire, a credit report, or an earlier document — does a later, disagreeing document value get held for review. This keeps automatic extraction from silently changing information a person has already confirmed, while making sure extracted values are not left sitting behind an empty placeholder.

## Configuration

- **Structured data types** on file slots (income data, asset data, personal data, prompt data) enable structured data extraction from uploaded documents.

## Edge Cases & Limitations

- Identity document extraction (driver's licenses and passports) is currently turned off. Enter each filer's name, date of birth, and address manually until automatic extraction returns.
- When an insurance card lists more than one vehicle, only the first vehicle on the card is extracted. Add any additional vehicles manually.

## Related Features

- [Document Collection](./README.md)
- [Income Documents](./income-documents.md)
- [Document Requests](./document-requests.md)
- [Questionnaires](../questionnaires/README.md)
