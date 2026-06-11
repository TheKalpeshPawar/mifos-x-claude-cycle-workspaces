# Mifos-X Open Banking — Consumer Open Banking KMP App

**Vision:** Build a Kotlin Multiplatform (KMP) consumer Open Banking app — a regulated Third-Party Provider (AISP + PISP) on HSBC's UK/CE Open Banking sandbox — that lets a person connect their HSBC account by consent and redirect-based authorisation, then view their finances and initiate payments from a single Compose Multiplatform codebase across Android, iOS, Desktop, and Web.

---

## Product Overview

### Personas

**Consumer (Alex)**
- Age: 28, Tech-savvy retail customer
- Needs: Connect a bank account safely, see balances and transactions in one place, send money, set up recurring payments, manage who can access their data
- Motivation: Convenience, security, transparency and control over their finances
- Primary flows: Connect HSBC account (consent + authorise at the bank) → View accounts → Review transactions → Pay → Manage consents

This is a single-persona consumer product. There is no field-officer or agent-banking persona — HSBC Open Banking is consumer PSD2 and exposes no officer/onboarding/KYC surface.

### Brand Identity

| Attribute | Value |
|---|---|
| Primary Color | Deep Indigo `#1800B1` |
| Secondary Color | Muted Violet `#575899` |
| Error / Debit | Red `#BA1A1A` |
| Font Family | Outfit (all surfaces) |
| Tone | Professional, Trustworthy, Transparent |
| Key Message | "Your bank, your data, your control" |

---

## Architecture

### Tech Stack

| Layer | Tech | Notes |
|---|---|---|
| UI | Compose Multiplatform 1.8.2 | Single KMP UI codebase |
| Networking | Ktor 3.2.0 + Ktorfit 2.5.2 | HSBC Open Banking REST client (OBIE v4.0) over mTLS |
| State Management | Store5 + BaseViewModel + ScreenDataStream | Stream-First reactive architecture |
| Local Storage | Room KMP 2.7.2 | Cross-platform persistence (consent + token cache) |
| Serialization | Kotlinx Serialization | Type-safe JSON, `@Serializable` routes |
| Dependency Injection | Koin 4.1.0 | Lightweight, multiplatform |
| Navigation | Jetpack Navigation Compose | Type-safe `@Serializable` route objects |
| Build System | Gradle 8.0+ + kmp-product-flavors 2.4.3 | Variant matrix + source set gating |

### External API Consumer (no owned backend)

This project owns no backend and no database. It is a pure KMP client that consumes the external HSBC UK/CE Open Banking REST API. The artifacts under `idea-layer/server/` are CLIENT contracts (Ktorfit codegen inputs), not owned-backend schema. The only local persistence is a cache of the active consent and access/refresh tokens.

### Module Structure

Based on **kmp-project-template** conventions (reusing its module layout):

```
cmp-android / cmp-ios / cmp-desktop / cmp-web   ← platform entry points
cmp-navigation                                   ← navigation hub
cmp-shared                                       ← SharedApp() + theme host

core:analytics · core:common · core:data         ← shared infrastructure
core:database · core:datastore · core:designsystem
core:domain · core:model · core:network · core:ui

# Consumer feature modules
feature:consent · feature:home · feature:accounts · feature:transactions
feature:send-money · feature:beneficiaries · feature:standing-orders
feature:direct-debits · feature:atm-locator · feature:pfm
feature:products · feature:consents · feature:notifications
feature:profile · feature:settings
```

### Navigation Assembly

The app wires a single consumer navigation graph inside `cmp-navigation`. Entry is gated by consent: on launch, Splash checks for a valid, authorised account-access consent and token. With no consent the user enters the consent-onboarding journey; with a valid consent they land on Home.

**`ConsumerNavigation.kt`**
```kotlin
@Composable
fun App() {
    NavHost(startDestination = SplashRoute) {
        splashGraph()
        consentGraph()          // consent-intro → consent-request → bank-authorize-handoff → auth-callback
        composable<NavbarRoute> {
            BottomNavHost {
                homeGraph()
                accountsGraph()
                payGraph()      // send-money → authorize handoff → result
                insightsGraph() // pfm-dashboard, business-insights
                moreGraph()     // profile, settings, consents, notifications
            }
        }
    }
}
```

---

## Backend Integration

### HSBC UK/CE Open Banking — OBIE Read/Write Standard v4.0

**Resource Base URL:** `https://secure.sandbox.ob.hsbc.co.uk` (UK Personal — mTLS resource host)
**Authorize Base URL:** `https://sandbox.ob.hsbc.co.uk` (UK Personal — OAuth authorize host)
**Standard:** OBIE UK Open Banking Read/Write v4.0 (CE HSBCnet + Malta Personal on v3.1)
**Default brand:** `uk-personal` (1 of 10 per-brand host sets)

### Authentication — FAPI 1.0 Advanced (consent + redirect)

There is NO in-app password and NO DirectLogin. The user authenticates at HSBC during a redirect; Strong Customer Authentication (SCA) happens at the bank, never in-app.

- **Transport:** mutual TLS (mTLS) — QWAC transport cert + QSEAL signing cert.
- **Onboarding:** Dynamic Client Registration (DCR) — `POST /register` with a signed SSA (software statement) → client credentials.
- **Authorization:** OAuth2 — `client_credentials` stages a consent, then `authorization_code` + PKCE (S256) for PSU authorisation. Pattern: create-consent → authorize → token → resource.
- **Message signing:** detached JWS in the `x-jws-signature` header on write calls; `x-fapi-*` headers throughout.
- **Redirect URI:** `org.mifos.openbanking://oauth/callback`

### Consent-driven model

Every account read requires a prior AUTH-status account-access-consent and a consent-scoped access token. Every payment requires its own payment-consent and a fresh authorise redirect (one payment = one consent = one authorisation). The Initiation block submitted to the payment endpoint must byte-match the authorised consent.

### API Groups (14 groups, 85 endpoints)

| Group | Role | Purpose |
|---|---|---|
| Authentication & Onboarding | security | DCR, OAuth2 token, PSU authorise redirect |
| Account Information (AISP) | aisp | accounts, balances, transactions, beneficiaries, standing orders, direct debits, scheduled payments, party, products, statements (read-only) |
| Confirmation of Funds (CBPII) | cbpii | pre-payment funds check |
| Variable Recurring Payments (VRP) | pisp | recurring / sweeping payments |
| Domestic Payment | pisp | single immediate domestic payment |
| Domestic Scheduled Payment | pisp | future-dated domestic payment |
| Domestic Standing Order | pisp | recurring domestic schedule |
| International Payment | pisp | cross-currency payment |
| International Scheduled Payment | pisp | future-dated international payment |
| International Standing Order | pisp | recurring international schedule |
| File Payment / bulk | pisp | ISO 20022 pain.001 batch payment |
| Multi-Bill Payment | pisp (HSBC-specific) | UK Business bulk bill pay |
| Event Notification | events | real-time consent-revoked + status events |
| Open Data | opendata | unauthenticated ATM/branch locator + product reference |

**Credential Storage:**
- mTLS certs, signing keys, client ID, software statement: gitignored local materials + `.env.local`, referenced by env-var name only (never values) — RULE-CREDS-LIFECYCLE-001.
- Access/refresh tokens: encrypted local cache, scoped to the active consent, auto-refresh on 401.

---

## Core Models

### Domain Objects (Shared)

```yaml
# idea-layer/dtos/Account.yaml — OBIE AISP shape (read-only)
Account:
  accountId: String
  currency: String
  accountType: Personal | Business
  accountSubType: CurrentAccount | Savings | CreditCard
  nickname: String
  account:                       # identification block
    schemeName: String           # e.g. UK.OBIE.SortCodeAccountNumber
    identification: String
    name: String
  servicer: ServicingInstitution
```

```yaml
# idea-layer/dtos/Transaction.yaml — OBIE AISP shape (read-only)
Transaction:
  transactionId: String
  accountId: String
  creditDebitIndicator: Credit | Debit
  status: Booked | Pending
  amount: Money                  # Amount + Currency
  bookingDateTime: Instant
  valueDateTime: Instant
  transactionInformation: String
  merchantDetails: MerchantDetails
  proprietaryBankTransactionCode: String
```

```yaml
# idea-layer/dtos/Consent.yaml — the access-control object (new SoT)
Consent:
  consentId: String
  type: AccountAccess | DomesticPayment | InternationalPayment | FundsConfirmation | VRP
  status: AWAU | AUTH | EXPD | RJCT | Revoked
  permissions: List<String>      # ReadAccountsDetail, ReadBalances, ReadTransactionsDetail, ...
  expirationDateTime: Instant
  creationDateTime: Instant
```

---

## Feature Roadmap

### Phase 1: Consent Onboarding (MVP foundation)

1. **Splash & consent gate** — restore consent/token, route to onboarding or Home
2. **Consent intro & request** — explain data-sharing, pick permissions, create account-access-consent
3. **Bank authorise handoff** — build signed authorise request, redirect to HSBC
4. **Auth callback** — exchange code for token, confirm consent AUTH, enter app

### Phase 2: Account Information (AIS)

1. **Home** — connected-account overview, recent transactions, quick actions
2. **Accounts** — list, detail, balances
3. **Transactions** — history, search, detail, tagging
4. **Beneficiaries / Standing Orders / Direct Debits / Scheduled Payments** — read-only AIS views
5. **Products & Statements** — read-only reference

### Phase 3: Payments (PISP)

1. **Domestic payment** — build, funds-check (CoF), authorise at bank, submit, poll status
2. **Domestic scheduled & standing order** — future-dated and recurring
3. **International payment** — cross-currency with exchange-rate information
4. **Payment result / declined** — terminal states with transaction handoff

### Phase 4: Advanced Capabilities

1. **Variable Recurring Payments (VRP)** — recurring / sweeping mandates
2. **Confirmation of Funds (CoF)** — standalone funds check
3. **Open Data** — ATM/branch locator + product comparison (unauthenticated)
4. **Event Notification** — real-time consent-revoked + payment status events
5. **Consent management** — view and revoke data-sharing consents

---

## Screen Inventory (39 Screens)

### Consent & Authorisation (7 screens)

| Screen | Purpose | API Group |
|---|---|---|
| splash | Consent/token gate + routing | — |
| consent-intro | Explain data sharing, start connect | — |
| consent-request | Pick permissions, create account-access-consent | AISP |
| bank-authorize-handoff | Build signed authorise request, redirect to HSBC | auth |
| auth-callback | Exchange code for token, confirm consent AUTH | auth |
| consent-declined | PSU declined / callback error recovery | — |
| consent-expired | Re-consent when prior consent EXPD/RJCT/revoked | AISP |

### Account Information (15 screens)

| Screen | Purpose | API Group |
|---|---|---|
| home | Connected-account overview, recent activity | AISP |
| accounts | Authorised account list | AISP |
| account-detail | Single account + balances | AISP |
| transactions | Transaction history + search | AISP |
| transaction-detail | Single transaction receipt | AISP |
| transaction-tags | Categorise transactions (local PFM) | AISP |
| beneficiaries | Read-only beneficiaries | AISP |
| standing-orders | Read-only standing orders | AISP |
| standing-order-detail | Single standing order | AISP |
| direct-debits | Read-only direct debits | AISP |
| direct-debit-detail | Single mandate | AISP |
| products | Product reference + comparison | AISP / Open Data |
| pfm-dashboard | Spending insights, budgets | AISP |
| pfm-settings | Budget / category configuration | AISP |
| business-insights | Business cashflow insights | AISP |

### Payments (10 screens)

| Screen | Purpose | API Group |
|---|---|---|
| send-money | Pick payee / account, payment kind | PISP |
| send-money-amount | Amount entry + Confirmation-of-Funds check | PISP / CBPII |
| send-money-confirm | Review, create payment-consent | PISP |
| payment-authorize-handoff | Build signed authorise request, redirect to HSBC | auth |
| payment-result | Terminal payment status | PISP |
| payment-declined | PSU declined / consent RJCT recovery | PISP |
| standing-order-create | Author a domestic standing order | PISP |
| standing-order-edit | Edit a standing order | PISP |
| auth-callback | Shared redirect-return (also used by consent) | auth |
| atm-locator | ATM / branch finder | Open Data |

### Consents, Notifications & App (7 screens)

| Screen | Purpose | API Group |
|---|---|---|
| consent-manager | View / revoke data-sharing consents | events / AISP |
| notifications | Event feed (consent-revoked, payment status) | events |
| profile | User-visible app profile | — |
| settings | App preferences | — |
| about | App info, version, legal links | — |
| terms-of-service | Legal | — |
| privacy-policy | Legal | — |
| licenses | Open-source attributions | — |

> `auth-callback` and `atm-locator` are listed once in their primary group; the navigation graph reuses `auth-callback` across both the consent and payment authorise journeys.

---

## Navigation Architecture

### Consumer Navigation Graph

```
Splash
  ├─ no consent → Consent Intro → Consent Request → Bank Authorize Handoff → Auth Callback
  │                                                     │
  │                                                     ├─ AUTH → Home
  │                                                     └─ declined → Consent Declined
  ├─ valid consent → Home (Bottom Nav)
  └─ expired/revoked → Consent Expired → Consent Request

Home (Bottom Nav)
  ├─ Home → Account Detail → Transaction Detail
  ├─ Accounts → Account Detail
  ├─ Pay → Send Money → Amount (CoF) → Confirm → Payment Authorize Handoff → Auth Callback → Payment Result
  ├─ Insights → PFM Dashboard / Business Insights
  └─ More → Profile / Settings / Consents / Notifications / About
```

---

## Design System

### Color Tokens

| Token | Value | Usage |
|---|---|---|
| primary | #1800B1 | CTAs, active states, FAB |
| on_primary | #FFFFFF | Text on primary surfaces |
| primary_container | #403CD8 | Balance cards, highlights |
| secondary | #575899 | Secondary actions |
| error | #BA1A1A | Errors, debit amounts, destructive |
| surface | #FCF8FF | Cards, containers |
| background | #FCF8FF | App background |
| on_background | #1B1B24 | Primary text |
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
- Custom: AccountCard, TransactionRow, ConsentCard, PermissionToggle

---

## Quality Standards

- **Type Safety:** 100% Kotlin, non-null by default
- **Null Safety:** Explicit optionals via `?`
- **Testability:** ViewModel + StateFlow + repository pattern
- **Accessibility:** Material 3 A11y semantics
- **Performance:** <500ms account load, <200ms transaction list
- **Security:** mTLS, detached JWS on writes, TLS 1.3, no plaintext token storage

---

## Success Metrics

1. **Adoption:** 1000+ connected consumers in pilot
2. **Connect success:** >90% of started consent journeys reach AUTH
3. **Payment success:** >95% of authorised payments reach a settled status
4. **NPS:** >50
5. **Uptime:** 99.9% availability

---

## Timeline

- **M1 (Jan–Mar):** Consent onboarding + AIS (accounts, transactions)
- **M2 (Apr–Jun):** Payments (domestic, scheduled, standing order, international)
- **M3 (Jul–Sep):** VRP, CoF, Open Data, Event Notification, consent management
- **M4 (Oct–Dec):** Production hardening, scale testing

---

## Ideas Backlog

| # | Description | Feature | Status |
|---|---|---|---|
