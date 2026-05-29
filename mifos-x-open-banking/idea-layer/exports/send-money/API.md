# API Reference — Send Money

| Field    | Value                                  |
|----------|----------------------------------------|
| Feature  | send-money                             |
| Base URL | https://apisandbox.openbankproject.com |

---

## GET /obp/v5.1.0/banks/{bankId}/accounts

**Auth:** DirectLogin
**Tag:** Accounts
**Trigger:** Screen entry — populate `from_account_selector`

### Path Parameters

| Name   | Type   | Value    |
|--------|--------|----------|
| bankId | String | gh.29.uk |

### Response Fields

| Field             | Type               | Description                                    |
|-------------------|--------------------|------------------------------------------------|
| accounts          | List\<Account\>    | Accounts for the authenticated user            |
| accounts[].id     | String             | Account identifier                             |
| accounts[].label  | String             | Display name e.g. "Primary Checking"           |
| accounts[].balance| Amount             | Contains `currency` (String) and `amount` (String) |
| accounts[].currency | String           | Currency code e.g. "GBP"                       |

**Pre-fill display:** "Primary Checking — £4,250.00 available"

### Error Codes

| Code | Message          |
|------|------------------|
| 400  | INVALID_BANK_ID  |
| 401  | USER_NOT_LOGGED_IN|
| 404  | BANK_NOT_FOUND   |

---

## GET /obp/v4.0.0/banks/{bankId}/accounts/{accountId}/{viewId}/counterparties

**Auth:** DirectLogin
**Tag:** Counterparties
**Trigger:** Screen entry — populate `beneficiary_search` and `recent_beneficiaries_row`

### Path Parameters

| Name      | Type   | Value            |
|-----------|--------|------------------|
| bankId    | String | gh.29.uk         |
| accountId | String | Primary account ID from accounts response |
| viewId    | String | owner            |

### Response Fields

| Field                                    | Type                    | Description                              |
|------------------------------------------|-------------------------|------------------------------------------|
| counterparties                           | List\<Counterparty\>    | Saved beneficiaries                      |
| counterparties[].id                      | String                  | Counterparty identifier                  |
| counterparties[].name                    | String                  | Beneficiary display name                 |
| counterparties[].other_bank_routing_address | String               | Beneficiary bank e.g. "Barclays UK"      |
| counterparties[].other_account_routing_address | String            | Beneficiary account number / IBAN        |

**Recent beneficiaries (sample):** John Smith (Barclays UK), Sarah Williams (HSBC UK)

### Error Codes

| Code | Message          |
|------|------------------|
| 400  | INVALID_BANK_ID  |
| 401  | USER_NOT_LOGGED_IN|

---

## POST /obp/v4.0.0/account/check/scheme/iban

**Auth:** DirectLogin
**Tag:** Account
**Trigger:** User manually enters an IBAN in `beneficiary_search` — validate before enabling Continue

### Request Fields

| Field   | Type   | Description                              |
|---------|--------|------------------------------------------|
| address | String | The IBAN to validate (field named "address" in OBP schema) |

### Response Fields

| Field    | Type    | Description                        |
|----------|---------|------------------------------------|
| is_valid | Boolean | `true` if IBAN checksum is valid   |

---

## GET /obp/v3.1.0/banks/{bankId}/accounts/{accountId}/owner/funds-available

**Auth:** DirectLogin
**Tag:** Account
**Trigger:** After Continue tap — verify sufficient funds before navigating to confirmation

### Path Parameters

| Name      | Type   | Value         |
|-----------|--------|---------------|
| bankId    | String | gh.29.uk      |
| accountId | String | selectedAccountId |

### Query Parameters

| Name     | Type   | Example | Description           |
|----------|--------|---------|-----------------------|
| amount   | String | "100.00"| Payment amount string |
| currency | String | "GBP"   | Payment currency      |

### Response Fields

| Field  | Type   | Description                                     |
|--------|--------|-------------------------------------------------|
| answer | String | `"yes"` if funds available, `"no"` if insufficient |

---

## POST /obp/v5.1.0/banks/{bankId}/accounts/{accountId}/owner/transaction-request-types/SEPA/transaction-requests

**Auth:** DirectLogin
**Tag:** TransactionRequests
**Trigger:** User confirms payment on `send-money-confirm` screen — not sent directly from this screen

### Path Parameters

| Name      | Type   | Value                         |
|-----------|--------|-------------------------------|
| bankId    | String | gh.29.uk                      |
| accountId | String | selectedAccountId             |

### Request Body (SEPA)

```json
{
  "to": {
    "iban": "<beneficiary IBAN>"
  },
  "value": {
    "currency": "GBP",
    "amount": "100.00"
  },
  "description": "Payment for invoice #1234"
}
```

### Response Fields

| Field      | Type      | Description                                |
|------------|-----------|--------------------------------------------|
| id         | String    | Transaction request ID                     |
| type       | String    | "SEPA"                                     |
| status     | String    | "INITIATED" or "COMPLETED"                 |
| start_date | DateTime  | ISO-8601 request creation timestamp        |
| end_date   | DateTime  | ISO-8601 expected completion timestamp     |
| challenge  | Challenge | SCA challenge (if applicable)              |
| charge     | Charge    | Applied fee details                        |

### Error Codes

| Code | Message                   | UI Behaviour                               |
|------|---------------------------|--------------------------------------------|
| 400  | INVALID_JSON_FORMAT       | Error banner with field guidance           |
| 403  | INSUFFICIENT_AUTHORISATION| Navigate to login                          |
| 404  | BANK_ACCOUNT_NOT_FOUND    | Error banner on confirmation screen        |
| 422  | INSUFFICIENT_FUNDS        | Error: "Insufficient funds in account."    |

---

_Generated by /idea export | 2026-05-29_
