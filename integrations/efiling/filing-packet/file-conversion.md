# PDF and Image Conversion

## Overview

Court electronic filing systems (CM/ECF) reject PDFs with editable layers and image files filed under a PDF name. When Glade compiles a filing packet, it flattens PDFs and converts photos to PDF automatically, and blocks the filing when a slot the court expects as a PDF still holds something that is not one.

## Key Behaviors

### PDF flattening in filing packets

Court electronic filing systems (CM/ECF) reject PDFs that contain editable layers such as fillable form fields, annotations, or sticky notes. Client-uploaded documents — cover sheets, local forms, photo IDs, mortgage statements — frequently arrive as non-flat PDFs and would otherwise cause the court to reject the packet.

- When Glade compiles an eFiling packet, every PDF source in the packet is automatically **flattened** before the documents are merged. Form fields, comments, and annotations are baked into the page so the final packet meets CM/ECF requirements without manual intervention.
- Flattening is transparent — your team does not need to enable a setting or pre-process files. Uploads continue to behave the same way as before; the filing packet that goes to the court is what changes.
- If flattening fails on a particular file for any reason, Glade falls back to including the original file in the packet rather than blocking the filing. The filing proceeds and the failure is reported internally for follow-up.
- Glade-generated petition PDFs can also be flattened on output when the workflow that produced them requests it, so signature blocks and form fields render as a static page rather than as fillable form widgets.

### Image uploads in filing packets

Client-uploaded documents sometimes arrive as photos — for example, a phone picture of a signed Certificate of Credit Counseling saved as a JPEG or PNG. Court filing systems reject these when they reach the court as image data under a PDF name.

- When Glade compiles a filing packet, image files (JPEG and PNG) are automatically converted to a single-page PDF before the packet goes to the court, so a photographed document files successfully without your team re-scanning or re-saving it.
- Conversion is transparent — there is no setting to enable, and uploads continue to behave the same way. Only JPEG and PNG images are converted; other file types pass through unchanged.
- If conversion fails for a particular image, Glade falls back to including the original file rather than blocking the filing, and reports the failure internally for follow-up.

### A photo that could not be converted stops the filing

The fallback above — include the original file when conversion fails — is safe for a supporting document, but not for a slot the court expects to be a PDF. A photo of a signed form filed under a PDF name reaches the court as image data, and the court either rejects the packet or times out mid-submission with nothing to point at.

- **A filing is now blocked before it starts when a packet slot the court expects as a PDF holds something that is not one.** The submission is refused, and the message names the documents at fault by the packet slot they occupy — for example, *Statement of Social Security (Form 121)* — so your team knows which upload to replace.
- **Replace the file with a real PDF to clear it.** Re-uploading the same photo does not help; convert or re-scan it, or ask the client for a PDF. Conversion is attempted automatically first, so a photo that reaches this block is one Glade could not convert — most often a very large phone picture.
- **The attorney override for missing required documents does not clear this block.** That override exists for a document your firm has decided the case does not need. A non-PDF in a PDF slot is not a missing document, it is a file the court cannot read, so signing off on it is not offered.
- **Slots the court expects as plain text are unaffected.** The creditor and debtor data files a district takes as text files are still filed as text. The check applies only to slots whose expected format is PDF.

This was reported on a Chapter 7 case where a 24-megapixel phone photo titled *Signature Pages* had been tagged as Form 121. Conversion overflowed, the original JPEG went to the court under a `.pdf` name, and the filing timed out. Nothing on the case indicated why.

## Edge Cases & Limitations

- The non-PDF check is decided from the packet slot the document occupies, not from inspecting the file your team recognizes it as. A file whose format Glade cannot determine at all is treated as not a PDF and blocks the filing, so a document that should be filable may need re-uploading before it is accepted.
- Filings submitted before this check existed could reach the court with an image under a PDF name. If a packet was rejected or timed out without an explanation, check the tagged documents for a photo — the filing can be resubmitted once it is replaced.

## Related Features

- [Filing Packet](./README.md)
- [Adding documents to the packet](./adding-documents.md)
- [Clearing blocking findings](../pre-filing-review/clearing-findings.md)
