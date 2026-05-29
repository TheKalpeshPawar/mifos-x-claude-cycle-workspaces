# API Reference — Customer Messages

| Field    | Value                                       |
|----------|---------------------------------------------|
| Feature  | customer-messages                           |
| Base URL | https://apisandbox.openbankproject.com      |

---

## GET /obp/v5.1.0/banks/{bankId}/customers/{customerId}/messages

**Auth:** DirectLogin
**Tag:** Customer-Messages
**Trigger:** `loadMessages()` on screen open / `RetryLoad` event

Fetches all message threads for the given customer. The ViewModel groups results into `threads: List<MessageThread>` and derives `unreadCount` from entries where `read_date` is null or absent. The three most recent threads are displayed on screen; all threads are searchable via `filteredThreads`.

### Path Parameters

| Name       | Type   | Description                                                     |
|------------|--------|-----------------------------------------------------------------|
| bankId     | String | Bank identifier, e.g. `gh.29.uk`                               |
| customerId | String | OBP customer identifier, resolved from active session context   |

### Response Fields

| Field              | Type   | Description                                                          |
|--------------------|--------|----------------------------------------------------------------------|
| id                 | String | Unique message identifier                                            |
| description        | String | Full message body text                                               |
| transport          | String | Delivery channel — `"sms"`, `"email"`, `"ftp"`, or `"post"`        |
| from_department    | String | Originating bank department (e.g. "Loans", "Compliance", "Cards")   |
| from_person        | String | Name of the staff member who sent the message                        |
| date               | String | ISO-8601 timestamp when the message was created                      |

### Demo Data

| id          | description (truncated)                                        | transport | from_department | from_person      | date                     |
|-------------|----------------------------------------------------------------|-----------|-----------------|------------------|--------------------------|
| msg-ke-001  | Your loan application #LN-2026-0341 has been approved…         | sms       | Loans           | Amina Odhiambo   | 2026-05-20T08:15:00Z     |
| msg-ke-002  | Your KYC documents have been verified successfully…            | email     | Compliance      | Brian Otieno     | 2026-05-18T14:30:00Z     |
| msg-ke-003  | Reminder: Your fixed deposit of KES 100,000 matures…          | sms       | Support         | Grace Mwangi     | 2026-05-15T10:00:00Z     |
| msg-ke-004  | Statement for April 2026 is now available. Total credits…      | email     | Support         | David Kamau      | 2026-05-01T06:00:00Z     |
| msg-ke-005  | Your Visa debit card ending 4821 has been temporarily blocked… | sms       | Cards           | Fatuma Hassan    | 2026-04-28T16:45:00Z     |
| msg-ke-006  | Overdraft facility of KES 50,000 has been approved…            | email     | Loans           | Peter Njoroge    | 2026-04-22T09:00:00Z     |

### ViewModel Mapping

| Response Field   | ViewModel Field              | Transformation                                          |
|------------------|------------------------------|---------------------------------------------------------|
| id               | MessageThread.id             | Direct                                                  |
| description      | MessageThread.previewText    | Truncated to first 60 chars for thread card display     |
| from_person      | MessageThread.senderName     | Initials derived for avatar (e.g. "Amina Odhiambo" → "AO") |
| from_department  | MessageThread.department     | Direct                                                  |
| transport        | MessageThread.transport      | Direct                                                  |
| date             | MessageThread.timestamp      | Formatted to relative string ("2 min ago", "1 hr ago", "Yesterday") |
| (absent)         | MessageThread.isUnread       | Derived — true when no `read_date` in response          |

### Error Codes

| Code | OBP Error           | UI Handling                                                     |
|------|---------------------|-----------------------------------------------------------------|
| 400  | BAD_REQUEST         | Show error banner with retry                                    |
| 401  | UNAUTHORIZED        | Navigate to login / refresh DirectLogin token                   |
| 404  | CUSTOMER_NOT_FOUND  | Show error banner — "Customer record not found", no retry       |
| 500  | (server error)      | Show error banner with retry                                    |

---

## POST /obp/v4.0.0/banks/{bankId}/customers/{customerId}/messages

**Auth:** DirectLogin
**Tag:** Customer-Messages
**Trigger:** `send_message` action on `send_message_button` tap inside `compose_sheet` dialog

Sends a new message from the field officer to the selected customer. On success, the compose dialog dismisses and the thread list refreshes. The `isSending` state flag activates a loading indicator on the send button while the request is in flight.

### Path Parameters

| Name       | Type   | Description                                                     |
|------------|--------|-----------------------------------------------------------------|
| bankId     | String | Bank identifier, e.g. `gh.29.uk`                               |
| customerId | String | OBP customer identifier for the selected recipient              |

### Request Body Fields

| Field           | Type   | Required | Notes                                                                  |
|-----------------|--------|----------|------------------------------------------------------------------------|
| message         | String | Yes      | Full message text from `compose_message_input`                         |
| from_department | String | Yes      | Populated from authenticated officer's department profile              |
| from_person     | String | Yes      | Populated from authenticated officer's display name                    |
| transport       | String | Yes      | Delivery channel — must be one of `"sms"`, `"email"`, `"ftp"`, `"post"` |

### Demo Request Template

```json
{
  "message": "Please note your account statement for the period ending May 2026 is now available. Log in to Online Banking to view and download your statement.",
  "from_department": "Support",
  "from_person": "Amina Odhiambo",
  "transport": "email"
}
```

### Response

On success (HTTP 201): OBP returns the created message object. The ViewModel dispatches `MessageSent` event, closes compose dialog (`isComposeOpen = false`, `composeDraft = null`), and calls `loadMessages()` to refresh the thread list.

### Error Codes

| Code | OBP Error            | UI Handling                                                            |
|------|----------------------|------------------------------------------------------------------------|
| 400  | BAD_REQUEST          | Show inline validation error on compose form; keep dialog open         |
| 401  | UNAUTHORIZED         | Navigate to login / refresh DirectLogin token                          |
| 404  | CUSTOMER_NOT_FOUND   | Show error banner in compose dialog — "Customer not found"             |
| 500  | (server error)       | Dispatch SEND_FAILED; show error banner in dialog with retry option     |

---

_Generated by /idea export | 2026-05-30_
