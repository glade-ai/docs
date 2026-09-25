# Case Documents

## Overview

A case document is a form your firm fills in on its own behalf rather than sending out to a client — a local court form, a district cover sheet, an internal worksheet. You upload the PDF, Glade turns the boxes on it into a questionnaire your team completes on the case, and the completed answers are printed back onto the PDF. Case documents are set up by whoever maintains your firm's templates and used by attorneys and paralegals on individual cases.

Because a case document is a questionnaire underneath, most of what is written about [Questionnaires](questionnaires/README.md) — fields, conditional logic, autofills, locking, and PDF generation — applies to it. This page covers what is specific to a document built from an uploaded PDF.

## Key Behaviors

### Uploading a PDF

When you upload a fillable PDF, Glade reads the form fields already on it and creates one questionnaire field for each. A four-field form arrives as four fields ready to be arranged, rather than as an empty document.

- Previously no fields were detected at all, so every uploaded PDF produced an empty case document and each box had to be placed by hand in the editor. If your team abandoned a form because setting it up box by box was not worth the effort, it is worth uploading again.
- **A flat or scanned PDF has no form fields to read**, so it still yields none and its boxes are placed by hand. This is unchanged.

### Creating the document

Creating a case document opens the template editor with the uploaded form's fields in place.

- For a period, creation reported an error even though the document had in fact been created. Because the dialog stayed open, people clicked again — and **each retry created another complete copy**. Creation now succeeds and takes you into the editor.
- A related problem left the editor empty immediately after creation, on a document whose section had no field filling its PDF yet. The section keeps its link to the PDF, so the editor opens on the form rather than on nothing.

### Fields connected to case data

Where Glade can match a field on the PDF to something the case record already knows — a debtor's name, an address, the case number — it connects the two with a **two-way link** rather than copying the value across once.

- **The link keeps working.** A change to the case record updates the field, and an answer entered on the case document is written back to the case record. Previously the value was copied once when the document was created and then froze, so a case document could disagree with the rest of the case and nothing indicated it.
- **A field Glade cannot confidently match is left unconnected** rather than connected to something approximate. Fill it in by hand, or connect it yourself in the editor.
- **Re-reading the PDF does not disturb the connections you have set up.** Only fields that are newly added by the re-read are matched; anything already configured is left as it is.

### Re-saving after you edit the PDF

Editing the PDF and saving the case document again rebuilds the questionnaire from the form. The settings your team authored on the fields are carried across:

- **Conditional logic is kept**, on fields and on sections. Previously a later PDF edit wiped the conditions that had been set up, and there was nothing to indicate they had gone — they had to be re-authored from memory.
- **Renaming a field in the PDF editor keeps its settings.** A renamed field used to look like a brand-new one, so its lock, its case-data connection, and its conditions were dropped. A rename is exactly the edit an author makes, so this was easy to hit and tedious to recover from.
- **Numbered field labels are accepted.** A label such as `1. Debtor Name` produced a field name Glade rejected, which blocked the save. Names are now generated in a form Glade accepts, and fields that already exist keep the names they have, so a re-save does not change what your team has already configured.

## Configuration

- Case documents are set up per firm by whoever maintains your questionnaire templates. There are no firm-wide settings of their own.
- A questionnaire is marked as generating a case document on the template, which is what enables PDF generation from its answers — see [Template Settings](questionnaires/templates/template-settings.md).
- Field-level settings — lock, conditional visibility, case-data connection, autofill — are configured per field in the template editor, the same way as on any questionnaire.

## Edge Cases & Limitations

- A flat or scanned PDF yields no fields on upload. Its boxes have to be placed by hand.
- **Duplicate templates created by the failed-creation retries are not cleaned up automatically.** If your firm has two or three identical copies of the same case document from that period, delete the extras by hand.
- Case documents created before fields were detected on upload are not rebuilt. Re-upload the PDF if you want the fields read from it.
- Conditional logic and field settings lost to an earlier PDF edit or field rename are not recoverable — they have to be authored again, once.
- Generating the PDF from a case document does not submit or complete it, and does not advance the case. See [Generating a PDF from a case document](questionnaires/petition/signatures.md#generating-a-pdf-from-a-case-document).
- A case document your team has uploaded can be placed into an electronic filing packet slot, where it supersedes the generated version — see [Electronic Court Filing](../integrations/efiling/README.md).

> TODO: Confirm where case documents are created and edited in the dashboard, and which roles can upload or edit one.

> TODO: Confirm whether an existing case document can be re-matched to case data on demand, or only when fields are newly added.

## Related Features

- [Questionnaires](questionnaires/README.md) — a case document is a questionnaire built from an uploaded PDF.
- [Signature Pages](./signature-pages.md)
- [Document Collection](document-collection/README.md)
- [Electronic Court Filing](../integrations/efiling/README.md) — filing a case document as part of a packet.
