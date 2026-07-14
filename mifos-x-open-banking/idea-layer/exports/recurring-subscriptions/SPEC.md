<!-- source: screens/recurring-subscriptions/ui.yaml -->
<!-- source_hash: regenerated-2026-07-14 -->
<!-- generated: 2026-07-14T21:00:00Z -->

# SPEC — recurring-subscriptions

_Generated: 2026-07-14 · Source: idea-layer/screens/recurring-subscriptions/ui.yaml_

---

## 1. Feature Overview

**Name:** Recurring Payments  
**Archetype:** index_list  
**Cluster:** pfm  
**Status:** enriched → designed  
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
| `org.jetbrains.kotlinx:kotlinx-datetime` | DatePeriod comparisons for cadence detection |

**Cross-feature dependency:**

| Feature | Access | Contract |
|---|---|---|
| `transactions` | read-only | Reads `List<TransactionInformation>` from local DataStore cache; performs no writes |

---

## 2. Screen Inventory

| Screen | Archetype | Initial state | Shell |
|---|---|---|---|
| recurring-subscriptions | index_list | loading | Bottom nav visible · Top app bar "Recurring Payments" · Back leading icon · No FAB |

### 2.1 Component Layout by State

**State: `loading`**

| Component | Type | Description |
|---|---|---|
| `loading_skeleton` | shimmer (rows=5) | Placeholder while recurrence algorithm runs over cached transactions |

**State: `content`**

| Component | Type | Description |
|---|---|---|
| `detected_notice` | banner (icon=info_outline) | Informs user these are in-app detections, distinct from bank-registered standing orders and direct debits |
| `summary_card` | card (elevation=1) | Summary of total monthly cost and detected subscription count |
| `summary_label` | text (labelMedium, color=secondary) | Static label for total monthly cost metric |
| `summary_amount` | text (headlineMedium, color=error) | `£{summary.total_monthly}` — GBP total normalised to monthly cadence |
| `summary_count` | text (bodySmall, color=on-surface-variant) | `{summary.count} subscriptions` |
| `subscriptions_list` | list (items_source=`{subscriptions}`) | Sorted by monthly cost descending |
| `subscription_row` | list_item (icon=autorenew) | Merchant name, cadence + next date, trailing amount |
| `detected_badge` | chip (variant=assist) | "Detected" badge — pattern is in-app, not from bank API |

**subscription_row on_click:**
```
action: navigate_transactions
target: transactions
params:
  merchant: "{item.merchant}"
```

**State: `empty`**

| Component | Type | Description |
|---|---|---|
| `empty_state` | empty_state (icon=autorenew) | No qualifying patterns found (< 2 occurrences per merchant) |

**State: `error`**

| Component | Type | Description |
|---|---|---|
| `error_state` | error_state (icon=error_outline) | DataStore read or deserialisation failure |
| `retry_button` | outlined_button | `on_click: retry_load_subscriptions` |

---

## 3. State Model

**ViewModel:** `RecurringSubscriptionsViewModel`

| State | Trigger | Description |
|---|---|---|
| `loading` | Initial composition / retry | Algorithm running over cached transactions |
| `content` | Detection complete, ≥ 1 pattern | `subscriptions` + `summary` populated |
| `empty` | No qualifying patterns | < 2 occurrences per merchant or empty cache |
| `error` | DataStore IOException / deserialisation failure | Retry available |

**State fields:**

| Field | Type | Description |
|---|---|---|
| `uiState` | `RecurringSubscriptionsUiState` | Sealed class: Loading / Content(subscriptions, summary) / Empty / Error(throwable) |
| `subscriptions` | `List<RecurringSubscription>` | Detected patterns sorted by `monthly_equivalent` descending |
| `summary.total_monthly` | Float (2dp) | Sum of all `monthly_equivalent` values |
| `summary.count` | Int | Length of `subscriptions` list |

**RecurringSubscription fields:**

| Field | Type | Description |
|---|---|---|
| `item.merchant` | String | Normalised merchant name (lower-case, stripped legal suffixes) |
| `item.cadence` | String | Weekly / Fortnightly / Monthly / Annual |
| `item.amount` | Float | Per-occurrence amount in GBP |
| `item.next_date` | String | Projected next payment date |
| `item.monthly_equivalent` | Float | Normalised monthly cost used for sorting and summary |

**VM Actions:**

| Action | Signature | Side effects |
|---|---|---|
| `loadSubscriptions` | `suspend fun loadSubscriptions()` | Reads cached transactions; groups by merchant; infers cadence; computes next_date and monthly_equivalent; sorts by monthly_equivalent desc |
| `retryLoadSubscriptions` | `fun retryLoadSubscriptions()` | Resets error state → loading; re-invokes loadSubscriptions() |
| `navigateTransactions` | `fun navigateTransactions(merchant: String)` | Emits NavigateTransactions(merchant) event; NavHost routes to transactions with merchant filter param |

**DI dependencies:** `TransactionRepository`, `DateTimeProvider`

**Error cases:**

| ID | Trigger | Handling |
|---|---|---|
| EC-RS-001 | < 2 qualifying recurrent transactions per merchant | Transition to empty state |
| EC-RS-002 | Transaction cache empty (no sync performed yet) | Transition to empty state with instructional body text |
| EC-RS-003 | DataStore read throws IOException or serialisation error | Transition to error state; display retry button |

---

## 4. Navigation

| Entry | Source | Trigger |
|---|---|---|
| → recurring-subscriptions | pfm-dashboard | Tap "Subscriptions" chip |

| From | To | Trigger | Params |
|---|---|---|---|
| recurring-subscriptions | transactions | Tap subscription_row | `merchant: String` — normalised merchant name |

Transactions screen applies a case-insensitive `contains` filter on the merchant param.

---

## 5. API Dependencies

**Client-only feature — no server API.**

No OBIE endpoints are called. The recurrence algorithm runs entirely on the local DataStore
transaction cache. The cache is populated by the transactions feature
(`List<TransactionInformation>`); recurring-subscriptions is a read-only consumer.

---

## 6. Design Tokens

Design system: **Open Banking — Trust Blue** (Material 3, seed `#266489`, aesthetic: minimalist-ui)

| Token | Value | Usage in this feature |
|---|---|---|
| `colors.error` | `#BA1A1A` | `summary_amount` text color (GBP total — draws attention to cost) |
| `colors.secondary` | `#50606E` | `summary_label` text color |
| `colors.on_surface_variant` | `#41474D` | `summary_count` text color |
| `colors.surface_container` | `#EBEEF3` | Summary card background |
| `typography.headlineMedium` | 28sp / 400 | Summary amount |
| `typography.labelMedium` | 12sp / 500 | Summary label, detected badge |
| `typography.bodySmall` | 12sp / 400 | Summary count, supporting text on rows |
| `typography.bodyMedium` | 14sp / 400 | Supporting text (cadence + next date) |
| `spacing.screen_padding` | 16dp | Horizontal screen padding |
| `rounded.medium` | 12dp | Summary card radius |
| `colors.primary` | `#266489` | autorenew icon, active nav |
| `accessibility.min_touch_target_dp` | 48dp | Subscription rows (tap targets) |
