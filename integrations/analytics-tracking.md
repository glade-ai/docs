# Analytics Tracking Integrations

## Overview

Glade lets firms connect their own Google Analytics and Meta (Facebook) tracking accounts to measure client activity on booking and payment confirmation pages. When configured, Glade fires tracking events from the firm's own measurement IDs alongside Glade's own analytics, so firms can attribute client conversions in their own dashboards and ad platforms.

This is useful for firms that run paid advertising or want to track how clients move from inquiry to booking or payment.

## Key Behaviors

- When a client completes a **booking**, a tracking event fires on the booking confirmation page using the firm's Google Analytics measurement ID and Meta pixel ID.
- When a client completes a **payment or purchase**, a tracking event fires on the payment confirmation page using both IDs.
- Glade's own internal analytics continue to run alongside the firm's tracking — enabling the firm's IDs does not replace Glade's tracking.
- Both integrations are independent. A firm can enable Google Analytics only, Meta only, or both.

## Configuration

Both integrations are configured in **Account Settings** under **Integrations**.

| Setting | Description |
|---------|-------------|
| **Google Analytics Measurement ID** | The `G-XXXXXXXXXX` ID from your Google Analytics property. Events are sent to this property on confirmation pages. |
| **Meta Pixel ID** | The numeric pixel ID from your Meta Business account. PageView and relevant events are sent using this ID. |

To connect an integration, open the settings modal for the relevant service, enter your ID, and save.

## Edge Cases & Limitations

- Tracking only fires on confirmation pages (booking confirmation and payment/purchase confirmation). It does not fire on other pages in Glade.
- If a client's browser blocks third-party tracking (ad blockers, browser privacy settings), events may not be captured. This is outside Glade's control.
- Setting up conversions, audiences, or ad campaigns based on the tracked events is done in Google Analytics or Meta — Glade only fires the events.

## Related Features

- [Appointments / Scheduling](../appointments/scheduling.md)
- [Online Payments](../payments/online-payments.md)
