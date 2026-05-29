# API Reference — Customer 360 Profile

| Field    | Value                                       |
|----------|---------------------------------------------|
| Feature  | customer-detail                             |
| Base URL | https://apisandbox.openbankproject.com      |

---

## GET /obp/v5.1.0/banks/{bankId}/customers/{customerId}

**Auth:** DirectLogin
**Tag:** Customers
**Trigger:** `loadDashboardData()` on screen entry; `RetryLoadEvent` on retry tap

Fetches the full customer record for the given `customerId` within the bank. Drives the hero header (name, initials, member-since, KYC badge), quick-stats (KYC status), personal information card (legal name, DOB, email, phone), and KYC banners. The `kyc_status` boolean controls which KYC banner renders and whether the KYC Verified badge appears.

### Path Parameters

| Name       | Type   | Example               | Description           |
|------------|--------|-----------------------|-----------------------|
| bankId     | String | ke.equity.001         | Bank identifier       |
| customerId | String | cust-ke-001-wanjiru   | Customer identifier   |

### Response Fields

| Field                       | Type                | Description                                                     |
|-----------------------------|---------------------|-----------------------------------------------------------------|
| bank_id                     | String              | Bank identifier                                                 |
| customer_id                 | String              | Customer unique identifier                                      |
| customer_number             | String              | Human-readable account reference (e.g. "EQKE-2024-00147")     |
| legal_name                  | String              | Full legal name — drives `customer_full_name` text component    |
| mobile_phone_number         | String              | E.164 format — drives `personal_info_phone`                     |
| email                       | String              | Email address — drives `personal_info_email`                    |
| face_image                  | FaceImage           | `{ url: String, date: String }` — avatar image URL             |
| date_of_birth               | String              | ISO date (YYYY-MM-DD) — drives `personal_info_dob`             |
| relationship_status         | String              | Enum: SINGLE / MARRIED / DIVORCED / WIDOWED                    |
| dependants                  | Int                 | Number of dependants                                            |
| dob_of_dependants           | List\<String\>      | ISO dates of dependant DOBs                                     |
| credit_rating               | CreditRating        | `{ rating: String, source: String }` e.g. `{ "A", "CRB Africa" }` |
| credit_limit                | Amount              | `{ currency: String, amount: String }` credit limit             |
| highest_education_attained  | String              | e.g. "UNIVERSITY"                                               |
| employment_status           | String              | e.g. "EMPLOYED"                                                 |
| kyc_status                  | Boolean             | `true` = verified → show verified banner; `false` → pending banner |
| last_ok_date                | String              | ISO-8601 timestamp of last KYC check — drives KYC banner date   |
| title                       | String              | Honorific (Mr / Mrs / Dr etc.)                                  |
| branch_id                   | String              | Assigned branch identifier                                      |
| name_suffix                 | String              | Suffix (Jr / Sr etc.), may be empty                             |

### Demo Data

| Field               | Value                                    |
|---------------------|------------------------------------------|
| bank_id             | ke.equity.001                            |
| customer_id         | cust-ke-001-wanjiru                      |
| customer_number     | EQKE-2024-00147                          |
| legal_name          | Wanjiru Kamau                            |
| mobile_phone_number | +254712345678                            |
| email               | wanjiru.kamau@gmail.com                  |
| date_of_birth       | 1988-03-22                               |
| relationship_status | MARRIED                                  |
| dependants          | 2                                        |
| credit_rating       | { rating: "A", source: "CRB Africa" }   |
| credit_limit        | { currency: "KES", amount: "500000.00" } |
| employment_status   | EMPLOYED                                 |
| kyc_status          | true                                     |
| last_ok_date        | 2026-05-10T09:30:00Z                     |
| title               | Mrs                                      |
| branch_id           | branch-westlands-nbi                     |

### Error Codes

| Code | Message                                     | UI Handling                                    |
|------|---------------------------------------------|------------------------------------------------|
| 401  | Unauthorized — missing or invalid token     | Navigate to login screen                       |
| 403  | Forbidden — insufficient permissions        | Show error state with contact support message  |
| 404  | Customer not found                          | Transition to `empty` state                    |
| 500  | Internal server error                       | Transition to `error` state with retry button  |

---

## GET /obp/v5.1.0/banks/{bankId}/customers/{customerId}/accounts

**Auth:** DirectLogin
**Tag:** Accounts
**Trigger:** `loadDashboardData()` on screen entry — parallel to customer fetch; `RetryLoadEvent` on retry tap

Fetches all accounts associated with this customer. The `CustomerDetailViewModel` sums `balance.amount` values to compute `totalBalance` shown in `stat_total_balance`, and counts entries for `stat_accounts_count`. Account details also populate the Accounts tab content.

### Path Parameters

| Name       | Type   | Example               | Description         |
|------------|--------|-----------------------|---------------------|
| bankId     | String | ke.equity.001         | Bank identifier     |
| customerId | String | cust-ke-001-wanjiru   | Customer identifier |

### Response Fields

| Field                          | Type                   | Description                                              |
|--------------------------------|------------------------|----------------------------------------------------------|
| accounts                       | List\<Account\>        | Array of account objects                                 |
| accounts[].id                  | String                 | Account unique identifier                                |
| accounts[].label               | String                 | Display label (e.g. "Wanjiru Savings Account")          |
| accounts[].number              | String                 | Account number                                           |
| accounts[].bank_id             | String                 | Bank identifier                                          |
| accounts[].account_type        | String                 | SAVINGS / CURRENT / CHECKING                             |
| accounts[].balance             | Amount                 | `{ currency: String, amount: String }`                  |
| accounts[].account_routings    | List\<AccountRouting\> | `[{ scheme: String, address: String }]` e.g. IBAN       |

### Demo Data

| id                    | label                      | account_type | balance.currency | balance.amount |
|-----------------------|----------------------------|--------------|------------------|----------------|
| acct-ke-001-savings   | Wanjiru Savings Account    | SAVINGS      | KES              | 187450.00      |
| acct-ke-002-current   | Wanjiru Current Account    | CURRENT      | KES              | 42800.00       |

**Aggregated display values:**
- `stat_accounts_count` → "2 Accounts"
- `stat_total_balance` → "KES 230,250" (sum of 187,450 + 42,800)

### Error Codes

| Code | Message                                     | UI Handling                                   |
|------|---------------------------------------------|-----------------------------------------------|
| 401  | Unauthorized — missing or invalid token     | Navigate to login screen                      |
| 403  | Forbidden — insufficient permissions        | Show error state; stats row shows "—"         |
| 404  | Customer or bank not found                  | Stats row shows "0 Accounts"                  |
| 500  | Internal server error                       | Transition to `error` state with retry button |

---

## GET /obp/v5.0.0/banks/{bankId}/customers/{customerId}/customer-account-links

**Auth:** DirectLogin
**Tag:** Customer
**Trigger:** `loadDashboardData()` on screen entry — supplementary load; retrieves link records joining customer to accounts when ownership is managed via the link table

Returns customer-account link records used by `CustomerRepository` to resolve the canonical set of accounts belonging to this customer.

### Path Parameters

| Name       | Type   | Example               | Description         |
|------------|--------|-----------------------|---------------------|
| bankId     | String | ke.equity.001         | Bank identifier     |
| customerId | String | cust-ke-001-wanjiru   | Customer identifier |

### Response Fields

| Field                            | Type                        | Description                               |
|----------------------------------|-----------------------------|-------------------------------------------|
| links                            | List\<CustomerAccountLink\> | Array of link objects                     |
| links[].customer_account_link_id | String                      | Unique link record identifier             |
| links[].account_id               | String                      | References the linked account `id`        |

### Demo Data

| customer_account_link_id      | account_id              |
|-------------------------------|-------------------------|
| cal-001-wanjiru-savings        | acct-ke-001-savings     |
| cal-002-wanjiru-current        | acct-ke-002-current     |

### Error Codes

| Code | Message                                     | UI Handling                                   |
|------|---------------------------------------------|-----------------------------------------------|
| 401  | Unauthorized — missing or invalid token     | Navigate to login screen                      |
| 403  | Forbidden — insufficient permissions        | Show error state with contact support message |
| 404  | Customer not found                          | Empty accounts tab                            |
| 500  | Internal server error                       | Transition to `error` state with retry button |

---

_Generated by /idea export | 2026-05-30_
