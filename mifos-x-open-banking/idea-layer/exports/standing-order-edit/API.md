# API Reference — Standing Order Edit

| Field    | Value                                   |
|----------|-----------------------------------------|
| Feature  | standing-order-edit                     |
| Base URL | https://apisandbox.openbankproject.com  |

---

## PUT /obp/v4.0.0/banks/{bank_id}/accounts/{account_id}/owner/standing-order/{standing_order_id}

**Auth:** DirectLogin (header: `DirectLogin token=<token>`)
**Tag:** Standing-Orders
**Trigger:** `saveStandingOrder()` — fires when user taps "Save Changes" and `validateForm()` passes all client-side checks

Updates the mutable fields (amount, frequency, start date, optional final date) of an existing standing order. Beneficiary name, IBAN, and currency are **immutable** after creation and must not be included in the PUT request body.

### Path Parameters

| Name              | Type   | Required | Demo Value               | Description                                                 |
|-------------------|--------|----------|--------------------------|-------------------------------------------------------------|
| bank_id           | String | Yes      | mifos.uk.gb.01           | OBP bank identifier for the source account                  |
| account_id        | String | Yes      | acc-alex-gbp-current-001 | Source account ID — from navigation param / ViewModel state |
| standing_order_id | String | Yes      | SO-2026-0001             | Standing order ID — from navigation param / ViewModel state |

### Request Body

```json
{
  "amount_value": "1200.00",
  "amount_currency": "GBP",
  "when": {
    "frequency": "MONTHLY",
    "start_date": "2026-01-01",
    "final_date": null
  }
}
```

### Request Fields

| Field           | Type    | Required | Enum / Format                    | Description                                               |
|-----------------|---------|----------|----------------------------------|-----------------------------------------------------------|
| amount_value    | String  | Yes      | Decimal string (e.g. "1200.00") | New payment amount; must be > 0                           |
| amount_currency | String  | Yes      | ISO 4217 (e.g. "GBP")          | Must match source account currency — fixed to GBP in app  |
| when.frequency  | String  | Yes      | DAILY / WEEKLY / MONTHLY / YEARLY| Payment recurrence cadence                               |
| when.start_date | String  | Yes      | YYYY-MM-DD (e.g. "2026-01-01") | First date the payment runs; must not be in the past      |
| when.final_date | String? | No       | YYYY-MM-DD or null              | Last date the payment runs; null = runs indefinitely      |

### Response Fields

| Field           | Type    | Description                                              |
|-----------------|---------|----------------------------------------------------------|
| id              | String  | Standing order identifier (SO-2026-0001)                 |
| bank_id         | String  | OBP bank identifier                                      |
| account_id      | String  | Source account ID                                        |
| counterparty.name | String| Beneficiary name (immutable — Landlord Holdings Ltd)    |
| amount_value    | String  | Updated payment amount                                   |
| amount_currency | String  | Currency code (GBP — unchanged by this PUT)             |
| when.frequency  | String  | Updated frequency                                        |
| when.start_date | String  | Updated start date                                       |
| when.final_date | String? | Updated final date, null = ongoing                       |
| active          | Boolean | Unchanged by PUT — reflects current activation status    |

### Demo Data

**Request (pre-filled defaults from form):**

| Field               | Value          |
|---------------------|----------------|
| amount_value        | "1200.00"      |
| amount_currency     | "GBP"          |
| when.frequency      | "MONTHLY"      |
| when.start_date     | "2026-01-01"   |
| when.final_date     | null           |

**Response (HTTP 200):**

| Field               | Value                      |
|---------------------|----------------------------|
| id                  | SO-2026-0001               |
| bank_id             | mifos.uk.gb.01             |
| account_id          | acc-alex-gbp-current-001   |
| counterparty.name   | Landlord Holdings Ltd      |
| amount_value        | 1200.00                    |
| amount_currency     | GBP                        |
| when.frequency      | MONTHLY                    |
| when.start_date     | 2026-01-01                 |
| when.final_date     | null                       |
| active              | true                       |

### Error Codes

| Code | OBP Message                      | UI Error Displayed                                                                     |
|------|----------------------------------|----------------------------------------------------------------------------------------|
| 400  | INVALID_STANDING_ORDER_VALUES    | soe_error_banner: "Couldn't save your changes. Check the amount and try again."       |
| 401  | USER_NOT_LOGGED_IN               | Navigate to login screen; session expired                                              |
| 403  | INSUFFICIENT_AUTHORISATION       | soe_error_banner: "Couldn't save your changes. Check the amount and try again."       |
| 404  | STANDING_ORDER_NOT_FOUND         | soe_error_banner: "Couldn't save your changes. Check the amount and try again."       |
| 409  | STANDING_ORDER_ALREADY_CANCELLED | soe_error_banner: "This standing order has been cancelled and can no longer be edited." |

### Success Flow

On HTTP 200 the ViewModel:
1. Sets `isSaving = false`, transitions `uiState` from Saving → Content
2. Emits `NavigateToDetail` event
3. UI pops back to standing-order-detail (back stack pop)
4. standing-order-detail re-fetches from the server and reflects the updated values

### Client-side Validation (before API call)

`validateForm()` runs on every `OnSave` event before the PUT is dispatched. Both checks must pass; if either fails the API call is not made and the error is surfaced as field-level ViewModel state.

| Field       | Rule                          | ViewModel Field  | Error Message Surfaced                              |
|-------------|-------------------------------|------------------|-----------------------------------------------------|
| amount      | Must be > BigDecimal.ZERO    | amountError      | "Enter an amount greater than £0.00."              |
| startDate   | Must be >= LocalDate.now()   | startDateError   | "Start date can't be in the past."                 |

Field errors surface inline below their respective input (M3 `supportingText` slot with error color #BA1A1A). The soe_error_banner is reserved for server-returned errors (non-2xx responses or network timeout).

---

_Generated by /idea export | 2026-05-30_
