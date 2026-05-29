# API Reference — Confirm Payment

| Field    | Value                                      |
|----------|--------------------------------------------|
| Feature  | send-money-confirm                         |
| Base URL | https://apisandbox.openbankproject.com     |

---

## POST /obp/v5.1.0/banks/{bankId}/accounts/{accountId}/owner/transaction-request-types/SEPA/transaction-requests

**Auth:** DirectLogin (header: `DirectLogin token=<token>`)
**Tag:** TransactionRequests
**Trigger:** `ConfirmClicked` event — fires when user taps "Confirm & Send" in `review` or `content` state

Submits a SEPA transaction request against the user's source account. On HTTP 200/201 the ViewModel emits `PaymentSucceeded` and navigates to `home`. On non-2xx response or network failure the ViewModel emits `PaymentFailed` and shows an inline error banner.

### Path Parameters

| Name      | Type   | Description                                              |
|-----------|--------|----------------------------------------------------------|
| bankId    | String | OBP bank identifier, e.g. `gh.29.uk`                    |
| accountId | String | Source account ID carried forward from send-money state  |

### Request Body

```json
{
  "value": {
    "currency": "GBP",
    "amount": "500.00"
  },
  "to": {
    "iban": "GB29NWBK60161331926819"
  },
  "description": "Rent August 2026",
  "charge_policy": "SHARED"
}
```

### Request Fields

| Field          | Type   | Required | Description                                                       |
|----------------|--------|----------|-------------------------------------------------------------------|
| value.currency | String | Yes      | ISO 4217 currency code — from `currency` state field (default GBP)|
| value.amount   | String | Yes      | Decimal string, e.g. "500.00" — from `amount` state field         |
| to.iban        | String | Yes      | Beneficiary IBAN — from `iban` state field (spaces stripped)      |
| description    | String | Yes      | Payment reference string (≤35 chars) — from `reference` state field|
| charge_policy  | String | No       | "SHARED" (default), "SENDER", or "RECEIVER"                       |

### Response Fields

| Field                  | Type           | Description                                                    |
|------------------------|----------------|----------------------------------------------------------------|
| id                     | String         | Transaction request identifier                                 |
| type                   | String         | "SEPA"                                                         |
| status                 | String         | INITIATED / COMPLETED / FAILED                                 |
| start_date             | DateTime       | ISO-8601 submission timestamp                                  |
| charge                 | Object         | Fee breakdown object                                           |
| charge.summary         | String         | Human-readable fee description, e.g. "RTGS transfer fee"      |
| charge.value.amount    | String         | Fee amount decimal string, e.g. "0.00"                        |
| charge.value.currency  | String         | Fee currency code, e.g. "GBP"                                 |
| challenge              | Challenge?     | SCA challenge object; null if no strong authentication required|
| transaction_ids        | List\<String\> | Created transaction IDs — populated on COMPLETED status        |

### Demo Data

| Field                   | Demo Value                        |
|-------------------------|-----------------------------------|
| id                      | txreq-ke-20260523-001             |
| type                    | SEPA                              |
| status                  | COMPLETED                         |
| start_date              | 2026-05-23T14:05:00+03:00         |
| charge.summary          | RTGS transfer fee                 |
| charge.value.amount     | 0.00                              |
| charge.value.currency   | GBP                               |
| challenge.id            | chal-ke-001                       |
| challenge.allowed_attempts | 3                              |
| challenge.challenge_type| OTP                               |
| transaction_ids[0]      | txn-ke-20260523-88201             |

### Error Codes

| Code | OBP Message              | UI Error Displayed                                                  |
|------|--------------------------|---------------------------------------------------------------------|
| 400  | INVALID_JSON_FORMAT      | Inline validation banner — check field mapping                      |
| 403  | INSUFFICIENT_AUTHORISATION| "Payment could not be processed. Please try again."                |
| 404  | BANK_ACCOUNT_NOT_FOUND   | "Payment could not be processed. Please try again."                |
| 422  | INSUFFICIENT_FUNDS       | "Insufficient funds in your account."                              |
| 423  | DAILY_LIMIT_EXCEEDED     | "This payment exceeds your daily transfer limit."                  |

### Success Flow

On HTTP 200/201 the ViewModel emits `PaymentSucceeded`. The UI:
1. Clears the submit spinner on `confirm_send_button`
2. Shows snackbar: "Payment of £500.00 sent to John Smith"
3. Navigates to `home` (replaces back stack — user cannot navigate back to confirm screen)

### Error Flow

On non-2xx or network failure the ViewModel emits `PaymentFailed`. The UI:
1. Re-enables `confirm_send_button`
2. Shows inline error banner matching the OBP error code → ViewModel error message mapping
3. User may retry or tap "Edit Payment" to return to send-money and correct beneficiary details

---

_Generated by /idea export | 2026-05-30_
