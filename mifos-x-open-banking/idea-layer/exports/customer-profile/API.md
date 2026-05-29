# API Reference — Customer Profile

| Field    | Value                                       |
|----------|---------------------------------------------|
| Feature  | customer-profile                            |
| Base URL | https://apisandbox.openbankproject.com      |

---

## GET /obp/v5.1.0/banks/{bankId}/customers/{customerId}

**Auth:** DirectLogin
**Tag:** Customers
**Trigger:** `CustomerProfileViewModel.loadCustomer()` on screen entry; `RetryLoad` event on error banner tap

Fetches the full customer record for the given `customerId` at `bankId`. All three screen sections (Personal Information, Address, Employment) are populated from this single response. Individual data rows display skeleton shimmers until this call resolves.

### Path Parameters

| Name       | Type   | Example                    | Description                     |
|------------|--------|----------------------------|---------------------------------|
| bankId     | String | rbs                        | Bank identifier (OBP bank_id)   |
| customerId | String | cust-ke-001-wanjiru        | OBP customer identifier         |

### Response Fields

| Field                               | Type   | Description                                                     |
|-------------------------------------|--------|-----------------------------------------------------------------|
| customer_id                         | String | OBP customer UUID                                               |
| legal_name                          | String | Full legal name — maps to `full_name_value`                     |
| date_of_birth                       | String | ISO-8601 date (YYYY-MM-DD) — formatted as "DD Month YYYY (Age: N)" |
| national_id_number                  | String | National identification number — displayed in monospace         |
| tax_pin                             | String | KRA Tax PIN — displayed in monospace                            |
| mobile_phone_number                 | String | E.164 phone — rendered as `tel:` link                           |
| email                               | String | Email address — rendered as `mailto:` link                      |
| address                             | Object | Nested address object                                           |
| address.line_1                      | String | Street address line 1                                           |
| address.line_2                      | String | Street address line 2 / area                                    |
| address.city                        | String | City                                                            |
| address.county                      | String | County — displayed as "{county}, Kenya"                         |
| address.postcode                    | String | Postal code — displayed as "Postcode: {postcode}"              |
| address.country_code                | String | ISO 3166-1 alpha-2 country code                                 |
| address.status                      | String | Address status (e.g. "ACTIVE")                                  |
| employment_details                  | Object | Nested employment object                                        |
| employment_details.employer_name    | String | Employer name — maps to `employer_value`                        |
| employment_details.employment_status| String | e.g. "EMPLOYED", "SELF_EMPLOYED" — used to derive display type |
| employment_details.title            | String | Job title (informational, not displayed in current screen)      |
| employment_details.start_date       | String | Employment start date (informational, not displayed)            |

### Demo Data

| Field                  | Value                            |
|------------------------|----------------------------------|
| customer_id            | cust-ke-001-wanjiru              |
| legal_name             | Wanjiru Kamau                    |
| date_of_birth          | 1988-03-22                       |
| national_id_number     | 28456789                         |
| tax_pin                | A987654321W                      |
| mobile_phone_number    | +254712345678                    |
| email                  | wanjiru.kamau@gmail.com          |
| address.line_1         | 26 Westlands Road                |
| address.line_2         | Westlands                        |
| address.city           | Nairobi                          |
| address.county         | Nairobi County                   |
| address.postcode       | 00100                            |
| address.country_code   | KE                               |
| employment.employer    | Safaricom PLC                    |
| employment.status      | EMPLOYED                         |
| employment.title       | Senior Software Engineer         |

**Derived display values (ViewModel mapping):**
- `full_name_value` ← `legal_name`: "Wanjiru Kamau"
- `dob_value` ← `date_of_birth` (formatted): "22 March 1988 (Age: 38)"
- `national_id_value` ← `national_id_number`: "28456789"
- `tax_pin_value` ← `tax_pin`: "A987654321W"
- `phone_link` content ← `mobile_phone_number`: "+254 712 345 678"
- `email_link` content ← `email`: "wanjiru.kamau@gmail.com"
- `address_street` ← `address.line_1 + ", " + address.line_2`: "26 Westlands Road, Westlands"
- `address_county` ← `address.county + ", Kenya"`: "Nairobi County, Kenya"
- `address_postcode` ← `"Postcode: " + address.postcode`: "Postcode: 00100"
- `employer_value` ← `employment_details.employer_name`: "Safaricom PLC"
- `income_value` ← (supplementary / future field): "KES 85,000"
- `employment_type_value` ← `employment_details.employment_status` mapped: "Permanent"

### Error Codes

| Code | OBP Message         | UI Handling                                                                       |
|------|---------------------|-----------------------------------------------------------------------------------|
| 400  | BAD_REQUEST         | Per-row error banner: "Could not load customer profile. Please try again."        |
| 401  | UNAUTHORIZED        | Navigate to login screen (session expired)                                        |
| 404  | CUSTOMER_NOT_FOUND  | Full-screen error: "Customer record not found." No retry (fatal for this screen)  |

---

## PUT /obp/v5.1.0/banks/{bankId}/customers/{customerId}

**Auth:** DirectLogin
**Tag:** Customers
**Trigger:** `save_customer_info` action (dispatched when user confirms edits in `editing` state)

Submits updated customer information. The screen transitions from `editing → saving` while this request is in flight. On success, transitions to `content` with refreshed data. On failure, transitions back to `editing` with a `SAVE_FAILED` error banner.

### Path Parameters

| Name       | Type   | Example             | Description             |
|------------|--------|---------------------|-------------------------|
| bankId     | String | rbs                 | Bank identifier         |
| customerId | String | cust-ke-001-wanjiru | OBP customer identifier |

### Request Body Fields

| Field                | Type   | Description                                  |
|----------------------|--------|----------------------------------------------|
| legal_name           | String | Updated full legal name                      |
| mobile_phone_number  | String | Updated phone number (E.164 format)          |
| email                | String | Updated email address                        |

### Response Fields

| Field          | Type   | Description                                             |
|----------------|--------|---------------------------------------------------------|
| customer_id    | String | Confirmed customer UUID                                 |
| legal_name     | String | Persisted legal name (ViewModel refreshes display)      |
| last_ok_date   | String | ISO-8601 timestamp of last successful KYC verification  |

### Demo Data (update response)

| Field          | Value                             |
|----------------|-----------------------------------|
| customer_id    | cust-ke-001-wanjiru               |
| legal_name     | Wanjiru Kamau-Njoroge             |
| last_ok_date   | 2026-05-30T00:00:00Z              |

### Error Codes

| Code | OBP Message       | UI Handling                                                                  |
|------|-------------------|------------------------------------------------------------------------------|
| 400  | VALIDATION_FAILED | Inline field validation error; remain in `editing` state                     |
| 401  | UNAUTHORIZED      | Navigate to login (session expired mid-edit)                                 |
| 404  | CUSTOMER_NOT_FOUND| Error banner: "Customer record no longer exists." Navigate back on dismiss   |

---

_Generated by /idea export | 2026-05-30_
