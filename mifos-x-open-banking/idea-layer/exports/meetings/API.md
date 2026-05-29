# API Reference — Meetings

| Field    | Value                                            |
|----------|--------------------------------------------------|
| Feature  | meetings                                         |
| Base URL | https://apisandbox.openbankproject.com           |
| Auth     | DirectLogin — `DirectLogin token="<token>"` header |

---

## GET /obp/v3.1.0/banks/{bankId}/meetings

**Auth:** DirectLogin
**Tag:** Meetings
**Trigger:** `loadMeetings()` on screen entry; re-called on `DaySelected` event (client-side filter by `selectedDate`)

### Path Parameters

| Name   | Type   | Description         |
|--------|--------|---------------------|
| bankId | String | OBP bank identifier |

### Response Fields

| Field      | Type   | Description                                                      |
|------------|--------|------------------------------------------------------------------|
| meeting_id | String | Unique meeting identifier                                        |
| provider   | String | Meeting provider (e.g. "Google Meet", "In-Person", "Phone")      |
| provider_id| String | Provider-specific meeting ID (e.g. Google Meet link ID)          |
| purpose_id | String | Meeting purpose code (e.g. "account_opening", "kyc_review")     |
| bank_id    | String | Bank identifier                                                  |
| present    | Object | `present.staff_user_id` + `present.customer_user_id`            |
| keys       | Map    | Meeting metadata keys                                            |
| values     | Map    | Meeting metadata values                                          |

### Sample Response (demo data)

```json
[
  {
    "meeting_id": "MTG-2026-001",
    "provider": "Google Meet",
    "provider_id": "abc-defg-hij",
    "purpose_id": "account_opening",
    "bank_id": "gh.29.uk",
    "present": { "staff_user_id": "officer-001", "customer_user_id": "cust-jmwangi" }
  }
]
```

### Error Codes

| Code | Error              |
|------|--------------------|
| 400  | BAD_REQUEST        |
| 401  | UNAUTHORIZED       |
| 404  | CUSTOMER_NOT_FOUND |

---

## POST /obp/v3.1.0/banks/{bankId}/meetings

**Auth:** DirectLogin
**Tag:** Meetings
**Trigger:** `confirm_meeting(draft: MeetingDraft)` — officer taps "Confirm Meeting" in the schedule dialog

Note: The OBP meetings endpoint uses a deeply nested body structure. `MeetingDraft` must be mapped to this shape exactly.

### Path Parameters

| Name   | Type   | Description         |
|--------|--------|---------------------|
| bankId | String | OBP bank identifier |

### Request Fields

| Field                                   | Type   | Required | Description                             |
|-----------------------------------------|--------|----------|-----------------------------------------|
| creator.name                            | String | Yes      | Officer's full name                     |
| creator.email_address                   | String | Yes      | Officer's email                         |
| creator.mobile_phone                    | String | Yes      | Officer's phone number                  |
| invitees[].contact_details.name         | String | Yes      | Customer's full name                    |
| invitees[].contact_details.email_address| String | Yes      | Customer's email                        |
| invitees[].contact_details.mobile_phone | String | Yes      | Customer's phone                        |
| invitees[].status                       | String | Yes      | Invitation status (e.g. "invited")      |
| purpose_id                              | String | Yes      | Meeting purpose code                    |
| provider                                | String | Yes      | Meeting type/provider                   |

### Request Body Example

```json
{
  "creator": {
    "name": "Field Officer Njoroge",
    "email_address": "njoroge@mifos.org",
    "mobile_phone": "+254700000001"
  },
  "invitees": [
    {
      "contact_details": {
        "name": "John Mwangi",
        "email_address": "john.mwangi@example.com",
        "mobile_phone": "+254700000100"
      },
      "status": "invited"
    }
  ],
  "purpose_id": "account_opening",
  "provider": "Google Meet"
}
```

### Response Fields

| Field      | Type   | Description                           |
|------------|--------|---------------------------------------|
| meeting_id | String | Created meeting UUID                  |
| provider   | String | Confirmed meeting provider            |
| provider_id| String | Provider-specific ID (Google Meet link)|
| purpose_id | String | Confirmed purpose code                |
| bank_id    | String | Bank identifier                       |

### Error Codes

| Code | Error                                              |
|------|----------------------------------------------------|
| 400  | VALIDATION_FAILED — missing required nested fields |
| 401  | UNAUTHORIZED                                       |
| 404  | CUSTOMER_NOT_FOUND                                 |

---

_Generated by /idea export | 2026-05-29_
