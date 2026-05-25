# Mifos-X Open Banking — Dual-Persona KMP Application

**Vision:** Build a Kotlin Multiplatform (KMP) banking super-app powered by the Open Bank Project (OBP) API v7.0.0, delivering two distinct personas (Consumer & Field Officer) from a single codebase via KMP Product Flavors.

---

## Product Overview

### Personas

**Consumer (Alex)**
- Age: 28, Tech-savvy retail customer
- Needs: Self-service account management, fast payments, expense tracking, card control
- Motivation: Convenience, security, control over finances
- Primary flows: View accounts → Check balance → Send money → Manage cards

**Field Officer (Priya)**
- Age: 35, Agent Banking representative  
- Needs: Customer onboarding, KYC compliance, account applications, document collection
- Motivation: Efficiency, regulatory compliance, relationship building
- Primary flows: Search customer → Onboard new account → Collect KYC → Create application

### Brand Identity

| Attribute | Value |
|---|---|
| Primary Color | Mifos Deep Purple `#1800B1` |
| Secondary Color | Banking Teal `#008B8B` |
| Accent | Green `#4CAF50` |
| Font Family | Inter (Headlines), Manrope (Body) |
| Tone | Professional, Trustworthy, Efficient |
| Key Message | "Banking for Everyone" |

---

## Architecture

### Tech Stack

| Layer | Tech | Notes |
|---|---|---|
| UI | Compose Multiplatform | Single KMP UI codebase |
| Networking | Ktor Client | OBP API v7.0.0 REST client |
| State Management | Store5 / BaseViewModel | Reactive, error-resilient |
| Local Storage | SQLDelight | Cross-platform persistence |
| Serialization | Kotlinx Serialization | Type-safe JSON |
| Dependency Injection | Koin | Lightweight, multiplatform |
| Build System | Gradle (KMP plugins) | Kotlin Multiplatform Plugin v0.11+ |

### Product Flavors (KMP Product Flavors)

Single source code tree compiles to **two distinct apps**:

**Flavor: `consumer`**
- Navigation: Home → Accounts → Pay → Cards → More
- Feature set: Account mgmt, transactions, payments, cards, beneficiaries, ATM locator
- API subset: Accounts, Transactions, TransactionRequests, Cards, Counterparties, ATM, FX

**Flavor: `fieldOfficer`**
- Navigation: Dashboard → Customers → Applications → Messages → More
- Feature set: Customer search, onboarding, KYC, applications, messaging, meetings
- API subset: Customers, KYC, Account-Applications, Customer-Messages, Meetings, Retail/Corporate

Both flavors share:
- Authentication layer (DirectLogin)
- Core domain models (Account, Transaction, Customer, KYC, etc.)
- Persistence layer (SQLDelight schema)
- Navigation router (flavor-specific implementation)

---

## Backend Integration

### Open Bank Project API v7.0.0

**Base URL:** `https://apisandbox.openbankproject.com`  
**Authentication:** DirectLogin (Direct API token auth — no OAuth required for sandbox)

**Available Endpoints** (118+ across 89 tags):
- **Accounts** (89 endpoints): Account creation, listing, detail, balance, permissions
- **Transactions** (33 endpoints): Transaction history, filtering, counterparty transactions
- **TransactionRequests** (14 endpoints): Payment requests, approvals
- **Cards** (18 endpoints): Card details, activation, limits, transactions
- **Counterparties** (39 endpoints): Beneficiary management, metadata
- **ATM** (12 endpoints): ATM locations, services by coordinates
- **Branch** (11 endpoints): Branch details, locations
- **FX** (6 endpoints): Currency pairs, exchange rates
- **Customers** (89 endpoints): Customer CRUD, corporate structures, account applications
- **KYC** (15 endpoints): KYC documents, status, compliance
- **Customer-Messages** (11 endpoints): Message threading, history
- **Meetings** (8 endpoints): Meeting creation, scheduling, history
- **Standing-Orders** (8 endpoints): Recurring payment setup
- **Consolidated** (6 endpoints): Multi-account views, activity aggregation

**Credential Storage:**
- Consumer Key: Public in `.env.local` (sandbox)
- Username/Password: `.env.local` only (sandbox)
- Token: Obtained at runtime via DirectLogin POST to `/obp/v4.0.0/banks/{bank}/direct_login`

---

## Core Models

### Domain Objects (Shared)

```yaml
# idea-layer/dtos/Account.yaml
Account:
  id: String
  label: String
  type: CHECKING | SAVINGS | BUSINESS
  balance: Money
  currency: String
  iban: String
  swift: String
  branchId: String
  status: ACTIVE | INACTIVE | CLOSED
  owners: List<User>
  product: Product
```

```yaml
# idea-layer/dtos/Transaction.yaml
Transaction:
  id: String
  accountId: String
  type: DEBIT | CREDIT
  amount: Money
  currency: String
  counterpartyAccount: Account
  counterpartyName: String
  date: Instant
  description: String
  transactionType: SEPA | ACH | DOMESTIC | WIRE
  status: PENDING | COMPLETED | FAILED
  metadata: Map<String, String>
```

```yaml
# idea-layer/dtos/Customer.yaml
Customer:
  id: String
  name: String
  email: String
  phone: String
  dateOfBirth: LocalDate
  address: Address
  taxId: String
  accounts: List<Account>
  kycStatus: NOT_STARTED | IN_PROGRESS | VERIFIED | REJECTED
  accountApplications: List<AccountApplication>
  relationshipStatus: PROSPECT | ACTIVE | DORMANT | CLOSED
```

---

## Feature Roadmap

### Phase 1: MVP (Consumer Persona)

1. **Authentication** — DirectLogin flow, session management
2. **Home Dashboard** — Account overview, recent transactions, quick actions
3. **Accounts** — List, detail, balance, statement
4. **Transactions** — History, filter, detail view, counterparty info
5. **Send Money** — Domestic transfers, SEPA, ACH routing
6. **Beneficiaries** — List, add, edit, delete counterparties

### Phase 2: Field Officer Onboarding

1. **Customer Search** — By name, email, account number
2. **Customer Profile** — View customer details, relationship history
3. **KYC Review** — Document collection, verification workflow
4. **Account Application** — Submit new account requests, track status
5. **Customer Messages** — Thread-based messaging

### Phase 3: Enhancement

1. **Standing Orders** — Recurring payment setup and management
2. **Cards** — Card details, activation, transaction history
3. **ATM Locator** — Map-based ATM finder, branch locations
4. **FX Rates** — Live currency rates, conversion calculator
5. **Notifications** — Push alerts for transactions, KYC status

---

## Screen Inventory (30+ Screens)

### Consumer Persona (13 screens)

| Screen | Purpose | OBP API Tags |
|---|---|---|
| Splash | App startup | — |
| Login | DirectLogin form | Authentication |
| Home | Account overview | Accounts, Transactions |
| Accounts | List all accounts | Accounts |
| Account Detail | Account info & actions | Accounts |
| Transactions | Transaction history | Transactions |
| Transaction Detail | Transaction info | Transactions |
| Send Money | Payment initiation | TransactionRequests |
| Send Confirm | Review payment | TransactionRequests |
| Beneficiaries | Manage payees | Counterparties |
| Cards | Card management | Cards |
| Standing Orders | Recurring payments | Standing-Orders |
| More | User preferences, logout | — |

### Field Officer Persona (11 screens)

| Screen | Purpose | OBP API Tags |
|---|---|---|
| FO Dashboard | Agent overview | Customers, Consolidated |
| Customer Search | Find customers | Customers |
| Customer Detail | Customer profile | Customers, Accounts |
| Customer Onboarding | New customer flow | Customers |
| Corporate Onboarding | Business customer flow | Customers |
| KYC Review | Document verification | KYC |
| Account Applications | Manage applications | Account-Applications |
| Application Detail | Application info | Account-Applications |
| Customer Messages | Messaging thread | Customer-Messages |
| Meetings | Meeting scheduling | Meetings |
| More | Help, settings, logout | — |

### Shared Screens (4 screens)

| Screen | Purpose |
|---|---|
| Splash | Startup animation |
| Login | DirectLogin UI |
| Profile | User info editing |
| Settings | App preferences |

---

## Navigation Architecture

### Consumer Navigation Graph

```
Splash → Login → Home (Bottom Nav)
  ├─ Home → Account Detail → Transactions → Transaction Detail
  ├─ Accounts → Account Detail
  ├─ Pay → Send Money → Send Confirm → Success
  ├─ Cards → Card Detail
  ├─ More → Profile / Settings / About / Logout
```

### Field Officer Navigation Graph

```
Splash → Login → Dashboard (Bottom Nav)
  ├─ Dashboard → Recent activity
  ├─ Customers → Customer Search → Customer Detail
  │   ├─ Customer Detail → Profile
  │   ├─ Customer Detail → KYC Review
  │   └─ Customer Detail → Account Applications
  ├─ Applications → Application Detail → Approve / Reject
  ├─ Messages → Message Thread → Compose
  └─ More → Profile / Settings / Help / Logout
```

---

## Design System

### Color Tokens

| Token | Value | Usage |
|---|---|---|
| primary | #1800B1 | CTAs, active states |
| secondary | #008B8B | Secondary actions |
| success | #4CAF50 | Positive actions |
| error | #FF5252 | Errors, destructive |
| warning | #FFA726 | Warnings, alerts |
| info | #29B6F6 | Info messages |
| surface | #FFFFFF | Cards, containers |
| background | #F5F5F5 | App background |
| text_primary | #1F1F1F | Primary text |
| text_secondary | #757575 | Secondary text |

### Typography

| Level | Font | Size | Weight |
|---|---|---|---|
| display-lg | Inter | 32px | 600 |
| headline-lg | Inter | 24px | 600 |
| body-lg | Manrope | 16px | 400 |
| body-md | Manrope | 14px | 400 |
| body-sm | Manrope | 12px | 400 |

### Component Library

- Button (contained, outlined, text)
- Text Field (single, multi-line, search)
- Card, Dialog, Sheet
- TopAppBar, BottomNavigation, FAB
- Snackbar, ProgressIndicator, Badge
- List, Grid, Spacer
- Custom: AccountCard, TransactionRow, BeneficiaryItem

---

## Quality Standards

- **Type Safety:** 100% Kotlin, non-null by default
- **Null Safety:** Explicit optionals via `?`
- **Testability:** ViewModel + StateFlow + repository pattern
- **Accessibility:** Material 3 A11y semantics
- **Performance:** <500ms account load, <200ms transaction list
- **Security:** TLS 1.3, HTTPS only, no plaintext storage

---

## Success Metrics

1. **Adoption:** 1000+ active consumer users, 100+ field officers in pilot
2. **Transaction Volume:** 10K+ monthly transactions
3. **NPS:** >50 for both personas
4. **Uptime:** 99.9% availability
5. **Load Time:** <2s home screen

---

## Timeline

- **M1 (Jan–Mar):** Consumer MVP (Auth, Accounts, Transactions)
- **M2 (Apr–Jun):** Field Officer MVP (Search, Onboarding, KYC)
- **M3 (Jul–Sep):** Enhancement (Cards, ATM, Standing Orders)
- **M4 (Oct–Dec):** Production hardening, scale testing
