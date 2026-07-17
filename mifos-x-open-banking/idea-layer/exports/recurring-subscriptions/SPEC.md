<!-- source: screens/recurring-subscriptions/ui.yaml -->
<!-- source_hash: regenerated-2026-07-16 -->
<!-- generated: 2026-07-16T00:00:00Z -->

# SPEC — recurring-subscriptions

_Generated: 2026-07-16 · Source: idea-layer/screens/recurring-subscriptions/ui.yaml_

---

## 1. Feature Overview

**Name:** Recurring Payments  
**Archetype:** index_list  
**Cluster:** pfm  
**Status:** enriched → designed → approved  
**Quality score:** 97  
**Acceptance refs:** FR-011  

**Description:**  
Detects recurring payments in cached AIS transactions via `kotlinx-datetime` `DatePeriod`
comparisons. Groups by normalised merchant name (≥ 2 occurrences, ± 5 day tolerance) to
infer Weekly / Fortnightly / Monthly / Annual cadences; projects next expected date; normalises
all cadences to monthly equivalent (Annual ÷ 12, Weekly × 52/12, Fortnightly × 26/12).
No network calls; reads local DataStore transaction cache written by the transactions feature.
Tapping a subscription row navigates to merchant-filtered transaction history.

**Libraries:**

| Library | Purpose |
|---|---|
| `kotlinx-datetime` | `DatePeriod` comparisons for cadence detection and next-date projection |

**Cross-feature dependency:**

| Feature | Access | Contract |
|---|---|---|
| `transactions` | read-only | Reads `List<TransactionInformation>` from local DataStore cache; performs no writes |

---

## 2. Screen Inventory

| Screen | Archetype | Initial state | Shell |
|---|---|---|---|
| recurring-subscriptions | index_list | loading | Bottom nav visible · Top app bar `{strings.recurring_subscriptions.title}` · Back leading icon · No FAB |

---

## 3. States

| State | Trigger |
|---|---|
| `loading` | Screen mounts / retry; algorithm running over cached transactions |
| `content` | Detection complete, ≥ 1 qualifying pattern found |
| `empty` | < 2 occurrences per merchant or empty cache |
| `error` | `DataStoreReadException` or `TransactionDeserializationException` during cache read |

---

## 4. Components

### State: `loading`

| ID | Type | State binding | Purpose |
|---|---|---|---|
| `loading_skeleton` | shimmer (rows=5) | loading | Placeholder while recurrence algorithm runs over cached transactions |

### State: `content`

| ID | Type | State binding | Purpose |
|---|---|---|---|
| `detected_notice` | banner (icon=info_outline) | content | Informs user these are in-app detections, distinct from bank-registered standing orders and direct debits |
| `summary_card` | card (elevation=1) | content | Summary of total monthly cost and detected subscription count; verify `summary.total_monthly` + `summary.count` |
| `summary_label` | text (labelMedium, color=secondary) | content | Static label for total monthly cost metric |
| `summary_amount` | text (headlineMedium, color=error) | content | `£{summary.total_monthly}` — GBP total normalised to monthly cadence across all cadences |
| `summary_count` | text (bodySmall, color=on-surface-variant) | content | `{summary.count} {strings.recurring_subscriptions.subscriptions_suffix}` |
| `subscriptions_list` | list (items_source=`{subscriptions}`) | content | Detected recurring payment entries sorted by monthly cost descending |
| `subscription_row` | list_item (icon=autorenew) | content | Merchant name label; `{item.cadence} · Next: {item.next_date}` supporting text; `£{item.amount}` trailing |
| `detected_badge` | chip (variant=assist) — child of subscription_row | content | Visual badge indicating pattern was detected in-app, not sourced from bank API |

**subscription_row action contract:**

| Component | Action | Effect | Library refs | Description |
|---|---|---|---|---|
| `subscription_row` | `navigate_transactions` | navigate | — | Navigates to the transactions screen filtered by merchant name, allowing the user to review the individual transactions that make up this detected recurring-payment pattern. |

```
on_click:
  action: navigate_transactions
  target: transactions
  params:
    merchant: "{item.merchant}"
```

### State: `empty`

| ID | Type | State binding | Purpose |
|---|---|---|---|
| `empty_state` | empty_state (icon=autorenew) | empty | No qualifying patterns found (< 2 occurrences per merchant or empty cache) |

### State: `error`

| ID | Type | State binding | Purpose |
|---|---|---|---|
| `error_state` | error_state (icon=error_outline) | error | DataStore read or deserialisation failure; user can retry |
| `retry_button` | outlined_button — child of error_state | error | Re-runs recurring-payment detection algorithm over locally cached DataStore transactions; transitions Error → Loading |

**retry_button action contract:**

| Component | Action | Effect | Library refs | Description |
|---|---|---|---|---|
| `retry_button` | `retry_load_subscriptions` | transform_state | `androidx.datastore`, `kotlinx-datetime` | Re-runs the recurring-payment detection algorithm over the locally cached DataStore transactions, returning the screen from Error back to Loading and then Content or Empty without issuing any network request. |

---

## 5. ViewModel Contract

**ViewModel:** `RecurringSubscriptionsViewModel`  
**State class:** `RecurringSubscriptionsState`  
**Sealed class:** `RecurringSubscriptionsUiState`

### State Fields

| Field | Type | Description |
|---|---|---|
| `uiState` | `RecurringSubscriptionsUiState` | Sealed class: Loading \| Content(subscriptions, summary) \| Empty \| Error(throwable) |
| `subscriptions` | `List<RecurringSubscription>` | Detected recurring payment patterns sorted by `monthly_equivalent` descending |
| `summary` | `RecurringSummary` | Aggregated `total_monthly` (Float, 2dp) and `count` (Int) across all cadences |

### Sealed Class Members

| Member | Fields |
|---|---|
| `Loading` | — |
| `Content` | `subscriptions: List<RecurringSubscription>`, `summary: RecurringSummary` |
| `Empty` | — |
| `Error` | `throwable: Throwable` |

### Error Types

| Type | Severity | Trigger |
|---|---|---|
| `DataStoreReadException` | error | DataStore throws `IOException` during cached transaction read |
| `TransactionDeserializationException` | error | Deserialisation of cached transaction list fails |

### Actions

| Action | Signature | Side Effects |
|---|---|---|
| `loadSubscriptions` | `suspend fun loadSubscriptions()` | Reads full cached transaction corpus from DataStore; groups by normalised merchant name; filters groups with ≥ 2 occurrences; infers cadence via `kotlinx-datetime` DatePeriod (± 5 day tolerance); computes `next_date`; derives `monthly_equivalent`; sorts by `monthly_equivalent` desc; transitions uiState loading → content \| empty \| error |
| `retryLoadSubscriptions` | `fun retryLoadSubscriptions()` | Resets uiState error → loading; re-invokes `loadSubscriptions()` |
| `navigateTransactions` | `fun navigateTransactions(merchant: String)` | Emits `NavigateTransactions(merchant)` navigation event consumed by NavHost; transactions screen applies case-insensitive `contains` filter on the normalised merchant param |

### DI

`TransactionRepository`, `DateTimeProvider`

---

## 6. Error Cases

| ID | Trigger | Handling |
|---|---|---|
| EC-RS-001 | Fewer than 2 qualifying recurrent transactions per merchant across all cached data | Transition to empty state |
| EC-RS-002 | Transaction cache empty (no sync performed yet) | Transition to empty state with instructional body text |
| EC-RS-003 | DataStore read throws `IOException` or serialisation error | Transition to error state; display `error_state` with retry button |

---

## 7. Navigation

| Entry | Source | Trigger |
|---|---|---|
| → recurring-subscriptions | pfm-dashboard | Tap "Subscriptions" chip |

| From | To | Trigger | Params |
|---|---|---|---|
| recurring-subscriptions | transactions | Tap `subscription_row` | `merchant: String` — normalised merchant name |

Transactions screen applies a case-insensitive `contains` filter on the merchant param. The normalised form (e.g. `Netflix`) is passed, not the raw transaction description (e.g. `NETFLIX.COM UK LTD`).

---

## 8. Test Scenarios

13 scenarios (source: `screens/recurring-subscriptions/tests.yaml`)

| ID | Description | State | Priority |
|---|---|---|---|
| TC-RS-001 | Loading state shows shimmer skeleton while pattern-detection algorithm runs | loading | high |
| TC-RS-002 | Content state renders 7 detected subscriptions sorted by monthly cost descending | content | high |
| TC-RS-003 | Annual cadence amount normalised to monthly equivalent in total | content | high |
| TC-RS-004 | Tapping a subscription row fires navigate_transactions and navigates to merchant-filtered transactions | content | high |
| TC-RS-005 | Total is sum of all monthly-equivalent amounts across all cadences | content | medium |
| TC-RS-006 | Empty state when fewer than 2 qualifying occurrences per merchant | empty | high |
| TC-RS-007 | Error state renders when DataStore read throws IOException | error | high |
| TC-RS-008 | Retry button resets to loading state and re-runs detection | error | medium |
| TC-RS-009 | Weekly cadence amount normalised to monthly equivalent in summary total | content | high |
| TC-RS-010 | Fortnightly cadence amount normalised to monthly equivalent in summary total | content | medium |
| TC-RS-011 | Merchant normalisation merges legal-suffix variants into single subscription row | content | high |
| TC-RS-012 | navigate_transactions params carry normalised merchant name, not raw transaction description | content | high |
