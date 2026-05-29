# Features — Mifos X Open Banking

All 45 features organized by flavor and OBP API integration points.
Updated 2026-05-29 — added consumer-home, standing-order-edit.

---

## Consumer Persona Features

### Core Banking (9 features)

| Feature | Screen | OBP API Endpoint | Description |
|---|---|---|---|
| **splash** | Splash | — | App startup animation, branding |
| **login** | Login | `POST /v4.0.0/banks/{bank}/direct_login` | DirectLogin authentication |
| **home** | Home | Accounts, Transactions | Account overview, balance, recent transactions |
| **accounts** | Accounts, Account Detail | `GET /v3.0.0/banks/{bank}/accounts` | List and view account details |
| **transactions** | Transactions, Transaction Detail | `GET /accounts/{account_id}/transactions` | View transaction history, filtering |
| **send-money** | Send Money, Send Confirm | `POST /accounts/{account_id}/transaction-request-types/SEPA` | Initiate payments (SEPA, ACH) |
| **beneficiaries** | Beneficiaries | `GET /banks/{bank}/counterparties` | Manage payee list |
| **cards** | Cards, Card Detail | `GET /accounts/{account_id}/cards` | View card details, transactions |
| **standing-orders** | Standing Orders | `GET /accounts/{account_id}/standing-orders` | Create & manage recurring payments |

| **consumer-home** | Consumer Home | `GET /my/accounts`, `GET /accounts/{id}/transactions` | Personalised consumer home dashboard — balance, quick actions, recent transactions |
| **standing-order-edit** | Standing Order Edit | `PUT /accounts/{accountId}/standing-order/{id}` | Edit amount, frequency, start/end date for existing standing order |

### Enhancement Features (4 features)

| Feature | Screen | OBP API Endpoint | Description |
|---|---|---|---|
| **fx-rates** | FX Rates | `GET /banks/{bank}/fx` | Live currency rates, conversion calculator |
| **atm-locator** | ATM Finder | `GET /banks/{bank}/atms` | Map-based ATM finder |
| **notifications** | — | Firebase Cloud Messaging | Transaction alerts, KYC status updates |
| **profile** | Profile, Settings | — | User preferences, security settings |

---

## Field Officer Persona Features

### Core Agent Banking (7 features)

| Feature | Screen | OBP API Endpoint | Description |
|---|---|---|---|
| **fo-dashboard** | FO Dashboard | `GET /customers`, Consolidated | Agent's active customer list, pending applications |
| **customer-search** | Customer Search | `GET /banks/{bank}/customers` | Find customers by name, email, ID |
| **customer-detail** | Customer Detail, Customer Profile | `GET /customers/{customer_id}` | View customer demographics, accounts, status |
| **onboarding** | Onboarding, Corporate Onboarding | `POST /customers` | Collect customer info, create account requests |
| **kyc** | KYC Review | `GET /customers/{customer_id}/kyc_documents`, `PUT` | Upload, verify KYC documents |
| **account-applications** | Account Applications, Application Detail | `GET /banks/{bank}/account-applications` | Manage new account requests |
| **customer-messages** | Customer Messages | `GET /customers/{customer_id}/messages` | Thread-based customer messaging |

### Enhancement Features (2 features)

| Feature | Screen | OBP API Endpoint | Description |
|---|---|---|---|
| **meetings** | Meetings | `POST /customers/{customer_id}/meetings` | Schedule & track customer meetings |
| **corporate-customers** | Corporate Onboarding, Customer Detail | `GET /customers/{customer_id}/corporate_location` | Manage corporate customer structures |

---

## Shared Features (4 features)

| Feature | Screen | OBP API Endpoint | Description |
|---|---|---|---|
| **splash** | Splash | — | Startup animation (shared) |
| **login** | Login | `POST /v4.0.0/banks/{bank}/direct_login` | DirectLogin (shared) |
| **profile** | Profile | — | User info editing, flavor-independent |
| **settings** | Settings, More | — | App theme, language, notifications |

---

## Complete Screen List (45 Screens)

### Consumer Screens (23)

1. **home** — `consumer`
2. **consumer-home** — `consumer`
3. **accounts** — `consumer`
4. **account-detail** — `consumer`
5. **transactions** — `consumer`
6. **transaction-detail** — `consumer`
7. **transaction-tags** — `consumer`
8. **send-money** — `consumer`
9. **send-money-confirm** — `consumer`
10. **beneficiaries** — `consumer`
11. **cards** — `consumer`
12. **card-detail** — `consumer`
13. **standing-orders** — `consumer`
14. **standing-order-detail** — `consumer`
15. **standing-order-edit** — `consumer`
16. **direct-debits** — `consumer`
17. **direct-debit-detail** — `consumer`
18. **atm-locator** — `consumer`
19. **fx-rates** — `consumer`
20. **consent-manager** — `consumer`
21. **notifications** — `consumer`
22. **pfm-dashboard** — `consumer`
23. **products** — `consumer`

### Field Officer Screens (12)

1. **fo-dashboard** — `fieldOfficer`
2. **customer-search** — `fieldOfficer`
3. **customer-detail** — `fieldOfficer`
4. **customer-profile** — `fieldOfficer`
5. **customer-onboarding** — `fieldOfficer`
6. **corporate-onboarding** — `fieldOfficer`
7. **kyc-review** — `fieldOfficer`
8. **account-applications** — `fieldOfficer`
9. **application-detail** — `fieldOfficer`
10. **customer-messages** — `fieldOfficer`
11. **meetings** — `fieldOfficer`
12. **agent-registration** — `fieldOfficer`

### Shared Screens (10)

1. **splash** — both
2. **login** — both
3. **forgot-password** — both
4. **change-password** — both
5. **profile** — both
6. **settings** — both
7. **about** — both
8. **terms-of-service** — both
9. **privacy-policy** — both
10. **licenses** — both

---

## Feature Quality Baseline

All features start at quality score **50/100** (scaffold). Progression:

- **≥50:** Scaffolded (template-generated)
- **≥70:** Enriched (design tokens, state models, navigation edges)
- **≥85:** Fully specced (SPEC.md, API contract, mockups)
- **≥95:** Implemented (Kotlin code, tests passing)

---

## OBP API Coverage

| API Tag | Consumer | Field Officer | Endpoints |
|---|---|---|---|
| Accounts | ✓ | ✓ | 89 |
| Transactions | ✓ | ✓ | 33 |
| TransactionRequests | ✓ | — | 14 |
| Cards | ✓ | — | 18 |
| Counterparties | ✓ | — | 39 |
| ATM | ✓ | — | 12 |
| Branch | — | ✓ | 11 |
| FX | ✓ | — | 6 |
| Customers | — | ✓ | 89 |
| KYC | — | ✓ | 15 |
| Customer-Messages | — | ✓ | 11 |
| Meetings | — | ✓ | 8 |
| Standing-Orders | ✓ | — | 8 |
| Consolidated | ✓ | ✓ | 6 |

---

## Notes

- All features use **KMP Product Flavors** to enable/disable screens per flavor
- **DirectLogin** is the sole authentication method (no OAuth complexity in MVP)
- **Navigation** is flavor-aware: Consumer bottom-nav ≠ Field Officer bottom-nav
- **Shared layers:** DTOs, domain models, API client, local storage schema — all KMP
- **State management:** Store5 repositories + ViewModels per feature
