# mifos-x-open-banking — Requirements

Functional requirements mirror `idea-layer/idea-plan.yaml` §9 (the approved requirements source). Each FR is keyed to a feature and is the coverage source the idea-layer FR-coverage check reads. Grouped by product area below.

## Functional Requirements

### Authentication & Consent (HSBC FAPI — replaces OBP DirectLogin)

| ID | Description |
|---|---|
| FR-001 | User authenticates via HSBC Open Banking OAuth2 (FAPI 1.0 Advanced): client onboards via Dynamic Client Registration, then consent → PSU authorisation (authorization_code + PKCE, mTLS, detached JWS) → access token. Replaces OBP DirectLogin. There is no in-app password — SCA happens at the bank. |
| FR-002 | User starts the "Connect your HSBC account" journey from an intro screen explaining what Open Banking data sharing means. |
| FR-003 | User selects the data-sharing permissions and the app creates an account-access consent (status AWAU) before redirecting to the bank to authorise. |
| FR-004 | On deep-link return the app exchanges the authorisation code for a consent-scoped access token and confirms the consent reached AUTH before reading any account data. |
| FR-005 | When a prior consent is EXPD/RJCT or revoked, the user is routed to re-consent rather than into the app. |

### Consumer Banking — Account Information (AISP, read-only, consent-gated)

| ID | Description |
|---|---|
| FR-010 | Consumer sees account summary cards, recent transactions, and quick-action shortcuts on the home dashboard. |
| FR-011 | Consumer can view all authorised accounts (current, savings) with balance and status. |
| FR-012 | Consumer can view individual account details including balances and recent transactions. |
| FR-013 | Consumer can browse transaction history with date range filtering and text search. |
| FR-015 | Consumer can view their read-only beneficiaries from the AISP feed (add/edit/delete is not supported under Open Banking). |
| FR-018 | Consumer can view their read-only standing orders and open standing-order detail. |
| FR-019 | Consumer can view active direct debit mandates and their detail (read-only under AISP). |
| FR-024 | Consumer can view spending insights, budget progress, and category breakdowns over connected accounts. |
| FR-025 | Consumer can browse product reference data and compare available banking products. |
| FR-026 | Consumer can tag and categorize transactions for personal tracking (local PFM annotation). |
| FR-027 | Consumer can view business cashflow insights across their connected accounts. |

### Consumer Banking — Payments (PISP — consent → authorise → submit → status)

| ID | Description |
|---|---|
| FR-014 | Consumer can initiate a payment by selecting a payee/account and payment kind (domestic, scheduled, standing-order, international), then confirming. |
| FR-041 | Consumer enters the transfer amount and the app runs a Confirmation-of-Funds check against the source account balance before continuing. |
| FR-043 | Consumer sees a terminal payment result (amount, payee, payment id) after the bank authorisation and submission, with links to transaction detail and back to home. |
| FR-044 | Consumer authors and edits a domestic standing order (amount, frequency, start/end date, beneficiary) via the PISP standing-order consent flow. |
| FR-045 | Consumer can initiate an international (cross-currency) payment with exchange-rate information surfaced before authorising. |
| FR-046 | Payment authorisation is performed at HSBC via a redirect handoff (SCA at the bank); the app submits the payment only after the consent is authorised and never collects an SCA code in-app. |

### Consumer Banking — Consent, Notifications & Discovery

| ID | Description |
|---|---|
| FR-020 | Consumer can find nearby ATMs and branches using geolocation via unauthenticated Open Data. |
| FR-022 | Consumer can review and revoke active data-sharing consents granted to the app. |
| FR-023 | Consumer receives in-app event notifications (consent-revoked, payment status) via the Event Notification feed. |

---

## Non-Functional Requirements

These NFRs apply across all features regardless of product scope. They are determined by the architecture choice (Stream-First KMP) and must hold for any future feature added.

### Cross-platform

| ID | Description |
|---|---|
| NFR-001 | App MUST build and run on Android, iOS, Desktop (JVM), Web (Wasm + JS) from one Kotlin codebase. |
| NFR-002 | UI rendering MUST be Compose Multiplatform — no platform-specific UI fallbacks for shared screens. |
| NFR-003 | Platform-specific concerns (locale source, native splash, file paths) MUST use `expect`/`actual` via `Platform.kt`. |

### Architecture

| ID | Description |
|---|---|
| NFR-004 | All ViewModels MUST extend `BaseViewModel` and expose state via `ScreenDataStream` (Stream-First pattern). |
| NFR-005 | Network-backed repositories MUST use Store5 (`mobile.kotlin.store`) for cache-then-network behavior. |
| NFR-006 | DI MUST use Koin (`org.koin.koin-core`) with feature-scoped modules; no service-locators outside `koinInject`. |

### Observability

| ID | Description |
|---|---|
| NFR-007 | App MUST log uncaught crashes to Firebase Crashlytics (Android-only, no-op elsewhere). |
| NFR-008 | App MUST report cold-start + frame-time metrics to Firebase Performance (Android-only). |

### Performance

| ID | Description |
|---|---|
| NFR-009 | Cold start on mid-tier Android (Pixel 6a-class): < 1.5 s. |
| NFR-010 | Navigation between screens: transitions complete within 300 ms. |

### Accessibility

| ID | Description |
|---|---|
| NFR-011 | All interactive components MUST have minimum 48dp touch target (Material 3). |
| NFR-012 | Color contrast for text MUST meet WCAG AA (≥ 4.5:1 normal text). |
| NFR-013 | All images MUST have content descriptions; navigation actions MUST have accessibility labels. |

### Internationalization

| ID | Description |
|---|---|
| NFR-014 | All user-visible strings MUST live in `composeResources/values/strings.xml` and use string resources, no hard-coded literals. |
| NFR-015 | Date display MUST use locale-aware formatting. |
| NFR-016 | Currency display (when applicable) MUST use locale-aware formatting. |
