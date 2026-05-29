# API Reference — New Customer Onboarding

| Field    | Value                                       |
|----------|---------------------------------------------|
| Feature  | customer-onboarding                         |
| Base URL | https://apisandbox.openbankproject.com      |

The onboarding flow chains 10 sequential OBP API calls on Submit. Steps 1–3 correspond to form completion phases; steps 4–10 finalise KYC, attributes, user-account linkage, and account application. All calls use DirectLogin authentication. The `customer_id` returned from Step 1 is threaded through all subsequent calls.

---

## POST /obp/v5.0.0/banks/{bankId}/customers

**Auth:** DirectLogin
**Tag:** Customer
**Trigger:** `submit` action — Step 1 of 10 on submit_button tap

Creates the customer record in the OBP core banking system using personal information collected in Step 1 of the form.

### Path Parameters

| Name   | Type   | Description     |
|--------|--------|-----------------|
| bankId | String | Bank identifier |

### Request Body Fields

| Field                       | Type    | Required | Description                                   |
|-----------------------------|---------|----------|-----------------------------------------------|
| legal_name                  | String  | Yes      | Full legal name (first + last name combined)  |
| mobile_phone_number         | String  | Yes      | E.164 format e.g. "+254723456789"             |
| email                       | String  | No       | Optional email address                        |
| date_of_birth               | String  | Yes      | ISO-8601 date e.g. "1992-06-14"               |
| title                       | String  | No       | Salutation e.g. "Mr"                          |
| relationship_status         | String  | No       | e.g. "SINGLE", "MARRIED"                      |
| employment_status           | String  | No       | e.g. "SELF_EMPLOYED", "EMPLOYED"              |
| highest_education_attained  | String  | No       | e.g. "UNIVERSITY"                             |
| credit_rating.rating        | String  | No       | CRB rating e.g. "B"                           |
| credit_rating.source        | String  | No       | CRB source e.g. "Metropol CRB"                |
| credit_limit.currency       | String  | No       | e.g. "KES"                                    |
| credit_limit.amount         | String  | No       | e.g. "150000.00"                              |
| face_image.url              | String  | No       | Selfie URL from liveness capture              |
| face_image.date             | String  | No       | ISO-8601 date of capture                      |
| kyc_status                  | Boolean | Yes      | Initial KYC status; always false on creation  |
| branch_id                   | String  | No       | Originating branch identifier                 |

### Response Fields

| Field       | Type   | Description                                     |
|-------------|--------|-------------------------------------------------|
| customer_id | String | Created customer UUID — used in steps 2–10      |
| bank_id     | String | Bank identifier                                 |

### Demo Data

| legal_name      | mobile_phone_number | date_of_birth | credit_rating.rating | kyc_status | branch_id        |
|-----------------|---------------------|---------------|----------------------|------------|------------------|
| Kipchoge Rotich | +254723456789       | 1992-06-14    | B                    | false      | branch-karen-nbi |

### Error Codes

| Code | Message                                      | UI Handling                                       |
|------|----------------------------------------------|---------------------------------------------------|
| 400  | Invalid request body                         | Show VALIDATION_FAILED with field details         |
| 401  | Unauthorized — DirectLogin token expired     | Navigate to login                                 |
| 409  | Customer already exists                      | Show SUBMIT_FAILED — "Customer already registered"|
| 500  | OBP server error                             | Show SUBMIT_FAILED + retry                        |

---

## POST /obp/v3.1.0/banks/{bankId}/customers/{customerId}/address

**Auth:** DirectLogin
**Tag:** Customer
**Trigger:** `submit` action — Step 2 of 10 (after customer_id returned from Step 1)

Adds the customer's primary residential address from Step 2 of the form. Uses the singular `/address` path (not `/addresses`).

### Path Parameters

| Name       | Type   | Description                         |
|------------|--------|-------------------------------------|
| bankId     | String | Bank identifier                     |
| customerId | String | Customer UUID from Step 1 response  |

### Request Body Fields

| Field        | Type         | Required | Description                               |
|--------------|--------------|----------|-------------------------------------------|
| line_1       | String       | Yes      | Primary street line e.g. "14 Ngong Road"  |
| line_2       | String       | No       | Secondary address e.g. "Karen Estate"     |
| line_3       | String       | No       | Third address line (null if unused)       |
| city         | String       | Yes      | City name e.g. "Nairobi"                  |
| county       | String       | No       | County e.g. "Nairobi County"              |
| state        | String       | No       | State/region e.g. "Nairobi"              |
| postcode     | String       | Yes      | Postal code e.g. "00502"                  |
| country_code | String       | Yes      | ISO 3166-1 alpha-2 e.g. "KE"             |
| tags         | List<String> | No       | e.g. ["HOME", "PRIMARY"]                  |
| status       | String       | No       | e.g. "ACTIVE"                             |

### Demo Data

| line_1        | line_2       | city    | postcode | country_code | tags              | status |
|---------------|--------------|---------|----------|--------------|-------------------|--------|
| 14 Ngong Road | Karen Estate | Nairobi | 00502    | KE           | HOME, PRIMARY     | ACTIVE |

### Error Codes

| Code | Message              | UI Handling                |
|------|----------------------|----------------------------|
| 400  | Invalid address      | Show VALIDATION_FAILED     |
| 401  | Unauthorized         | Navigate to login          |
| 404  | Customer not found   | Show SUBMIT_FAILED         |
| 500  | OBP server error     | Show SUBMIT_FAILED + retry |

---

## POST /obp/v3.1.0/banks/{bankId}/customers/{customerId}/tax-residence

**Auth:** DirectLogin
**Tag:** Customer
**Trigger:** `submit` action — Step 3 of 10

Records the customer's tax residence with the Kenya Revenue Authority (KRA) domain and tax identification number.

### Path Parameters

| Name       | Type   | Description                         |
|------------|--------|-------------------------------------|
| bankId     | String | Bank identifier                     |
| customerId | String | Customer UUID from Step 1 response  |

### Request Body Fields

| Field      | Type   | Required | Description                                  |
|------------|--------|----------|----------------------------------------------|
| domain     | String | Yes      | Tax authority domain e.g. "KRA"              |
| tax_number | String | Yes      | Tax identification number e.g. "A123456789K" |

### Demo Data

| domain | tax_number  |
|--------|-------------|
| KRA    | A123456789K |

### Error Codes

| Code | Message            | UI Handling                |
|------|--------------------|----------------------------|
| 400  | Invalid tax data   | Show VALIDATION_FAILED     |
| 401  | Unauthorized       | Navigate to login          |
| 500  | OBP server error   | Show SUBMIT_FAILED + retry |

---

## PUT /obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_documents/{kycDocumentId}

**Auth:** DirectLogin
**Tag:** KYC
**Trigger:** `submit` action — Step 4 of 10 (caller supplies kycDocumentId UUID)

Uploads the KYC identity document record. Records metadata for the uploaded document; binary images are handled by `DocumentUploadService` prior to this call.

### Path Parameters

| Name          | Type   | Description                                |
|---------------|--------|--------------------------------------------|
| bankId        | String | Bank identifier                            |
| customerId    | String | Customer UUID from Step 1 response         |
| kycDocumentId | String | Caller-supplied UUID for the KYC document  |

### Request Body Fields

| Field           | Type   | Required | Description                               |
|-----------------|--------|----------|-------------------------------------------|
| customer_number | String | Yes      | Internal customer number                  |
| type            | String | Yes      | Document type e.g. "NATIONAL_ID"          |
| number          | String | Yes      | Document number e.g. "34567890"           |
| issue_date      | String | Yes      | ISO-8601 date of issue                    |
| expiry_date     | String | Yes      | ISO-8601 date of expiry                   |
| description     | String | No       | Human-readable description                |

### Demo Data

| customer_number | type        | number   | issue_date | expiry_date | description                             |
|-----------------|-------------|----------|------------|-------------|-----------------------------------------|
| EQKE-2026-00221 | NATIONAL_ID | 34567890 | 2018-03-10 | 2028-03-09  | Kenya National ID Card — front and back |

### Error Codes

| Code | Message               | UI Handling                |
|------|-----------------------|----------------------------|
| 400  | Invalid document data | Show UPLOAD_FAILED         |
| 401  | Unauthorized          | Navigate to login          |
| 404  | Customer not found    | Show SUBMIT_FAILED         |
| 500  | OBP server error      | Show UPLOAD_FAILED + retry |

---

## PUT /obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_check/{kycCheckId}

**Auth:** DirectLogin
**Tag:** KYC
**Trigger:** `submit` action — Step 5 of 10 (caller supplies kycCheckId UUID)

Records the KYC verification check result performed by the Field Officer during the onboarding session.

### Path Parameters

| Name       | Type   | Description                               |
|------------|--------|-------------------------------------------|
| bankId     | String | Bank identifier                           |
| customerId | String | Customer UUID from Step 1 response        |
| kycCheckId | String | Caller-supplied UUID for the KYC check    |

### Request Body Fields

| Field           | Type    | Required | Description                                      |
|-----------------|---------|----------|--------------------------------------------------|
| customer_number | String  | Yes      | Internal customer number                         |
| date            | String  | Yes      | ISO-8601 datetime of check                       |
| how             | String  | Yes      | Method: "in_person", "video_call", "document"    |
| staff_user_id   | String  | Yes      | Field officer user ID                            |
| staff_name      | String  | Yes      | Field officer display name                       |
| satisfied       | Boolean | Yes      | Whether KYC check was satisfied                  |
| comments        | String  | No       | Notes on check procedure                         |

### Demo Data

| customer_number | date                 | how       | staff_name     | satisfied | comments                                                                            |
|-----------------|----------------------|-----------|----------------|-----------|-------------------------------------------------------------------------------------|
| EQKE-2026-00221 | 2026-05-22T11:00:00Z | in_person | Amina Odhiambo | true      | Original national ID verified. Selfie matched. Address confirmed via utility bill.  |

### Error Codes

| Code | Message            | UI Handling                |
|------|--------------------|----------------------------|
| 400  | Invalid check data | Show SUBMIT_FAILED         |
| 401  | Unauthorized       | Navigate to login          |
| 500  | OBP server error   | Show SUBMIT_FAILED + retry |

---

## PUT /obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_statuses

**Auth:** DirectLogin
**Tag:** KYC
**Trigger:** `submit` action — Step 6 of 10 (no ID in path — appends new status entry)

Sets the customer's KYC status to approved after all checks pass. Uses the plural `/kyc_statuses` path with no trailing UUID — each call appends a new status row.

### Path Parameters

| Name       | Type   | Description                         |
|------------|--------|-------------------------------------|
| bankId     | String | Bank identifier                     |
| customerId | String | Customer UUID from Step 1 response  |

### Request Body Fields

| Field           | Type    | Required | Description                         |
|-----------------|---------|----------|-------------------------------------|
| customer_number | String  | Yes      | Internal customer number            |
| ok              | Boolean | Yes      | KYC passed: true / failed: false    |
| date            | String  | Yes      | ISO-8601 datetime of status update  |

### Demo Data

| customer_number | ok   | date                 |
|-----------------|------|----------------------|
| EQKE-2026-00221 | true | 2026-05-22T11:30:00Z |

### Error Codes

| Code | Message              | UI Handling                |
|------|----------------------|----------------------------|
| 400  | Invalid status data  | Show SUBMIT_FAILED         |
| 401  | Unauthorized         | Navigate to login          |
| 500  | OBP server error     | Show SUBMIT_FAILED + retry |

---

## POST /obp/v4.0.0/banks/{bankId}/customers/{customerId}/attribute

**Auth:** DirectLogin
**Tag:** Customer-Attribute
**Trigger:** `submit` action — Step 7 of 10 (singular `/attribute` path)

Adds a customer-level attribute for supplementary metadata — records the customer's preferred language.

### Path Parameters

| Name       | Type   | Description                         |
|------------|--------|-------------------------------------|
| bankId     | String | Bank identifier                     |
| customerId | String | Customer UUID from Step 1 response  |

### Request Body Fields

| Field | Type   | Required | Description                                     |
|-------|--------|----------|-------------------------------------------------|
| name  | String | Yes      | Attribute key e.g. "PREFERRED_LANGUAGE"         |
| type  | String | Yes      | Value type: "STRING", "INTEGER", "BOOLEAN"      |
| value | String | Yes      | Attribute value e.g. "SWAHILI"                  |

### Demo Data

| name               | type   | value   |
|--------------------|--------|---------|
| PREFERRED_LANGUAGE | STRING | SWAHILI |

### Error Codes

| Code | Message           | UI Handling                |
|------|-------------------|----------------------------|
| 400  | Invalid attribute | Show SUBMIT_FAILED         |
| 401  | Unauthorized      | Navigate to login          |
| 500  | OBP server error  | Show SUBMIT_FAILED + retry |

---

## POST /obp/v4.0.0/banks/{bankId}/user_customer_links

**Auth:** DirectLogin
**Tag:** Customer
**Trigger:** `submit` action — Step 8 of 10 (underscore path: `user_customer_links`)

Links the authenticated OBP user account to the newly created customer record, enabling self-service access.

### Path Parameters

| Name   | Type   | Description     |
|--------|--------|-----------------|
| bankId | String | Bank identifier |

### Request Body Fields

| Field                 | Type    | Required | Description                                   |
|-----------------------|---------|----------|-----------------------------------------------|
| user_id               | String  | Yes      | OBP user UUID                                 |
| customer_id           | String  | Yes      | Customer UUID from Step 1 response            |
| can_see_private_alias | Boolean | No       | Allow user to see private alias; default false |

### Demo Data

| user_id              | customer_id        | can_see_private_alias |
|----------------------|--------------------|-----------------------|
| user-kipchoge-rotich | cust-ke-002-rotich | true                  |

### Error Codes

| Code | Message                    | UI Handling                |
|------|----------------------------|----------------------------|
| 400  | Invalid link data          | Show SUBMIT_FAILED         |
| 401  | Unauthorized               | Navigate to login          |
| 404  | User or customer not found | Show SUBMIT_FAILED         |
| 500  | OBP server error           | Show SUBMIT_FAILED + retry |

---

## POST /obp/v3.1.0/banks/{bankId}/account-applications

**Auth:** DirectLogin
**Tag:** Account-Application
**Trigger:** `submit` action — Step 9 of 10 (hyphen path: `account-applications`)

Creates an account application for a standard KES savings product tied to the new customer.

### Path Parameters

| Name   | Type   | Description     |
|--------|--------|-----------------|
| bankId | String | Bank identifier |

### Request Body Fields

| Field                     | Type   | Required | Description                                        |
|---------------------------|--------|----------|----------------------------------------------------|
| product_code              | String | Yes      | Bank product code e.g. "SAVINGS_KES_STANDARD"      |
| user_id                   | String | Yes      | OBP user UUID                                      |
| customer_id               | String | Yes      | Customer UUID from Step 1 response                 |
| proposed_balance.currency | String | No       | Opening balance currency e.g. "KES"                |
| proposed_balance.amount   | String | No       | Opening balance e.g. "5000.00"                     |

### Response Fields

| Field                  | Type   | Description                        |
|------------------------|--------|------------------------------------|
| account_application_id | String | Created application UUID           |

### Demo Data

| product_code         | user_id              | customer_id        | proposed_balance.currency | proposed_balance.amount |
|----------------------|----------------------|--------------------|---------------------------|-------------------------|
| SAVINGS_KES_STANDARD | user-kipchoge-rotich | cust-ke-002-rotich | KES                       | 5000.00                 |

### Error Codes

| Code | Message                   | UI Handling                |
|------|---------------------------|----------------------------|
| 400  | Invalid application data  | Show SUBMIT_FAILED         |
| 401  | Unauthorized              | Navigate to login          |
| 404  | Product not found         | Show SUBMIT_FAILED         |
| 500  | OBP server error          | Show SUBMIT_FAILED + retry |

---

## POST /obp/v5.0.0/banks/{bankId}/customer-account-links

**Auth:** DirectLogin
**Tag:** Customer
**Trigger:** `submit` action — Step 10 of 10 (hyphen path: `customer-account-links`). Final step — on success navigates to kyc-review.

Links the customer to their newly created account. The account_id is obtained from the account application approval or direct account creation response.

### Path Parameters

| Name   | Type   | Description     |
|--------|--------|-----------------|
| bankId | String | Bank identifier |

### Request Body Fields

| Field             | Type   | Required | Description                                         |
|-------------------|--------|----------|-----------------------------------------------------|
| customer_id       | String | Yes      | Customer UUID from Step 1 response                  |
| account_id        | String | Yes      | Account UUID from account-application or creation   |
| relationship_type | String | Yes      | e.g. "OWNER", "JOINT", "AGENT"                      |

### Demo Data

| customer_id        | account_id                    | relationship_type |
|--------------------|-------------------------------|-------------------|
| cust-ke-002-rotich | acct-ke-003-rotich-savings    | OWNER             |

### Error Codes

| Code | Message                        | UI Handling                |
|------|--------------------------------|----------------------------|
| 400  | Invalid link data              | Show SUBMIT_FAILED         |
| 401  | Unauthorized                   | Navigate to login          |
| 404  | Customer or account not found  | Show SUBMIT_FAILED         |
| 500  | OBP server error               | Show SUBMIT_FAILED + retry |

---

_Generated by /idea export | 2026-05-30_
