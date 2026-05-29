# API Reference — Field Officer Dashboard

| Field    | Value                                       |
|----------|---------------------------------------------|
| Feature  | fo-dashboard                                |
| Base URL | https://apisandbox.openbankproject.com      |

---

## GET /obp/v5.1.0/banks/{bankId}/customers

**Auth:** DirectLogin
**Tag:** Customers
**Trigger:** `loadDashboard()` on screen open / `RetryLoadEvent`

Used to derive: `activeCustomerCount`, `kycPendingCount`, KYC expiry alerts (`kyc_status=expiring_soon`), and new lead alerts (`status=lead, created_today=true`).

### Path Parameters

| Name   | Type   | Value    | Description       |
|--------|--------|----------|-------------------|
| bankId | String | gh.29.uk | Bank identifier   |

### Response Fields

| Field                           | Type              | Description                                              |
|---------------------------------|-------------------|----------------------------------------------------------|
| customers                       | List\<Customer\>  | Full customer list for the branch                        |
| customers[].customer_id         | String            | Unique customer identifier                               |
| customers[].legal_name          | String            | Full legal name e.g. "John Mwangi"                       |
| customers[].kyc_status          | String            | "pending" / "expiring_soon" / "verified" / "expired"     |
| customers[].customer_number     | String            | Displayed customer reference number                      |
| customers[].mobile_phone_number | String            | Customer contact phone                                   |
| customers[].date_of_birth       | String            | ISO-8601 date of birth                                   |

### Derived Bindings (ViewModel)

| ViewModel Field         | Derivation                                                    |
|-------------------------|---------------------------------------------------------------|
| activeCustomerCount     | `customers.length`                                           |
| kycPendingCount         | `customers.filter(kyc_status == "pending").length`           |
| actionAlerts[kyc_expiry]| `customers.filter(kyc_status == "expiring_soon")` → alert rows|
| actionAlerts[new_lead]  | `customers.filter(status == "lead" && created_today == true)`|

### Demo Data

| customer_id | legal_name    | kyc_status     | Notes                          |
|-------------|---------------|----------------|--------------------------------|
| CUS-001     | John Mwangi   | expiring_soon  | KYC expires in 3 days          |
| CUS-002     | Peter Kamau   | pending        | New retail lead (today)        |
| …124 total  | …             | various        | 3 with kyc_status=pending      |

### Error Codes

| Code | Message                        | UI Handling                                  |
|------|--------------------------------|----------------------------------------------|
| 401  | Unauthorized — missing token   | Navigate to login                            |
| 404  | Bank not found                 | Show error state with retry                  |
| 500  | Internal server error          | Show error state with retry                  |

---

## GET /obp/v5.1.0/banks/{bankId}/account-applications

**Auth:** DirectLogin
**Tag:** Account-Applications
**Trigger:** `loadDashboard()` on screen open / `RetryLoadEvent`

Used to derive: `pendingApplicationCount`, long-pending application alerts, corporate inquiry alerts.

### Path Parameters

| Name   | Type   | Value    | Description     |
|--------|--------|----------|-----------------|
| bankId | String | gh.29.uk | Bank identifier |

### Response Fields

| Field                                            | Type                      | Description                                    |
|--------------------------------------------------|---------------------------|------------------------------------------------|
| account_applications                             | List\<AccountApplication\>| All applications for the bank                  |
| account_applications[].account_application_id   | String                    | Unique application identifier                  |
| account_applications[].product_code             | String                    | Product type e.g. "retail", "corporate"        |
| account_applications[].proposed_balance         | Amount                    | Object: {currency, amount}                     |
| account_applications[].status                   | String                    | "pending" / "inquiry" / "approved" / "rejected"|
| account_applications[].date_of_application      | String                    | ISO-8601 application submission date           |

### Derived Bindings (ViewModel)

| ViewModel Field                      | Derivation                                                                          |
|--------------------------------------|-------------------------------------------------------------------------------------|
| pendingApplicationCount              | `account_applications.filter(status == "pending").length`                           |
| actionAlerts[long_pending]           | `account_applications.filter(status == "pending" && days_pending >= 7)`             |
| actionAlerts[corporate_inquiry]      | `account_applications.filter(product_code == "corporate" && status == "inquiry")`  |

### Demo Data

| application_id | product_code | status  | days_pending | Notes                            |
|----------------|--------------|---------|--------------|----------------------------------|
| APP-101        | retail       | pending | 7            | Sarah Odhiambo — overdue         |
| APP-102        | corporate    | inquiry | 2            | Acme Trading Ltd                 |
| …5 total       | …            | pending | …            | total pendingApplicationCount=5  |

### Error Codes

| Code | Message                        | UI Handling                               |
|------|--------------------------------|-------------------------------------------|
| 401  | Unauthorized — missing token   | Navigate to login                         |
| 404  | Bank not found                 | Show error state with retry               |
| 500  | Internal server error          | Show error state with retry               |

---

_Generated by /idea export | 2026-05-29_
