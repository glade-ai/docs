# Video Consultations

## Overview

Video consultations allow firms to conduct appointments remotely using Google Meet or Microsoft Teams. When a firm enables video conferencing on a product, Glade automatically generates a meeting link for each booking by creating a video session through the firm's connected calendar provider. Both the firm member and the client can join the meeting directly from Glade with a single click.

## Key Behaviors

### How video meetings are created

- Video meetings are generated automatically when a booking is created. No manual setup is required per appointment.
- The meeting link is created through the firm's connected calendar provider:
  - **Google Calendar** generates a Google Meet link.
  - **Microsoft Outlook** generates a Microsoft Teams link.
- The generated meeting link is stored on the booking and accessible to both parties.
- If the firm has no connected calendar with video capabilities, no meeting link is generated.

### Supported video platforms

| Platform | Calendar Provider | How it works |
|----------|------------------|--------------|
| Google Meet | Google Calendar | Glade creates a calendar event with Google Meet conferencing automatically attached. |
| Microsoft Teams | Outlook / Exchange Online | Glade creates an Outlook event with an online meeting enabled, generating a Teams link. |

Glade does not host video sessions itself. All video functionality depends on the firm's existing Google or Microsoft account.

### Joining a video consultation

- **Clients** see a "Join" button on their booking card in the client portal. Clicking it opens the meeting link in a new browser tab.
- **Firm members** see an "Open meeting link" or "Join Meeting" button on the booking detail page in the dashboard.
- Both parties are taken to the video platform's native interface (Google Meet or Microsoft Teams), where standard video call features are available.

### When meeting links appear

- The meeting link is available as soon as the booking is created (if video is enabled on the product).
- Links persist on the booking for the full duration — before, during, and after the appointment.
- If a booking is rescheduled, the meeting link updates with the calendar event. The link may change or stay the same depending on the provider.

### Appointment types that support video

- **Online Session** — primary type designed for video consultations. Video link is enabled by default.
- **Consultation** — general consultation type. Video can be optionally enabled.
- **In-Person Session** — primarily for physical meetings, but video can be optionally enabled as a hybrid option.
- **Chat Session** — for text-based services. Typically does not use video.

### Payment and billing

- Video consultations are treated as standard bookable products in Glade's billing system.
- Firms can set pricing tiers for their video sessions or offer them for free.
- Payment happens through the normal invoice flow. Video does not add separate charges.
- Cancellation and refund policies follow standard booking rules.

### Recording

- Glade does not manage video recording directly.
- Recording is handled by the video platform itself (Google Meet or Microsoft Teams), subject to the firm's settings on that platform.
- Recordings are stored in the platform's native storage (Google Drive for Meet, OneDrive/SharePoint for Teams).

### Session duration

- The appointment duration is defined by the product's session length configuration (e.g., 30 minutes, 60 minutes).
- Glade does not automatically end the video call when the scheduled time is up. The video platform's own timeout behavior applies.
- Both parties can stay on the call beyond the scheduled end time if the platform allows.

### Concurrent booking limits

- Each product can set a maximum number of concurrent bookings (default: 1).
- This prevents a firm member from being double-booked for overlapping video sessions.
- Combined with calendar sync, this ensures no conflicts with external commitments.

## Configuration

| Setting | Description |
|---------|-------------|
| Video conference link | Enable or disable automatic video link generation per product. |
| Connected calendar | Firm must have a Google Calendar or Outlook account connected. This determines which video platform is used. |
| Primary calendar | The calendar where Glade creates booking events with video links. |
| Product type | Choose Online Session, Consultation, In-Person Session, or Chat Session. |
| Session duration | Length of the video appointment. |
| Concurrent booking limit | Maximum overlapping bookings allowed per time slot (default: 1). |

## Edge Cases & Limitations

- Video links are only generated if the firm has a connected calendar provider (Google or Outlook). Without a connected calendar, no meeting link is created even if the product has video enabled.
- If the connected calendar's OAuth token expires, new bookings may not generate meeting links until the calendar is reconnected.
- There is no in-app video interface. Users are always redirected to the external video platform.
- Recording, waiting room, and admission controls are managed entirely by the video platform, not by Glade.
- The meeting link may change if a booking is rescheduled, depending on provider behavior.
- Firms cannot choose between Google Meet and Teams per booking. The platform is determined by which calendar provider is connected.
- If a firm has both Google and Outlook connected, the primary calendar determines which video platform is used.

## Related Features

- [Scheduling](./scheduling.md)
- [Calendar Sync](./calendar-sync.md)
- [Reminders](./reminders.md)
