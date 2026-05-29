# API Reference — Consumer Home

| Field    | Value                                  |
|----------|----------------------------------------|
| Feature  | consumer-home                          |
| Base URL | https://apisandbox.openbankproject.com |

---

## GET /obp/v4.0.0/my/accounts

**Auth:** DirectLogin
**Tag:** Accounts
**Trigger:** `loadConsumerHome()` on `ScreenOpened` / `RetryLoad` event

Fetches all consumer accounts across connected banks. The `ConsumerHomeViewModel` uses the first account to populate the balance card: `totalBalance`, `primaryAccount.label` (chip), and the balance amount (£4,250.00). All accounts contribute to month-to-date income and spend summaries.

### Response Fields

| Field            | Type            | Description                                                           |
|------------------|-----------------|-----------------------------------------------------------------------|
| accounts         | List\<Account\> | Top-level list of account objects                                     |
| id               | String          | Unique account identifier (used as `accountId` for transactions call) |
| bank_id          | String          | Bank identifier — e.g. `mifos.uk.gb.01`                              |
| label            | String          | Human-readable account name — e.g. "Primary Checking"                |
| balance.amount   | String          | Current balance as decimal string — e.g. `"4250.00"`                 |
| balance.currency | String          | ISO 4217 currency code — e.g. `"GBP"`                                |

### Demo Data

| id                        | bank_id         | label            | balance.amount | balance.currency |
|---------------------------|-----------------|------------------|----------------|------------------|
| acc-alex-gbp-current-001  | mifos.uk.gb.01  | Primary Checking | 4250.00        | GBP              |
| acc-alex-gbp-savings-002  | mifos.uk.gb.01  | Everyday Savings | 11820.45       | GBP              |

**ViewModel mapping:**
- `primaryAccount` ← first account (`acc-alex-gbp-current-001`, label "Primary Checking")
- `totalBalance` ← sum of all `balance.amount` values
- `ch_balance_amount` displays `£4,250.00`; `ch_account_name_chip` displays "Primary Checking"

### Error Codes

| Code | OBP Message         | UI Handling                                |
|------|---------------------|--------------------------------------------|
| 401  | USER_NOT_LOGGED_IN  | Dispatch `auth_error`; navigate to login   |
| 404  | BANK_NOT_FOUND      | Dispatch `network_error`; show error state |
| 500  | OBP server error    | Dispatch `network_error`; show error state |

---

## GET /obp/v4.0.0/banks/{bankId}/accounts/{accountId}/transactions

**Auth:** DirectLogin
**Tag:** Transactions
**Trigger:** `loadConsumerHome()` on `ScreenOpened` / `RetryLoad` event — called after accounts response resolves `accountId`

Fetches the 3 most recent transactions for the primary account. The response populates three white transaction cards: Coffee Shop (DEBIT, -£3.50 from Greenwood Coffee), Salary (CREDIT, +£3,200.00 from Mifos Microfinance Ltd), Supermarket (DEBIT, -£42.80 from FreshMart Supermarket). Tapping any card navigates to `transaction-detail`.

### Path Parameters

| Name      | Type   | In   | Value                     | Description                               |
|-----------|--------|------|---------------------------|-------------------------------------------|
| bankId    | String | path | mifos.uk.gb.01            | Bank identifier from accounts response    |
| accountId | String | path | acc-alex-gbp-current-001  | Primary account ID from accounts response |

### Query Parameters

| Name           | Type   | In    | Default | Description                   |
|----------------|--------|-------|---------|-------------------------------|
| limit          | Int    | query | 3       | Return only the 3 most recent |
| sort_direction | String | query | DESC    | Newest first                  |

### Response Fields

| Field                     | Type   | Description                                                 |
|---------------------------|--------|-------------------------------------------------------------|
| transactions              | List   | Top-level list of transaction objects                       |
| id                        | String | Transaction identifier                                      |
| this_account.id           | String | Account the transaction belongs to                          |
| other_account.holder.name | String | Counterparty display name — e.g. "Greenwood Coffee"         |
| details.type              | String | `"DEBIT"` or `"CREDIT"`                                    |
| details.description       | String | Short description — e.g. `"Coffee Shop"`, `"Salary"`        |
| details.posted            | String | ISO-8601 timestamp — e.g. `"2026-05-29T08:14:00Z"`          |
| details.value.amount      | String | Signed decimal — `"-3.50"` (debit) or `"3200.00"` (credit) |
| details.value.currency    | String | ISO 4217 code — e.g. `"GBP"`                               |

### Demo Data

| id                           | other_account.holder.name | details.type | details.value.amount | details.posted           |
|------------------------------|---------------------------|--------------|----------------------|--------------------------|
| txn-coffee-20260529-001      | Greenwood Coffee          | DEBIT        | -3.50                | 2026-05-29T08:14:00Z     |
| txn-salary-20260528-002      | Mifos Microfinance Ltd    | CREDIT       | 3200.00              | 2026-05-28T06:00:00Z     |
| txn-supermarket-20260527-003 | FreshMart Supermarket     | DEBIT        | -42.80               | 2026-05-27T17:42:00Z     |

**UI mapping:**
- `ch_transaction_item_1` ← "Coffee Shop — £3.50" (DEBIT, today)
- `ch_transaction_item_2` ← "Salary — £3,200.00" (CREDIT, yesterday)
- `ch_transaction_item_3` ← "Supermarket — £42.80" (DEBIT, 2 days ago)

### Error Codes

| Code | OBP Message            | UI Handling                                |
|------|------------------------|--------------------------------------------|
| 401  | USER_NOT_LOGGED_IN     | Dispatch `auth_error`; navigate to login   |
| 404  | BANK_ACCOUNT_NOT_FOUND | Dispatch `network_error`; show error state |

---

_Generated by /idea export | 2026-05-30_
