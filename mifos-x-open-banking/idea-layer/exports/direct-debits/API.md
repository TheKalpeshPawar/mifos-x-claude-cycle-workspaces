# API Reference — Direct Debits

| Field    | Value                                       |
|----------|---------------------------------------------|
| Feature  | direct-debits                               |
| Base URL | https://apisandbox.openbankproject.com      |

---

## GET /obp/v4.0.0/banks/{bankId}/accounts/{accountId}/owner/direct-debits

**Auth:** DirectLogin
**Tag:** Direct-Debit
**Trigger:** `loadDashboardData()` on screen entry / `RetryLoad` event

Retrieves all direct debit mandates authorised on the specified account. The `DirectDebitsViewModel` maps the response list to `List<DirectDebit>`, derives `activeCount` (mandates where `active == true`), and renders mandate cards. The first call on screen entry sets `uiState` to `Loading`; on success it transitions to `Populated` (or `Empty` if the list is empty).

### Path Parameters

| Name      | Type   | Value               | Description                   |
|-----------|--------|---------------------|-------------------------------|
| bankId    | String | ke.equity.001       | Bank identifier               |
| accountId | String | acct-ke-001-savings | Account identifier            |

### Response Fields

| Field                          | Type              | Description                                              |
|--------------------------------|-------------------|----------------------------------------------------------|
| direct_debits                  | List\<DirectDebit\>| Array of mandate objects                                |
| direct_debits[].direct_debit_id| String            | Unique OBP mandate identifier                            |
| direct_debits[].bank_id        | String            | Bank identifier                                          |
| direct_debits[].account_id     | String            | Account identifier                                       |
| direct_debits[].counterparty_id| String            | Counterparty (payee) identifier                          |
| direct_debits[].amount_value   | String            | Mandate amount as a decimal string (e.g. "15.99")        |
| direct_debits[].amount_currency| String            | ISO 4217 currency code (e.g. "GBP", "KES")              |
| direct_debits[].start_date     | String            | Mandate start date (ISO 8601)                            |
| direct_debits[].end_date       | String            | Mandate end date / next collection date (ISO 8601)       |
| direct_debits[].active         | Boolean           | `true` = Active mandate; `false` = Cancelled             |
| direct_debits[].to             | DirectDebitCounterparty | Payee routing details                             |
| direct_debits[].to.name        | String            | Payee display name (e.g. "Netflix", "Spotify")           |
| direct_debits[].to.bank_routing| Object            | Payee bank routing (scheme + address)                    |
| direct_debits[].to.account_routing| Object         | Payee account routing (scheme + address)                 |

### Demo Data

| direct_debit_id        | to.name                        | amount_value | amount_currency | active | end_date   |
|------------------------|--------------------------------|--------------|-----------------|--------|------------|
| dd-ke-001-kplc         | Kenya Power & Lighting Co.     | 4500.00      | KES             | true   | 2026-12-31 |
| dd-ke-002-nairobi-water| Nairobi City Water & Sewerage Co. | 1800.00   | KES             | true   | 2027-01-31 |
| dd-ke-003-safaricom    | Safaricom PLC — Home Fibre     | 2500.00      | KES             | false  | 2026-06-30 |

> **Note:** UI exemplar content (Netflix £15.99, Spotify £10.99, PureGym £29.99) is used in `ui.yaml` for GBP-market wireframing. The `demo-data.yaml` above reflects the KES/Kenyan bank context for integration testing. Both sets exercise the same data path.

### Error Codes

| Code | Message                  | UI Handling                                              |
|------|--------------------------|----------------------------------------------------------|
| 401  | USER_NOT_LOGGED_IN       | Navigate to login screen; clear session                  |
| 403  | INSUFFICIENT_AUTHORISATION| Show error state: "You don't have permission to view this account" |
| 404  | BANK_ACCOUNT_NOT_FOUND   | Show error state with retry; log analytics event         |

---

## POST /obp/v4.0.0/banks/{bankId}/accounts/{accountId}/owner/direct-debit

**Auth:** DirectLogin
**Tag:** Direct-Debit
**Trigger:** "Set Up Direct Debit" FAB tap → mandate setup bottom sheet confirmation

Creates a new direct debit mandate for the account. Also used internally to process the cancel flow — the cancel action calls the OBP cancel endpoint via the `DirectDebitRepository.cancelMandate(mandateId)` method; upon success the screen reloads mandate list and decrements `activeCount`.

### Path Parameters

| Name      | Type   | Value               | Description        |
|-----------|--------|---------------------|--------------------|
| bankId    | String | ke.equity.001       | Bank identifier    |
| accountId | String | acct-ke-001-savings | Account identifier |

### Request Fields

| Field           | Type                    | Required | Description                                          |
|-----------------|-------------------------|----------|------------------------------------------------------|
| start_date      | String (ISO 8601)       | yes      | Mandate start date e.g. "2026-06-01"                 |
| end_date        | String (ISO 8601)       | yes      | Mandate end / final collection date e.g. "2027-05-31"|
| to              | DirectDebitCounterparty | yes      | Payee routing object                                 |
| to.name         | String                  | yes      | Payee display name                                   |
| to.bank_routing | Object (scheme+address) | yes      | Bank routing details                                 |
| to.account_routing| Object (scheme+address)| yes     | Account routing details                              |
| amount_value    | String                  | yes      | Amount as decimal string e.g. "3000.00"              |
| amount_currency | String (ISO 4217)       | yes      | Currency code e.g. "KES"                             |

### Response Fields

| Field           | Type    | Description                                       |
|-----------------|---------|---------------------------------------------------|
| direct_debit_id | String  | Newly created mandate OBP identifier              |
| bank_id         | String  | Bank identifier echoed                            |
| account_id      | String  | Account identifier echoed                         |
| counterparty_id | String  | OBP-resolved counterparty ID for payee            |
| amount_value    | String  | Confirmed mandate amount                          |
| amount_currency | String  | Confirmed currency                                |
| start_date      | String  | Mandate start date echoed                         |
| end_date        | String  | Mandate end date echoed                           |
| active          | Boolean | `true` — newly created mandates are active        |

### Demo Data (request template)

| Field           | Value                                        |
|-----------------|----------------------------------------------|
| start_date      | 2026-06-01                                   |
| end_date        | 2027-05-31                                   |
| amount_value    | 3000.00                                      |
| amount_currency | KES                                          |
| to.name         | NHIF — National Hospital Insurance Fund      |
| to.bank_routing | scheme: SORT, address: KCBL-005              |
| to.account_routing | scheme: ACCOUNT_NUMBER, address: 5500112233|

### Error Codes

| Code | Message                  | UI Handling                                              |
|------|--------------------------|----------------------------------------------------------|
| 400  | INVALID_BANK_ID          | Show inline validation: "Invalid bank ID. Contact support." |
| 401  | USER_NOT_LOGGED_IN       | Navigate to login; clear session                         |
| 403  | INSUFFICIENT_AUTHORISATION| Show error banner: "You don't have permission to set up direct debits" |
| 404  | BANK_ACCOUNT_NOT_FOUND   | Show error banner with retry                             |

---

_Generated by /idea export | 2026-05-30_
