# Email Actions

## Overview

A **Send email** action sends the configured email to the resolved recipients when an automation fires. This doc covers who the email is sent from, who receives it, how its formatting is preserved, and how a run's email can be re-sent from the run history. The tokens available in the subject and body are covered in [Email Tokens](./email-tokens.md).

## Key Behaviors

- **Sender identity**: automation emails are sent from your firm owner's email address, and the sender name shown to recipients is your firm's name. Replies go to the firm owner. If the email provider refuses that address because it has not been verified as an approved sender, Glade sends the message from `support@glade.ai` instead so the notice still reaches its recipients. The content is unchanged; only the address it arrives from differs. Automation emails arriving from the Glade support address are the signal to get your firm's sending address verified — until then, replies go to Glade support rather than to your firm.

### Recipients

Recipients are the people who receive the email when the automation fires. Three recipient kinds are supported and can be combined on a single automation:

- **Case-party token** — automatically resolves to the email address of a person on the case. Supported tokens are `debtor1`, `debtor2`, and `attorney`.
- **Team member** — a specific Glade team member at your firm. The system verifies the team member still belongs to your firm at fire time; soft-deleted team members are skipped.
- **Literal email** — a fixed email address you type in.

If an automation has no resolvable recipients at fire time (for example because every recipient was a team member who was removed), the run is logged as skipped and no email is sent.

### Line breaks and paragraphs in the email

The email you compose is sent with its spacing intact.

- A single line break in the editor arrives as a single line break. Writing `Date:` and `Time:` on consecutive lines produces two adjacent rows in the recipient's mail client, not two paragraphs with a gap between them.
- A blank line between two blocks of text starts a new paragraph, with the spacing you would expect.
- Bulleted and numbered lists and headings keep their spacing as well.

Recipients using Gmail and Outlook see the same spacing as everyone else. Emails sent before this was corrected went out either with the line breaks stripped or with every line separated by a full paragraph gap; those messages are not resent.

### Re-sending an automation email

A run's email can be sent again from the automation's run history — useful when the first send failed, when a recipient deleted it, or when the template has since been corrected and the notice needs to go out with the right wording.

- The email is rebuilt from the automation's **current** template and re-sent against the **original** notice, so a correction to the subject or body is reflected in the re-sent message while the case and hearing details stay those of the notice that triggered the run.
- Re-sending does not create a second run, does not create another task, and does not count as another firing of the automation. The run's history records the re-send in place rather than as a duplicate entry.
- Recipients are resolved again at the moment you re-send, so someone who has since left the firm is dropped and a corrected address is used.

> TODO: Confirm where the re-send action appears on a run in the automations UI, and which roles can use it.

## Configuration

| Setting | Description |
|---------|-------------|
| Recipients | Combination of case-party tokens, team members, and literal email addresses. |
| Subject and body | Email content with optional tokens — see [Email Tokens](./email-tokens.md). |

## Edge Cases & Limitations

- If a recipient is a soft-deleted team member, that recipient is skipped at fire time. The automation still fires for any remaining recipients.
- Re-sending an email re-sends only the email. A **Create task** action on the same automation is not run again, so a run that failed to create its task is not repaired by a re-send.
- A re-sent email uses the automation's template as it stands now. There is no way to re-send the message exactly as it was originally worded once the template has been edited.
- The fallback to the Glade support address is a delivery safeguard, not a substitute for verifying your firm's sending address. It applies per message, so every automation email keeps going out from the support address until the firm's own address is verified.

## Related Features

- [Court Notice Automations](./README.md)
- [Email Tokens](./email-tokens.md)
- [Automations and Actions](./automations-and-actions.md)
- [Create Task Actions](./create-task-actions.md)
