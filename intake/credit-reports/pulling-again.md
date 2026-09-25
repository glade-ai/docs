# Pulling a Report Again

## Overview

A credit report that has already come back for a debtor normally is not requested again. This page covers the two situations where a debtor does need a fresh report: your team re-pulling a named debtor whose stored report is unusable (typically because of a consumer security freeze), and a client enrolling with the bureau again after a case converts from Chapter 7 to Chapter 13.

## Key Behaviors

### Re-pulling a debtor's report

A credit report that has already come back for a debtor normally cannot be requested again. That protects the client — a second request means a second hard inquiry on their credit file, and a second charge to your firm — and it is what lets a joint case add a co-debtor later without re-pulling the debtor whose report is already on file.

Sometimes a stored report is genuinely unusable, and your team needs a fresh one. The common cause is a **consumer security freeze**: the bureau accepts the request, returns a report, and Glade stores and completes it, but the report contains nothing because the client's file is frozen. Nothing about it looks like a failure. Once the client lifts the freeze, the case is left holding a finished, empty report.

- **Your team can ask for a named debtor's report to be pulled again.** You choose the debtor; Glade re-requests only that debtor's report, over the top of the one already stored.
- **Glade never decides this for you.** It acts only on the debtor you name. This is deliberate: an empty report with no error on it is indistinguishable from the report of a client with no credit history, so a rule that re-pulled anything that "looked empty" would put unrequested hard inquiries on clients who never needed one.
- **Only a debtor who already has a stored report can be re-pulled.** Naming a debtor whose report has not come back yet does nothing — they are already going to be pulled.
- **Glade also detects some freezes on its own.** Where the bureau states the freeze in the report, the case offers a re-pull without your team having to ask. The explicit re-pull covers the cases it cannot detect, which are the ones where the bureau sends no freeze message at all. Both routes do the same thing.

Re-pull when the report itself is unusable and the reason has been resolved — the client has lifted their freeze, for example. It is not the fix for a report that came back with accounts that then failed to reach the schedules; see [When a report comes back with no creditors](./importing-creditors.md#when-a-report-comes-back-with-no-creditors), where the stored report needs re-reading rather than re-requesting.

> TODO: Confirm where the re-pull action appears on the credit report card and which roles can run it.

### What a re-pull costs

- **A re-pull is a fresh pull and is billed as its own pull** at the standard rate. It replaces the stored report for that debtor rather than being held alongside it.
- **On a joint report, only the debtor you name is affected.** The co-debtor's report is left exactly as it is, so a clean co-debtor takes no second hard inquiry and no second charge.
- **A re-pull counts against your firm's pull attempt limit** for the case, like any other pull.

### Enrolling again after a chapter conversion

When a case converts from Chapter 7 to Chapter 13, the new chapter carries its own credit report, so the client is asked to complete the bureau's identity enrollment again in the client portal.

- **A client who enrolled on the earlier chapter can complete it.** Glade recognises the identity the bureau already holds for that person at your firm and carries straight on to verification, rather than registering them a second time — which the bureau refuses.
- Previously the client could not get past enrollment at all. The bureau rejected the second registration as an identity it had already seen, so the Chapter 13 report could not be obtained and the filing stalled with nothing the client could do. A client who was blocked this way can retry enrollment now.
- The earlier enrollment is only reused where it belongs to the **same person at the same firm**. An enrollment at another firm is never reused.
- A client enrolling for the first time is unaffected and registers as before.

> TODO: Confirm whether the client is prompted to re-enroll automatically on conversion or has to be sent the enrollment step again, and whether the Chapter 13 report is billed as a separate pull.

## Edge Cases & Limitations

- Re-pulling a debtor's report replaces the stored one rather than keeping both, so the empty report a freeze produced is not retained as a record of the attempt. Note what you need from it before re-pulling.
- Re-pulling while the client's freeze is still in place returns another empty report, billed as a pull. Confirm with the client that the freeze has been lifted first.
- The pull attempt limit counts re-pulls. On a case that has already used its attempts, the limit has to be raised in firm settings before a re-pull can run.

## Related Features

- [Credit Reports](./README.md)
- [Pulling a Credit Report](./pulling-a-report.md)
- [Importing Creditors from a Report](./importing-creditors.md)
- [Client Portal](../client-portal/README.md)
- [Settings](../../back-office/settings.md)
