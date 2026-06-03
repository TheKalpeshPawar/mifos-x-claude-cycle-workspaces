# API Reference — Beneficiaries

| Field    | Value                                  |
|----------|----------------------------------------|
| Feature  | beneficiaries                          |
| Base URL | https://apisandbox.openbankproject.com |

> Contract verified against live OBP sandbox 2026-06-03 (bank `ac.bank.uk`, account `ac.checking.001`, view `owner`).

---

## GET /obp/v4.0.0/banks/{bankId}/accounts/{accountId}/{viewId}/counterparties

**Auth:** DirectLogin
**Tag:** Counterparties
**Trigger:** `ScreenOpened` / `RefreshTriggered` — loads the explicit counterparty list for the primary account. BeneficiariesViewModel splits into `recentBeneficiaries` (ordered by latest matching transaction) and `beneficiaries` (full list, sorted by `sortOrder`).

### Path Parameters

| Name      | Type   | Value         | Description                                              |
|-----------|--------|---------------|---------------------------------------------------------|
| bankId    | String | ac.bank.uk    | OBP bank identifier (from ObpConfig)                     |
| accountId | String | (dynamic)     | Account id from the authenticated user's accounts list   |
| viewId    | String | owner         | Account view granting counterparty access                |

### Response Fields

| Field                                                | Type           | Description                                                       |
|------------------------------------------------------|----------------|------------------------------------------------------------------|
| counterparties                                       | List\<Object\> | Array of counterparty objects                                    |
| counterparties[].counterparty_id                     | String         | Unique counterparty identifier (UUID)                            |
| counterparties[].name                                | String         | Beneficiary display name (e.g. "TechStart Ltd")                |
| counterparties[].description                         | String         | Relationship/purpose note (e.g. "Freelance-gig payee at Mifos")|
| counterparties[].currency                            | String         | ISO 4217 currency (e.g. "GBP")                                  |
| counterparties[].this_bank_id                        | String         | The owning account's bank id                                     |
| counterparties[].this_account_id                     | String         | The owning account id                                            |
| counterparties[].this_view_id                        | String         | The view the counterparty was created through (owner)            |
| counterparties[].other_bank_routing_scheme           | String         | "OBP", "BIC", etc. (OBP → resolvable to bank name)            |
| counterparties[].other_bank_routing_address          | String         | Bank id (OBP scheme) or BIC code                                 |
| counterparties[].other_branch_routing_scheme         | String         | Branch routing scheme (often empty)                             |
| counterparties[].other_branch_routing_address        | String         | Branch routing address (often empty)                            |
| counterparties[].other_account_routing_scheme        | String         | "IBAN", "OBP", etc.                                           |
| counterparties[].other_account_routing_address       | String         | IBAN or account id (e.g. "GB29MFOS98765601001234")            |
| counterparties[].other_account_secondary_routing_scheme  | String     | Secondary routing scheme (often empty)                          |
| counterparties[].other_account_secondary_routing_address | String     | Secondary routing address (often empty)                         |
| counterparties[].is_beneficiary                      | Boolean        | true when flagged as a trusted beneficiary                      |
| counterparties[].created_by_user_id                  | String         | OBP user id who created this counterparty                        |
| counterparties[].bespoke                             | List\<Object\> | Arbitrary `{key, value}` pairs (often empty)                    |

### Demo Data (real sandbox rows, account ac.checking.001)

| name                | description                      | currency | other_bank_routing_scheme | other_bank_routing_address | other_account_routing_scheme | other_account_routing_address | is_beneficiary |
|---------------------|----------------------------------|----------|---------------------------|----------------------------|------------------------------|-------------------------------|----------------|
| Savings Counterparty| Internal savings target for R5   | EUR      | OBP                       | ac.bank.uk                 | OBP                          | ac.savings.001                | true           |
| TechStart Ltd       | Freelance-gig payee at Mifos     | GBP      | OBP                       | mifos-x-openbank           | OBP                          | mifos.techstart.current       | true           |
| Costa Coffee        | card purchase                    | EUR      | OBP                       | ac.bank.uk                 | OBP                          | ac.savings.001                | true           |
| Tesco Express       | card purchase                    | EUR      | BIC                       | TESCGB2L                   | IBAN                         | GB29TESC60161331926819        | true           |

### Error Codes

| Code | Message                          | Description                                          | UI Handling                                |
|------|----------------------------------|------------------------------------------------------|--------------------------------------------|
| 401  | OBP-20001: User not logged in    | DirectLogin token absent or expired                  | Re-authenticate via POST /my/logins/direct |
| 404  | OBP-30018: Bank Account not found| accountId not found for authenticated user           | Show error state, surface retry            |
| 404  | OBP-30005: View not found        | viewId not valid for the account                     | Show error state                           |

---

## POST /obp/v4.0.0/banks/{bankId}/accounts/{accountId}/{viewId}/counterparties

**Auth:** DirectLogin
**Tag:** Counterparties
**Trigger:** `AddBeneficiaryClicked` → add-beneficiary sheet submit. Creates an explicit counterparty, then the list refreshes.

### Request Body

| Field                                    | Type           | Required | Notes                                  |
|------------------------------------------|----------------|----------|----------------------------------------|
| name                                     | String         | yes      | Beneficiary display name               |
| description                              | String         | yes      | Relationship/purpose note              |
| currency                                 | String         | yes      | ISO 4217 (e.g. "GBP")                |
| other_account_routing_scheme             | String         | yes      | "IBAN" / "OBP"                      |
| other_account_routing_address            | String         | yes      | IBAN or account id                     |
| other_bank_routing_scheme                | String         | yes      | "BIC" / "OBP"                       |
| other_bank_routing_address               | String         | yes      | BIC or bank id                         |
| other_branch_routing_scheme              | String         | yes      | may be ""                            |
| other_branch_routing_address             | String         | yes      | may be ""                            |
| other_account_secondary_routing_scheme   | String         | yes      | may be ""                            |
| other_account_secondary_routing_address  | String         | yes      | may be ""                            |
| is_beneficiary                           | Boolean        | yes      | true                                   |
| bespoke                                   | List\<Object\> | yes      | may be `[]`                          |

### Response

`201` — returns the created counterparty (same shape as the GET row, plus `metadata`). Key field: `counterparty_id`.

### Error Codes

| Code | Message                              | UI Handling                                  |
|------|--------------------------------------|----------------------------------------------|
| 400  | OBP-10001: Incorrect json format     | Validate form fields                         |
| 400  | OBP-30014: Counterparty already exists | Surface "A payee with that name exists"     |

---

## GET /obp/v4.0.0/banks/{bankId}

**Auth:** DirectLogin
**Tag:** Bank
**Trigger:** Per unique `other_bank_routing_address` (OBP scheme only). Resolves a bank id to a display name; results cached in `BanksRepository`.

### Response Fields

| Field      | Type   | Description                              |
|------------|--------|------------------------------------------|
| id         | String | Bank id (e.g. "ac.bank.uk")            |
| short_name | String | Short code (e.g. "ACBK")               |
| full_name  | String | Display name (e.g. "Afternoon Coffee Bank") |
| logo       | String | Logo URL                                 |

### Error Codes

| Code | Message                    | UI Handling                              |
|------|----------------------------|------------------------------------------|
| 404  | OBP-30001: Bank not found  | Fall back to showing the routing code    |

---

## GET /obp/v3.0.0/my/banks/{bankId}/accounts/{accountId}/transactions

**Auth:** DirectLogin
**Tag:** Transaction
**Trigger:** Loaded once per account to derive each beneficiary's last-payment amount/date and recency. Join `transactions[].details.description` ↔ `counterparties[].name`; use the most recent `details.posted` and `details.value.amount`/`currency`. Owned by the transactions screen; reused read-only here.

---

_Generated by /idea export | 2026-06-03_
