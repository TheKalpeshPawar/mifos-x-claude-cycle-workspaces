# API Reference — Application Detail

| Field      | Value                                        |
|------------|----------------------------------------------|
| Feature    | application-detail                           |
| Base URL   | https://apisandbox.openbankproject.com       |
| Auth       | DirectLogin — header: `DirectLogin token=<token>` |

---

## Fetch Application Detail

**GET** `/obp/v5.1.0/banks/{bankId}/account-applications/{applicationId}`

**Auth:** DirectLogin

**Path Params:**

| Param         | Type   | Description                   |
|---------------|--------|-------------------------------|
| bankId        | String | OBP bank identifier           |
| applicationId | String | Account application UUID      |

**Response Example:**
```json
{
  "account_application_id": "app-uuid-001",
  "product_code": "SAVINGS_KCB_001",
  "user": {
    "user_id": "obp-user-uuid",
    "provider": "obp",
    "username": "john.mwangi"
  },
  "customer": {
    "customer_id": "customer-uuid-001",
    "customer_number": "CUST-20260520-001"
  },
  "date_of_application": "2026-05-20T10:30:00Z",
  "date_last_modified": "2026-05-20T10:30:00Z",
  "status": "PENDING",
  "account_routing": {
    "scheme": "IBAN",
    "address": ""
  }
}
```

**Response Fields:**

| Field                  | Type   | Description                                      |
|------------------------|--------|--------------------------------------------------|
| account_application_id | String | Application UUID                                 |
| product_code           | String | Banking product code ("SAVINGS_KCB_001")        |
| user.user_id           | String | OBP user UUID of the applicant                   |
| user.username          | String | OBP username                                     |
| customer.customer_id   | String | Customer UUID                                    |
| customer.customer_number| String| Bank-assigned customer number                   |
| date_of_application    | String | ISO-8601 submission timestamp                    |
| date_last_modified     | String | ISO-8601 last modification timestamp             |
| status                 | String | PENDING \| APPROVED \| REJECTED                 |
| account_routing        | Object | scheme + address (populated post-approval)       |

**Errors:**

| Code | Error                | Description                        |
|------|----------------------|------------------------------------|
| 400  | BAD_REQUEST          | Malformed request                  |
| 401  | UNAUTHORIZED         | Invalid DirectLogin token          |
| 404  | APPLICATION_NOT_FOUND| No application with this ID        |

---

## Update Application Status (Approve / Reject)

**PUT** `/obp/v5.1.0/banks/{bankId}/account-applications/{applicationId}`

**Auth:** DirectLogin

**Path Params:**

| Param         | Type   | Description                   |
|---------------|--------|-------------------------------|
| bankId        | String | OBP bank identifier           |
| applicationId | String | Account application UUID      |

**Request Body (Approve):**
```json
{
  "status": "APPROVED"
}
```

**Request Body (Reject):**
```json
{
  "status": "REJECTED"
}
```

**Request Fields:**

| Field  | Type   | Values                      | Description                    |
|--------|--------|-----------------------------|--------------------------------|
| status | String | APPROVED \| REJECTED        | Decision on the application    |

**Response Example:**
```json
{
  "account_application_id": "app-uuid-001",
  "status": "APPROVED",
  "date_last_modified": "2026-05-25T14:22:00Z"
}
```

**Response Fields:**

| Field                  | Type   | Description                      |
|------------------------|--------|----------------------------------|
| account_application_id | String | Application UUID                 |
| status                 | String | Updated status (APPROVED/REJECTED)|
| date_last_modified     | String | ISO-8601 timestamp of decision   |

**Errors:**

| Code | Error                | Description                              |
|------|----------------------|------------------------------------------|
| 400  | VALIDATION_FAILED    | Invalid status value                     |
| 401  | UNAUTHORIZED         | Invalid DirectLogin token                |
| 404  | APPLICATION_NOT_FOUND| No application with this ID             |

---

## Decision Flow — Sequence

```
Field Officer reviews application OBP-2026-00234 (John Kamau Mwangi)

Approve flow:
  1. Officer adds review notes (local only — not sent to OBP)
  2. PUT /banks/{bankId}/account-applications/{applicationId}
     body: { "status": "APPROVED" }
  3. On 200: show success banner "Application approved successfully"
  4. Navigate to customer-detail after short delay

Reject flow:
  1. PUT /banks/{bankId}/account-applications/{applicationId}
     body: { "status": "REJECTED" }
  2. On 200: show rejection banner, stay on screen

Request Information flow:
  1. No API call — navigate to customer-messages
  2. customer-messages opens with pre-filled context about this application
```

---

## Supporting: Fetch KYC Status (for kyc_status_row display)

**GET** `/obp/v5.1.0/customers/{customerId}/kyc_documents`

Used to determine whether the KYC verified row should show "Verified ✓" (green) or a pending state. The detail screen reads this in parallel with the application fetch.

**Response Fields:** kyc_document_id, customer_id, type, status, is_valid

See kyc-review API.md for full reference.

---

*Generated by /idea export | 2026-05-25*
