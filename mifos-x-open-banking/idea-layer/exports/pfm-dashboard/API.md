# API Reference — Spending Insights (PFM Dashboard)

| Field | Value |
|---|---|
| Feature | pfm-dashboard |
| Base URL | https://apisandbox.openbankproject.com |
| Auth Scheme | DirectLogin (header: `DirectLogin token=<token>`) |

---

## Overview

The PFM dashboard uses two OBP API families:

1. **Transactions feed** — fetched per account and filtered by date range for the active period; aggregated locally to produce category totals, merchant totals, and income/spend summaries.
2. **Personal data fields** — used as a lightweight key-value store for user-defined budget limits, keyed by convention `pfm_budget_<categoryId>`.

No server-side PFM aggregation is required. All category attribution, merchant grouping, and budget comparison logic runs on-device.

---

## GET /obp/v6.0.0/my/accounts/{account_id}/transactions

**Tag:** Transactions
**Purpose:** Fetch transactions for a given account filtered by date range. Called once per linked account for the selected period. The client aggregates results to produce category breakdowns, merchant totals, income/spend summaries, and top merchants.

### Path Parameters

| Parameter | Type | Description |
|---|---|---|
| account_id | String | The OBP account identifier |

### Query Parameters

| Parameter | Type | Required | Example | Description |
|---|---|---|---|---|
| from_date | String (ISO 8601) | Yes | `2026-05-01T00:00:00Z` | Start of the selected period (inclusive) |
| to_date | String (ISO 8601) | Yes | `2026-05-31T23:59:59Z` | End of the selected period (inclusive) |
| limit | Int | No | `500` | Max transactions per page (default 50; use 500 for PFM aggregation) |
| offset | Int | No | `0` | Pagination offset |
| sort_direction | String | No | `DESC` | `ASC` or `DESC` by date |

### Period → Date Range Mapping

| PfmPeriod | from_date | to_date |
|---|---|---|
| THIS_MONTH | First day of current month 00:00:00Z | Last day of current month 23:59:59Z |
| LAST_MONTH | First day of previous month 00:00:00Z | Last day of previous month 23:59:59Z |
| LAST_3_MONTHS | 3 months ago first day 00:00:00Z | Yesterday 23:59:59Z |
| CUSTOM | User-selected start 00:00:00Z | User-selected end 23:59:59Z |

### Response Shape

```json
{
  "transactions": [
    {
      "id": "transaction_id",
      "this_account": {
        "id": "account_id",
        "bank_routing": { "scheme": "OBP", "address": "bank_id" }
      },
      "other_account": {
        "id": "counterpart_id",
        "holder": { "name": "Tesco" }
      },
      "details": {
        "type": "SEPA",
        "description": "TESCO STORES 2985",
        "posted": "2026-05-03T09:14:22Z",
        "completed": "2026-05-03T09:14:22Z",
        "value": { "currency": "GBP", "amount": "-14.27" },
        "new_balance": { "currency": "GBP", "amount": "2185.73" }
      },
      "metadata": {
        "narrative": "",
        "tags": [],
        "images": []
      }
    }
  ]
}
```

### Response Fields

| Field | Type | Description |
|---|---|---|
| transactions | List\<Transaction\> | Array of transaction objects |
| id | String | Unique transaction identifier |
| other_account.holder.name | String | Counterpart name — used as merchant name for grouping |
| details.value.amount | String | Signed decimal string; negative = debit (spend), positive = credit (income) |
| details.value.currency | String | ISO 4217 currency code (e.g. "GBP") |
| details.posted | String (ISO 8601) | Transaction posted timestamp — used for period filtering |
| details.description | String | Raw transaction description — used for category attribution |

### Local Aggregation Logic

| Output | Source | Rule |
|---|---|---|
| totalSpent | Sum of transactions where amount < 0 | Absolute value sum of all debit amounts |
| totalReceived | Sum of transactions where amount > 0 | Sum of all credit amounts |
| categoryBreakdown | Category attributed per transaction | Client-side rules: description keywords → category enum |
| topMerchants | Grouped by other_account.holder.name | Top 4 by total absolute spend descending |
| overallBudget % | totalSpent / overallBudgetLimit | Fetched from personal data fields (key: `pfm_budget_overall`) |

### Error Codes

| Code | OBP Error | Client Behaviour |
|---|---|---|
| 400 | INVALID_DATE_FORMAT | Show error state with retry |
| 401 | USER_NOT_LOGGED_IN | Redirect to login |
| 404 | ACCOUNT_NOT_FOUND | Skip account silently; surface warning if all accounts fail |
| 500 | OBP_CONNECTOR_CANNOT_RETURN_DATA | Show error state with retry |

---

## GET /obp/v6.0.0/my/personal-data-fields

**Tag:** User
**Purpose:** Read all personal data fields for the authenticated user. PFM budget limits are stored by convention with the prefix `pfm_budget_<categoryId>`. The overall monthly budget is stored as `pfm_budget_overall`.

### Stored Budget Keys

| Key | Category | Example Value |
|---|---|---|
| `pfm_budget_overall` | Overall monthly budget | `"1500"` |
| `pfm_budget_food_dining` | Food & Dining | `"350"` |
| `pfm_budget_transport` | Transport | `"200"` |
| `pfm_budget_shopping` | Shopping | `"150"` |
| `pfm_budget_bills` | Bills | `"500"` |
| `pfm_budget_entertainment` | Entertainment | `"100"` |

### Response Fields

| Field | Type | Description |
|---|---|---|
| personal_data_fields | List\<PersonalDataField\> | Array of all personal data field objects |
| name | String | Field key (e.g. `"pfm_budget_food_dining"`) |
| value | String | Field value as a decimal string — client parses to BigDecimal |

### Error Codes

| Code | OBP Error | Client Behaviour |
|---|---|---|
| 401 | USER_NOT_LOGGED_IN | Redirect to login |
| 403 | INSUFFICIENT_AUTHORISATION | Show error; surface "budget unavailable" fallback — hide budget progress section |

---

## POST /obp/v6.0.0/my/personal-data-fields

**Tag:** User
**Purpose:** Create or update a personal data field. Used when the user sets or edits a budget limit for a category (or the overall budget).

### Request Body

| Field | Type | Required | Example | Description |
|---|---|---|---|---|
| name | String | Yes | `"pfm_budget_food_dining"` | Must follow `pfm_budget_<categoryId>` convention |
| value | String | Yes | `"350"` | Decimal string representing budget amount in account currency |

### Response Fields

| Field | Type | Description |
|---|---|---|
| name | String | The key that was created or updated |
| value | String | The stored value |

### Error Codes

| Code | OBP Error | Client Behaviour |
|---|---|---|
| 400 | INVALID_FIELD_NAME | Show SAVE_FAILED error; keep sheet open |
| 401 | USER_NOT_LOGGED_IN | Redirect to login |
| 403 | INSUFFICIENT_AUTHORISATION | Show SAVE_FAILED error; keep sheet open |

---

## Data Flow Summary

```
1. PfmDashboardViewModel.init()
   ├── GET /my/personal-data-fields         → parse pfm_budget_* keys → BudgetEntry list
   └── for each linked account:
       └── GET /my/accounts/{id}/transactions
           ?from_date=<period_start>
           &to_date=<period_end>
           &limit=500
           → aggregate locally:
               totalSpent, totalReceived
               categoryBreakdown (5 categories)
               topMerchants (top 4)

2. On PeriodSelected(period):
   └── Re-fetch transactions with updated from/to dates
       → re-aggregate → emit DataLoaded event

3. On BudgetEditClicked(categoryId) → user submits:
   └── POST /my/personal-data-fields { name, value }
       → on success: re-fetch personal-data-fields → refresh BudgetEntry list
```

---

*Generated by /idea export | 2026-05-25*
