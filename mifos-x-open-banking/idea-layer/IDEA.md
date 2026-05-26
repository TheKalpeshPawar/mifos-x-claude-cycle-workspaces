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
| Primary Color | Sage Green `#4C662B` |
| Secondary Color | Muted Teal `#386663` |
| Error / Debit | Red `#BA1A1A` |
| Font Family | Outfit (all surfaces) |
| Tone | Professional, Trustworthy, Efficient |
| Key Message | "Banking for Everyone" |

---

## Architecture

### Tech Stack

| Layer | Tech | Notes |
|---|---|---|
| UI | Compose Multiplatform 1.8.2 | Single KMP UI codebase |
| Networking | Ktor 3.2.0 + Ktorfit 2.5.2 | OBP API v7.0.0 REST client |
| State Management | Store5 + BaseViewModel + ScreenDataStream | Stream-First reactive architecture |
| Local Storage | Room KMP 2.7.2 | Cross-platform persistence |
| Serialization | Kotlinx Serialization | Type-safe JSON, `@Serializable` routes |
| Dependency Injection | Koin 4.1.0 | Lightweight, multiplatform |
| Navigation | Jetpack Navigation Compose | Type-safe `@Serializable` route objects |
| Build System | Gradle 8.0+ + kmp-product-flavors 2.4.3 | Variant matrix + source set gating |

### Product Flavors (kmp-product-flavors v2.4.3)

**Plugin:** `io.github.mobilebytelabs.kmp-product-flavors`

Applied in `cmp-navigation/build.gradle.kts`:
```kotlin
plugins {
    id("com.google.devtools.ksp")
    id("io.github.mobilebytelabs.kmp-product-flavors") version "2.4.3"
}

kmpFlavors {
    flavors {
        register("consumer") { isDefault.set(true) }
        register("fieldOfficer")
    }
    buildTypes {
        register("debug")   { isDefault.set(true) }
        register("release")
    }
}
```

Build a variant: `./gradlew :cmp-android:assembleConsumerDebug` or `./gradlew :cmp-android:assembleFieldOfficerRelease`  
Or via properties: `-PkmpFlavor=fieldOfficerDebug`

The plugin generates `FlavorConfig.VARIANT_NAME` + per-flavor source sets:

| Source Set | Used By |
|---|---|
| `src/commonMain/` | Both flavors — shared navigation scaffold (splash, login, auth gate) |
| `src/commonConsumer/` | Consumer flavor — wires consumer navigation graph |
| `src/commonFieldOfficer/` | Field Officer flavor — wires field officer navigation graph |

### Module Structure

Based on **kmp-project-template** conventions (reusing its module layout):

```
cmp-android / cmp-ios / cmp-desktop / cmp-web   ← platform entry points
cmp-navigation                                   ← navigation hub (flavor-gated)
cmp-shared                                       ← SharedApp() + theme host

core:analytics · core:common · core:data         ← unchanged from template
core:database · core:datastore · core:designsystem
core:domain · core:model · core:network · core:ui

# Shared feature modules (both flavors)
feature:splash · feature:login
feature:profile · feature:settings

# Consumer-only feature modules
feature:home · feature:accounts · feature:transactions
feature:send-money · feature:beneficiaries · feature:cards
feature:standing-orders · feature:atm-locator · feature:fx-rates

# Field Officer-only feature modules
feature:fo-dashboard · feature:customer-search · feature:customer-detail
feature:customer-onboarding · feature:corporate-onboarding
feature:kyc-review · feature:account-applications
feature:customer-messages · feature:meetings
```

### VARIANT_DEPENDENCY_EXCLUDES

`cmp-navigation/VARIANT_DEPENDENCY_EXCLUDES.yaml`:
```yaml
# Consumer excludes all FO feature modules
consumer:
  exclude:
    - :feature:fo-dashboard
    - :feature:customer-search
    - :feature:customer-detail
    - :feature:customer-onboarding
    - :feature:corporate-onboarding
    - :feature:kyc-review
    - :feature:account-applications
    - :feature:customer-messages
    - :feature:meetings

# Field Officer excludes all consumer-specific modules
fieldOfficer:
  exclude:
    - :feature:home
    - :feature:accounts
    - :feature:transactions
    - :feature:send-money
    - :feature:beneficiaries
    - :feature:cards
    - :feature:standing-orders
    - :feature:atm-locator
    - :feature:fx-rates
```

### Navigation Assembly

Each flavor wires its own navigation graph inside `cmp-navigation`:

**`src/commonConsumer/ConsumerNavigation.kt`**
```kotlin
@Composable
fun ConsumerApp() {
    NavHost(startDestination = SplashRoute) {
        splashGraph()
        loginGraph()
        // consumer bottom nav host:
        composable<ConsumerNavbarRoute> {
            ConsumerBottomNavHost {
                homeGraph()
                accountsGraph()
                sendMoneyGraph()
                cardsGraph()
                moreGraph() // profile, settings, standing-orders, ATM, FX
            }
        }
    }
}
```

**`src/commonFieldOfficer/FieldOfficerNavigation.kt`**
```kotlin
@Composable
fun FieldOfficerApp() {
    NavHost(startDestination = SplashRoute) {
        splashGraph()
        loginGraph()
        composable<FoDashboardNavbarRoute> {
            FoBottomNavHost {
                foDashboardGraph()
                customerSearchGraph()
                accountApplicationsGraph()
                customerMessagesGraph()
                moreGraph() // profile, settings, meetings
            }
        }
    }
}
```

---

## Backend Integration

### Open Bank Project API v7.0.0

**Base URL:** `https://apisandbox.openbankproject.com`  
**API Version:** v5.1.0 (primary), v4.0.0 (DirectLogin compat)

### Authentication (Dual Method)

**1. DirectLogin** — Form-based, sandbox-friendly
- `POST /obp/v4.0.0/my/logins/direct`
- Header: `Authorization: DirectLogin username="...", password="...", consumer_key="..."`
- Returns session token
- Best for: development, testing, sandbox

**2. OAuth/OIDC** — Production-grade, authorization_code + PKCE
- OIDC Provider: `obp-oidc`
- Discovery: `GET /obp/v5.1.0/well-known`
- Authorization: `https://apisandbox-oidc.openbankproject.com/obp-oidc/auth`
- Token: `https://apisandbox-oidc.openbankproject.com/obp-oidc/token`
- UserInfo: `https://apisandbox-oidc.openbankproject.com/obp-oidc/userinfo`
- JWKS: `https://apisandbox-oidc.openbankproject.com/obp-oidc/jwks`
- Revocation: `https://apisandbox-oidc.openbankproject.com/obp-oidc/revoke`
- Grant types: `authorization_code`, `refresh_token`, `client_credentials`
- Scopes: `openid`, `profile`, `email`
- Signing: RS256
- Claims: `sub`, `name`, `email`, `email_verified`
- Redirect URI: `org.mifos.openbanking://oauth/callback`
- Best for: production, secure multi-device auth, token refresh

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
- Consumer Key: `.env.local` (sandbox), `.env.production` (production)
- DirectLogin creds: `.env.local` only (sandbox development)
- OAuth tokens: Encrypted local storage via `CredentialStore` (at runtime)
- Refresh tokens: Encrypted local storage, auto-refresh on 401

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
| primary | #4C662B | CTAs, active states, FAB |
| on_primary | #FFFFFF | Text on primary surfaces |
| primary_container | #CDEDA3 | Balance cards, highlights |
| secondary | #386663 | Secondary actions |
| error | #BA1A1A | Errors, debit amounts, destructive |
| warning | #E8A317 | Warnings, pending states |
| surface | #FFFFFF | Cards, containers |
| background | #F9FAEF | App background |
| on_background | #1A1C16 | Primary text |
| on_surface_variant | #44483D | Secondary text |

### Typography

| Level | Font | Size | Weight |
|---|---|---|---|
| display-lg | Outfit | 32px | 600 |
| headline-lg | Outfit | 24px | 600 |
| body-lg | Outfit | 16px | 400 |
| body-md | Outfit | 14px | 400 |
| body-sm | Outfit | 12px | 400 |

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
