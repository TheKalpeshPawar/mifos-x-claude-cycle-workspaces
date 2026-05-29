# API Reference — Account Applications

| Field    | Value                                       |
|----------|---------------------------------------------|
| Feature  | account-applications                        |
| Base URL | https://apisandbox.openbankproject.com      |

---

## GET /obp/v5.1.0/banks/{bankId}/account-applications

**Auth:** DirectLogin
**Tag:** Account-Applications
**Trigger:** `loadApplications()` on screen open; re-triggered on `RetryLoad` event. Filter changes are client-side only (no re-fetch).

Fetches all account applications submitted under the given bank. The `AccountApplicationsViewModel` receives the full list, computes `counts` (total/pending/approved/rejected), stores in `applications`, and derives `filteredApplications` from `activeFilter`.

### Path Parameters

| Name   | Type   | Required | Value    | Description                    |
|--------|--------|----------|----------|--------------------------------|
| bankId | String | Yes      | gh.29.uk | OBP bank identifier            |

### Request Headers

| Header        | Value                         | Description                          |
|---------------|-------------------------------|--------------------------------------|
| Authorization | DirectLogin token={token}     | Field officer session token          |
| Content-Type  | application/json              |                                      |

### Response Fields

| Field                    | Type   | Description                                                             |
|--------------------------|--------|-------------------------------------------------------------------------|
| account_application_id   | String | Unique application identifier (e.g. `app-001-ke-2026-05-mwangi`)       |
| product_code             | String | Requested product code (e.g. `SAVINGS_KES_PERSONAL`, `CURRENT_KES_BUSINESS`) |
| user                     | Object | OBP user who submitted the application                                  |
| user.user_id             | String | OBP user identifier                                                     |
| user.username            | String | Username (e.g. `john.mwangi`)                                           |
| user.email               | String | User email (e.g. `john.mwangi@kcb.co.ke`)                              |
| customer                 | Object | Associated customer record                                              |
| customer.customer_id     | String | Customer identifier (e.g. `cust-001-mwangi`)                           |
| customer.legal_name      | String | Full legal name (e.g. `John Kamau Mwangi`)                              |
| customer.customer_number | String | Bank-assigned customer number (e.g. `KCB-2026-001142`)                 |
| date_of_application      | String | ISO-8601 timestamp of submission (e.g. `2026-05-10T08:32:00Z`)         |
| date_last_modified       | String | ISO-8601 timestamp of last status change                                |
| status                   | String | Enum: `PENDING` \| `APPROVED` \| `REJECTED`                            |

### Demo Data

All 5 demo items from `demo-data.yaml` — rendered as the full `content` state:

| account_application_id              | product_code            | customer.legal_name       | customer_number      | date_of_application      | status   |
|-------------------------------------|-------------------------|---------------------------|----------------------|--------------------------|----------|
| app-001-ke-2026-05-mwangi           | SAVINGS_KES_PERSONAL    | John Kamau Mwangi         | KCB-2026-001142      | 2026-05-10T08:32:00Z     | PENDING  |
| app-002-ke-2026-05-odhiambo         | CURRENT_KES_BUSINESS    | Sarah Auma Odhiambo       | EQT-2026-005381      | 2026-05-12T11:15:00Z     | APPROVED |
| app-003-ke-2026-05-kamau            | FIXED_DEPOSIT_KES_12M   | Peter Njoroge Kamau       | COOP-2026-008820     | 2026-05-15T14:45:00Z     | REJECTED |
| app-004-ke-2026-05-wanjiru          | SAVINGS_KES_JUNIOR      | Grace Nyambura Wanjiru    | NCBA-2026-003315     | 2026-05-18T09:00:00Z     | PENDING  |
| app-005-ke-2026-05-kipchoge         | CURRENT_KES_SACCO       | David Kiprotich Kipchoge  | KCB-2026-009901      | 2026-05-20T16:30:00Z     | APPROVED |

**Derived counts (demo):**

| Filter   | Count |
|----------|-------|
| ALL      | 5     |
| PENDING  | 2     |
| APPROVED | 2     |
| REJECTED | 1     |

> Note: The ui.yaml content state shows "All (8) / Pending (3) / Approved (3) / Rejected (2)" counts on filter chips — those reflect a fuller production scenario. The demo-data.yaml provides 5 canonical items for development and testing.

### Sample Response (abbreviated)

```json
{
  "account_applications": [
    {
      "account_application_id": "app-001-ke-2026-05-mwangi",
      "product_code": "SAVINGS_KES_PERSONAL",
      "user": {
        "user_id": "usr-mwangi-001",
        "username": "john.mwangi",
        "email": "john.mwangi@kcb.co.ke"
      },
      "customer": {
        "customer_id": "cust-001-mwangi",
        "legal_name": "John Kamau Mwangi",
        "customer_number": "KCB-2026-001142"
      },
      "date_of_application": "2026-05-10T08:32:00Z",
      "date_last_modified": "2026-05-10T08:32:00Z",
      "status": "PENDING"
    },
    {
      "account_application_id": "app-002-ke-2026-05-odhiambo",
      "product_code": "CURRENT_KES_BUSINESS",
      "user": {
        "user_id": "usr-odhiambo-002",
        "username": "sarah.odhiambo",
        "email": "sarah.odhiambo@equity.co.ke"
      },
      "customer": {
        "customer_id": "cust-002-odhiambo",
        "legal_name": "Sarah Auma Odhiambo",
        "customer_number": "EQT-2026-005381"
      },
      "date_of_application": "2026-05-12T11:15:00Z",
      "date_last_modified": "2026-05-14T09:20:00Z",
      "status": "APPROVED"
    }
  ]
}
```

### Error Codes

| Code | OBP Error String   | Cause                                              | UI Handling                                  |
|------|--------------------|----------------------------------------------------|----------------------------------------------|
| 400  | `BAD_REQUEST`      | Invalid `bankId` or malformed request              | Show error state with Retry; log to analytics |
| 401  | `UNAUTHORIZED`     | DirectLogin token missing, expired, or revoked     | Redirect to login screen; clear session token |
| 404  | `BANK_NOT_FOUND`   | `bankId` does not exist in OBP sandbox             | Show error state with Retry                  |
| 500  | _(server error)_   | OBP internal error                                 | Show error state with Retry; exponential backoff |

---

_Generated by /idea export | 2026-05-30_
