# Connecting PACER

## Overview

Before Glade can file on a firm's behalf, the firm connects its PACER credentials from the PACER integration settings. Glade uses those credentials to log in to PACER during each filing.

## Key Behaviors

### Connecting PACER credentials

- Firms provide their PACER account email and two-factor authentication key from the PACER integration settings.
- Credentials are stored encrypted and linked to the firm's account.
- PACER session tokens are cached to avoid repeated logins across filings.

### PACER login failures

When a filing fails because Glade could not log in to PACER, the case status dashboard reports **"PACER login failed."** without advising you to check your credentials.

Login failures are frequently not a credential problem — a two-factor prompt that timed out while waiting is the most common cause — so the message no longer points your team at credentials that are usually correct. Where a more specific reason is available, it appears in the case's filing log. Retry the filing first; only re-enter your PACER details if the failures continue.

## Configuration

| Setting | Description |
|---------|-------------|
| PACER credentials | Email and 2FA key, entered in integration settings |

## Edge Cases & Limitations

- PACER passwords are not stored — they are passed only at filing time. The 2FA key is stored encrypted.
- Reconnecting after a credential change requires re-entering the 2FA key.
- If the PACER session token expires mid-filing, the submission fails and can be retried.

## Related Features

- [PACER Integration](./README.md)
- [Filing workflow](./filing-workflow.md)
- [Filing progress](../efiling/filing-progress.md)
