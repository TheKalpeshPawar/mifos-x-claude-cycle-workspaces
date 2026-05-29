# API Reference — Customer Profile

| Field    | Value                                     |
|----------|-------------------------------------------|
| Feature  | customer-profile                          |
| Base URL | https://apisandbox.openbankproject.com    |

---

## GET /obp/v5.1.0/banks/{bankId}/customers/{customerId}

**Auth:** DirectLogin
**Tag:** Customers
**Trigger:** Screen entry — `loadCustomerProfile(customerId)` called on initial state; also on RetryLoad event

### Path Parameters

| Name       | Type   | Value          |
|------------|--------|----------------|
| bankId     | String | gh.29.uk       |
| customerId | String | (from navigation args) |

### Response Fields

| Field                     | Type   | Description                                               |
|---------------------------|--------|-----------------------------------------------------------|
| customer_id               | String | Unique OBP customer identifier                            |
| legal_name                | String | Full legal name — maps to full_name_value                 |
| date_of_birth             | String | ISO-8601 date — formatted as "dd MMMM yyyy (Age: N)"     |
| national_id_number        | String | National ID — maps to national_id_value                  |
| tax_pin                   | String | KRA Tax PIN — maps to tax_pin_value                      |
| mobile_phone_number       | Object | `{ prefix: "+254", number: "722123456" }` — maps to phone_link |
| email                     | String | Email address — maps to email_link                       |
| address                   | Object | Contains line_1, city, county, postcode — maps to address section |
| address.line_1            | String | Street address — maps to address_street_row               |
| address.city              | String | City — part of address_street_row                         |
| address.county            | String | County — maps to address_county_row                      |
| address.postcode          | String | Postcode — maps to address_postcode_row                  |
| employment_details        | Object | Employer, income, type — maps to employment section       |
| employment_details.employer_name | String | Employer name — maps to employer_value            |
| employment_details.monthly_income | Object | `{ amount, currency }` — maps to income_value    |
| employment_details.employment_status | String | "EMPLOYED", "SELF_EMPLOYED", etc.              |

### Sample Response (condensed)

```json
{
  "customer_id": "cust-001-jmwangi",
  "legal_name": "John Kamau Mwangi",
  "date_of_birth": "1985-03-14",
  "national_id_number": "KE12345678",
  "tax_pin": "A001234567M",
  "mobile_phone_number": { "prefix": "+254", "number": "722123456" },
  "email": "john.mwangi@gmail.com",
  "address": {
    "line_1": "123 Moi Avenue",
    "city": "Nairobi",
    "county": "Nairobi County",
    "country_code": "KE",
    "postcode": "00100"
  },
  "employment_details": {
    "employer_name": "Safaricom PLC",
    "monthly_income": { "amount": "85000.00", "currency": "KES" },
    "employment_status": "EMPLOYED"
  }
}
```

### Error Codes

| Code | Message                                         |
|------|-------------------------------------------------|
| 400  | BAD_REQUEST — malformed customerId              |
| 401  | UNAUTHORIZED — DirectLogin token expired        |
| 404  | CUSTOMER_NOT_FOUND — customerId does not exist  |
| 500  | OBP server error                                |

---

## PUT /obp/v5.1.0/banks/{bankId}/customers/{customerId}

**Auth:** DirectLogin
**Tag:** Customers
**Trigger:** `save_customer_info` action — fires when user confirms edits in editing state

### Path Parameters

| Name       | Type   | Value          |
|------------|--------|----------------|
| bankId     | String | gh.29.uk       |
| customerId | String | (from screen state) |

### Request Fields

| Field              | Type   | Required | Description                              |
|--------------------|--------|----------|------------------------------------------|
| legal_name         | String | No       | Updated full legal name                  |
| mobile_phone_number| Object | No       | Updated phone `{ prefix, number }`       |
| email              | String | No       | Updated email address                    |
| address            | Object | No       | Updated address fields                   |
| employment_details | Object | No       | Updated employer, income, type           |

### Response Fields

| Field       | Type   | Description                                  |
|-------------|--------|----------------------------------------------|
| customer_id | String | Confirmed customer ID                        |
| legal_name  | String | Updated legal name as stored                 |
| last_ok_date| String | ISO-8601 timestamp of last successful update |

### Error Codes

| Code | Message                                         |
|------|-------------------------------------------------|
| 400  | VALIDATION_FAILED — invalid field value         |
| 401  | UNAUTHORIZED                                    |
| 404  | CUSTOMER_NOT_FOUND                              |
| 500  | OBP server error                                |

---

_Generated by /idea export | 2026-05-29_
