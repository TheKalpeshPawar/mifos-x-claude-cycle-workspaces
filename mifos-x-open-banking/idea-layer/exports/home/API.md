# API Reference — Home Dashboard

| Field    | Value                                       |
|----------|---------------------------------------------|
| Feature  | home                                        |
| Base URL | https://apisandbox.openbankproject.com      |

---

## GET /obp/v5.1.0/banks/{bankId}/accounts

**Auth:** DirectLogin
**Tag:** Accounts
**Trigger:** `loadDashboardData()` on screen open / `RetryLoad` event

Fetches all accounts for the bank to identify the primary checking account for the hero card. The first account of type "CHECKING" is used as `primaryAccount`.

### Path Parameters

| Name   | Type   | Value    | Description     |
|--------|--------|----------|-----------------|
| bankId | String | gh.29.uk | Bank identifier |

### Response Fields

| Field                    | Type                   | Description                       |
|--------------------------|------------------------|-----------------------------------|
| id                       | String                 | Account identifier                |
| label                    | String                 | Account display label             |
| account_type             | String                 | e.g. "CHECKING", "SAVINGS"        |
| balance                  | Object                 | Contains currency + amount        |
| balance.currency         | String                 | e.g. "GBP"                        |
| balance.amount           | String                 | e.g. "4250.00"                    |
| account_routings         | List\<AccountRouting\> | Routing numbers / IBAN            |

### Demo Data

| id         | label             | account_type | balance.amount | account_routing |
|------------|-------------------|--------------|----------------|-----------------|
| acc-0130   | Primary Checking  | CHECKING     | 4250.00        | •••• 0130       |
| acc-0245   | Savings           | SAVINGS      | 7840.25        | •••• 0245       |
| acc-0391   | Joint Current     | CHECKING     | 390.25         | •••• 0391       |

### Error Codes

| Code | Message                                      | UI Handling                  |
|------|----------------------------------------------|------------------------------|
| 401  | Unauthorized — DirectLogin token expired     | Navigate to login            |
| 404  | Bank not found                               | Show error state, retry      |
| 500  | OBP server error                             | Show error state, retry      |

---

## GET /obp/v5.1.0/my/banks/{bankId}/accounts/{accountId}/transactions

**Auth:** DirectLogin
**Tag:** Transactions
**Trigger:** `loadDashboardData()` on screen open / `RetryLoad` event

Fetches the 5 most recent transactions for the primary account, displayed in the Recent Transactions section (up to 3 shown in the home view).

### Path + Query Parameters

| Name           | Type   | In    | Value                    | Description                          |
|----------------|--------|-------|--------------------------|--------------------------------------|
| bankId         | String | path  | gh.29.uk                 | Bank identifier                      |
| accountId      | String | path  | (from accounts response) | Primary account ID                   |
| limit          | Int    | query | 5                        | Return only the 5 most recent        |
| sort_direction | String | query | DESC                     | Newest first                         |

### Response Fields

| Field                  | Type   | Description                             |
|------------------------|--------|-----------------------------------------|
| id                     | String | Transaction identifier                  |
| this_account           | Object | Account reference                       |
| other_account          | Object | Counterparty reference                  |
| details.type           | String | Transaction type e.g. "DEBIT", "CREDIT" |
| details.description    | String | Merchant or reference description       |
| details.posted         | String | ISO-8601 posted timestamp               |
| details.value.currency | String | e.g. "GBP"                             |
| details.value.amount   | String | Signed amount e.g. "−42.50", "3200.00" |

### Demo Data

| id     | details.description | details.type | details.value.amount | details.posted            |
|--------|---------------------|--------------|----------------------|---------------------------|
| txn-1  | Tesco Supermarket   | DEBIT        | -42.50               | 2026-05-23T14:32:00Z      |
| txn-2  | Salary Payment      | CREDIT       | 3200.00              | 2026-05-22T09:00:00Z      |
| txn-3  | EDF Energy          | DEBIT        | -94.20               | 2026-05-20T10:15:00Z      |

### Error Codes

| Code | Message          | UI Handling              |
|------|------------------|--------------------------|
| 401  | Unauthorized     | Navigate to login        |
| 404  | Account not found| Show error state, retry  |

---

## GET /obp/v3.0.0/my/accounts

**Auth:** DirectLogin
**Tag:** Accounts
**Trigger:** `loadDashboardData()` on screen open — cross-bank aggregation for total balance chip

Returns account summaries across all connected banks. The HomeViewModel sums `balance.amount` values to compute `totalBalance` and `totalAccountCount` for the total balance chip ("Total across 3 accounts: £12,480.50").

### Response Fields

| Field           | Type   | Description                      |
|-----------------|--------|----------------------------------|
| id              | String | Account identifier               |
| label           | String | Account display name             |
| balance.currency| String | Currency code                    |
| balance.amount  | String | Account balance                  |
| bank_id         | String | Bank identifier                  |

### Aggregated Demo Values

| Metric              | Value      |
|---------------------|------------|
| totalAccountCount   | 3          |
| totalBalance        | £12,480.50 |
| Primary Checking    | £4,250.00  |
| Savings             | £7,840.25  |
| Joint Current       | £390.25    |

### Error Codes

| Code | Message                                      | UI Handling             |
|------|----------------------------------------------|-------------------------|
| 401  | Unauthorized — DirectLogin token expired     | Navigate to login       |
| 500  | OBP server error                             | Show error state, retry |

---

_Generated by /idea export | 2026-05-29_
