<!-- source: screens/scheduled-payments/ui.yaml -->
<!-- source_hash: regenerated-2026-07-16 -->
<!-- generated: 2026-07-16T00:00:00Z -->

# SPEC — scheduled-payments

_Generated: 2026-07-16 · Source: idea-layer/screens/scheduled-payments/ui.yaml_

---

## 1. Feature Overview

**Name:** Scheduled Payments  
**Archetype:** index_list  
**Cluster:** payments-context  
**Status:** enriched → designed → approved  
**Quality score:** 96  
**Acceptance refs:** FR-006  

**Description:**  
Calls `GET /accounts/{AccountId}/scheduled-payments` via ktorfit to retrieve
`OBReadScheduledPayment3`. ViewModel maps each `Data.ScheduledPayment` to a UiModel:
`CreditorAccount.Name` (payee display name); `InstructedAmount.Amount` +
`InstructedAmount.Currency` formatted as a currency string (e.g. `GBP 842.00`);
`ScheduledPaymentDateTime` (ISO-8601) formatted as `EEE d MMM yyyy`
(e.g. `Thu 31 Jul 2026`); `ScheduledType` enum mapped to a human-readable chip label —
`Execution` → `'Execution date'` (money leaves account on that date),
`Arrival` → `'Arrival date'` (funds arrive at beneficiary on that date);
`CreditorAccount.Identification` (UK sort code + account number, e.g. `08-32-00 12001039`)
shown as destination account; `Reference` as payment narrative. Read-only under AISP
consent using `ReadScheduledPaymentsDetail` permission.
`ScheduledType` icon: `calendar_today` for Execution, `arrow_downward` for Arrival.

**Libraries:**

| Library | Purpose |
|---|---|
| `ktorfit` | HSBC AIS HTTP client for `GET /accounts/{AccountId}/scheduled-payments` |
| `hsbc-obie-ais-v4.0:scheduled-payments` | `OBReadScheduledPayment3` response schema; `ScheduledType` Execution/Arrival enum |

---

## 2. Screen Inventory

| Screen | Archetype | Initial state | Shell |
|---|---|---|---|
| scheduled-payments | index_list | loading | Bottom nav visible · Top app bar `{strings.sp_screen_title}` · Back leading icon · No FAB |

**Route:** `accounts/{accountId}/scheduled-payments`  
**Entry point:** account-detail (tap Scheduled chip, passes `accountId`)

---

## 3. States

| State | Trigger |
|---|---|
| `loading` | Screen mounts; `GET /accounts/{AccountId}/scheduled-payments` in flight |
| `content` | API returns non-empty `Data.ScheduledPayment[]` |
| `empty` | API returns empty `Data.ScheduledPayment[]` |
| `error` | 401 TokenExpired / 403 ConsentRevoked / 429 RateLimited / IOException NetworkError |

---

## 4. Components

### State: `loading`

| ID | Type | State binding | Purpose |
|---|---|---|---|
| _(no id)_ | progress_indicator (variant=circular) | loading | Indicate async fetch of `OBReadScheduledPayment3` from HSBC AIS endpoint |

### State: `content` — all states (navigation)

| ID | Type | State binding | Purpose |
|---|---|---|---|
| `back_button` | icon_button (icon=arrow_back) | all | Return user to account-detail screen; discards scheduled-payments context |

**back_button action contract:**

| Component | Action | Effect | Library refs | Description |
|---|---|---|---|---|
| `back_button` | `navigate_back` | navigate | — | Pops the scheduled-payments screen from the back stack, returning the user to account-detail. |

### State: `content` — list

| ID | Type | State binding | Purpose |
|---|---|---|---|
| `scheduled_payments_list` | list (scroll_direction=vertical, api_id=scheduled-payments-list) | content | Render full `OBReadScheduledPayment3 Data.ScheduledPayment` array for the account |
| `scheduled_payment_card` | card (elevation=1) — child of list | content | Container per scheduled payment; groups all payment fields for one future-dated instruction |
| `sp_payee_name` | text (titleMedium, role=title) — child of card | content | Payee name from `CreditorAccount.Name`; `i18n: skip` (proper noun) |
| `sp_amount` | text (headlineSmall, color=error, role=amount) — child of card | content | `{item.InstructedAmount.Currency} {item.InstructedAmount.Amount}` (e.g. `GBP 842.00`); `i18n: skip` |
| `sp_scheduled_date` | text (bodySmall, color=on-surface-variant, role=body) — child of card | content | `{strings.sp_due_prefix} {item.scheduledDateFormatted}` — ISO-8601 ScheduledPaymentDateTime formatted as `EEE d MMM yyyy` by ViewModel |
| `sp_type_chip` | chip (variant=assist, color=secondary-container) — child of card | content | `ScheduledType` chip: `'Execution date'` (icon=`calendar_today`) or `'Arrival date'` (icon=`arrow_downward`); ViewModel maps OBIE enum to label, icon, and a11y string |
| `sp_account_id` | text (labelSmall, color=on-surface-variant, role=caption) — child of card | content | `{strings.sp_account_prefix} {item.CreditorAccount.Identification}` — destination sort code + account number; `i18n: skip` |
| `sp_reference` | text (labelSmall, color=on-surface-variant, role=caption) — child of card | content | `{strings.sp_ref_prefix} {item.Reference}` — payment narrative |

### State: `empty`

| ID | Type | State binding | Purpose |
|---|---|---|---|
| `empty_scheduled_payments` | empty_state (icon=schedule) | empty | Zero-result state when `Data.ScheduledPayment[]` is empty in OBIE response |

### State: `error`

| ID | Type | State binding | Purpose |
|---|---|---|---|
| `error_state` | empty_state (variant=error, icon=error_outline) | error | Surface typed API errors (401/403/429/network) with actionable `{error.message}` |
| `retry_button` | button (variant=filled) — child of error_state | error | Re-triggers `LoadScheduledPayments` ViewModel action after transient failure |

**retry_button action contract:**

| Component | Action | Effect | Library refs | Description |
|---|---|---|---|---|
| `retry_button` | `retry_load` | call_api | `ktorfit`, `hsbc-obie-ais-v4.0:scheduled-payments` | Re-triggers `LoadScheduledPayments` ViewModel action after a transient failure (401, 429, or network error), issuing `GET /accounts/{AccountId}/scheduled-payments` and returning to Loading then Content or Empty. |

---

## 5. ViewModel Contract

**ViewModel:** `ScheduledPaymentsViewModel`  
**State class:** `ScheduledPaymentsState`  
**Sealed class:** `ScheduledPaymentsUiState`

### State Fields

| Field | Type | Description |
|---|---|---|
| `uiState` | `ScheduledPaymentsUiState` | Sealed class governing which UI surface is active |

### Sealed Class Members

| Member | Fields |
|---|---|
| `Loading` | — |
| `Content` | `scheduledPayments: List<ScheduledPaymentUiModel>` |
| `Empty` | — |
| `Error` | `type: ScheduledPaymentsError`, `message: String` |

### Error Types

| Type | HTTP trigger | Recovery |
|---|---|---|
| `TokenExpired` | 401 | Route to login screen |
| `ConsentRevoked` | 403 | Route to consent-list screen |
| `RateLimited` | 429 | Retry button shown; exponential back-off in ViewModel |
| `NetworkError` | IOException / timeout | Retry button re-triggers `LoadScheduledPayments` |

### Actions

| Action | Signature | Side Effects |
|---|---|---|
| `LoadScheduledPayments` | `suspend fun loadScheduledPayments(accountId: String)` | Sets `uiState = Loading`; calls `GET /accounts/{accountId}/scheduled-payments` via Ktorfit `AisApiService`; maps response via `toUiModel()` — formats `ScheduledPaymentDateTime`, maps `ScheduledType` enum to label/icon/a11y; sets `uiState = Content` \| `Empty` \| `Error` |
| `RetryLoad` | `fun retryLoad()` | Re-invokes `LoadScheduledPayments` with same `accountId` |
| `NavigateBack` | `fun navigateBack()` | Emits `NavigationEvent.Back` to `NavController` |

**`toUiModel()` mapping notes:**

- `ScheduledPaymentDateTime` ISO-8601 → `scheduledDateFormatted` (`EEE d MMM yyyy`)
- `ScheduledType.Execution` → `scheduledTypeLabel='Execution date'`, `scheduledTypeIcon='calendar_today'`, `scheduledTypeA11y='Money leaves your account on {date}'`
- `ScheduledType.Arrival` → `scheduledTypeLabel='Arrival date'`, `scheduledTypeIcon='arrow_downward'`, `scheduledTypeA11y='Funds arrive at {payee} on {date}'`

### DI

- `AisApiService` — Koin inject; Ktorfit implementation from client-layer
- `ScheduledPaymentUiModelMapper` — maps `OBReadScheduledPayment3` to `UiModel`

---

## 6. Error Cases

| ID | Trigger | User message | Recovery |
|---|---|---|---|
| `TokenExpired` | HTTP 401 from HSBC AIS | Session expired. Please log in again. | Route to login screen |
| `ConsentRevoked` | HTTP 403 from HSBC AIS | Account access consent has been revoked. | Route to consent-list screen |
| `RateLimited` | HTTP 429 from HSBC AIS | Too many requests. Please wait a moment and try again. | Retry button; exponential back-off in ViewModel |
| `NetworkError` | IOException / timeout | No network connection. Check your connection and retry. | Retry button re-triggers `LoadScheduledPayments` |
| `EmptyResult` | `Data.ScheduledPayment[]` is empty | No future-dated payments are pending for this account. | Empty state shown; no retry button |

---

## 7. Navigation

| Entry | Source | Trigger | Params |
|---|---|---|---|
| → scheduled-payments | account-detail | Tap Scheduled chip | `accountId: String` |

| From | To | Trigger |
|---|---|---|
| scheduled-payments | account-detail | Tap back button |

---

## 8. Test Scenarios

8 scenarios (source: `screens/scheduled-payments/tests.yaml`)

| ID | Description | State | Priority |
|---|---|---|---|
| TC-SP-001 | Scheduled payments list loads and renders all pending payments | content | p0 |
| TC-SP-002 | Loading state shown during scheduled payments fetch | loading | p0 |
| TC-SP-003 | Empty state when no scheduled payments pending | empty | p1 |
| TC-SP-004 | Error state with Retry button on 401 token expired | error | p0 |
| TC-SP-005 | Back button navigates to account-detail | content | p1 |
| TC-SP-006 | Error state shows consent-revoked message on 403 | error | p1 |
| TC-SP-007 | ScheduledType=Arrival renders 'Arrival date' chip with arrow_downward icon | content | p1 |
| TC-SP-008 | CreditorAccount.Identification (sort code + account number) is displayed in each card | content | p2 |
