# API Reference — Direct Debits

| Field    | Value                                       |
|----------|---------------------------------------------|
| Feature  | direct-debits                               |
| Base URL | https://apisandbox.openbankproject.com      |

---

## GET /obp/v4.0.0/banks/{bankId}/accounts/{accountId}/owner/direct-debits

**Auth:** DirectLogin
**Tag:** Direct-Debit
**Trigger:** `loadDirectDebits()` on screen open / `RetryLoad` event / post-cancel refresh

### Path Parameters

| Name       | Type   | Value         | Description                         |
|------------|--------|---------------|-------------------------------------|
| bankId     | String | gh.29.uk      | Bank identifier                     |
| accountId  | String | (from session)| Primary account ID from AccountRepository |

### Response Fields

| Field                            | Type               | Description                                             |
|----------------------------------|--------------------|---------------------------------------------------------|
| direct_debits                    | List\<DirectDebit\>| Array of mandate objects                                |
| direct_debits[].direct_debit_id  | String             | Unique mandate identifier (internal)                    |
| direct_debits[].bank_id          | String             | Bank identifier                                         |
| direct_debits[].account_id       | String             | Account identifier the mandate applies to               |
| direct_debits[].counterparty_id  | String             | OBP counterparty ID for the merchant                    |
| direct_debits[].amount_value     | String             | Amount collected per period e.g. "15.99"                |
| direct_debits[].amount_currency  | String             | ISO currency code e.g. "GBP"                            |
| direct_debits[].start_date       | String             | ISO-8601 mandate start date                             |
| direct_debits[].end_date         | String             | ISO-8601 mandate end / next-collection date             |
| direct_debits[].active           | Boolean            | true = Active, false = Cancelled                        |

### Demo Data Mapping

| Mandate    | amount_value | amount_currency | active | Mandate Reference  |
|------------|--------------|-----------------|--------|--------------------|
| Netflix    | 15.99        | GBP             | true   | DD-NF-20240301     |
| Spotify    | 10.99        | GBP             | true   | DD-SP-20231115     |
| PureGym    | 29.99        | GBP             | false  | DD-GYM-20220601    |

### Error Codes

| Code | OBP Message              | UI Handling                                      |
|------|--------------------------|--------------------------------------------------|
| 401  | USER_NOT_LOGGED_IN       | Navigate to login                                |
| 403  | INSUFFICIENT_AUTHORISATION | Show error state, do not retry automatically   |
| 404  | BANK_ACCOUNT_NOT_FOUND   | Show error state with retry button               |
| 500  | Server error             | Show error state with retry button               |

---

## POST /obp/v4.0.0/banks/{bankId}/accounts/{accountId}/owner/direct-debit

**Auth:** DirectLogin
**Tag:** Direct-Debit
**Trigger:** User completes new mandate setup via FAB bottom sheet

### Path Parameters

| Name      | Type   | Value         |
|-----------|--------|---------------|
| bankId    | String | gh.29.uk      |
| accountId | String | (from session)|

### Request Body

| Field             | Type                    | Required | Description                                     |
|-------------------|-------------------------|----------|-------------------------------------------------|
| start_date        | String                  | yes      | ISO-8601 mandate start date                     |
| end_date          | String                  | yes      | ISO-8601 first collection / end date            |
| to                | DirectDebitCounterparty | yes      | Counterparty object identifying the merchant    |
| amount_value      | String                  | yes      | Amount per period e.g. "15.99"                  |
| amount_currency   | String                  | yes      | ISO currency code e.g. "GBP"                    |

### Response Fields

| Field             | Type    | Description                              |
|-------------------|---------|------------------------------------------|
| direct_debit_id   | String  | Generated mandate identifier             |
| bank_id           | String  | Bank identifier                          |
| account_id        | String  | Account identifier                       |
| counterparty_id   | String  | Merchant counterparty reference          |
| amount_value      | String  | Confirmed amount value                   |
| amount_currency   | String  | Confirmed currency                       |
| start_date        | String  | Confirmed start date                     |
| end_date          | String  | Confirmed end / next collection date     |
| active            | Boolean | true on successful creation              |

### Error Codes

| Code | OBP Message              | UI Handling                         |
|------|--------------------------|-------------------------------------|
| 400  | INVALID_BANK_ID          | Show inline validation error        |
| 401  | USER_NOT_LOGGED_IN       | Navigate to login                   |
| 403  | INSUFFICIENT_AUTHORISATION | Show error banner, allow retry     |
| 404  | BANK_ACCOUNT_NOT_FOUND   | Show error banner                   |

---

_Generated by /idea export | 2026-05-29_
