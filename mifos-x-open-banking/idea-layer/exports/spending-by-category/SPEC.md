<!-- source: screens/spending-by-category/ui.yaml -->
<!-- source_hash: regenerated-2026-07-16 -->
<!-- generated: 2026-07-16T00:00:00Z -->

# SPEC — spending-by-category

_Generated: 2026-07-16 · Source: idea-layer/screens/spending-by-category/ui.yaml_

---

## 1. Feature Overview

**Name:** Spending By Category  
**Archetype:** dashboard  
**Cluster:** pfm  
**Status:** enriched → designed → approved  
**Quality score:** 95  
**Acceptance refs:** FR-011  

**Description:**  
Groups cached AIS debits by `MerchantCategory` / `ProprietaryBankTransactionCode` (MCC-derived)
and aggregates amount, transaction count, and percentage-of-total per category.
Period windows (`this_month` / `last_month` / `3_months`) use `kotlinx-datetime`
`LocalDate` ranges relative to `Clock.System.now()`. Aggregation runs in
`viewModelScope` using Kotlin coroutines; period chip selection re-aggregates without
network calls — pure in-memory computation over the local Room transaction cache. Result
list is sorted by amount descending. Drill-down to transactions passes category as a
URI-encoded filter param.

**Libraries:**

| Library | Purpose |
|---|---|
| `kotlinx-datetime` | `LocalDate` ranges for period windows; `Clock.System.now()` reference point |
| `kotlin-coroutines` | Async in-memory aggregation in `viewModelScope` |

**Local store:** Room/SQLDelight `pfm_room_cache` (shared with pfm-dashboard and budgets;
~50 MB max; TTL 24 h; cleared via Settings → Clear Local Data).

---

## 2. Screen Inventory

| Screen | Archetype | Initial state | Shell |
|---|---|---|---|
| spending-by-category | dashboard | loading | Bottom nav visible · Top app bar `{strings.sbc.screen_title}` · Back leading icon · No FAB |

**Entry points:** pfm-dashboard → "By Category" chip; pfm-dashboard → tap top-category row (passes `category` param)

---

## 3. States

| State | Trigger |
|---|---|
| `loading` | Screen mounts or period chip tapped; aggregation coroutine running |
| `content` | Aggregation complete, ≥ 1 category with debit transactions in selected period |
| `empty` | No debit transactions in Room cache for selected date range (EC-SBC-001) |
| `error` | Room query or in-memory aggregation throws an exception (EC-SBC-002) |

---

## 4. Components

### Period Selector (all states)

| ID | Type | State binding | Purpose |
|---|---|---|---|
| `period_selector` | chip_group (variant=single_select, scroll_direction=horizontal) | loading, content, empty, error | Period filter chip group; exactly one chip selected at a time; triggers re-aggregation on change |
| `period_this_month` | chip (variant=filter, selected=true by default) — child of chip_group | all | Default-selected period chip; represents current calendar month |
| `period_last_month` | chip (variant=filter) — child of chip_group | all | Previous calendar month period filter |
| `period_3_months` | chip (variant=filter) — child of chip_group | all | 3-month rolling window (last 90 days) period filter |

**period_this_month action contract:**

| Component | Action | Effect | Library refs | Description |
|---|---|---|---|---|
| `period_this_month` | `select_period` (params: `period='this_month'`) | transform_state | `kotlinx-coroutines` | Selects the this_month period window and re-aggregates cached Room debit transactions for the current calendar month by category; no network call. |

**period_last_month action contract:**

| Component | Action | Effect | Library refs | Description |
|---|---|---|---|---|
| `period_last_month` | `select_period` (params: `period='last_month'`) | transform_state | `kotlinx-coroutines` | Selects the last_month period window and re-aggregates cached Room debit transactions for the previous calendar month by category; no network call. |

**period_3_months action contract:**

| Component | Action | Effect | Library refs | Description |
|---|---|---|---|---|
| `period_3_months` | `select_period` (params: `period='3_months'`) | transform_state | `kotlinx-coroutines` | Selects the 3-month rolling period window and re-aggregates cached Room debit transactions for the last 90 days by category; no network call. |

### State: `loading`

| ID | Type | State binding | Purpose |
|---|---|---|---|
| `loading_skeleton` | skeleton (5 shimmer shapes) | loading | Loading skeleton while category aggregation runs; each shimmer block mirrors real list row height |

Shimmer shapes: card (100% × 80dp), text (60% × 16dp), block (100% × 56dp) × 3.

### State: `content`

| ID | Type | State binding | Purpose |
|---|---|---|---|
| `spend_summary_card` | card (elevation=1) | content | Total spend summary card; updates when period chip changes |
| `total_spend_label` | text (labelMedium, color=on_surface_variant) — child of card | content | `{strings.sbc.total_spend.header}` interpolated with `{period.label}` (e.g. `Total Spend — June 2026`) |
| `total_spend_amount` | text (headlineMedium, color=error) — child of card | content | `£{period.total_spend}` — formatted GBP total for period; `i18n: skip` (currency-formatted at runtime) |
| `category_list` | list (items_source=`{categories}`, divider=true) | content | Category breakdown list sorted by amount descending; percentages sum to 100% |
| `category_row` | list_item (icon=`{item.icon}`) — child of list | content | Category name label; `{item.transaction_count}` + `{item.percentage}%` supporting text; `£{item.amount}` trailing (`i18n_trailing: skip`); tapping drills into transactions |
| `category_progress_bar` | linear_progress (color=primary) — child of category_row | content | Progress bar for category share; `value={item.fraction}` (0.0–1.0, where `fraction = percentage / 100`) |

**category_row action contract:**

| Component | Action | Effect | Library refs | Description |
|---|---|---|---|---|
| `category_row` | `navigate_category_transactions` (params: `category='{item.name}'`) | navigate | — | Navigates to the transactions screen with the selected category pre-applied as a URI-encoded filter, showing all debit transactions contributing to this category's spend total. |

### State: `empty`

| ID | Type | State binding | Purpose |
|---|---|---|---|
| `empty_state` | empty_state (icon=pie_chart) | empty | No debit transactions in cache for selected period; period selector remains interactive |

### State: `error`

| ID | Type | State binding | Purpose |
|---|---|---|---|
| `error_state` | error_state (icon=warning_amber) | error | Category computation failed; retry button visible |
| `retry_button` | button (variant=tonal) — child of error_state (via `action:`) | error | Re-triggers `category_spend_compute` for currently selected period |

**retry_button action contract:**

| Component | Action | Effect | Library refs | Description |
|---|---|---|---|---|
| `retry_button` | `retry_compute` (params: `period='{selected_period}'`) | transform_state | `kotlinx-coroutines` | Re-triggers `category_spend_compute` for the currently selected period from the local Room transaction cache after a computation error; no network call is made. |

---

## 5. ViewModel Contract

**ViewModel:** `SpendingByCategoryViewModel`  
**State class:** `SpendingByCategoryState`  
**Sealed class:** `SpendingByCategoryUiState`

### State Fields

| Field | Type | Description |
|---|---|---|
| `uiState` | `SpendingByCategoryUiState` | Sealed class governing active UI surface |
| `categories` | `List<CategorySpend>` | Aggregated categories sorted by amount descending |
| `selectedPeriod` | `SpendingPeriod` | Currently active period: `this_month` / `last_month` / `3_months` |
| `periodTotalSpend` | `String` | Formatted GBP total for the selected period |
| `periodLabel` | `String` | Human-readable period label (e.g. `June 2026`, `May 2026`, `Apr–Jun 2026`) |

### Sealed Class Members

| Member | Description |
|---|---|
| `Loading` | Aggregation coroutine running |
| `Content` | Categories sorted by amount desc; `periodTotalSpend` + `periodLabel` computed |
| `Empty` | No debit transactions in Room cache for selected period (EC-SBC-001) |
| `Error` | Room query or in-memory aggregation exception (EC-SBC-002) |

### Error Types

| Type | Trigger |
|---|---|
| `RoomQueryError` | Room query or in-memory aggregation throws exception (EC-SBC-002) |

### Actions

| Action | Signature | Side Effects |
|---|---|---|
| `selectPeriod` | `fun selectPeriod(period: SpendingPeriod)` | Sets `uiState = Loading`; reads cached Room transactions filtered by `CreditDebitIndicator=Debit` and `kotlinx-datetime` `LocalDate` range; groups by auto-assigned category tag (MCC-derived); computes per-group `totalAmount`, `transactionCount`, `percentageOfTotal` (1dp), `fraction` (0.0–1.0); sorts descending by `totalAmount`; sets `uiState = Content` \| `Empty` \| `Error` |
| `navigateCategoryTransactions` | `fun navigateCategoryTransactions(category: String)` | Emits navigation event to `TransactionsRoute` with `categoryFilter` param URI-encoded |
| `retryCompute` | `fun retryCompute()` | Re-triggers `selectPeriod` with currently selected period; transitions error → loading |

### DI

- `PfmTransactionCache` — Room/SQLDelight; cached `OBTransaction6` debit rows (`pfm_room_cache`)

---

## 6. Error Cases

| ID | Trigger | Handling |
|---|---|---|
| EC-SBC-001 | No debit transactions in local Room cache for selected date range | Transition to empty state; period selector remains interactive |
| EC-SBC-002 | Room query or in-memory aggregation throws an exception | Transition to error state; retry button dispatches `retryCompute` |
| EC-SBC-003 | Local Room cache is cleared (Settings → Clear Local Data or `consent_revoked` event) while screen is active or between navigation visits | Next `selectPeriod` / `on_mount` call produces 0 rows → `UiState.Empty`; period selector remains interactive; no auto-sync triggered — cache refill is the AIS sync layer's responsibility |

---

## 7. Navigation

| Entry | Source | Trigger | Params |
|---|---|---|---|
| → spending-by-category | pfm-dashboard | Tap "By Category" chip | — |
| → spending-by-category | pfm-dashboard | Tap top-category row | `category: String` |

| From | To | Trigger | Params |
|---|---|---|---|
| spending-by-category | transactions | Tap `category_row` | `category: String` (URI-encoded) |

---

## 8. Test Scenarios

7 scenarios (source: `screens/spending-by-category/tests.yaml`)

| ID | Description | State | Priority |
|---|---|---|---|
| TC-SBC-001 | Loading skeleton renders while category aggregation is in progress | loading | high |
| TC-SBC-002 | Category breakdown renders correctly for This Month (June 2026) | content | high |
| TC-SBC-003 | Tapping a category row navigates to transactions filtered by that category | content | high |
| TC-SBC-004 | Selecting Last Month period recomputes categories from May 2026 data | content | high |
| TC-SBC-005 | Selecting 3 Months period aggregates Apr–Jun 2026 across all cached transactions | content | medium |
| TC-SBC-006 | Empty state renders when no transactions exist for selected period | empty | medium |
| TC-SBC-007 | Error state renders with retry button when aggregation fails | error | low |
