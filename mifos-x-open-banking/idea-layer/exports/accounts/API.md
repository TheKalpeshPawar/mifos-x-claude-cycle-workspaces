# API Reference — My Accounts

| Field    | Value                                       |
|----------|---------------------------------------------|
| Feature  | accounts                                    |
| Base URL | https://apisandbox.openbankproject.com      |

---

## GET /obp/v3.0.0/banks/{bankId}/accounts

**Auth:** DirectLogin
**Tag:** Accounts
**Trigger:** `loadAccounts()` on screen open / `RetryLoad` event

Fetches all accounts for the specified bank. The `AccountsViewModel` maps the response to `List<BankAccount>`, populates `accounts` and `filteredAccounts` (initially unfiltered), computes `totalBalance` by summing all `balance.amount` values, and groups accounts into `groupedByBank: Map<String, List<BankAccount>>` for bank-section rendering. Client-side `searchAccounts(query)` filters `filteredAccounts` by name, number, or label without issuing additional network calls; `groupedByBank` is recomputed from `filteredAccounts` on each query change.

### Path Parameters

| Name   | Type   | In   | Value    | Description                         |
|--------|--------|------|----------|-------------------------------------|
| bankId | String | path | gh.29.uk | Mifos X sandbox bank identifier     |

### Request Headers

| Header        | Value                           | Description                    |
|---------------|---------------------------------|--------------------------------|
| Authorization | DirectLogin token=`<token>`     | Session token from auth flow   |
| Content-Type  | application/json                |                                |

### Response Fields

| Field                         | Type                   | Description                                                                       |
|-------------------------------|------------------------|-----------------------------------------------------------------------------------|
| id                            | String                 | Unique account identifier                                                         |
| label                         | String                 | Human-readable account name (e.g. `"Primary Checking"`)                          |
| account_type                  | String                 | Account category: `"CHECKING"`, `"SAVINGS"`, `"BUSINESS"`, `"CURRENT"`           |
| balance                       | Object                 | Balance wrapper                                                                   |
| balance.currency              | String                 | ISO 4217 currency code (e.g. `"GBP"`, `"USD"`)                                   |
| balance.amount                | String                 | Decimal balance as string (e.g. `"4250.00"`)                                      |
| account_routings              | List\<AccountRouting\> | One or more routing entries for the account                                       |
| account_routings[].scheme     | String                 | Routing scheme: `"IBAN"`, `"AccountNumber"`                                       |
| account_routings[].address    | String                 | Routing value (IBAN string or account number)                                     |

### Demo Data

| id                   | label              | account_type | balance.currency | balance.amount | routing[0].scheme | routing[0].address              |
|----------------------|--------------------|--------------|------------------|----------------|-------------------|---------------------------------|
| acc_checking_primary | Primary Checking   | CHECKING     | GBP              | 4250.00        | IBAN              | DE89 3704 0044 0532 0130 00     |
| acc_savings_goal     | Holiday Savings    | SAVINGS      | GBP              | 6180.50        | IBAN              | DE89 3704 0044 0532 0131 00     |
| acc_business_main    | Business Current   | BUSINESS     | GBP              | 2050.00        | IBAN              | DE89 3704 0044 0532 0132 00     |

### Computed Values (AccountsViewModel — client-side)

| Computation      | Logic                                                                  | Demo Result         |
|------------------|------------------------------------------------------------------------|---------------------|
| totalBalance     | Sum of all `balance.amount.toBigDecimal()`                            | £12,480.50          |
| filteredAccounts | Filter `accounts` by `searchQuery` (name, number, label; empty → all) | Varies by query     |
| groupedByBank    | Group `filteredAccounts` by bank institution name                      | 2 groups (3 cards)  |
| bankSubtotal     | Sum of `balance.amount` per group key                                  | £10,430.50 / £2,050.00 |

### Error Codes

| Code | Message                                           | UI Handling                                                          |
|------|---------------------------------------------------|----------------------------------------------------------------------|
| 401  | Unauthorized — DirectLogin token missing or expired | Show `error` state; display `auth_error` message; redirect to login |
| 404  | Bank not found                                    | Show `error` state; show retry button                                |
| 500  | OBP server error                                  | Show `error` state; show retry button                                |

---

_Generated by /idea export | 2026-06-02_
