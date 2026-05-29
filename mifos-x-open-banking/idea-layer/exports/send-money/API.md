# API Reference — Send Money

| Field    | Value                                       |
|----------|---------------------------------------------|
| Feature  | send-money                                  |
| Base URL | https://apisandbox.openbankproject.com      |

---

## GET /obp/v5.1.0/banks/{bankId}/accounts

**Auth:** DirectLogin
**Tag:** Accounts
**Trigger:** `loadSenderAccounts()` on screen entry — populates `from_account_selector` dropdown

Fetches all accounts for the authenticated user at the given bank. The ViewModel maps each entry to a selectable `AccountOption` used in `from_account_selector`. The first account in the response pre-fills the selector on load.

### Path Parameters

| Name   | Type   | Example         | Description         |
|--------|--------|-----------------|---------------------|
| bankId | String | ke.equity.bank  | Bank identifier     |

### Response Fields

| Field                       | Type           | Description                                          |
|-----------------------------|----------------|------------------------------------------------------|
| accounts                    | List\<Object\> | Array of account objects                             |
| accounts[].id               | String         | Unique account identifier                            |
| accounts[].label            | String         | Display label including account type and masked number |
| accounts[].balance          | Object         | Balance wrapper                                      |
| accounts[].balance.amount   | String         | Balance value as decimal string                      |
| accounts[].balance.currency | String         | ISO 4217 currency code                               |
| accounts[].currency         | String         | Account currency (same as balance.currency)          |

### Demo Data

| id                  | label                            | balance.amount | balance.currency |
|---------------------|----------------------------------|----------------|------------------|
| acc-equity-ke-001   | Equity Jijenge Savings — *4521   | 87430.50       | KES              |
| acc-equity-ke-002   | Equity Current — *7803           | 23150.00       | KES              |

### Error Codes

| Code | Message             | UI Handling                                      |
|------|---------------------|--------------------------------------------------|
| 400  | INVALID_BANK_ID     | Show error state, prompt user to re-authenticate |
| 401  | USER_NOT_LOGGED_IN  | Navigate to login screen                         |
| 404  | BANK_NOT_FOUND      | Show error state with retry                      |

---

## GET /obp/v4.0.0/banks/{bankId}/accounts/{accountId}/{viewId}/counterparties

**Auth:** DirectLogin
**Tag:** Counterparties
**Trigger:** `loadBeneficiaries()` — populates `beneficiary_search` results and `recent_beneficiaries_row` chips

Fetches all saved counterparties (beneficiaries) for the selected source account. The first two counterparties in the response are rendered as quick-select chips in `recent_beneficiaries_row`. All counterparties populate the `beneficiary_search` results list.

### Path Parameters

| Name      | Type   | Example           | Description                                   |
|-----------|--------|-------------------|-----------------------------------------------|
| bankId    | String | ke.equity.bank    | Bank identifier                               |
| accountId | String | acc-equity-ke-001 | Source account identifier                     |
| viewId    | String | owner             | Account view — always "owner" for this feature |

### Response Fields

| Field                                          | Type           | Description                              |
|------------------------------------------------|----------------|------------------------------------------|
| counterparties                                 | List\<Object\> | Array of counterparty objects            |
| counterparties[].id                            | String         | Unique counterparty identifier           |
| counterparties[].name                          | String         | Beneficiary display name                 |
| counterparties[].other_bank_routing_address    | String         | Bank routing address (e.g. ke.kcb.bank)  |
| counterparties[].other_account_routing_address | String         | Beneficiary account number / IBAN        |

### Demo Data

| id         | name              | other_bank_routing_address | other_account_routing_address  |
|------------|-------------------|----------------------------|-------------------------------|
| cp-001-ke  | Wycliffe Ochieng  | ke.kcb.bank                | KE61KCBA00001234567890        |
| cp-002-ke  | Naomi Gitau       | ke.cooperative.bank        | KE61COOP00009876543210        |
| cp-003-ke  | Salim Abdalla     | ke.absa.bank               | KE61ABSA00001122334455        |
| cp-004-ke  | Margaret Wairimu  | ke.equity.bank             | KE61EQBA00006677889900        |

### Error Codes

| Code | Message            | UI Handling                          |
|------|--------------------|--------------------------------------|
| 400  | INVALID_BANK_ID    | Show error banner, retain form state |
| 401  | USER_NOT_LOGGED_IN | Navigate to login screen             |

---

## POST /obp/v4.0.0/account/check/scheme/iban

**Auth:** DirectLogin
**Tag:** Account
**Trigger:** `validateIban()` — called when user manually types an IBAN-format string in `beneficiary_search` before form submission

Validates that a typed IBAN is well-formed and recognized by the OBP sandbox. Note: the request body field is named `address`, not `iban`.

### Request Body

| Field   | Type   | Required | Description                                                         |
|---------|--------|----------|---------------------------------------------------------------------|
| address | String | Yes      | The IBAN string to validate — field name is "address" not "iban"   |

### Response Fields

| Field    | Type    | Description                                   |
|----------|---------|-----------------------------------------------|
| is_valid | Boolean | true if IBAN is structurally valid and known  |

### Demo Data

| address                   | is_valid |
|---------------------------|----------|
| KE61KCBA00001234567890    | true     |
| INVALIDIBAN               | false    |

### Error Codes

| Code | Message            | UI Handling                                   |
|------|--------------------|-----------------------------------------------|
| 400  | INVALID_JSON_FORMAT| Show inline error on beneficiary_search field |
| 401  | USER_NOT_LOGGED_IN | Navigate to login screen                      |

---

## GET /obp/v3.1.0/banks/{bankId}/accounts/{accountId}/owner/funds-available

**Auth:** DirectLogin
**Tag:** Account
**Trigger:** `checkFundsAvailable()` — called after amount is entered and before enabling the Continue button; also called during final validation on Continue tap

Checks whether the selected source account has sufficient funds to cover the entered amount in the specified currency. Returns a plain "yes" or "no" answer string.

### Path Parameters

| Name      | Type   | Example           | Description               |
|-----------|--------|-------------------|---------------------------|
| bankId    | String | ke.equity.bank    | Bank identifier           |
| accountId | String | acc-equity-ke-001 | Source account identifier |

### Query Parameters

| Name     | Type   | Example  | Description                      |
|----------|--------|----------|----------------------------------|
| amount   | String | 5000.00  | Amount to check (decimal string) |
| currency | String | KES      | ISO 4217 currency code           |

### Response Fields

| Field  | Type   | Description                               |
|--------|--------|-------------------------------------------|
| answer | String | "yes" if funds available, "no" otherwise  |

### Demo Data

| amount   | currency | answer |
|----------|----------|--------|
| 5000.00  | KES      | yes    |
| 99999.00 | KES      | no     |

### Error Codes

| Code | Message                | UI Handling                                       |
|------|------------------------|---------------------------------------------------|
| 400  | INVALID_BANK_ID        | Show error banner                                 |
| 401  | USER_NOT_LOGGED_IN     | Navigate to login screen                          |
| 404  | BANK_ACCOUNT_NOT_FOUND | Show error state, prompt account re-selection     |

---

## POST /obp/v5.1.0/banks/{bankId}/accounts/{accountId}/owner/transaction-request-types/SEPA/transaction-requests

**Auth:** DirectLogin
**Tag:** TransactionRequests
**Trigger:** `initiateSepaPayment()` — called from `send-money-confirm` screen after user confirms; this screen (send-money) collects and validates all inputs but the actual POST is dispatched by the confirmation step

Initiates a SEPA credit transfer transaction request. Returns a transaction request object including a challenge if SCA (Strong Customer Authentication) is required. The `charge` field shows the actual fee applied (KES 50.00 per OBP sandbox configuration).

### Path Parameters

| Name      | Type   | Example           | Description              |
|-----------|--------|-------------------|--------------------------|
| bankId    | String | ke.equity.bank    | Source bank identifier   |
| accountId | String | acc-equity-ke-001 | Source account identifier|

### Request Body

| Field            | Type   | Required | Description                                  |
|------------------|--------|----------|----------------------------------------------|
| to.iban          | String | Yes      | Beneficiary IBAN                             |
| value.currency   | String | Yes      | ISO 4217 code (e.g. "KES")                  |
| value.amount     | String | Yes      | Payment amount as decimal string             |
| description      | String | No       | Payment reference (max 35 characters)        |

### Response Fields

| Field                      | Type     | Description                                           |
|----------------------------|----------|-------------------------------------------------------|
| id                         | String   | Transaction request identifier                        |
| type                       | String   | Always "SEPA" for this endpoint                      |
| status                     | String   | "INITIATED" on success; "FAILED" on rejection        |
| start_date                 | DateTime | ISO-8601 timestamp when request was created          |
| end_date                   | DateTime | ISO-8601 timestamp when request expires              |
| challenge                  | Object   | SCA challenge if required                            |
| challenge.id               | String   | Challenge identifier                                 |
| challenge.allowed_attempts | Int      | Max OTP attempts (typically 3)                       |
| challenge.challenge_type   | String   | "OTP" for SMS-based SCA                              |
| charge                     | Object   | Applied fee                                          |
| charge.summary             | String   | Fee description (e.g. "Transfer fee")               |
| charge.value.amount        | String   | Fee amount (e.g. "50.00")                            |
| charge.value.currency      | String   | Fee currency (e.g. "KES")                            |

### Demo Data

| id                    | type | status    | challenge.challenge_type | charge.value.amount |
|-----------------------|------|-----------|--------------------------|---------------------|
| txreq-ke-20260523-001 | SEPA | INITIATED | OTP                      | 50.00               |

### Error Codes

| Code | Message                    | UI Handling                                                         |
|------|----------------------------|---------------------------------------------------------------------|
| 400  | INVALID_JSON_FORMAT        | Show error banner on confirmation screen                            |
| 403  | INSUFFICIENT_AUTHORISATION | Navigate to login or show permission error                          |
| 404  | BANK_ACCOUNT_NOT_FOUND     | Return to send-money, show error banner with account re-select CTA  |
| 422  | INSUFFICIENT_FUNDS         | Return to send-money, show error banner "Insufficient funds"        |

---

_Generated by /idea export | 2026-05-30_
