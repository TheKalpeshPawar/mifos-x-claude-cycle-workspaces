# API Reference — Application Detail

| Field    | Value                                    |
|----------|------------------------------------------|
| Feature  | application-detail                       |
| Base URL | https://apisandbox.openbankproject.com   |

---

## GET /obp/v5.1.0/banks/{bankId}/account-applications/{applicationId}

**Auth:** DirectLogin
**Tag:** Account-Applications
**Trigger:** Screen entry — loads full application record including customer identity, KYC status, and account routing on `ApplicationDetailViewModel` init

Fetches the complete account application record for the given `applicationId`. The response populates the application header (reference number, status chip), customer info card (legal name), application details card (product code → account type label, requested limit, purpose), and drives KYC status display. The `status` field controls the initial `decisionMade` state (PENDING / APPROVED / REJECTED).

### Path Parameters

| Name          | Type   | Description                                         |
|---------------|--------|-----------------------------------------------------|
| bankId        | String | OBP bank identifier (e.g. "gh.29.uk")               |
| applicationId | String | Account application UUID (e.g. "app-002-ke-2026-05-odhiambo") |

### Response Fields

| Field                   | Type    | Description                                                      |
|-------------------------|---------|------------------------------------------------------------------|
| account_application_id  | String  | Application UUID — displayed as reference number (after prefix "OBP-…") |
| product_code            | String  | Banking product code (e.g. "CURRENT_KES_BUSINESS" → shown as "KCB Savings Account") |
| user.user_id            | String  | OBP user UUID of the applicant                                   |
| user.username           | String  | OBP login username (e.g. "sarah.odhiambo")                      |
| user.email              | String  | Applicant email (e.g. "sarah.odhiambo@equity.co.ke")            |
| customer.customer_id    | String  | Customer UUID                                                    |
| customer.legal_name     | String  | Full legal name shown in customer_name component                 |
| customer.customer_number| String  | Bank-assigned customer number (e.g. "EQT-2026-005381")          |
| customer.mobile         | String  | Mobile number in E.164 format (e.g. "+254723456789")            |
| customer.national_id    | String  | National ID document number                                      |
| date_of_application     | String  | ISO-8601 submission timestamp — formatted as "DD Mon YYYY" in UI |
| date_last_modified      | String  | ISO-8601 last modification timestamp                             |
| status                  | String  | PENDING \| APPROVED \| REJECTED — drives decisionMade state     |
| account_routing.scheme  | String  | Routing scheme (e.g. "AccountNumber") — populated post-approval |
| account_routing.address | String  | Account number or IBAN — populated post-approval                 |

### Demo Data

| Field                   | Value                                   |
|-------------------------|-----------------------------------------|
| account_application_id  | app-002-ke-2026-05-odhiambo            |
| product_code            | CURRENT_KES_BUSINESS                    |
| user.user_id            | usr-odhiambo-002                        |
| user.username           | sarah.odhiambo                          |
| user.email              | sarah.odhiambo@equity.co.ke            |
| customer.customer_id    | cust-002-odhiambo                       |
| customer.legal_name     | Sarah Auma Odhiambo                     |
| customer.customer_number| EQT-2026-005381                         |
| customer.mobile         | +254723456789                           |
| customer.national_id    | 32456789                                |
| date_of_application     | 2026-05-12T11:15:00Z                    |
| date_last_modified      | 2026-05-14T09:20:00Z                    |
| status                  | APPROVED                                |
| account_routing.scheme  | AccountNumber                           |
| account_routing.address | 0110204857399                           |

### Error Codes

| Code | OBP Error             | UI Handling                                            |
|------|-----------------------|--------------------------------------------------------|
| 400  | BAD_REQUEST           | Show error state with "Unable to load application details" |
| 401  | UNAUTHORIZED          | Navigate to login — DirectLogin token expired          |
| 404  | APPLICATION_NOT_FOUND | Show empty state "Application details not available"   |

---

## PUT /obp/v5.1.0/banks/{bankId}/account-applications/{applicationId}

**Auth:** DirectLogin
**Tag:** Account-Applications
**Trigger:** `approve_application_button` tap (sends status: "APPROVED") or `reject_application_button` tap (sends status: "REJECTED"). Sets `isSubmitting = true` while in flight; reverts to false on error.

Submits the field officer's decision on the account application. A successful response transitions the `decisionMade` state to APPROVED or REJECTED and triggers the corresponding UI banner. On APPROVED, the screen navigates back to customer-detail after a short delay.

### Path Parameters

| Name          | Type   | Description                                         |
|---------------|--------|-----------------------------------------------------|
| bankId        | String | OBP bank identifier (e.g. "gh.29.uk")               |
| applicationId | String | Account application UUID matching the loaded record  |

### Request Body

| Field  | Type   | Required | Values                | Description                            |
|--------|--------|----------|-----------------------|----------------------------------------|
| status | String | Yes      | APPROVED \| REJECTED  | Field officer decision on the application |

### Response Fields

| Field                  | Type   | Description                                              |
|------------------------|--------|----------------------------------------------------------|
| account_application_id | String | Application UUID — confirms the record updated           |
| status                 | String | Updated status (APPROVED or REJECTED) — matches request  |
| date_last_modified     | String | ISO-8601 timestamp of decision — shown in UI as confirmation |

### Demo Data

| Field                  | Value                        |
|------------------------|------------------------------|
| account_application_id | app-002-ke-2026-05-odhiambo |
| status                 | APPROVED                     |
| date_last_modified     | 2026-05-14T09:20:00Z         |

### Error Codes

| Code | OBP Error             | UI Handling                                                     |
|------|-----------------------|-----------------------------------------------------------------|
| 400  | VALIDATION_FAILED     | Show inline error: "Invalid status value — please try again"   |
| 401  | UNAUTHORIZED          | Navigate to login — DirectLogin token expired                   |
| 404  | APPLICATION_NOT_FOUND | Show error: "Application no longer exists or was already closed" |

---

_Generated by /idea export | 2026-05-30_
