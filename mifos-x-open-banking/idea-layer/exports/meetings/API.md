# API Reference — Meetings

| Field    | Value                                               |
|----------|-----------------------------------------------------|
| Feature  | meetings                                            |
| Base URL | https://apisandbox.openbankproject.com              |
| Auth     | DirectLogin — `DirectLogin token="<token>"` header  |

---

## GET /obp/v3.1.0/banks/{bankId}/meetings

**Auth:** DirectLogin
**Tag:** Meetings
**Trigger:** `loadMeetings()` on screen entry (initial state = loading); re-triggered on `RetryLoad` event; client-side filter by `selectedDate` after load to produce `filteredMeetings`.

Fetches all meetings for the given bank. The client derives `meeting_count_per_day` for the week-strip calendar dot indicators and filters by `selectedDate` for the meeting card list. Scheduled-at and duration metadata are stored under the `keys` / `values` parallel arrays (OBP meeting schema).

### Path Parameters

| Name   | Type   | Description                      |
|--------|--------|----------------------------------|
| bankId | String | OBP bank identifier (e.g. ke.equity.bank) |

### Response Fields

| Field       | Type           | Description                                                                     |
|-------------|----------------|---------------------------------------------------------------------------------|
| meeting_id  | String         | Unique meeting identifier                                                       |
| provider    | String         | Meeting provider name (e.g. "Zoom", "GoogleMeet", "InPerson", "Phone")         |
| provider_id | String         | Provider-specific meeting link or room ID                                       |
| purpose_id  | String         | Meeting purpose code (e.g. "loan-review", "account-opening", "mortgage-consultation") |
| bank_id     | String         | Bank identifier                                                                 |
| present     | Object         | Nested creator + invitees objects with contact details and status               |
| present.creator.name            | String | Officer's full name                                             |
| present.creator.email_address   | String | Officer's email                                                 |
| present.creator.mobile_phone    | String | Officer's phone                                                 |
| present.invitees[]              | List   | Invitee objects — each with contact_details + status            |
| present.invitees[].contact_details.name           | String | Customer full name                    |
| present.invitees[].contact_details.email_address  | String | Customer email                        |
| present.invitees[].contact_details.mobile_phone   | String | Customer phone                        |
| present.invitees[].status       | String | "confirmed" or "pending"                                        |
| keys        | List\<String\> | Metadata keys (e.g. "scheduled_at", "duration_minutes")                        |
| values      | List\<String\> | Metadata values (parallel to keys — e.g. "2026-05-28T10:00:00+03:00", "30")   |

### Demo Data

Sourced from `idea-layer/screens/meetings/demo-data.yaml`:

| meeting_id          | provider    | purpose_id               | creator.name      | invitee.name   | scheduled_at                  | duration_minutes | invitee.status |
|---------------------|-------------|--------------------------|-------------------|----------------|-------------------------------|------------------|----------------|
| mtg-001-ke-2026     | Zoom        | loan-review              | Amina Wanjiru     | James Otieno   | 2026-05-28T10:00:00+03:00     | 30               | confirmed      |
| mtg-002-ke-2026     | Zoom        | account-opening          | Brian Kamau       | Faith Njeri    | 2026-05-30T14:30:00+03:00     | 45               | pending        |
| mtg-003-ke-2026     | GoogleMeet  | mortgage-consultation    | Grace Muthoni     | Peter Ndegwa   | 2026-06-02T09:00:00+03:00     | 60               | confirmed      |

**UI mapping notes:**
- `meeting_card_1` (Account Opening Meeting, John Mwangi, 10:00 AM, Google Meet, 1 hr) → maps to `obp_get_meetings.meetings[0]`
- `meeting_card_2` (KYC Review, Sarah Odhiambo, 2:00 PM, Nairobi Branch, 30 min) → maps to `obp_get_meetings.meetings[1]`
- `meeting_card_3` (New Prospect Introductory Call, Peter Kamau, Tomorrow 11:00 AM) → maps to `obp_get_meetings.meetings[2]`
- `upcoming_section_header` derives count = 3 from `obp_get_meetings`
- `week_strip_calendar` derives `meeting_count_per_day` from `obp_get_meetings.meetings`

### Error Codes

| Code | Constant           | UI Handling                                                     |
|------|--------------------|-----------------------------------------------------------------|
| 400  | BAD_REQUEST        | Show error banner "Could not load schedule." + retry            |
| 401  | UNAUTHORIZED       | Navigate to login screen                                        |
| 404  | CUSTOMER_NOT_FOUND | Show error banner "Could not load schedule." + retry            |

---

## POST /obp/v3.1.0/banks/{bankId}/meetings

**Auth:** DirectLogin
**Tag:** Meetings
**Trigger:** `confirm_meeting(draft: MeetingDraft)` — officer taps "Confirm Meeting" in the create_meeting_sheet dialog; `create_meeting_sheet` shows loading_indicator state during submission.

Creates a new meeting. The OBP meetings body uses deeply-nested `creator.{name,email_address,mobile_phone}` and `invitees[].contact_details.{name,email_address,mobile_phone}` + `invitees[].status`. `MeetingDraft` in the ViewModel must map to this shape exactly before POST.

### Path Parameters

| Name   | Type   | Description               |
|--------|--------|---------------------------|
| bankId | String | OBP bank identifier       |

### Request Fields

| Field                                     | Type   | Required | Description                                                      |
|-------------------------------------------|--------|----------|------------------------------------------------------------------|
| creator.name                              | String | Yes      | Field officer's full name                                        |
| creator.email_address                     | String | Yes      | Field officer's email address                                    |
| creator.mobile_phone                      | String | Yes      | Field officer's mobile phone number                              |
| invitees[].contact_details.name           | String | Yes      | Customer's full name (from meeting_customer_autocomplete)        |
| invitees[].contact_details.email_address  | String | Yes      | Customer's email address                                         |
| invitees[].contact_details.mobile_phone   | String | Yes      | Customer's mobile phone number                                   |
| invitees[].status                         | String | Yes      | Invitation status — set to "invited" on creation                 |
| purpose_id                                | String | Yes      | Meeting purpose code from meeting_type_select mapping            |
| provider                                  | String | Yes      | Provider string from meeting_type_select (In-Person / Online Google Meet / Phone Call) |

### Request Body Example

```json
{
  "creator": {
    "name": "Amina Wanjiru",
    "email_address": "amina.wanjiru@equitybank.co.ke",
    "mobile_phone": "+254722334455"
  },
  "invitees": [
    {
      "contact_details": {
        "name": "John Mwangi",
        "email_address": "john.mwangi@example.com",
        "mobile_phone": "+254700112233"
      },
      "status": "invited"
    }
  ],
  "purpose_id": "account-opening",
  "provider": "GoogleMeet"
}
```

### Response Fields

| Field       | Type   | Description                                             |
|-------------|--------|---------------------------------------------------------|
| meeting_id  | String | Created meeting UUID                                    |
| provider    | String | Confirmed meeting provider                              |
| provider_id | String | Provider-specific ID / meeting link assigned by server  |
| purpose_id  | String | Confirmed purpose code                                  |
| bank_id     | String | Bank identifier                                         |

### Error Codes

| Code | Constant          | UI Handling                                                                        |
|------|-------------------|------------------------------------------------------------------------------------|
| 400  | VALIDATION_FAILED | Show banner "Could not schedule meeting. Check your connection and try again." + retry |
| 401  | UNAUTHORIZED      | Navigate to login screen                                                           |
| 404  | CUSTOMER_NOT_FOUND| Show banner "Could not schedule meeting." + retry                                  |

---

_Generated by /idea export | 2026-05-30_
