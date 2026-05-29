# API Reference — Customer 360 Profile

| Field    | Value                                       |
|----------|---------------------------------------------|
| Feature  | customer-detail                             |
| Base URL | https://apisandbox.openbankproject.com      |

---

## GET /obp/v5.1.0/banks/{bankId}/customers/{customerId}

**Auth:** DirectLogin
**Tag:** Customers
**Trigger:** `loadCustomerDetail(customerId)` on screen open / `RetryLoadEvent`

### Path Parameters

| Name       | Type   | Description                           |
|------------|--------|---------------------------------------|
| bankId     | String | Bank identifier (e.g. "gh.29.uk")     |
| customerId | String | OBP customer ID from customer-search  |

### Response Fields

| Field                     | Type       | Description                                                |
|---------------------------|------------|------------------------------------------------------------|
| bank_id                   | String     | Bank identifier                                            |
| customer_id               | String     | Unique customer identifier                                 |
| customer_number           | String     | Bank-assigned customer reference number                    |
| legal_name                | String     | Full legal name (e.g. "John Kamau Mwangi")                |
| mobile_phone_number       | String     | Contact phone (e.g. "+254 722 123 456")                    |
| email                     | String     | Email address (e.g. "john.mwangi@gmail.com")               |
| face_image.url            | String     | Profile photo URL (if present)                             |
| face_image.date           | String     | Photo capture date                                         |
| date_of_birth             | String     | ISO-8601 date of birth (e.g. "1985-03-14")                |
| relationship_status       | String     | Relationship status string                                 |
| dependants                | Int        | Number of dependants                                       |
| credit_rating.rating      | String     | Credit rating code                                         |
| credit_limit.currency     | String     | Credit limit currency                                      |
| credit_limit.amount       | String     | Credit limit amount                                        |
| highest_education_attained| String     | Education level                                            |
| employment_status         | String     | Employment status                                          |
| kyc_status                | Boolean    | `true` = KYC verified; `false` = pending                  |
| last_ok_date              | String     | ISO-8601 timestamp of last KYC check / last account OK     |
| title                     | String     | Title (Mr/Mrs/Dr etc.)                                     |
| branch_id                 | String     | Assigned branch identifier                                 |
| name_suffix               | String     | Name suffix if applicable                                  |

### Error Codes

| Code | OBP Error Key          | UI Behaviour                                               |
|------|------------------------|------------------------------------------------------------|
| 401  | USER_NOT_LOGGED_IN     | Navigate to login                                          |
| 403  | INSUFFICIENT_AUTHORISATION | Show error state                                       |
| 404  | CUSTOMER_NOT_FOUND     | Show `empty` state — customer archived or ID invalid       |
| 500  | INTERNAL_SERVER_ERROR  | Show `error` state with retry                              |

---

## GET /obp/v5.1.0/banks/{bankId}/customers/{customerId}/accounts

**Auth:** DirectLogin
**Tag:** Accounts
**Trigger:** `loadCustomerDetail(customerId)` on screen open — parallel to customer fetch

### Path Parameters

| Name       | Type   | Description                           |
|------------|--------|---------------------------------------|
| bankId     | String | Bank identifier                       |
| customerId | String | OBP customer ID                       |

### Response Fields

| Field                    | Type                    | Description                               |
|--------------------------|-------------------------|-------------------------------------------|
| accounts                 | List\<Account\>         | All accounts linked to the customer        |
| id                       | String                  | Account identifier                        |
| label                    | String                  | Account display name                      |
| number                   | String                  | Account number                            |
| bank_id                  | String                  | Bank identifier                           |
| account_routings         | List\<AccountRouting\>  | Routing numbers / IBANs                   |
| balance.currency         | String                  | Account currency                          |
| balance.amount           | String                  | Account balance                           |
| account_type             | String                  | e.g. "CHECKING", "SAVINGS"                |

### Sample Display Mapping

- `stat_accounts_count`: `accounts.size` → "2 Accounts"
- `stat_total_balance`: sum of `balance.amount` across all accounts → "KES 145,200"

### Error Codes

| Code | OBP Error Key              | UI Behaviour                                         |
|------|----------------------------|------------------------------------------------------|
| 401  | USER_NOT_LOGGED_IN         | Navigate to login                                    |
| 403  | INSUFFICIENT_AUTHORISATION | Stats row shows "—" for balance                      |
| 404  | CUSTOMER_NOT_FOUND         | Stats row shows "0 Accounts"                         |

---

## GET /obp/v5.0.0/banks/{bankId}/customers/{customerId}/customer-account-links

**Auth:** DirectLogin
**Tag:** Customer
**Trigger:** Optional supplementary load for Accounts tab content

### Path Parameters

| Name       | Type   | Description             |
|------------|--------|-------------------------|
| bankId     | String | Bank identifier         |
| customerId | String | OBP customer ID         |

### Response Fields

| Field                      | Type   | Description                                    |
|----------------------------|--------|------------------------------------------------|
| links                      | List\<CustomerAccountLink\> | All account links for the customer |
| customer_account_link_id   | String | Link record identifier                         |
| account_id                 | String | Linked account ID (references accounts list)   |

### Error Codes

| Code | OBP Error Key              | UI Behaviour              |
|------|----------------------------|---------------------------|
| 401  | USER_NOT_LOGGED_IN         | Navigate to login         |
| 404  | CUSTOMER_NOT_FOUND         | Empty accounts tab        |

---

_Generated by /idea export | 2026-05-29_
