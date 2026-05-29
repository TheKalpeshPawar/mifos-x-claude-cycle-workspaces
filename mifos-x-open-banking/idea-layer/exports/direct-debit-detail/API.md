# API Reference — Direct Debit Detail

| Field    | Value                                     |
|----------|-------------------------------------------|
| Feature  | direct-debit-detail                       |
| Base URL | https://apisandbox.openbankproject.com    |

---

## GET /obp/v5.0.0/banks/{bankId}/accounts/{accountId}/direct-debit/{directDebitId}

**Auth:** DirectLogin
**Tag:** DirectDebits
**Trigger:** `loadMandate(mandateId)` on screen entry and `OnRetryClicked` event

### Path Parameters

| Name          | Type   | Value                         |
|---------------|--------|-------------------------------|
| bankId        | String | gh.29.uk                      |
| accountId     | String | (from navigation arguments — linked account ID) |
| directDebitId | String | (from navigation arguments — mandate ID)        |

### Response Fields

| Field              | Type    | Description                                                        |
|--------------------|---------|-------------------------------------------------------------------|
| direct_debit_id    | String  | Unique mandate identifier — maps to mandateReference              |
| bank_id            | String  | Bank identifier                                                   |
| account_id         | String  | Linked account identifier — maps to linkedAccountMasked           |
| date_signed        | String  | ISO-8601 date the mandate was authorised — maps to mandateStartDate |
| date_starts        | String  | ISO-8601 date mandate becomes active                              |
| date_expires       | String? | ISO-8601 expiry date; null if perpetual                           |
| date_cancelled     | String? | ISO-8601 cancellation date; null if active                        |
| date_updated       | String  | ISO-8601 last update timestamp                                    |
| date_of_next_payment | String| ISO-8601 next scheduled collection — maps to nextPaymentDate      |
| period             | String  | Frequency code: "MONTHLY", "WEEKLY", "QUARTERLY", "ANNUAL"       |
| amount             | Object  | Contains `value` (String e.g. "15.99") + `currency` (e.g. "GBP") |
| amount.value       | String  | Mandate amount — maps to mandateAmount display                    |
| amount.currency    | String  | Currency code — prepended to formatted amount                     |
| virtual_account    | Object  | Merchant virtual account reference                                |

### Derived Fields (ViewModel)

| ViewModel Field        | Derived From                                      |
|------------------------|---------------------------------------------------|
| merchantName           | virtual_account.label or mandate counterparty name|
| merchantLogoUrl        | domain-based favicon lookup from merchant name    |
| mandateStatus          | Derived: null date_cancelled + not expired = "Active"; date_cancelled set = "Cancelled" |
| mandateFrequency       | period → formatted label ("Monthly" etc.)         |
| linkedAccountMasked    | account_id last 4 chars prefixed with "****"      |

### Sample Response

```json
{
  "direct_debit_id": "MDT-2024-00947",
  "bank_id": "gh.29.uk",
  "account_id": "acc-4521",
  "date_signed": "2024-01-12",
  "date_starts": "2024-01-15",
  "date_expires": null,
  "date_cancelled": null,
  "date_updated": "2026-05-01T00:00:00Z",
  "date_of_next_payment": "2026-06-15",
  "period": "MONTHLY",
  "amount": { "value": "15.99", "currency": "GBP" },
  "virtual_account": { "label": "Netflix Entertainment" }
}
```

### Error Codes

| Code | Message                                             |
|------|-----------------------------------------------------|
| 403  | INSUFFICIENT_PERMISSIONS — user lacks mandate view  |
| 404  | MANDATE_NOT_FOUND — directDebitId does not exist    |
| 500  | OBP server error                                    |

---

## DELETE /obp/v5.0.0/banks/{bankId}/accounts/{accountId}/direct-debit/{directDebitId}

**Auth:** DirectLogin
**Tag:** DirectDebits
**Trigger:** `onCancelClicked()` after user confirms the cancellation confirmation dialog

### Path Parameters

| Name          | Type   | Value                        |
|---------------|--------|------------------------------|
| bankId        | String | gh.29.uk                     |
| accountId     | String | (from screen state)          |
| directDebitId | String | (from screen state mandateId)|

### Response Fields

| Field   | Type    | Description                                    |
|---------|---------|------------------------------------------------|
| success | Boolean | `true` on successful cancellation              |

### Error Codes

| Code | Message                                                       |
|------|---------------------------------------------------------------|
| 403  | INSUFFICIENT_PERMISSIONS — user cannot cancel this mandate    |
| 404  | MANDATE_NOT_FOUND                                             |
| 409  | MANDATE_ALREADY_CANCELLED — already in cancelled state        |
| 500  | OBP server error                                              |

---

_Generated by /idea export | 2026-05-29_
