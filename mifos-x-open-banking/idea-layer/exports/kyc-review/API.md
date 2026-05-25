# API Reference — KYC Document Review

| Field      | Value                                        |
|------------|----------------------------------------------|
| Feature    | kyc-review                                   |
| Base URL   | https://apisandbox.openbankproject.com       |
| Auth       | DirectLogin — header: `DirectLogin token=<token>` |

---

## Fetch KYC Documents

**GET** `/obp/v5.1.0/customers/{customerId}/kyc_documents`

**Auth:** DirectLogin

**Path Params:**

| Param      | Type   | Description         |
|------------|--------|---------------------|
| customerId | String | Customer UUID       |

**Response Fields:**

| Field           | Type    | Description                              |
|-----------------|---------|------------------------------------------|
| kyc_document_id | String  | Document UUID                            |
| customer_id     | String  | Owning customer UUID                     |
| type            | String  | NATIONAL_ID / SELFIE / PROOF_OF_ADDRESS  |
| status          | String  | UPLOADED / PENDING / VERIFIED            |
| date_added      | String  | ISO-8601 timestamp                       |
| is_valid        | Boolean | Whether document has been validated      |

**Errors:**

| Code | Error               |
|------|---------------------|
| 400  | BAD_REQUEST         |
| 401  | UNAUTHORIZED        |
| 404  | CUSTOMER_NOT_FOUND  |

---

## Update KYC Document Status

**PUT** `/obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_documents/{documentId}`

**Auth:** DirectLogin

**Path Params:**

| Param      | Type   | Description                        |
|------------|--------|------------------------------------|
| bankId     | String | OBP bank identifier                |
| customerId | String | Customer UUID                      |
| documentId | String | KYC document UUID (caller-supplied) |

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

**Response Fields:**

| Field           | Type    | Description                     |
|-----------------|---------|---------------------------------|
| kyc_document_id | String  | Document UUID                   |
| status          | String  | Updated document status         |
| is_valid        | Boolean | Validation result               |
| last_updated    | String  | ISO-8601 timestamp              |

**Errors:**

| Code | Error               |
|------|---------------------|
| 400  | VALIDATION_FAILED   |
| 401  | UNAUTHORIZED        |
| 404  | DOCUMENT_NOT_FOUND  |

---

## Record KYC Check

**PUT** `/obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_check/{kycCheckId}`

**Auth:** DirectLogin

**Path Params:**

| Param      | Type   | Description                          |
|------------|--------|--------------------------------------|
| bankId     | String | OBP bank identifier                  |
| customerId | String | Customer UUID                        |
| kycCheckId | String | Check UUID — caller-supplied         |

**Request Body (Approval):**
```json
{
  "customer_number": "CUST-20260525-001",
  "date": "2026-05-25T00:00:00Z",
  "how": "in_person",
  "staff_user_id": "officer-uid-001",
  "staff_name": "Field Officer Njoroge",
  "satisfied": true,
  "comments": "National ID front verified. Selfie matches. Risk: Low."
}
```

**Request Body (Rejection):**
```json
{
  "customer_number": "CUST-20260525-001",
  "date": "2026-05-25T00:00:00Z",
  "how": "in_person",
  "staff_user_id": "officer-uid-001",
  "staff_name": "Field Officer Njoroge",
  "satisfied": false,
  "comments": "National ID does not match selfie. Blurry documents."
}
```

**Request Fields:**

| Field         | Type    | Notes                                   |
|---------------|---------|-----------------------------------------|
| customer_number | String | Bank-assigned customer number         |
| date          | String  | ISO-8601 timestamp of check            |
| how           | String  | `in_person` \| `online` \| `postal`   |
| staff_user_id | String  | OBP user ID of the reviewing officer   |
| staff_name    | String  | Display name of the officer            |
| satisfied     | Boolean | true = approved, false = rejected      |
| comments      | String  | Rejection reason or approval notes     |

**Response Fields:**

| Field     | Type    | Description              |
|-----------|---------|--------------------------|
| id        | String  | KYC check UUID           |
| satisfied | Boolean | Decision recorded        |

**Errors:** 400 VALIDATION_FAILED · 401 UNAUTHORIZED

---

## Set KYC Status

**PUT** `/obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_statuses`

**Auth:** DirectLogin

Note: No ID in path. Each call **appends** a new entry to the customer's KYC status timeline.

**Path Params:**

| Param      | Type   | Description         |
|------------|--------|---------------------|
| bankId     | String | OBP bank identifier |
| customerId | String | Customer UUID       |

**Request Body (Approve — ok: true):**
```json
{
  "customer_number": "CUST-20260525-001",
  "ok": true,
  "date": "2026-05-25T00:00:00Z"
}
```

**Request Body (Reject — ok: false):**
```json
{
  "customer_number": "CUST-20260525-001",
  "ok": false,
  "date": "2026-05-25T00:00:00Z"
}
```

**Request Fields:**

| Field           | Type    | Notes                                    |
|-----------------|---------|------------------------------------------|
| customer_number | String  | Bank-assigned customer number            |
| ok              | Boolean | true = KYC approved, false = rejected    |
| date            | String  | ISO-8601 timestamp of status change      |

**Response Fields:**

| Field | Type    | Description               |
|-------|---------|---------------------------|
| ok    | Boolean | Status value as recorded  |

**Errors:** 400 VALIDATION_FAILED · 401 UNAUTHORIZED

---

## KYC Review Flow — Sequence

```
Field Officer taps Approve
  → PUT kyc_documents/{id}   (is_valid: true for each verified document)
  → PUT kyc_check/{id}       (satisfied: true, how: in_person)
  → PUT kyc_statuses         (ok: true)
  → Navigate to customer-detail

Field Officer taps Reject (with rejection reason)
  → PUT kyc_check/{id}       (satisfied: false, comments: reason)
  → PUT kyc_statuses         (ok: false)
  → Stay on kyc-review with rejection banner
```

---

*Generated by /idea export | 2026-05-25*
