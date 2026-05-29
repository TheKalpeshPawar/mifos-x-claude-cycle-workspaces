# API Reference — KYC Document Review

| Field    | Value                                            |
|----------|--------------------------------------------------|
| Feature  | kyc-review                                       |
| Base URL | https://apisandbox.openbankproject.com           |
| Auth     | DirectLogin — header: `DirectLogin token=<token>`|

---

## GET /obp/v5.1.0/customers/{customerId}/kyc_documents

**Auth:** DirectLogin
**Tag:** KYC
**Trigger:** `loadDocuments()` on screen entry

### Path Parameters

| Name       | Type   | Description     |
|------------|--------|-----------------|
| customerId | String | Customer UUID   |

### Response Fields

| Field           | Type    | Description                                     |
|-----------------|---------|-------------------------------------------------|
| kyc_document_id | String  | Document UUID                                   |
| customer_id     | String  | Owning customer UUID                            |
| type            | String  | NATIONAL_ID / SELFIE / PROOF_OF_ADDRESS         |
| status          | String  | UPLOADED / PENDING / VERIFIED                   |
| date_added      | String  | ISO-8601 timestamp                              |
| is_valid        | Boolean | Whether document has been validated             |

### Error Codes

| Code | Error              |
|------|--------------------|
| 400  | BAD_REQUEST        |
| 401  | UNAUTHORIZED       |
| 404  | CUSTOMER_NOT_FOUND |

---

## PUT /obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_documents/{documentId}

**Auth:** DirectLogin
**Tag:** KYC
**Trigger:** `approve_kyc()` — called per document before recording the KYC check

### Path Parameters

| Name       | Type   | Description                    |
|------------|--------|--------------------------------|
| bankId     | String | OBP bank identifier            |
| customerId | String | Customer UUID                  |
| documentId | String | KYC document UUID (caller-supplied) |

### Request Body

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

### Response Fields

| Field           | Type    | Description                 |
|-----------------|---------|-----------------------------|
| kyc_document_id | String  | Document UUID               |
| status          | String  | Updated document status     |
| is_valid        | Boolean | Validation result           |
| last_updated    | String  | ISO-8601 update timestamp   |

### Error Codes

| Code | Error              |
|------|--------------------|
| 400  | VALIDATION_FAILED  |
| 401  | UNAUTHORIZED       |
| 404  | DOCUMENT_NOT_FOUND |

---

## PUT /obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_check/{kycCheckId}

**Auth:** DirectLogin
**Tag:** KYC
**Trigger:** `approve_kyc()` or `reject_kyc()` — records the officer's decision with method and notes

### Path Parameters

| Name       | Type   | Description                        |
|------------|--------|------------------------------------|
| bankId     | String | OBP bank identifier                |
| customerId | String | Customer UUID                      |
| kycCheckId | String | Check UUID — caller-supplied       |

### Request Fields

| Field           | Type    | Notes                                      |
|-----------------|---------|--------------------------------------------|
| customer_number | String  | Bank-assigned customer number              |
| date            | String  | ISO-8601 timestamp of check                |
| how             | String  | `in_person` \| `online` \| `postal`       |
| staff_user_id   | String  | OBP user ID of reviewing officer           |
| staff_name      | String  | Display name of officer                    |
| satisfied       | Boolean | `true` = approved, `false` = rejected      |
| comments        | String  | Approval notes or rejection reason text    |

### Request Body (Approval)

```json
{
  "customer_number": "CUST-20260525-001",
  "date": "2026-05-29T00:00:00Z",
  "how": "in_person",
  "staff_user_id": "officer-uid-001",
  "staff_name": "Field Officer Njoroge",
  "satisfied": true,
  "comments": "National ID front verified. Selfie liveness passed. Risk: Low."
}
```

### Request Body (Rejection)

```json
{
  "customer_number": "CUST-20260525-001",
  "date": "2026-05-29T00:00:00Z",
  "how": "in_person",
  "staff_user_id": "officer-uid-001",
  "staff_name": "Field Officer Njoroge",
  "satisfied": false,
  "comments": "National ID back side not uploaded. Selfie does not match ID photo."
}
```

### Response Fields

| Field     | Type    | Description              |
|-----------|---------|--------------------------|
| id        | String  | KYC check UUID           |
| satisfied | Boolean | Decision as recorded     |

### Error Codes

| Code | Error             |
|------|-------------------|
| 400  | VALIDATION_FAILED |
| 401  | UNAUTHORIZED      |

---

## PUT /obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_statuses

**Auth:** DirectLogin
**Tag:** KYC
**Trigger:** Final call after kyc_check — appends a status entry to the customer's KYC timeline

Note: No document ID in path. Each call appends a new entry; does not overwrite prior entries.

### Path Parameters

| Name       | Type   | Description         |
|------------|--------|---------------------|
| bankId     | String | OBP bank identifier |
| customerId | String | Customer UUID       |

### Request Fields

| Field           | Type    | Notes                                      |
|-----------------|---------|--------------------------------------------|
| customer_number | String  | Bank-assigned customer number              |
| ok              | Boolean | `true` = KYC approved, `false` = rejected  |
| date            | String  | ISO-8601 timestamp of status change        |

### Request Body (Approve)

```json
{
  "customer_number": "CUST-20260525-001",
  "ok": true,
  "date": "2026-05-29T00:00:00Z"
}
```

### Request Body (Reject)

```json
{
  "customer_number": "CUST-20260525-001",
  "ok": false,
  "date": "2026-05-29T00:00:00Z"
}
```

### Response Fields

| Field | Type    | Description               |
|-------|---------|---------------------------|
| ok    | Boolean | Status value as recorded  |

### Error Codes

| Code | Error             |
|------|-------------------|
| 400  | VALIDATION_FAILED |
| 401  | UNAUTHORIZED      |

---

## KYC Review — API Call Sequence

```
APPROVE flow:
  1. PUT kyc_documents/{id}  for each verified document (is_valid: true)
  2. PUT kyc_check/{checkId} (satisfied: true, how: in_person, comments: risk notes)
  3. PUT kyc_statuses        (ok: true)
  4. Navigate to customer-detail

REJECT flow:
  1. PUT kyc_check/{checkId} (satisfied: false, comments: rejection reason)
  2. PUT kyc_statuses        (ok: false)
  3. Show rejection banner on kyc-review
```

---

_Generated by /idea export | 2026-05-29_
