# Petition Document Order

## Overview

Your firm can save the order its petition documents should appear in. Glade applies that order whenever it builds a petition for a case — drafts, signing copies and the compiled petition — so attorneys and paralegals don't have to rearrange the documents by hand on every case. A case your team has rearranged by hand keeps its own order.

## Key Behaviors

- **The firm's saved order is used every time a petition is built.** It applies to the marked draft, the unmarked copy for signatures, the signature pages, and the petition compiled for filing.
- **Documents your firm has placed come first, in your order.** Any document that isn't in your saved order follows them, in the order it would otherwise have had.
- **The creditor matrix stays the last page of the draft.**
- **Documents added to the questionnaire later fall into place.** When a new form or case document is added to a case, it is placed according to your firm's order instead of at the end.
- **Case documents** follow the firm order through the questionnaire section they belong to. This doesn't change whether a case document is included in the petition.
- **Existing cases** take the firm order the next time their petition is generated.
- **A case your team has rearranged keeps its own order.** Once someone drags documents into a different order in **Prepare Petition**, later automatic generation for that case no longer replaces that order with the firm's.
- Previously the order saved in Petition Settings was stored but never used. Generated petitions followed the questionnaire's section order whatever your firm had set.

## Configuration

| Setting | Where | Effect |
|---|---|---|
| Petition document order | [Petition Settings](../../../back-office/settings.md#petition-settings) | The order the firm's petition documents appear in on every generated petition. |
| Case-specific order | **Prepare Petition** on the case | Dragging documents into a new order there overrides the firm order for that case only. |

> TODO: Confirm the on-screen label of the document-order control in Petition Settings, and whether a case's custom order can be reset back to the firm order.

## Edge Cases & Limitations

- Petitions generated before this change are not rebuilt. Generate the petition again to get the firm order.
- Documents that are not part of the petition keep the place they already had in the case's document list.
- Once a case has been rearranged in Prepare Petition, changes to the firm's saved order no longer reach that case.

## Related Features

- [Petition](./README.md)
- [Generating a Draft Petition](./draft-petition.md)
- [Petition Settings](../../../back-office/settings.md#petition-settings)
- [Signature Pages](../../signature-pages.md)
