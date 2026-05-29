# API Reference — Spending Insights (PFM Dashboard)

| Field    | Value                                       |
|----------|---------------------------------------------|
| Feature  | pfm-dashboard                               |
| Base URL | https://apisandbox.openbankproject.com      |

---

## GET /obp/v6.0.0/my/personal-data-fields

**Auth:** DirectLogin
**Tag:** User
**Trigger:** `loadDashboardData()` on screen open / `RetryLoad` event / `PeriodSelected` event

Reads all personal data fields for the authenticated user. PFM budget limits follow the key convention `pfm_budget_<categoryId>` (e.g. `pfm_budget_food_dining`, `pfm_budget_transport`). The ViewModel collects all fields with this prefix and maps them to `List<BudgetEntry>` for `overallBudgetLimit` computation and per-category progress bars.

If no `pfm_budget_*` keys exist, `overallBudgetLimit` is null and the screen transitions to `no_budget_set` state.

### Response Fields

| Field                   | Type                      | Description                                               |
|-------------------------|---------------------------|-----------------------------------------------------------|
| personal_data_fields    | List\<PersonalDataField\> | All personal data fields for the user                     |
| name                    | String                    | Field key e.g. "pfm_budget_food_dining"                   |
| value                   | String                    | Field value e.g. "350" (GBP pence-denominated integer)    |

### Demo Data

| name                        | value  | Derived budget (GBP) |
|-----------------------------|--------|----------------------|
| pfm_budget_food_dining      | 35000  | £350.00              |
| pfm_budget_transport        | 20000  | £200.00              |
| pfm_budget_shopping         | 15000  | £150.00              |
| pfm_budget_bills            | 50000  | £500.00              |
| pfm_budget_entertainment    | 10000  | £100.00              |

> Note: demo-data.yaml uses KES values — the ui.yaml canonical demo uses GBP (£350, £200, £150, £500, £100). GBP values are authoritative for UI rendering.

### Overall Budget Derivation

| Metric              | Value      |
|---------------------|------------|
| overallBudgetLimit  | £1,500.00  |
| totalSpent          | £1,029.80  |
| totalReceived       | £3,200.00  |
| netBalance          | +£2,170.20 |
| budgetPercent       | 68%        |
| budgetRemaining     | £470.20    |

### Error Codes

| Code | Message                   | UI Handling                                       |
|------|---------------------------|---------------------------------------------------|
| 401  | USER_NOT_LOGGED_IN        | Navigate to login screen                          |
| 403  | INSUFFICIENT_AUTHORISATION| Show error state with "Contact support" message   |
| 500  | OBP server error          | Show error state, retry                           |

---

## POST /obp/v6.0.0/my/personal-data-fields

**Auth:** DirectLogin
**Tag:** User
**Trigger:** `BudgetEditClicked(categoryId)` → budget edit bottom sheet → save action → `ManageBudgetsClicked`

Creates or updates a budget entry for a specific spending category. The request key follows the convention `pfm_budget_<categoryId>`. On success, the ViewModel re-fetches personal data fields and recomputes all budget progress.

### Request Fields

| Field | Type   | Required | Example                  | Description                                    |
|-------|--------|----------|--------------------------|------------------------------------------------|
| name  | String | Yes      | "pfm_budget_food_dining" | Key following pfm_budget_<categoryId> pattern  |
| value | String | Yes      | "350"                    | Budget limit as integer string (GBP, no pence) |

### Request Examples

| categoryId    | name                         | value |
|---------------|------------------------------|-------|
| food_dining   | pfm_budget_food_dining       | 350   |
| transport     | pfm_budget_transport         | 200   |
| shopping      | pfm_budget_shopping          | 150   |
| bills         | pfm_budget_bills             | 500   |
| entertainment | pfm_budget_entertainment     | 100   |

### Response Fields

| Field | Type   | Description                   |
|-------|--------|-------------------------------|
| name  | String | Confirmed field key           |
| value | String | Confirmed field value         |

### Error Codes

| Code | Message                | UI Handling                                        |
|------|------------------------|----------------------------------------------------|
| 400  | INVALID_FIELD_NAME     | Show inline error in budget edit sheet             |
| 401  | USER_NOT_LOGGED_IN     | Navigate to login screen                           |
| 500  | OBP server error       | Show SAVE_FAILED snackbar, retain previous value   |

---

## GET /obp/v6.0.0/my/accounts/{account_id}/transactions

**Auth:** DirectLogin
**Tag:** Transactions
**Trigger:** `loadDashboardData()` on screen open / `RetryLoad` event / `PeriodSelected(period: PfmPeriod)` event

Fetches all transactions for the primary account within the selected period date window. The ViewModel aggregates the response to compute:
- `totalSpent` — sum of all DEBIT `value.amount` (absolute)
- `totalReceived` — sum of all CREDIT `value.amount`
- `categoryBreakdown` — grouped by merchant-category tag into `List<CategorySpend>`
- `topMerchants` — top 4 merchants by total spend as `List<MerchantSpend>`

Period windows:
- **This Month**: `from_date = first day of current month 00:00:00Z`, `to_date = last day of current month 23:59:59Z`
- **Last Month**: prior calendar month
- **Last 3 Months**: 3-month rolling window from today
- **Custom**: user-supplied date range from date picker

### Path + Query Parameters

| Name        | Type   | In    | Example                   | Description                              |
|-------------|--------|-------|---------------------------|------------------------------------------|
| account_id  | String | path  | acc-equity-ke-001         | Primary account identifier               |
| from_date   | String | query | 2026-05-01T00:00:00Z      | Period start (ISO-8601)                  |
| to_date     | String | query | 2026-05-31T23:59:59Z      | Period end (ISO-8601)                    |
| limit       | Int    | query | 500                       | Max transactions per fetch               |

### Response Fields

| Field                    | Type             | Description                                    |
|--------------------------|------------------|------------------------------------------------|
| transactions             | List\<Transaction\> | Transaction list for the period             |
| transaction_id           | String           | Unique transaction identifier                  |
| this_account             | AccountInfo      | Account the transaction belongs to             |
| details                  | TransactionDetails | Transaction details (type, description, value)|
| details.type             | String           | "DEBIT" or "CREDIT"                           |
| details.description      | String           | Merchant name or payment reference             |
| details.posted           | String           | ISO-8601 posted timestamp                      |
| value                    | AmountOfMoney    | Currency + amount                              |
| value.currency           | String           | e.g. "GBP"                                    |
| value.amount             | String           | Signed amount e.g. "-42.50", "3200.00"         |

### Demo Data (ui.yaml canonical — GBP)

| transaction_id | description          | type   | amount     | category      | merchant           | posted                   |
|----------------|----------------------|--------|------------|---------------|--------------------|--------------------------|
| txn-pfm-t01    | Tesco                | DEBIT  | -142.30    | Food & Dining | Tesco              | 2026-05-24T09:15:00Z     |
| txn-pfm-t02    | Netflix              | DEBIT  | -17.99     | Entertainment | Netflix            | 2026-05-01T00:00:00Z     |
| txn-pfm-t03    | Spotify              | DEBIT  | -11.99     | Entertainment | Spotify            | 2026-05-01T00:01:00Z     |
| txn-pfm-t04    | Transport for London | DEBIT  | -78.50     | Transport     | Transport for London| 2026-05-23T08:30:00Z    |
| txn-pfm-t05    | HSBC Mortgage        | DEBIT  | -450.00    | Bills         | HSBC               | 2026-05-02T09:00:00Z     |
| txn-pfm-t06    | Zara                 | DEBIT  | -89.30     | Shopping      | Zara               | 2026-05-18T14:00:00Z     |
| txn-pfm-t07    | Salary Payment       | CREDIT | +3200.00   | Income        | Employer           | 2026-05-01T09:00:00Z     |

### Aggregated PFM Values (populated state)

| Category Breakdown | Amount   | % of Spend |
|--------------------|----------|------------|
| Food & Dining      | £320.50  | 31.1%      |
| Transport          | £125.00  | 12.1%      |
| Shopping           | £89.30   | 8.7%       |
| Bills              | £450.00  | 43.7%      |
| Entertainment      | £45.00   | 4.4%       |
| **Total Spent**    | £1,029.80| 100%       |

| Top Merchants        | Total Spent | Transactions |
|----------------------|-------------|--------------|
| Tesco                | £142.30     | 8            |
| Transport for London | £78.50      | 23           |
| Netflix              | £17.99      | 1            |
| Spotify              | £11.99      | 1            |

### Error Codes

| Code | Message             | UI Handling                                  |
|------|---------------------|----------------------------------------------|
| 400  | INVALID_DATE_FORMAT | Show error state, retry with corrected range |
| 401  | USER_NOT_LOGGED_IN  | Navigate to login screen                     |
| 404  | ACCOUNT_NOT_FOUND   | Show error state + retry                     |
| 500  | OBP server error    | Show error state + retry                     |

---

_Generated by /idea export | 2026-05-30_
