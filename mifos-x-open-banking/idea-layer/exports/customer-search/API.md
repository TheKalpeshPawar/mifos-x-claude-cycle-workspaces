# API Reference — Find Customer

| Field    | Value                                       |
|----------|---------------------------------------------|
| Feature  | customer-search                             |
| Base URL | https://apisandbox.openbankproject.com      |

---

## GET /obp/v5.1.0/banks/{bankId}/customers

**Auth:** DirectLogin
**Tag:** Customers
**Trigger:** `search()` action on `SearchQueryChangedEvent` or `FilterSelectedEvent`; debounced after ≥2 chars typed

Fetches customers matching the text query and optional status filter. Results populate the customer results list as `CustomerSearchViewModel.searchResults`. Returns empty list → `no_results` state. Returns error → `error` state.

### Path Parameters

| Name   | Type   | Required | Description             |
|--------|--------|----------|-------------------------|
| bankId | String | Yes      | Bank identifier         |

### Query Parameters

| Name   | Type   | In    | Required | Description                                          |
|--------|--------|-------|----------|------------------------------------------------------|
| query  | String | query | No       | Free-text search: name, customer number, email       |
| status | String | query | No       | Filter by status: `active`, `prospect`, `dormant`. Omit for "All" |

### Response Fields

| Field                | Type             | Description                                     |
|----------------------|------------------|-------------------------------------------------|
| customers            | List\<Customer\> | Array of matching customer objects              |
| customer_id          | String           | Unique customer identifier                      |
| legal_name           | String           | Full legal name (drives initials avatar + name display) |
| kyc_status           | String           | `VERIFIED`, `PENDING`, `REJECTED` — drives KYC badge color |
| customer_number      | String           | Bank-issued customer number (e.g. EQKE-2024-00147) |
| mobile_phone_number  | String           | E.164 formatted mobile number                  |
| email                | String           | Customer email address                          |
| date_of_birth        | String           | ISO-8601 date string                            |
| last_ok_date         | String           | ISO-8601 timestamp of last successful KYC/interaction |

### Demo Data

| customer_id              | legal_name           | kyc_status | customer_number  | mobile_phone_number | last_ok_date         |
|--------------------------|----------------------|------------|------------------|---------------------|----------------------|
| cust-ke-001-wanjiru      | Wanjiru Kamau        | VERIFIED   | EQKE-2024-00147  | +254712345678       | 2026-05-10T09:30:00Z |
| cust-ke-002-rotich       | Kipchoge Rotich      | PENDING    | EQKE-2026-00221  | +254723456789       | 2026-05-22T11:30:00Z |
| cust-ke-003-atieno       | Atieno Ouma          | VERIFIED   | EQKE-2023-00089  | +254734567890       | 2026-04-28T14:00:00Z |
| cust-ke-004-mwangi       | James Mwangi Njoroge | VERIFIED   | EQKE-2022-00054  | +254745678901       | 2026-05-05T10:15:00Z |
| cust-ke-005-koech        | Cherotich Koech      | REJECTED   | EQKE-2026-00198  | +254756789012       | 2026-05-12T16:45:00Z |

### Error Codes

| Code | Message                                    | UI Handling                                          |
|------|--------------------------------------------|------------------------------------------------------|
| 400  | Invalid search parameters                  | Show inline search error; keep search input editable |
| 401  | Unauthorized — missing or invalid token    | Navigate to login screen                             |
| 500  | Internal server error                      | Transition to `error` state; show retry banner       |

---

## POST /obp/v4.0.0/banks/{bankId}/search/customers/mobile-phone-number

**Auth:** DirectLogin
**Tag:** Customer
**Trigger:** `ScanQrEvent` when QR code decoded to a phone number; or direct phone-number entry in search field (detected by "+254" prefix pattern)

Searches for a customer by exact mobile phone number. Returns a list (typically one entry) of matching customers. Used by the QR scanner flow — after scanning a QR that encodes a phone number, `QrScannerService` fires this endpoint to resolve the customer record before navigating to customer-detail.

### Path Parameters

| Name   | Type   | Required | Description     |
|--------|--------|----------|-----------------|
| bankId | String | Yes      | Bank identifier |

### Request Body

| Field               | Type   | Required | Description                        |
|---------------------|--------|----------|------------------------------------|
| mobile_phone_number | String | Yes      | E.164 mobile phone number to match |

### Response Fields

| Field     | Type             | Description                      |
|-----------|------------------|----------------------------------|
| customers | List\<Customer\> | Matching customers (typically 1) |

### Demo Data

| customer_id         | legal_name    | customer_number | mobile_phone_number | kyc_status |
|---------------------|---------------|-----------------|---------------------|------------|
| cust-ke-001-wanjiru | Wanjiru Kamau | EQKE-2024-00147 | +254712345678       | VERIFIED   |

### Error Codes

| Code | Message                                    | UI Handling                                     |
|------|--------------------------------------------|-----------------------------------------------------|
| 400  | Invalid phone number format                | Show search input error "Invalid phone number"  |
| 401  | Unauthorized — missing or invalid token    | Navigate to login screen                        |
| 404  | No customer found for this phone number    | Transition to `no_results` state                |
| 500  | Internal server error                      | Transition to `error` state; show retry banner  |

---

_Generated by /idea export | 2026-05-30_
