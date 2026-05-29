# API Reference — New Customer Onboarding

| Field    | Value                                     |
|----------|-------------------------------------------|
| Feature  | customer-onboarding                       |
| Base URL | https://apisandbox.openbankproject.com    |

---

## POST /obp/v5.0.0/banks/{bankId}/customers

**Auth:** DirectLogin
**Tag:** Customer
**Trigger:** Step 1 — triggered by `submit` action after step 4 review, first call in the 10-step chain

### Path Parameters

| Name   | Type   | Value    |
|--------|--------|----------|
| bankId | String | gh.29.uk |

### Request Fields

| Field              | Type   | Required | Description                                      |
|--------------------|--------|----------|--------------------------------------------------|
| legal_name         | String | Yes      | Full name from first_name_input + last_name_input|
| mobile_phone_number| Object | Yes      | `{ prefix: "+254", number: "722123456" }`        |
| email              | String | No       | From email_input                                 |
| national_id_number | String | Yes      | From national_id_input (e.g., "KE12345678")      |
| date_of_birth      | String | Yes      | ISO-8601 date from dob_input (e.g., "1985-03-14")|
| customer_number    | String | Yes      | Generated unique customer reference              |

### Response Fields

| Field       | Type   | Description                                   |
|-------------|--------|-----------------------------------------------|
| customer_id | String | Unique OBP customer ID — used in all steps 2–10|
| legal_name  | String | Confirmed legal name stored                   |

### Error Codes

| Code | Message                                           |
|------|---------------------------------------------------|
| 400  | MISSING_REQUIRED_FIELD — required field absent    |
| 401  | UNAUTHORIZED — DirectLogin token expired          |
| 409  | CUSTOMER_ALREADY_EXISTS — duplicate national ID   |

---

## POST /obp/v3.1.0/banks/{bankId}/customers/{customerId}/address

**Auth:** DirectLogin
**Tag:** Customer
**Trigger:** Step 2 — immediately after customer_id is obtained

### Request Fields

| Field      | Type   | Required | Description                        |
|------------|--------|----------|------------------------------------|
| line_1     | String | Yes      | From street_input (e.g., "123 Moi Avenue") |
| city       | String | Yes      | From city_input (e.g., "Nairobi")  |
| county     | String | No       | From county_select (e.g., "Nairobi County") |
| postcode   | String | Yes      | From postcode_input (e.g., "00100")|
| country    | String | Yes      | ISO country code (e.g., "KE")      |
| status     | String | Yes      | "current"                          |

### Error Codes

| Code | Message                                 |
|------|-----------------------------------------|
| 400  | INVALID_ADDRESS — missing required line_1 or city |
| 401  | UNAUTHORIZED                            |
| 404  | CUSTOMER_NOT_FOUND                      |

---

## PUT /obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_documents/{kycDocumentId}

**Auth:** DirectLogin
**Tag:** KYC
**Trigger:** Step 4 in submission chain — uploads the selected ID document

### Request Fields

| Field        | Type   | Required | Description                                                  |
|--------------|--------|----------|--------------------------------------------------------------|
| customer_number | String | Yes | Customer number from step 1 response                        |
| type         | String | Yes      | From id_type_select: "PASSPORT", "NATIONAL_ID", "DRIVERS_LICENCE" |
| number       | String | Yes      | From national_id_input (e.g., "KE12345678")                 |
| issue_date   | String | Yes      | ISO-8601 issue date (collected during upload flow)           |
| issue_place  | String | Yes      | Issuing authority location                                   |
| expiry_date  | String | No       | ISO-8601 expiry date if applicable                           |

### Error Codes

| Code | Message                              |
|------|--------------------------------------|
| 400  | INVALID_KYC_DOCUMENT — missing fields|
| 401  | UNAUTHORIZED                         |
| 404  | CUSTOMER_NOT_FOUND                   |

---

## PUT /obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_statuses

**Auth:** DirectLogin
**Tag:** KYC
**Trigger:** Step 6 in submission chain — records overall KYC status

### Request Fields

| Field    | Type    | Required | Description                               |
|----------|---------|----------|-------------------------------------------|
| ok       | Boolean | Yes      | `true` if documents passed liveness check |
| date     | String  | Yes      | ISO-8601 timestamp of the check            |

### Error Codes

| Code | Message                       |
|------|-------------------------------|
| 400  | INVALID_KYC_STATUS            |
| 401  | UNAUTHORIZED                  |
| 404  | CUSTOMER_NOT_FOUND            |

---

## POST /obp/v3.1.0/banks/{bankId}/account-applications

**Auth:** DirectLogin
**Tag:** Account-Application
**Trigger:** Step 9 in submission chain — creates account application

### Request Fields

| Field        | Type   | Required | Description                                |
|--------------|--------|----------|--------------------------------------------|
| product_code | String | Yes      | Account product code (e.g., "CURRENT")     |
| user_id      | String | No       | OBP user ID if already existing            |
| customer_id  | String | Yes      | From step 1 response                       |

### Response Fields

| Field                  | Type   | Description                          |
|------------------------|--------|--------------------------------------|
| account_application_id | String | ID of the created application        |
| status                 | String | Initial status: "REQUESTED"          |

### Error Codes

| Code | Message                              |
|------|--------------------------------------|
| 400  | INVALID_APPLICATION — missing fields |
| 401  | UNAUTHORIZED                         |
| 500  | OBP server error                     |

---

_Generated by /idea export | 2026-05-29_
