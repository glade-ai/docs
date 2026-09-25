# An Attorney Is Assigned to File

## Overview

A case can be prepared with the attorney left as **None**, and nothing used to stop it being submitted that way. On a firm whose account files for more than one attorney, the court's filing system then asks who the filing is for and the submission fails at that point — late, and with nothing on the case to say what was missing. The pre-filing review now checks this up front and blocks submission until an attorney is resolved.

## Key Behaviors

- The check passes when an attorney is **assigned to the case**, or when your firm has a **default filing attorney** set. A solo firm with a default set continues to pass without assigning anyone case by case.
- It applies to Chapter 7 and Chapter 13 alike, in every district.
- This check fails closed. If Glade cannot determine your firm's default filing attorney, the case is blocked rather than allowed through, so a filing is never released on an unanswered question about who is filing it.

## Configuration

- **Default filing attorney** — a firm-level setting. When set, cases without an assigned attorney pass this check.

## Edge Cases & Limitations

- Firms that file for several attorneys should confirm that cases carry an assignment, or that a default is set, before the next filing — a case with neither is blocked from this point on where it previously reached the court and failed there.

## Related Features

- [Pre-filing Review](./README.md)
- [Who can clear a blocking finding](./clearing-findings.md)
