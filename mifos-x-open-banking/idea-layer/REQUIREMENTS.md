# mifos-x-open-banking — Requirements

Functional requirements mirror `idea-layer/idea-plan.yaml` §9 (the approved requirements source). Each FR is keyed to a feature and is the coverage source the idea-layer FR-coverage check reads. Grouped by product area below.

## Functional Requirements

### Authentication

| ID | Description |
|---|---|
| FR-001 | User authenticates via OBP DirectLogin (username + password + consumer key) to obtain a session token. |
| FR-002 | User can request a password reset link sent to their registered email. |
| FR-003 | Authenticated user can change password with current-password verification. |

### Consumer Banking — Home & Accounts

| ID | Description |
|---|---|
| FR-010 | Consumer sees account summary cards, recent transactions, and quick-action shortcuts on the home dashboard. |
| FR-011 | Consumer can view all accounts (savings, current, loan) with balance and status. |
| FR-012 | Consumer can view individual account details including balance history and recent transactions. |
| FR-013 | Consumer can browse transaction history with date range filtering and text search. |

### Consumer Banking — Payments & Beneficiaries

| ID | Description |
|---|---|
| FR-014 | Consumer can initiate a money transfer by selecting a beneficiary, entering amount, and confirming. |
| FR-015 | Consumer can add, edit, and delete saved transfer recipients. |
| FR-041 | Consumer enters the transfer amount, selects the beneficiary and payment rail, and sees a live funds check against the source account balance before continuing. |
| FR-042 | Consumer enters the one-time SCA code to authorise an above-threshold payment (Strong Customer Authentication step) before submission. |
| FR-043 | Consumer sees a terminal payment confirmation showing the amount, payee, and transaction id, with links to the transaction detail and back to home. |

### Consumer Banking — Cards

| ID | Description |
|---|---|
| FR-016 | Consumer can view all payment cards, see balances, and navigate to card details. |
| FR-017 | Consumer can freeze/unfreeze a card and view card-specific transaction history. |

### Consumer Banking — Recurring & Mandates

| ID | Description |
|---|---|
| FR-018 | Consumer can view and manage recurring automated payments. |
| FR-019 | Consumer can view active direct debit mandates and cancel unwanted ones. |
| FR-044 | Consumer authors a new recurring standing order (amount, frequency, start/end date, beneficiary) and submits it via POST. |

### Consumer Banking — Discovery & Insights

| ID | Description |
|---|---|
| FR-020 | Consumer can find nearby ATMs and branches using geolocation. |
| FR-021 | Consumer can view live foreign exchange rates and convert between currencies. |
| FR-022 | Consumer can review and revoke OAuth consents granted to third-party apps. |
| FR-023 | Consumer receives in-app notifications for payment status, KYC updates, and alerts. |
| FR-024 | Consumer can view spending insights, budget progress, and category breakdowns. |
| FR-025 | Consumer can browse available banking products and view terms. |
| FR-026 | Consumer can tag and categorize transactions for personal tracking. |

### Field Officer

| ID | Description |
|---|---|
| FR-030 | Field officer sees daily metrics (customers onboarded, applications pending, meetings today). |
| FR-031 | Field officer can search customers by name, ID number, or phone. |
| FR-032 | Field officer views customer 360: accounts, KYC status, application history. |
| FR-033 | Field officer completes multi-step individual customer onboarding (personal info, KYC docs, account selection). |
| FR-034 | Field officer completes multi-step corporate onboarding (business info, directors, documentation). |
| FR-035 | Field officer reviews uploaded KYC documents and approves/rejects with notes. |
| FR-036 | Field officer reviews pending account applications with filtering by status. |
| FR-037 | Field officer approves or rejects an individual account application with comments. |
| FR-038 | Field officer can send and receive secure messages with assigned customers. |
| FR-039 | Field officer can schedule, view, and manage customer meetings. |
| FR-040 | New agent/field officer can register with required credentials for admin approval. |

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
