# API Reference — Transaction History

| Field    | Value                                  |
|----------|----------------------------------------|
| Feature  | transactions                           |
| Base URL | https://apisandbox.openbankproject.com |

---

## GET /obp/v5.1.0/my/banks/{bankId}/accounts/{accountId}/transactions

**Auth:** DirectLogin
**Tag:** Transactions
**Trigger:** `loadTransactions()` on ScreenOpened / RetryLoad / ClearFilters; `searchTransactions(query)` on SearchQueryChanged; `filterByType(filter)` on FilterTypeChanged; `filterByDateRange(range)` on DateRangeChanged; `loadNextPage()` on LoadMore

### Path Parameters

| Name      | Type   | Value          | Description                  |
|-----------|--------|----------------|------------------------------|
| bankId    | String | gh.29.uk       | OBP bank identifier          |
| accountId | String | (from session) | Account to fetch history for |

### Query Parameters

| Name           | Type   | In    | Required | Value / Example                      | Description                                |
|----------------|--------|-------|----------|--------------------------------------|--------------------------------------------|
| limit          | Int    | query | No       | 20                                   | Page size — default 20 rows per request    |
| offset         | Int    | query | No       | 0                                    | Pagination offset (0-indexed)              |
| from_date      | String | query | No       | 2026-04-25T00:00:00.000Z             | ISO-8601 start of date range               |
| to_date        | String | query | No       | 2026-05-25T23:59:59.999Z             | ISO-8601 end of date range                 |
| type           | String | query | No       | DEBIT, CREDIT, SEPA_CREDIT_TRANSFERS, UK_FASTER_PAYMENTS_SEND | Transaction type filter (omit for ALL) |
| sort_direction | String | query | No       | DESC                                 | Newest-first (default DESC)                |

### Response Fields

| Field                      | Type    | Description                                   |
|----------------------------|---------|-----------------------------------------------|
| id                         | String  | Transaction identifier                        |
| this_account               | Object  | Source account reference                      |
| other_account              | Object  | Counterparty reference                        |
| other_account.holder       | Object  | Counterparty name / alias info                |
| other_account.metadata     | Object  | Optional merchant metadata (logo URL)         |
| details.type               | String  | Transaction type (e.g. "DEBIT")               |
| details.description        | String  | Merchant or reference description             |
| details.posted             | String  | ISO-8601 posted timestamp                     |
| details.completed          | String  | ISO-8601 completed timestamp                  |
| details.new_balance.currency | String| Account balance currency after transaction    |
| details.new_balance.amount | String  | Account balance after transaction             |
| details.value.currency     | String  | Transaction currency (e.g. "GBP")             |
| details.value.amount       | String  | Signed amount (e.g. "-42.50", "3200.00")      |
| metadata                   | Object  | User metadata (tags, comments, narrative)     |

### Sample Response (single item)

```json
{
  "id": "txn_20260525_001",
  "this_account": { "id": "acc-primary-0130" },
  "other_account": {
    "holder": { "name": "Tesco PLC", "is_alias": false },
    "metadata": { "image_url": "https://cdn.obp.io/logos/tesco.png" }
  },
  "details": {
    "type": "DEBIT",
    "description": "TESCO STORES 1234",
    "posted": "2026-05-25T14:32:00Z",
    "completed": "2026-05-25T14:32:00Z",
    "new_balance": { "currency": "GBP", "amount": "4207.50" },
    "value": { "currency": "GBP", "amount": "-42.50" }
  },
  "metadata": { "narrative": null, "comments": [], "tags": [] }
}
```

### Error Codes

| Code | Message                              | UI Behaviour                                      |
|------|--------------------------------------|---------------------------------------------------|
| 400  | Invalid date range or filter params  | Show error card: "Could not load transactions"    |
| 401  | Unauthorized                         | Redirect to login screen                          |
| 404  | Account not found                    | Show error card with retry                        |
| 500  | OBP server error                     | Show error card with retry                        |

---

## Demo Data Shown in UI

| Row | Merchant           | Date        | Category  | Amount     | Type   |
|-----|--------------------|-------------|-----------|------------|--------|
| 1   | Tesco Supermarket  | 25 May 2026 | Groceries | -£42.50    | DEBIT  |
| 2   | Salary Payment     | 24 May 2026 | Income    | +£3,200.00 | CREDIT |
| 3   | EDF Energy         | 23 May 2026 | Utilities | -£94.20    | DEBIT  |

Monthly summary (Last 30 Days): Spent £1,240.30 | Received £3,200.00

---

_Generated by /idea export | 2026-05-29_
