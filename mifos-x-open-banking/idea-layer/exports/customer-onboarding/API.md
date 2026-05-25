# API Reference — New Customer Onboarding

| Field      | Value                                        |
|------------|----------------------------------------------|
| Feature    | customer-onboarding                          |
| Base URL   | https://apisandbox.openbankproject.com       |
| Auth       | DirectLogin — header: `DirectLogin token=<token>` |

---

## Step 1 — Create Customer

**POST** `/obp/v5.0.0/banks/{bankId}/customers`

**Auth:** DirectLogin

**Path Params:**

| Param  | Type   | Description         |
|--------|--------|---------------------|
| bankId | String | OBP bank identifier |

**Request Body:**
```json
{
  "legal_name": "John Kamau Mwangi",
  "mobile_phone_number": "+254722123456",
  "email": "john.mwangi@gmail.com",
  "face_image": {
    "url": "https://...",
    "date": "2026-05-25"
  },
  "date_of_birth": "1985-03-14",
  "relationship_status": "SINGLE",
  "dependants": 0,
  "highest_education_attained": "UNIVERSITY",
  "employment_status": "EMPLOYED",
  "kyc_status": false,
  "last_ok_date": "2026-05-25T00:00:00Z",
  "credit_rating": { "rating": "A", "source": "Metropol" },
  "credit_limit": { "currency": "KES", "amount": "500000.00" },
  "title": "Mr",
  "branch_id": "BRANCH_001",
  "nationality": "Kenyan",
  "customer_number": "CUST-20260525-001"
}
```

**Response Fields:**

| Field           | Type    | Description              |
|-----------------|---------|--------------------------|
| customer_id     | String  | Unique customer UUID     |
| legal_name      | String  | Full legal name          |
| customer_number | String  | Bank-assigned number     |
| kyc_status      | Boolean | Initial KYC status       |

**Errors:** 400 VALIDATION_FAILED · 401 UNAUTHORIZED · 409 CUSTOMER_ALREADY_EXISTS

---

## Step 2 — Add Customer Address

**POST** `/obp/v3.1.0/banks/{bankId}/customers/{customerId}/address`

**Request Body:**
```json
{
  "line_1": "123 Moi Avenue",
  "line_2": "",
  "line_3": "",
  "city": "Nairobi",
  "county": "Nairobi",
  "state": "Nairobi County",
  "postcode": "00100",
  "country_code": "KE",
  "tags": ["primary"],
  "status": "OBP_ADDRESS_STATUS_REGISTERED"
}
```

**Response Fields:** address_id, status

**Errors:** 400 VALIDATION_FAILED · 401 UNAUTHORIZED · 404 CUSTOMER_NOT_FOUND

---

## Step 3 — Add Tax Residence

**POST** `/obp/v3.1.0/banks/{bankId}/customers/{customerId}/tax-residence`

**Request Body:**
```json
{
  "domain": "INDIVIDUAL",
  "tax_number": "KE12345678",
  "date": "2026-05-25T00:00:00Z"
}
```

**Response Fields:** tax_residence_id, tax_number, domain

**Errors:** 400 VALIDATION_FAILED · 401 UNAUTHORIZED

---

## Step 4 — Upload KYC Document

**PUT** `/obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_documents/{kycDocumentId}`

Note: `kycDocumentId` is caller-supplied (client generates a UUID).

**Request Body:**
```json
{
  "customer_number": "CUST-20260525-001",
  "type": "NATIONAL_ID",
  "number": "KE12345678",
  "issue_date": "2020-01-15T00:00:00Z",
  "issue_place": "Nairobi",
  "expiry_date": "2030-01-14T00:00:00Z"
}
```

**Response Fields:** kyc_document_id, customer_id, type, number, is_valid

**Errors:** 400 VALIDATION_FAILED · 401 UNAUTHORIZED · 404 CUSTOMER_NOT_FOUND

---

## Step 5 — Record KYC Check

**PUT** `/obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_check/{kycCheckId}`

Note: `kycCheckId` is caller-supplied.

**Request Body:**
```json
{
  "customer_number": "CUST-20260525-001",
  "date": "2026-05-25T00:00:00Z",
  "how": "in_person",
  "staff_user_id": "officer-uid-001",
  "staff_name": "Field Officer Njoroge",
  "satisfied": true,
  "comments": "Identity verified in person. Documents match."
}
```

**Response Fields:** id, satisfied

**Errors:** 400 VALIDATION_FAILED · 401 UNAUTHORIZED

---

## Step 6 — Set KYC Status

**PUT** `/obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_statuses`

Note: No ID in path — this call appends to the status timeline.

**Request Body:**
```json
{
  "customer_number": "CUST-20260525-001",
  "ok": true,
  "date": "2026-05-25T00:00:00Z"
}
```

**Response Fields:** ok (Boolean)

**Errors:** 400 VALIDATION_FAILED · 401 UNAUTHORIZED

---

## Step 7 — Add Customer Attribute

**POST** `/obp/v4.0.0/banks/{bankId}/customers/{customerId}/attribute`

Note: Singular path — `/attribute` not `/attributes`.

**Request Body:**
```json
{
  "name": "ONBOARDING_SOURCE",
  "type": "STRING",
  "value": "FIELD_OFFICER_APP"
}
```

**Response Fields:** customer_attribute_id, name, type, value

**Errors:** 400 VALIDATION_FAILED · 401 UNAUTHORIZED

---

## Step 8 — Link User to Customer

**POST** `/obp/v4.0.0/banks/{bankId}/user_customer_links`

Note: Underscore path — `user_customer_links`.

**Request Body:**
```json
{
  "user_id": "obp-user-uuid",
  "customer_id": "customer-uuid-from-step-1"
}
```

**Response Fields:** user_customer_link_id, user_id, customer_id

**Errors:** 400 VALIDATION_FAILED · 401 UNAUTHORIZED · 409 LINK_ALREADY_EXISTS

---

## Step 9 — Create Account Application

**POST** `/obp/v3.1.0/banks/{bankId}/account-applications`

**Request Body:**
```json
{
  "product_code": "SAVINGS_KCB_001",
  "user_id": "obp-user-uuid",
  "customer_id": "customer-uuid-from-step-1"
}
```

**Response Fields:** account_application_id, product_code, user, customer, date_of_application, status

**Errors:** 400 VALIDATION_FAILED · 401 UNAUTHORIZED

---

## Step 10 — Link Customer to Account

**POST** `/obp/v5.0.0/banks/{bankId}/customer-account-links`

Note: Hyphen path — `customer-account-links`.

**Request Body:**
```json
{
  "customer_id": "customer-uuid-from-step-1",
  "account_id": "account-uuid",
  "relationship_type": "OWNER"
}
```

**Response Fields:** customer_account_link_id, customer_id, account_id, relationship_type

**Errors:** 400 VALIDATION_FAILED · 401 UNAUTHORIZED · 404 ACCOUNT_NOT_FOUND

---

*Generated by /idea export | 2026-05-25*
