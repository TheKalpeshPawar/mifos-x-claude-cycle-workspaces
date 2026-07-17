<!-- source: screens/standing-orders/ui.yaml -->
<!-- source_hash: regenerated-2026-07-16 -->
<!-- generated: 2026-07-16T00:00:00Z -->

# SPEC — standing-orders

_Generated: 2026-07-16 · Source: idea-layer/screens/standing-orders/ui.yaml_

---

## 1. Feature Overview

**Name:** Standing Orders  
**Archetype:** index_list  
**Cluster:** payments-context  
**Status:** enriched → designed → approved  
**Quality score:** 95  
**Acceptance refs:** FR-006  

**Description:**  
Calls `GET /accounts/{AccountId}/standing-orders` via ktorfit to retrieve
`OBReadStandingOrder6`. Maps `CreditorAccount.Name`, `CreditorAccount.Identification`,
`NextPaymentAmount`, `NextPaymentDateTime`, `FinalPaymentDateTime` (when non-null),
`Reference`, and `StandingOrderStatusCode` per `Data.StandingOrder`.
OBIE ISO 20022 frequency codes (`IntrvlMnthDay`, `IntrvlWkDay`, `IntrvlDay`, `IntrvlYear`)
are decoded to human-readable labels in `StandingOrdersViewModel` via a sealed
`FrequencyDecoder`; Active/Inactive status drives badge variant (primary/secondary);
`hasFinalPayment` flag controls `FinalPaymentDateTime` row visibility; summary label
(e.g. `'3 Active · 1 Inactive'`) is computed as `SummaryLabel` and emitted in
`UiState.Content`.

**Libraries:**

| Library | Purpose |
|---|---|
| `ktorfit` | HSBC AIS HTTP client for `GET /accounts/{AccountId}/standing-orders` |
| `hsbc-obie-ais-v4.0:standing-orders` | `OBReadStandingOrder6` response schema; OBIE ISO 20022 frequency codes; `StandingOrderStatusCode` enum |

**Consent requirement:** `ReadStandingOrdersDetail` AISP permission.  
Note: `ReadStandingOrders` alone is NOT sufficient — it omits `NextPaymentAmount` and `Reference`.

---

## 2. Screen Inventory

| Screen | Archetype | Initial state | Shell |
|---|---|---|---|
| standing-orders | index_list | loading | Bottom nav visible · Top app bar `{strings.standing_orders_screen_title}` · Back leading icon · No FAB |

**Route:** `StandingOrdersRoute(accountId: String)`  
**Entry point:** account-detail (tap Standing Orders chip, passes `accountId`)

---

## 3. States

| State | Trigger |
|---|---|
| `loading` | Screen mounts; `GET /accounts/{AccountId}/standing-orders` in flight |
| `content` | API returns non-empty `Data.StandingOrder[]`; `summaryLabel` computed |
| `empty` | API returns empty `Data.StandingOrder[]` |
| `error` | 401 `TokenExpiredError` / 403 `ConsentRevokedError` / 429 `RateLimitedError` / IOException `NetworkError` / 5xx `ServerError` |

---

## 4. Components

### State: `loading`

| ID | Type | State binding | Purpose |
|---|---|---|---|
| _(no id)_ | progress_indicator (variant=circular) | loading | Indicate async fetch of `OBReadStandingOrder6` from HSBC AIS endpoint |

### Navigation (all states)

| ID | Type | State binding | Purpose |
|---|---|---|---|
| `back_button` | icon_button (icon=arrow_back) | all | Return user to account-detail screen; emits `NavigationEvent.Back` |

**back_button action contract:**

| Component | Action | Effect | Library refs | Description |
|---|---|---|---|---|
| `back_button` | `navigate_back` | navigate | — | Pops the standing-orders screen from the back stack, returning the user to account-detail. |

### State: `content`

| ID | Type | State binding | Purpose |
|---|---|---|---|
| `summary_row` | text (labelMedium, color=on-surface-variant, role=subtitle) | content | ViewModel-computed summary label (e.g. `3 Active · 1 Inactive`) from `StandingOrderStatusCode` counts |
| `standing_orders_list` | list (scroll_direction=vertical, pull_to_refresh=true, pull_to_refresh_action=retry_load) | content | Full `OBReadStandingOrder6 Data.StandingOrder` array; pull-to-refresh re-triggers `LoadStandingOrders` |
| `standing_order_card` | card (elevation=1) — child of list | content | Per-standing-order container grouping all payment fields for one recurring instruction |
| `so_payee_name` | text (titleMedium, role=title) — child of card | content | Beneficiary name from `CreditorAccount.Name` |
| `so_status_badge` | badge — child of card | content | `Active` (variant=primary) / `Inactive` (variant=secondary); variant mapped in ViewModel from `StandingOrderStatusCode` |
| `so_amount` | text (headlineSmall, color=on-surface, role=amount) — child of card | content | `{item.NextPaymentAmount.Amount} {item.NextPaymentAmount.Currency}` (on-surface color — read-only banking view, not error) |
| `so_frequency` | text (bodySmall, color=on-surface-variant, role=body) — child of card | content | Human-readable frequency decoded in ViewModel via `FrequencyDecoder`; covers `IntrvlMnthDay`, `IntrvlWkDay`, `IntrvlDay`, `IntrvlYear` OBIE patterns; unknown codes fall back to raw OBIE code string |
| `so_next_date` | text (bodySmall, color=on-surface-variant, role=body) — child of card | content | `{strings.standing_orders_next_prefix} {item.NextPaymentDateTime}` — ISO-8601 formatted as `dd MMM yyyy` by ViewModel |
| `so_final_date` | text (bodySmall, color=on-surface-variant, role=body) — child of card | content | `{strings.standing_orders_final_prefix} {item.FinalPaymentDateTime}` — visible only when `{item.hasFinalPayment}` is true; `hasFinalPayment` flag set in ViewModel when `FinalPaymentDateTime != null` |
| `so_sort_code` | text (bodySmall, color=on-surface-variant, role=body) — child of card | content | `{item.CreditorAccount.Identification}` — UK sort code + account number (format: `40-12-09 65872310`) |
| `so_payment_ref` | text (bodySmall, color=on-surface-variant, role=body) — child of card | content | `{strings.standing_orders_ref_prefix} {item.Reference}` — payment reference (e.g. `RENT-FLAT12`) |

### State: `empty`

| ID | Type | State binding | Purpose |
|---|---|---|---|
| `empty_standing_orders` | empty_state (icon=autorenew) | empty | Zero-result state when `Data.StandingOrder[]` is empty in OBIE response |

### State: `error`

| ID | Type | State binding | Purpose |
|---|---|---|---|
| `error_state` | empty_state (variant=error, icon=error_outline) | error | Surface typed API errors (401/403/429/network/5xx) with ViewModel-resolved `{error.message}` |
| `retry_button` | button (variant=filled) — child of error_state | error | Re-triggers `LoadStandingOrders` ViewModel action after transient failure |

**retry_button action contract:**

| Component | Action | Effect | Library refs | Description |
|---|---|---|---|---|
| `retry_button` | `retry_load` | call_api | `ktorfit`, `hsbc-obie-ais-v4.0:standing-orders` | Re-triggers `LoadStandingOrders` ViewModel action after a transient failure (401, 429, or network error), issuing `GET /accounts/{AccountId}/standing-orders` and returning to Loading then Content or Empty. |

---

## 5. ViewModel Contract

**ViewModel:** `StandingOrdersViewModel`  
**State class:** `StandingOrdersState`  
**Sealed class:** `StandingOrdersUiState`

### State Fields

| Field | Type | Description |
|---|---|---|
| `accountId` | `String` | OBIE account identifier received as nav param from account-detail |
| `uiState` | `StandingOrdersUiState` | Sealed class governing which UI surface is active |

### Sealed Class Members

| Member | Fields | Description |
|---|---|---|
| `Loading` | — | `OBReadStandingOrder6` fetch in flight; no data available yet |
| `Content` | `standingOrders: List<StandingOrderViewModel>`, `summaryLabel: String` | Non-empty response; all transforms applied; `summaryLabel` = e.g. `'3 Active · 1 Inactive'` |
| `Empty` | — | `Data.StandingOrder[]` returned by HSBC is an empty array |
| `Error` | `errorType: StandingOrderErrorType`, `message: String` | Typed error; Retry button always visible |

### Error Types

| Type | HTTP trigger | Recovery |
|---|---|---|
| `TokenExpiredError` | 401 | Route to login screen |
| `ConsentRevokedError` | 403 | Route to consent-list screen |
| `RateLimitedError` | 429 | Retry button; retry after delay indicated in `Retry-After` header |
| `NetworkError` | IOException / timeout | Retry button re-triggers `LoadStandingOrders` |
| `ServerError` | 500, 503 | Retry button; persistent failure routes to support |

### Actions

| Action | Signature | Side Effects |
|---|---|---|
| `LoadStandingOrders` | `suspend fun loadStandingOrders(accountId: String)` | Sets `uiState = Loading`; calls `GET /accounts/{accountId}/standing-orders` via Ktorfit `AisApiService`; maps each order via `.withFrequencyLabel().withStatusVariant().withFinalPaymentFlag()`; computes `summaryLabel` from `Active`/`Inactive` counts; sets `uiState = Content` \| `Empty` \| `Error` |
| `RetryLoad` | `fun retryLoad()` | Re-invokes `LoadStandingOrders` with same `accountId` |
| `NavigateBack` | `fun navigateBack()` | Emits `NavigationEvent.Back` to `NavController` |

**`toUiModel()` transform notes:**

- `withFrequencyLabel()` — decodes OBIE ISO 20022 frequency code via `FrequencyDecoder` sealed class to a human-readable label (e.g. `IntrvlMnthDay:01:01` → `'Monthly on the 1st'`; `IntrvlWkDay:01:5` → `'Weekly every Friday'`); unknown codes fall back to the raw code string
- `withStatusVariant()` — `StandingOrderStatusCode.Active` → `status_variant=primary`; `Inactive` → `status_variant=secondary`
- `withFinalPaymentFlag()` — `hasFinalPayment = FinalPaymentDateTime != null`; controls `so_final_date` row visibility

### DI

- `StandingOrdersRepository` — `GET /accounts/{AccountId}/standing-orders` via ktorfit
- `NavigationController` — KMP navigation abstraction for route push/pop

---

## 6. Error Cases

| ID | Trigger | User message | Recovery |
|---|---|---|---|
| `TokenExpired` | HTTP 401 from HSBC AIS | Session expired. Please log in again. | Route to login screen |
| `ConsentRevoked` | HTTP 403 from HSBC AIS | Account access consent has been revoked. | Route to consent-list screen |
| `RateLimited` | HTTP 429 from HSBC AIS | Too many requests. Please wait a moment and try again. | Retry button re-triggers `LoadStandingOrders` after brief delay |
| `NetworkError` | IOException / timeout | No network connection. Check your connection and retry. | Retry button re-triggers `LoadStandingOrders` |
| `ServerError` | HTTP 500 / 503 from HSBC AIS | Something went wrong. Please try again later. | Retry button; persistent failure routes to support |
| `EmptyResult` | `Data.StandingOrder[]` is empty | No standing orders are set up for this account. | Empty state shown; no action needed |

---

## 7. Navigation

| Entry | Source | Trigger | Params |
|---|---|---|---|
| → standing-orders | account-detail | Tap Standing Orders chip | `accountId: String` |

| From | To | Trigger |
|---|---|---|
| standing-orders | account-detail | Tap back button |

---

## 8. Flow Decisions

| Decision | Condition | True Path | False Path |
|---|---|---|---|
| API response empty? | `Data.StandingOrder[]` has 0 entries | `UiState.Empty` | Map entries to `UiModel` list; `UiState.Content` with `summaryLabel` |
| HTTP error code? | 401 / 403 / 429 / 5xx / IOException | `UiState.Error(typedMessage)`; show Retry | Proceed to Content or Empty |
| `StandingOrderStatusCode = Active`? | `item.StandingOrderStatusCode == Active` | `status_variant = primary` (primary-colored badge) | `status_variant = secondary` (muted badge); item marked Inactive |
| `FinalPaymentDateTime` present? | `item.FinalPaymentDateTime != null` | `hasFinalPayment = true`; `so_final_date` row visible | `hasFinalPayment = false`; `so_final_date` row hidden |

---

## 9. Test Scenarios

13 scenarios (source: `screens/standing-orders/tests.yaml`)

| ID | Description | State | Priority |
|---|---|---|---|
| TC-SO-001 | Standing orders list loads and renders all active orders | content | p0 |
| TC-SO-002 | Loading state shown during standing orders fetch | loading | p0 |
| TC-SO-003 | Empty state when no standing orders set up | empty | p1 |
| TC-SO-004 | Error state with Retry button on 401 token expired | error | p1 |
| TC-SO-005 | Back button navigates to account-detail | content | p1 |
| TC-SO-006 | Inactive standing order renders secondary badge variant and shows final payment date | content | p1 |
| TC-SO-007 | 403 Consent Revoked shows distinct error message from 401 Token Expired | error | p1 |
| TC-SO-008 | 429 Rate Limited shows rate-limit specific message | error | p2 |
| TC-SO-009 | Weekly frequency code `IntrvlWkDay:01:5` decodes to `'Weekly every Friday'` | content | p1 |
| TC-SO-010 | Pull-to-refresh re-triggers standing orders load | content | p2 |
| TC-SO-011 | All interactive elements and key data fields have accessibility labels | content | p2 |
| TC-SO-012 | Network error (IOException) shows correct message and Retry button | error | p1 |
| TC-SO-013 | Unknown OBIE frequency code falls back to raw code string | content | p2 |
