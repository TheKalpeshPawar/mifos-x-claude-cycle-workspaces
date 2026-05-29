# API Reference — Field Officer Dashboard

| Field    | Value                                       |
|----------|---------------------------------------------|
| Feature  | fo-dashboard                                |
| Base URL | https://apisandbox.openbankproject.com      |

---

## GET /obp/v5.1.0/banks/{bankId}/customers

**Auth:** DirectLogin
**Tag:** Customers
**Trigger:** `FoDashboardViewModel.loadDashboardData()` on screen open / `RetryLoadEvent`

Fetches the full customer list for the branch. The ViewModel derives `activeCustomerCount` (total), `kycPendingCount` (filtered), and populates `actionAlerts` for KYC-expiry and new-lead card types.

### Path Parameters

| Name   | Type   | Required | Description             |
|--------|--------|----------|-------------------------|
| bankId | String | Yes      | Bank identifier (branch) |

### Response Fields

| Field                           | Type              | Description                                                        |
|---------------------------------|-------------------|--------------------------------------------------------------------|
| customers                       | List\<Customer\>  | Full customer list for the bank                                    |
| customers[].customer_id         | String            | Unique customer identifier e.g. "cust-ke-001-wanjiru"             |
| customers[].legal_name          | String            | Full legal name e.g. "Wanjiru Kamau"                              |
| customers[].kyc_status          | String            | Enum: "VERIFIED" / "PENDING" / "REJECTED" / "expiring_soon"       |
| customers[].customer_number     | String            | Branch reference number e.g. "EQKE-2024-00147"                    |
| customers[].mobile_phone_number | String            | Customer contact e.g. "+254712345678"                              |
| customers[].date_of_birth       | String            | ISO-8601 date of birth e.g. "1988-03-22"                          |

### Derived Bindings (FoDashboardViewModel)

| ViewModel Field              | Derivation                                                          |
|------------------------------|---------------------------------------------------------------------|
| `activeCustomerCount`        | `customers.length` → stat card "124"                               |
| `kycPendingCount`            | `customers.filter(kyc_status == "PENDING").length` → stat card "3" |
| `actionAlerts[kyc_expiry]`   | `customers.filter(kyc_status == "expiring_soon")` → KYC alert row  |
| `actionAlerts[new_lead]`     | `customers.filter(status == "lead" && created_today == true)` → new-lead row |

### Demo Data (from demo-data.yaml)

| customer_id            | legal_name            | kyc_status | customer_number   | mobile_phone_number |
|------------------------|-----------------------|------------|-------------------|---------------------|
| cust-ke-001-wanjiru    | Wanjiru Kamau         | VERIFIED   | EQKE-2024-00147   | +254712345678       |
| cust-ke-002-rotich     | Kipchoge Rotich       | PENDING    | EQKE-2026-00221   | +254723456789       |
| cust-ke-003-atieno     | Atieno Ouma           | VERIFIED   | EQKE-2023-00089   | +254734567890       |
| cust-ke-004-mwangi     | James Mwangi Njoroge  | VERIFIED   | EQKE-2022-00054   | +254745678901       |
| cust-ke-005-koech      | Cherotich Koech       | REJECTED   | EQKE-2026-00198   | +254756789012       |

> activeCustomerCount = 5 records (dashboard displays 124 — reflects full production set); kycPendingCount = 1 (Kipchoge Rotich, PENDING). Alert row demo: John Mwangi (expiring_soon) → "John Mwangi — KYC expires in 3 days". New lead demo: Peter Kamau → "New lead: Peter Kamau — Retail account request".

### Component States

| Component              | loading state  | error state                                              | empty state                              |
|------------------------|---------------|----------------------------------------------------------|------------------------------------------|
| stats_grid             | skeleton (×4) | banner: "Could not load dashboard metrics. Retry."       | box: "No statistics available at this time." |
| stat_active_customers  | skeleton (×1) | banner: "Unable to retrieve customer statistics."         | box: "No active customers found."        |
| stat_kyc_pending       | skeleton (×1) | banner: "Unable to retrieve KYC pending count."           | box: "No KYC submissions pending review." |
| alert_kyc_expiry_john  | skeleton (×1) | banner: "Could not load KYC expiry alerts."               | box: "No KYC renewals due soon."         |
| alert_new_lead_peter   | skeleton (×1) | banner: "Could not load new lead notifications."          | box: "No new leads today."               |

### Error Codes

| Code | Message                                  | UI Handling                     |
|------|------------------------------------------|---------------------------------|
| 401  | Unauthorized — missing or invalid token  | Navigate to login screen        |
| 404  | Bank not found                           | Show error state with retry     |
| 500  | Internal server error                    | Show error state with retry     |

---

## GET /obp/v5.1.0/banks/{bankId}/account-applications

**Auth:** DirectLogin
**Tag:** Account-Applications
**Trigger:** `FoDashboardViewModel.loadDashboardData()` on screen open / `RetryLoadEvent`

Fetches all account applications for the bank. The ViewModel derives `pendingApplicationCount` and populates `actionAlerts` for long-pending and corporate-inquiry card types.

### Path Parameters

| Name   | Type   | Required | Description             |
|--------|--------|----------|-------------------------|
| bankId | String | Yes      | Bank identifier (branch) |

### Response Fields

| Field                                          | Type                       | Description                                          |
|------------------------------------------------|----------------------------|------------------------------------------------------|
| account_applications                           | List\<AccountApplication\> | All applications for the bank                        |
| account_applications[].account_application_id | String                     | Unique identifier e.g. "appn-ke-001"                 |
| account_applications[].product_code           | String                     | e.g. "SAVINGS_KES_STANDARD", "CURRENT_KES_BUSINESS"  |
| account_applications[].proposed_balance        | Amount                     | Object: { currency: "KES", amount: "5000.00" }       |
| account_applications[].status                  | String                     | "PENDING" / "APPROVED" / "REJECTED" / "inquiry"      |
| account_applications[].date_of_application     | String                     | ISO-8601 submission timestamp                        |

### Derived Bindings (FoDashboardViewModel)

| ViewModel Field                  | Derivation                                                                                   |
|----------------------------------|----------------------------------------------------------------------------------------------|
| `pendingApplicationCount`        | `account_applications.filter(status == "PENDING").length` → stat card "5"                   |
| `actionAlerts[long_pending]`     | `account_applications.filter(status == "PENDING" && days_pending >= 7)` → application alert |
| `corporateInquiries`             | `account_applications.filter(product_code == "corporate" && status == "inquiry")` → corporate card |

### Demo Data (from demo-data.yaml)

| account_application_id | product_code            | proposed_balance    | status   | date_of_application   |
|------------------------|-------------------------|---------------------|----------|-----------------------|
| appn-ke-001            | SAVINGS_KES_STANDARD    | KES 5,000.00        | PENDING  | 2026-05-22T09:00:00Z  |
| appn-ke-002            | CURRENT_KES_BUSINESS    | KES 50,000.00       | APPROVED | 2026-05-19T14:30:00Z  |
| appn-ke-003            | FIXED_DEPOSIT_KES_12M   | KES 100,000.00      | PENDING  | 2026-05-21T11:15:00Z  |
| appn-ke-004            | SAVINGS_KES_JUNIOR      | KES 2,000.00        | REJECTED | 2026-05-18T08:45:00Z  |

> pendingApplicationCount = 2 (appn-ke-001, appn-ke-003 — dashboard displays 5 from production set). Long-pending alert: appn-ke-001 (submitted 2026-05-22, days_pending = 8 ≥ 7) → "Sarah Odhiambo — Application pending 7 days". Corporate alert: Acme Trading Ltd → "Acme Trading Ltd — New business account inquiry".

### Component States

| Component                       | loading state  | error state                                                | empty state                                     |
|---------------------------------|---------------|------------------------------------------------------------|--------------------------------------------------|
| stat_pending_applications       | skeleton (×1) | banner: "Could not load pending applications. Retry."      | box: "No pending applications. All caught up!"   |
| alert_application_pending_sarah | skeleton (×1) | banner: "Could not load overdue application alerts."        | box: "No applications overdue. Good work!"       |
| action_corporate_onboard        | skeleton (×1) | banner: "Could not load corporate onboarding requests."     | box: "No corporate account inquiries pending."   |

### Error Codes

| Code | Message                                  | UI Handling                     |
|------|------------------------------------------|---------------------------------|
| 401  | Unauthorized — missing or invalid token  | Navigate to login screen        |
| 404  | Bank not found                           | Show error state with retry     |
| 500  | Internal server error                    | Show error state with retry     |

---

_Generated by /idea export | 2026-05-30_
