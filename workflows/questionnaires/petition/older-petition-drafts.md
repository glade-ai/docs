# Older Petition Drafts

## Overview

Cases prepared before numbered petition drafts were introduced still hold petitions in the old places and under the old names: the petition drafts and the eFiling packet's **Petition** in **Forms & Schedules**, and automatically built copies named **Petition (Draft).pdf** and **Petition for Signatures (Draft).pdf**. Completing the questionnaire no longer builds or refreshes those automatic copies, so they stop matching later answers. Glade tidies these older documents up so they don't get mistaken for current ones. This page covers what moves, what gets renamed, and how renamed copies are treated.

## Key Behaviors

### Older petitions move to the Petitions folder

- Petition drafts and their signature pages in **Forms & Schedules** move to the case's **Petitions** folder, where numbered drafts are now filed.
- The eFiling packet's **Petition.pdf** moves from **Forms & Schedules** to **Petitions** too. Only its folder changes. It stays part of the filing.
- Drafts your team saved to a folder of its own choosing stay where they are.
- A document your team uploaded and named **Petition.pdf** stays where it is.

### Automatically built drafts are labeled as legacy

- **Petition (Draft).pdf** is renamed **Petition (Draft) - legacy.pdf**, and **Petition for Signatures (Draft).pdf** is renamed **Petition for Signatures (Draft) - legacy.pdf**.
- The rename changes only the name shown in Glade and used for downloads. The file itself is kept as it was, and nothing is deleted.
- Renamed legacy copies are never compiled into the filing **Petition** and are never merged into a new draft, even when one is selected.
- If signed signature pages are merged on a case that has no numbered drafts, they still go into the older draft, whether it has been renamed or not.

### Signed pages go back to the draft they came from

- Each numbered draft and its signature pages are tied to the **Generate petition** run that produced them. When the signed signature pages of a draft are merged back, they go into that run's draft, even if newer versions have been generated since.

## Edge Cases & Limitations

- Signature pages generated before drafts were tied to their run are matched to a draft the older way, by version number.
- Older petition drafts are moved and renamed as Glade applies this to your firm. If the **Generate petition** dialog or the eFiling petition selection still offers a renamed legacy draft, contact Glade support.

## Related Features

- [Petition](./README.md)
- [Generating a Draft Petition](./draft-petition.md)
- [Signature Pages](../../signature-pages.md)
- [eFiling Filing Packet](../../../integrations/efiling/filing-packet/README.md)
- [Case Documents](../../case-documents.md)
