# API Reference — Standing Order Detail

| Field    | Value                                      |
|----------|--------------------------------------------|
| Feature  | standing-order-detail                      |
| Base URL | https://apisandbox.openbankproject.com     |

---

## GET /v4.0.0/banks/{bank_id}/accounts/{account_id}/standing-orders/{standing_order_id}

**Auth:** DirectLogin
**Tag:** Standing-Orders
**Trigger:** `loadDetail(standingOrderId)` on screen entry and `RetryLoad` event

### Path Parameters

| Name              | Type   | Description                                             |
|-------------------|--------|---------------------------------------------------------|
| bank_id           | String | OBP bank identifier (e.g., `rbs`)                      |
| account_id        | String | Source account ID from navigation params                |
| standing_order_id | String | Standing order ID from navigation params                |

### Response Fields

| Field              | Type                       | Description                              |
|--------------------|----------------------------|------------------------------------------|
| id                 | String                     | Standing order identifier                |
| bank_id            | String                     | Bank identifier                          |
| account_id         | String                     | Source account identifier                |
| beneficiary_name   | String                     | Recipient display name                   |
| beneficiary_iban   | String                     | Recipient IBAN                           |
| beneficiary_bank   | String                     | Recipient bank name                      |
| amount_value       | String                     | Payment amount (e.g., "1200.00")         |
| amount_currency    | String                     | ISO 4217 currency code (e.g., "GBP")    |
| frequency          | String                     | DAILY / WEEKLY / MONTHLY / YEARLY        |
| start_date         | String                     | ISO-8601 date string                     |
| next_payment_date  | String                     | ISO-8601 next scheduled date             |
| final_date         | String?                    | ISO-8601 final date; null = Ongoing      |
| status             | String                     | ACTIVE / PAUSED / CANCELLED              |
| execution_history  | List\<StandingOrderExecution\> | Last 5 execution entries              |

### Error Codes

| Code | OBP Message               | UI Response                              |
|------|---------------------------|------------------------------------------|
| 401  | USER_NOT_LOGGED_IN        | Navigate to login                        |
| 403  | INSUFFICIENT_AUTHORISATION| Error state — "not found" message        |
| 404  | STANDING_ORDER_NOT_FOUND  | Error state — "Standing Order Not Found" |

---

## POST /v4.0.0/banks/{bank_id}/accounts/{account_id}/standing-orders/{standing_order_id}/pause

**Auth:** DirectLogin
**Tag:** Standing-Orders
**Trigger:** `PauseClicked` event

Idempotent. Returns the updated standing order with `status: PAUSED`.

### Error Codes

| Code | OBP Message                     | UI Response                                        |
|------|----------------------------------|----------------------------------------------------|
| 401  | USER_NOT_LOGGED_IN              | Navigate to login                                  |
| 404  | STANDING_ORDER_NOT_FOUND        | Snackbar: "Could not pause. Order not found."      |
| 409  | STANDING_ORDER_ALREADY_PAUSED   | Silently reload — label already shows "Resume"     |

---

## POST /v4.0.0/banks/{bank_id}/accounts/{account_id}/standing-orders/{standing_order_id}/resume

**Auth:** DirectLogin
**Tag:** Standing-Orders
**Trigger:** `ResumeClicked` event

Idempotent. Returns updated standing order with `status: ACTIVE`. Button label toggles based on current `status` field.

### Error Codes

| Code | OBP Message                   | UI Response                                |
|------|--------------------------------|--------------------------------------------|
| 401  | USER_NOT_LOGGED_IN            | Navigate to login                          |
| 404  | STANDING_ORDER_NOT_FOUND      | Snackbar error                             |
| 409  | STANDING_ORDER_NOT_PAUSED     | Silently reload                            |

---

## DELETE /v4.0.0/banks/{bank_id}/accounts/{account_id}/standing-orders/{standing_order_id}

**Auth:** DirectLogin
**Tag:** Standing-Orders
**Trigger:** `DeleteConfirmed` event (after user confirms in sod_delete_dialog)

Soft-deletes the standing order. No further payments will be initiated. On 200 the app navigates back to the standing-orders list.

### Error Codes

| Code | OBP Message             | UI Response                                         |
|------|-------------------------|-----------------------------------------------------|
| 401  | USER_NOT_LOGGED_IN      | Navigate to login                                   |
| 404  | STANDING_ORDER_NOT_FOUND| Snackbar: "Could not cancel. Order not found."      |

---

_Generated by /idea export | 2026-05-29_
