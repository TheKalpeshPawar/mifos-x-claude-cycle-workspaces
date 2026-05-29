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
**Trigger:** `KycReviewViewModel.loadDocuments()` on screen entry / `RetryLoad` event

Fetches all KYC documents submitted by the customer. The ViewModel maps the response list into `List<KycDocument>` — each entry drives one document card in the UI. The `loading` state is shown while this call is in flight.

### Path Parameters

| Name       | Type   | Description         |
|------------|--------|---------------------|
| customerId | String | Customer identifier |

### Response Fields

| Field           | Type    | Description                                                                     |
|-----------------|---------|---------------------------------------------------------------------------------|
| kyc_document_id | String  | Unique document identifier                                                      |
| customer_id     | String  | Owner customer identifier                                                       |
| type            | String  | NATIONAL_ID / UTILITY_BILL / PASSPORT / KRA_PIN_CERTIFICATE                     |
| status          | String  | PENDING_REVIEW / VERIFIED / REJECTED                                            |
| date_added      | String  | ISO-8601 upload timestamp                                                       |
| is_valid        | Boolean | Whether the document has been validated                                          |

### Demo Data

| kyc_document_id      | customer_id          | type                | status         | date_added               | is_valid |
|----------------------|----------------------|---------------------|----------------|--------------------------|----------|
| kycd-ke-001-natid    | cust-ke-002-rotich   | NATIONAL_ID         | PENDING_REVIEW | 2026-05-22T11:00:00Z     | false    |
| kycd-ke-002-utility  | cust-ke-002-rotich   | UTILITY_BILL        | PENDING_REVIEW | 2026-05-22T11:05:00Z     | false    |
| kycd-ke-003-passport | cust-ke-003-atieno   | PASSPORT            | VERIFIED       | 2023-11-14T09:30:00Z     | true     |
| kycd-ke-004-kra      | cust-ke-001-wanjiru  | KRA_PIN_CERTIFICATE | VERIFIED       | 2024-02-10T14:00:00Z     | true     |

### Error Codes

| Code | Message               | UI Handling                                    |
|------|-----------------------|------------------------------------------------|
| 400  | BAD_REQUEST           | Show error state with retry                    |
| 401  | UNAUTHORIZED          | Navigate to login                              |
| 404  | CUSTOMER_NOT_FOUND    | Show error state: "Customer record not found"  |

---

## PUT /obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_documents/{documentId}

**Auth:** DirectLogin
**Tag:** KYC
**Trigger:** `approve_kyc()` action — called per document to mark it valid before recording the check result

Updates the validity status of a specific KYC document. Called per-document by the ViewModel during the approve flow to mark submitted documents as `is_valid: true`. Also used to mark documents invalid during rejection.

### Path Parameters

| Name       | Type   | Description          |
|------------|--------|----------------------|
| bankId     | String | Bank identifier      |
| customerId | String | Customer identifier  |
| documentId | String | KYC document ID      |

### Response Fields

| Field           | Type    | Description                    |
|-----------------|---------|--------------------------------|
| kyc_document_id | String  | Document identifier            |
| status          | String  | Updated document status        |
| is_valid        | Boolean | Validity flag after update     |
| last_updated    | String  | ISO-8601 update timestamp      |

### Demo Data (response template)

| Field        | Value                    |
|--------------|--------------------------|
| status       | VERIFIED                 |
| is_valid     | true                     |
| last_updated | 2026-05-26T10:00:00Z     |

### Error Codes

| Code | Message            | UI Handling                                         |
|------|--------------------|-----------------------------------------------------|
| 400  | VALIDATION_FAILED  | Show error banner: "Document update failed"         |
| 401  | UNAUTHORIZED       | Navigate to login                                   |
| 404  | DOCUMENT_NOT_FOUND | Show error banner: "Document record not found"      |

---

## PUT /obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_check/{kycCheckId}

**Auth:** DirectLogin
**Tag:** KYC
**Trigger:** `approve_kyc()` or `reject_kyc()` action — records the officer's formal check decision

Records the field officer's KYC check result for the customer. The `kycCheckId` is caller-supplied (generated by the ViewModel as a UUID). `satisfied: true` on approval; `satisfied: false` on rejection. The `how` field captures the review method (in_person / online / postal).

### Path Parameters

| Name       | Type   | Description                         |
|------------|--------|-------------------------------------|
| bankId     | String | Bank identifier                     |
| customerId | String | Customer identifier                 |
| kycCheckId | String | Caller-supplied UUID for this check |

### Request Fields

| Name            | Type    | Required | Notes                              |
|-----------------|---------|----------|------------------------------------|
| customer_number | String  | Yes      | Customer account number            |
| date            | String  | Yes      | ISO-8601 check datetime            |
| how             | String  | Yes      | in_person \| online \| postal      |
| staff_user_id   | String  | Yes      | Logged-in officer user ID          |
| staff_name      | String  | Yes      | Logged-in officer display name     |
| satisfied       | Boolean | Yes      | true = approved, false = rejected  |
| comments        | String  | Yes      | Officer notes / rejection reason   |

### Demo Data — Approval request

| Field           | Value                                                                                               |
|-----------------|-----------------------------------------------------------------------------------------------------|
| customer_number | EQKE-2026-00221                                                                                     |
| date            | 2026-05-26T10:30:00Z                                                                                |
| how             | in_person                                                                                           |
| staff_user_id   | user-fo-amina                                                                                       |
| staff_name      | Amina Odhiambo                                                                                      |
| satisfied       | true                                                                                                |
| comments        | National ID and utility bill both verified. Photo match confirmed. Proceeding to approve KYC.       |

### Demo Data — Rejection request

| Field           | Value                                                                     |
|-----------------|---------------------------------------------------------------------------|
| customer_number | EQKE-2026-00221                                                           |
| date            | 2026-05-26T10:30:00Z                                                      |
| how             | in_person                                                                 |
| staff_user_id   | user-fo-amina                                                             |
| staff_name      | Amina Odhiambo                                                            |
| satisfied       | false                                                                     |
| comments        | National ID back side not uploaded. Selfie does not match ID photo.       |

### Response Fields

| Field     | Type    | Description                              |
|-----------|---------|------------------------------------------|
| id        | String  | Generated check record identifier        |
| satisfied | Boolean | Echo of the submitted satisfied flag     |

### Error Codes

| Code | Message        | UI Handling                                          |
|------|----------------|------------------------------------------------------|
| 400  | BAD_REQUEST    | Show APPROVAL_FAILED or REJECTION_FAILED error state |
| 401  | UNAUTHORIZED   | Navigate to login                                    |
| 404  | NOT_FOUND      | Show error state: "Customer or check not found"      |

---

## PUT /obp/v2.0.0/banks/{bankId}/customers/{customerId}/kyc_statuses

**Auth:** DirectLogin
**Tag:** KYC
**Trigger:** Final call in approve/reject flow — appends a status entry to the customer's KYC timeline after PUT kyc_check succeeds

Appends a KYC status entry to the customer's compliance timeline. No ID in path — the API always appends and does not overwrite. `ok: true` moves the customer to VERIFIED; `ok: false` records the rejection. On success the ViewModel emits `KycApproved` or `KycRejected`.

### Path Parameters

| Name       | Type   | Description         |
|------------|--------|---------------------|
| bankId     | String | Bank identifier     |
| customerId | String | Customer identifier |

### Request Fields

| Name            | Type    | Required | Notes                               |
|-----------------|---------|----------|-------------------------------------|
| customer_number | String  | Yes      | Customer account number             |
| ok              | Boolean | Yes      | true = KYC passed, false = failed   |
| date            | String  | Yes      | ISO-8601 status entry datetime      |

### Demo Data — Approval

| Field           | Value                |
|-----------------|----------------------|
| customer_number | EQKE-2026-00221      |
| ok              | true                 |
| date            | 2026-05-26T10:45:00Z |

### Demo Data — Rejection

| Field           | Value                |
|-----------------|----------------------|
| customer_number | EQKE-2026-00221      |
| ok              | false                |
| date            | 2026-05-26T10:45:00Z |

### Response Fields

| Field | Type    | Description                          |
|-------|---------|--------------------------------------|
| ok    | Boolean | Echo of the submitted ok flag        |

### Error Codes

| Code | Message      | UI Handling                                            |
|------|--------------|--------------------------------------------------------|
| 400  | BAD_REQUEST  | Show APPROVAL_FAILED or REJECTION_FAILED error state   |
| 401  | UNAUTHORIZED | Navigate to login                                      |

---

## KYC Review — API Call Sequence

```
APPROVE flow:
  1. PUT kyc_documents/{id}   for each verified document (is_valid: true)
  2. PUT kyc_check/{checkId}  (satisfied: true, how: in_person, comments: risk notes)
  3. PUT kyc_statuses          (ok: true)
  4. Emit KycApproved → navigate to customer-detail

REJECT flow:
  1. PUT kyc_check/{checkId}  (satisfied: false, comments: rejection reason)
  2. PUT kyc_statuses          (ok: false)
  3. Emit KycRejected → show rejection banner inline on kyc-review
```

---

_Generated by /idea export | 2026-05-30_
