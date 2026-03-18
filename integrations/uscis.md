# USCIS Integration

## Overview

Glade integrates with USCIS (United States Citizenship and Immigration Services) to automate immigration petition filing and case status tracking. Firms can submit Form I-129 (Petition for a Nonimmigrant Worker) for H-1B visa cases directly from Glade, and track case status updates using USCIS receipt numbers.

## Key Behaviors

### Connecting USCIS credentials

- Firms provide their USCIS account email, password, and two-factor authentication key.
- Credentials are stored encrypted and linked to the firm's account.
- 2FA is handled via TOTP (authenticator app codes) during automated sessions.

### Supported case types

- **Form I-129** — Petition for a Nonimmigrant Worker
- **Form I-907** — Premium Processing Service (filed alongside I-129)
- **Visa classifications**: H-1B and variants (1B1, 1B2, 1B3)

Submission basis types include: new employment, continuation of previously approved employment, change in employment, new concurrent employment, change of employer, and amended petition.

### Filing workflow

1. The firm prepares the case questionnaire in Glade with debtor/beneficiary information, employer details, and supporting documents.
2. An attorney initiates filing from the case view.
3. Glade automates the USCIS form submission:
   - Logs into my.uscis.gov with the firm's credentials and 2FA.
   - Selects the company and form type (I-129).
   - Fills form sections: getting started, applicant information, beneficiary information, employment details, H-classification supplement, and H-1B data collection.
   - Submits the form and captures the receipt number.
4. On success, the receipt number is stored on the case and the firm is notified.
5. On failure, error details are recorded and the firm can retry or file manually.

### Company management

- Firms can add companies and administrators to their USCIS account through Glade.
- Company details include: name, DBA, mailing address, and tax identification (EIN/SSN/ITIN).
- Administrators are added with name, email, and phone.

### Case status tracking

- Firms can query USCIS case status using receipt numbers.
- Status queries return: current action code, action date, status description, form type, and full case history.
- Case history includes all historical status updates with dates and jurisdiction information.

### Form data collected

The I-129 filing collects:

- **Getting started**: visa classification, cap selection, processing options, attorney/preparer info
- **Applicant**: company name, signatory, contact info, mailing address, tax IDs, fee exemption status
- **Beneficiary**: name, date of birth, immigration history, citizenship, contact address, prior filings
- **Employment**: job title, wage details, employment dates, employer info, work location, itinerary
- **H-classification supplement**: passport details, prior H-class stays, ownership questions, job duties
- **H-1B data collection**: education level, field of study, pay rate, DOT/NAICS codes, cap exemption determination

## Configuration

| Setting | Description |
|---------|-------------|
| USCIS credentials | Email, password, and 2FA key entered in integration settings |
| Company selection | Selected per filing from the available companies in the USCIS account |

## Edge Cases & Limitations

- Only H-1B visa petitions (Form I-129) are currently supported. Other immigration forms are not available.
- The firm's USCIS account must have 2FA enabled with a TOTP authenticator app — SMS-based 2FA is not supported.
- If the automated session is interrupted (login failure, page timeout), the submission is marked as failed. The attorney can retry or register a manually filed case number.
- Case status queries depend on the USCIS Torch API, which occasionally returns malformed responses. Glade handles these gracefully but status may be temporarily unavailable.
- Filing is asynchronous — the attorney does not need to keep the page open during submission.

## Related Features

- [Electronic Court Filing (eFiling)](./efiling.md)
- [PACER Integration](./pacer.md)
- [Workflows](../workflows/automation-rules.md)
