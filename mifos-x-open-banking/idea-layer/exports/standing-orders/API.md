# API Reference — Standing Orders

| Field    | Value                                  |
|----------|----------------------------------------|
| Feature  | standing-orders                        |
| Base URL | https://apisandbox.openbankproject.com |

---

## POST /obp/v4.0.0/banks/{bankId}/accounts/{accountId}/owner/standing-order

**Auth:** DirectLogin
**Tag:** Standing-Orders
**Trigger:** `create_standing_order` action — fired when user completes the create-standing-order flow and taps Confirm

Creates a new standing order on a specific bank account. OBP v4 provides a POST-only endpoint for this resource; there is no dedicated GET list endpoint. The Standing Orders list screen reconstructs visible orders by filtering recurring transaction-history entries (type: "StandingOrder") or from a local cache of application-created orders keyed by `id`. The `active` field in the response determines whether an order renders as an elevated white card (active) or an outlined muted card (paused).

### Path Parameters

| Name      | Type   | Example           | Description                    |
|-----------|--------|-------------------|--------------------------------|
| bankId    | String | ke.equity.bank    | Bank identifier (Equity Kenya) |
| accountId | String | acc-equity-ke-001 | Source account identifier      |

### Request Body Fields

| Field                                      | Type   | Required | Description                                                    |
|--------------------------------------------|--------|----------|----------------------------------------------------------------|
| counterparty.name                          | String | Yes      | Beneficiary display name                                       |
| counterparty.other_bank_routing_address    | String | Yes      | Destination bank routing code                                  |
| counterparty.other_account_routing_address | String | Yes      | Destination account number / IBAN                              |
| amount_value                               | String | Yes      | Payment amount as decimal string (e.g. "3500.00")              |
| amount_currency                            | String | Yes      | ISO-4217 currency code (e.g. "KES")                           |
| when.frequency                             | String | Yes      | Recurrence — "MONTHLY", "WEEKLY", "QUARTERLY"                  |
| when.start_date                            | String | Yes      | ISO-8601 date for first payment (e.g. "2026-01-05")           |
| when.final_date                            | String | No       | ISO-8601 date for last payment; omit for indefinite            |

### Response Fields

| Field                                      | Type                  | Description                                             |
|--------------------------------------------|-----------------------|---------------------------------------------------------|
| id                                         | String                | Unique standing order identifier                        |
| bank_id                                    | String                | Originating bank identifier                             |
| account_id                                 | String                | Originating account identifier                          |
| counterparty                               | Counterparty          | Beneficiary details object                              |
| counterparty.name                          | String                | Beneficiary display name                                |
| counterparty.other_bank_routing_address    | String                | Destination bank routing code                           |
| counterparty.other_account_routing_address | String                | Destination account number / IBAN                       |
| amount_value                               | String                | Payment amount as decimal string                        |
| amount_currency                            | String                | ISO-4217 currency code                                  |
| when                                       | StandingOrderSchedule | Schedule details object                                 |
| when.frequency                             | String                | Recurrence frequency                                    |
| when.start_date                            | String                | First payment date                                      |
| when.final_date                            | String                | Last payment date (nullable)                            |
| active                                     | Boolean               | Whether the standing order is currently active          |
| standing_orders                            | List\<StandingOrder\> | Full list (some OBP versions include this in response)  |

### Demo Data (from demo-data.yaml — Equity Bank Kenya, KES)

| id        | counterparty.name                           | amount_value | currency | frequency | start_date | final_date | active |
|-----------|---------------------------------------------|--------------|----------|-----------|------------|------------|--------|
| so-ke-001 | Nairobi Water & Sewerage — utility bill     | 3500.00      | KES      | MONTHLY   | 2026-01-05 | 2027-01-05 | true   |
| so-ke-002 | Safaricom Home Fibre — internet subscription | 6000.00     | KES      | MONTHLY   | 2026-02-15 | 2027-02-15 | true   |
| so-ke-003 | Amani Apartments Westlands — rent           | 45000.00     | KES      | MONTHLY   | 2026-01-01 | 2026-12-31 | true   |
| so-ke-004 | NHIF — health insurance contribution        | 1700.00      | KES      | MONTHLY   | 2026-03-01 | 2027-03-01 | false  |

### Error Codes

| Code | Message                    | UI Handling                                                   |
|------|----------------------------|---------------------------------------------------------------|
| 400  | INVALID_BANK_ID            | Show CREATE_FAILED inline error; highlight bank field          |
| 401  | USER_NOT_LOGGED_IN         | Redirect to login screen; clear session                       |
| 403  | INSUFFICIENT_AUTHORISATION | Show error: "You don't have permission for this account."     |
| 404  | BANK_ACCOUNT_NOT_FOUND     | Show LOAD_FAILED error state with retry; navigate back if persists |

---

_Generated by /idea export | 2026-05-30_
