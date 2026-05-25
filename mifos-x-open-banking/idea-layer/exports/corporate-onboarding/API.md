# API Reference — Corporate Customer Onboarding

| Field      | Value                                        |
|------------|----------------------------------------------|
| Feature    | corporate-onboarding                         |
| Base URL   | https://apisandbox.openbankproject.com       |
| Auth       | DirectLogin — header: `DirectLogin token=<token>` |

---

## Create Corporate Customer

**POST** `/obp/v5.1.0/banks/{bankId}/customers`

**Auth:** DirectLogin

**Path Params:**

| Param  | Type   | Description         |
|--------|--------|---------------------|
| bankId | String | OBP bank identifier |

**Request Body:**
```json
{
  "legal_name": "Kamau Enterprises Limited",
  "mobile_phone_number": "+254201234567",
  "email": "info@kamauenterprises.co.ke",
  "face_image": {
    "url": "https://...",
    "date": "2026-05-25"
  },
  "date_of_birth": "2019-01-01",
  "relationship_status": "CORPORATE",
  "dependants": 0,
  "highest_education_attained": "N/A",
  "employment_status": "SELF_EMPLOYED",
  "kyc_status": false,
  "last_ok_date": "2026-05-25T00:00:00Z",
  "credit_rating": { "rating": "B", "source": "CRB_KENYA" },
  "credit_limit": { "currency": "KES", "amount": "5000000.00" },
  "title": "Corp",
  "branch_id": "BRANCH_001",
  "nationality": "Kenyan",
  "customer_number": "CORP-20260525-001",
  "customer_type": "CORPORATE"
}
```

**Response Fields:**

| Field           | Type    | Description                      |
|-----------------|---------|----------------------------------|
| customer_id     | String  | Unique customer UUID             |
| legal_name      | String  | Registered company name          |
| customer_number | String  | Bank-assigned customer number    |
| customer_type   | String  | "CORPORATE"                      |
| kyc_status      | Boolean | Initial KYC status (false)       |

**Errors:**

| Code | Error                    | Description                           |
|------|--------------------------|---------------------------------------|
| 400  | VALIDATION_FAILED        | Missing or invalid required fields    |
| 401  | UNAUTHORIZED             | Invalid or expired DirectLogin token  |
| 409  | CUSTOMER_ALREADY_EXISTS  | Customer with same number exists      |

---

## Beneficial Owner Registration (repeated per owner)

Beneficial owners are linked via the customer attribute endpoint after company creation.

**POST** `/obp/v4.0.0/banks/{bankId}/customers/{customerId}/attribute`

**Request Body (Owner 1 — James Otieno Kamau):**
```json
{
  "name": "BENEFICIAL_OWNER_1",
  "type": "STRING",
  "value": "{\"name\":\"James Otieno Kamau\",\"id\":\"KE78901234\",\"ownership_percent\":60}"
}
```

**Request Body (Owner 2 — Grace Wanjiku Muthoni):**
```json
{
  "name": "BENEFICIAL_OWNER_2",
  "type": "STRING",
  "value": "{\"name\":\"Grace Wanjiku Muthoni\",\"id\":\"KE23456789\",\"ownership_percent\":25}"
}
```

**Response Fields:** customer_attribute_id, name, type, value

**Errors:** 400 VALIDATION_FAILED · 401 UNAUTHORIZED

---

## Upload Certificate of Incorporation (KYC Document)

**PUT** `/obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_documents/{kycDocumentId}`

**Request Body:**
```json
{
  "customer_number": "CORP-20260525-001",
  "type": "CERTIFICATE_OF_INCORPORATION",
  "number": "CPR/2019/123456",
  "issue_date": "2019-06-01T00:00:00Z",
  "issue_place": "Nairobi",
  "expiry_date": "2099-01-01T00:00:00Z"
}
```

**Response Fields:** kyc_document_id, customer_id, type, number, is_valid

**Errors:** 400 VALIDATION_FAILED · 401 UNAUTHORIZED · 404 CUSTOMER_NOT_FOUND

---

## Upload Tax Compliance Certificate (KYC Document)

**PUT** `/obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_documents/{kycDocumentId}`

**Request Body:**
```json
{
  "customer_number": "CORP-20260525-001",
  "type": "TAX_COMPLIANCE_CERTIFICATE",
  "number": "P051234567A",
  "issue_date": "2025-07-01T00:00:00Z",
  "issue_place": "Nairobi",
  "expiry_date": "2026-06-30T00:00:00Z"
}
```

**Response Fields:** kyc_document_id, customer_id, type, number, is_valid

---

## Set KYC Check (Corporate)

**PUT** `/obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_check/{kycCheckId}`

**Request Body:**
```json
{
  "customer_number": "CORP-20260525-001",
  "date": "2026-05-25T00:00:00Z",
  "how": "in_person",
  "staff_user_id": "officer-uid-001",
  "staff_name": "Field Officer Njoroge",
  "satisfied": true,
  "comments": "Certificate of incorporation and KRA PIN verified in person."
}
```

**Response Fields:** id, satisfied

---

## Set KYC Status (Corporate)

**PUT** `/obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_statuses`

**Request Body:**
```json
{
  "customer_number": "CORP-20260525-001",
  "ok": true,
  "date": "2026-05-25T00:00:00Z"
}
```

**Response Fields:** ok (Boolean)

---

## Create Account Application (Corporate)

**POST** `/obp/v3.1.0/banks/{bankId}/account-applications`

**Request Body:**
```json
{
  "product_code": "BUSINESS_CURRENT_001",
  "user_id": "obp-user-uuid",
  "customer_id": "corporate-customer-uuid"
}
```

**Response Fields:** account_application_id, product_code, user, customer, date_of_application, status

**Errors:** 400 VALIDATION_FAILED · 401 UNAUTHORIZED

---

*Generated by /idea export | 2026-05-25*
