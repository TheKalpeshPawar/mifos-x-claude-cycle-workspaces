# API Reference — My Accounts

| Field    | Value                                       |
|----------|---------------------------------------------|
| Feature  | accounts                                    |
| Base URL | https://apisandbox.openbankproject.com      |

---

## GET /obp/v5.1.0/banks/{bankId}/accounts

**Auth:** DirectLogin
**Tag:** Accounts
**Trigger:** `loadAccounts()` on screen open / `RetryLoad` event

Fetches all accounts for the specified bank. The `AccountsViewModel` maps the response to `List<BankAccount>`, sets `accounts` and `filteredAccounts` (initially unfiltered), and computes `totalBalance` by summing all `balance.amount` values. Client-side filter operations via `activeFilter` (ALL / CHECKING / SAVINGS / BUSINESS / CURRENT / MOBILE_WALLET) do not issue additional network calls.

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
| label                         | String                 | Human-readable account name (e.g. `"KES Savings — Personal"`)                    |
| account_type                  | String                 | Account category: `"CHECKING"`, `"SAVINGS"`, `"CURRENT"`, `"MOBILE_WALLET"`      |
| balance                       | Object                 | Balance wrapper                                                                   |
| balance.currency              | String                 | ISO 4217 currency code (e.g. `"KES"`, `"USD"`)                                   |
| balance.amount                | String                 | Decimal balance as string (e.g. `"142500.75"`)                                    |
| account_routings              | List\<AccountRouting\> | One or more routing entries for the account                                       |
| account_routings[].scheme     | String                 | Routing scheme: `"IBAN"`, `"AccountNumber"`, `"PhoneNumber"`                      |
| account_routings[].address    | String                 | Routing value (IBAN string, account number, or phone number)                      |

### Demo Data

| id                            | label                         | account_type  | balance.currency | balance.amount | routing[0].scheme | routing[0].address     |
|-------------------------------|-------------------------------|---------------|------------------|----------------|-------------------|------------------------|
| acc-mwangi-kes-savings-001    | KES Savings — Personal        | SAVINGS       | KES              | 142500.75      | IBAN              | KE1900200001001000001  |
| acc-mwangi-kes-current-002    | KES Current — Business        | CURRENT       | KES              | 875200.00      | IBAN              | KE1900200001001000002  |
| acc-mwangi-usd-savings-003    | USD Savings — Foreign Currency| SAVINGS       | USD              | 3840.50        | IBAN              | KE1900200001001000003  |
| acc-mwangi-mpesa-float-004    | M-Pesa Float Account          | MOBILE_WALLET | KES              | 12300.00       | PhoneNumber       | +254712345678          |

Each account also carries a second routing entry (`AccountNumber`) per the demo-data.yaml sibling.

### Computed Values (AccountsViewModel — client-side)

| Computation      | Logic                                                   | Demo Result |
|------------------|---------------------------------------------------------|-------------|
| totalBalance     | Sum of all `balance.amount.toBigDecimal()`             | KES 1,032,301.25 + USD 3,840.50 (multi-currency) |
| filteredAccounts | Filter `account_type` to match `activeFilter` enum     | Varies by selected tab |
| displayBalance   | Format `balance.amount` per `balance.currency` locale  | e.g. "KES 142,500.75" |

### Error Codes

| Code | Message                                           | UI Handling                                                    |
|------|---------------------------------------------------|----------------------------------------------------------------|
| 401  | Unauthorized — DirectLogin token missing or expired | Show `error` state; display `auth_error` message; redirect to login |
| 404  | Bank not found                                    | Show `error` state; show retry button                          |
| 500  | OBP server error                                  | Show `error` state; show retry button                          |

---

_Generated by /idea export | 2026-05-30_
