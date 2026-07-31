# Home — Feature Specification

> Generated from `screens/home/ui.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Source hash: `5f67cd986e56`
> Endpoints: 3 · DTOs: 3 · Components: 6 · Test scenarios: 13

## Lossless Export Contract

Lossless per RULE-EXPORT-ROUNDTRIP-001 — State Defaults, Error Matrix, Test Mapping and
Nav Origins below let the generators consume this file alone.

## 1. Overview

Landing screen (Home tab, bottom-nav order 0) showing the currently selected account.
**Deliberately thin:** hero balance card, then a recent-transactions preview. Aggregates AIS
data client-side; adds no endpoint of its own.

| Attribute | Value |
|---|---|
| Feature ID | `home` |
| Cluster | dashboard |
| Priority | must (FR-001, FR-003, FR-004) |
| Status | approved · quality 95 |
| Archetype | dashboard |
| Source module | `feature/home` — **implemented** |
| Graph | `homeGraph(onNavigateToTransactions, onNavigateToTransactionDetail)` |

**Three surfaces were removed** before this export and their idea-layer residue cleaned in the
same pass: a chip row, a quick-actions row (whose Pay was permanently disabled and whose
Statements was credit-card-only), and a spending-snapshot card linking to an Insights screen
that does not exist. `HomeData` consequently lost `spending` and `statementsAvailable`, and
`SpendingRowUi` is gone. `core/data`'s `SpendingCalculator` survives with its tests but has
**no production caller**.

## 2. Screen inventory

| Component | Type | Bound states |
|---|---|---|
| `loading_skeleton` | stack | loading |
| `hero_balance_card` | card | content — **also the account-switcher trigger** |
| `account_selector_sheet` | bottom_sheet | content (when `isAccountSelectorVisible`) |
| `recent_transactions_section` | stack | content |
| `empty_home` · `error_home` | empty_state, error_state | empty, error |

### The sheet is the project's only `ModalBottomSheet`

Tapping the hero card opens `AccountSelectorSheet` — the first and only one in this codebase.
It is split in two on purpose: a thin `ModalBottomSheet` wrapper plus a stateless
`AccountSelectorSheetContent` holding every interactive row, because a sheet renders in its own
window where `onNodeWithTag` is unreliable. The tests drive the content composable directly,
exactly as they do the other `*ScreenContent`. **If a second screen needs a sheet, promote that
wrapper to `core/ui` as a `Mifos*`.**

## 3. State model — `HomeViewModel`

**State fields:** `uiState: ScreenState<HomeData>` · `isAccountSelectorVisible: Boolean` ·
`accountId: String`
**State defaults:** `uiState = ScreenState.Loading` · `isAccountSelectorVisible = false`

`ScreenState` members: `Loading` · `Content` · `Empty` · `Error` · `NoNetwork` ·
`Unauthenticated`. Home is the **only** feature that renders through the shared
`core-base/ui/.../screen/ScreenContent.kt`; every pushed feature maps to its own sealed
`<F>UiState` instead.

**Actions:** `SelectAccount` · `OpenAccountSelector` · `DismissAccountSelector` · `RetryLoad`
**Events:** none (`E = Nothing`) — navigation is host-owned
**DI:** `AccountsRepository` · `BalancesRepository` · `TransactionsRepository` ·
`UserDataRepository`

**Sheet visibility lives on `HomeState`, beside `uiState` — not inside `HomeData`.** It is
presentation state, not loaded data. `SelectAccount` closes the sheet as it persists.

`BalancesRepository.balanceStream` and `TransactionsRepository.transactionsStream` are the only
two methods in the app using the `keyFlow` + `cacheKeyFor` overload — home's selected account
is the one key that changes without navigating.

## 4. Navigation

| Origin | Trigger | Target |
|---|---|---|
| `app_shell_bottom_nav` | Home tab (order 0) | `home` |
| `nav_host_start` | `HomeDestination` is the authenticated NavHost start | `home` |
| "View all" in recent transactions | tap | `transactions` (accountId) |
| recent transaction row | tap | `transaction-detail` (transactionId, accountId) |

**Home no longer navigates to account-detail** — that is reached from the Accounts tab.

> **Tab trap:** `navigateToTab` must target `tab.graphRoute`, never `startDestinationRoute`.
> Home's start route is also the NavHost start destination (the `popUpTo` target), so targeting
> the inner route made `restoreState` hand back the sibling tab and left Home unreachable.

## 5. API dependencies

| ID | Method | Path | Permission | Response DTO |
|---|---|---|---|---|
| `accounts-list` | GET | `/accounts` | ReadAccountsDetail | `OBReadAccount6` |
| `selected-account-balances` | GET | `/accounts/{AccountId}/balances` | ReadBalances | `OBReadBalance1` |
| `recent-transactions` | GET | `/accounts/{AccountId}/transactions` | ReadTransactionsDetail | `OBReadTransaction6` |

Balances and transactions fetch in parallel via `coroutineScope { async … }`. Full contracts in
`API.md`.

### Cache

| Resource | TTL | Source | Invalidated by |
|---|---|---|---|
| `allAccounts` | 300s | memory | account-switcher tap, app resume |
| `selectedAccountId` | ∞ | DataStore | — |

### Error matrix

| Case | Trigger | UI |
|---|---|---|
| EC-HOME-001 | 401 — token expired | Error + retry; recovery routes to login |
| EC-HOME-002 | 403 — permission absent from consent | Error, **non-recoverable**, directs to consent-list |
| EC-HOME-003 | 429 | Error, recoverable, exponential back-off |
| EC-HOME-004 | empty `Data.Account[]` | Empty, `reason=no_accounts` |
| EC-HOME-005 | consent absent or revoked | Empty, `reason=no_consent` |
| EC-HOME-006 | network | Error, recoverable |

## 6. Design tokens

`design-tokens.yaml` 2.1.0 — `balance_hero` (`displaySmall` mono), `amount` (credit `primary`,
debit `error`, running balances `neutral` and **unsigned**), `card` on `surfaceContainer`.
Canonical brand spec: `design-system/DESIGN.md` 1.1.0.

## 7. Test mapping

| TC | Assertion | Expected path |
|---|---|---|
| TC-HOME-001 | content for the default account | `feature/home/src/commonTest/.../HomeViewModelTest.kt` |
| TC-HOME-002 | shimmer skeletons during initial load | ↑ |
| TC-HOME-003 | switcher re-loads for a different account | ↑ |
| TC-HOME-006 | "View all" → transactions | ↑ |
| TC-HOME-007 | selector sheet opens, selects, dismisses | ↑ |
| TC-HOME-010 | 401 → error with retry | ↑ |
| TC-HOME-011 | 403 non-recoverable hides Retry | ↑ |
| TC-HOME-012 | empty with CTA when no accounts | ↑ |
| TC-HOME-013 | transaction row → transaction-detail | ↑ |
| TC-HOME-014 | credit-card balance-owed styling | `HomeScreenRobolectricTest.kt` |
| TC-HOME-015 | debit amounts in error colour | ↑ |
| TC-HOME-017 | 503 → recoverable error | ↑ |
| TC-HOME-018 | `selectedAccountId` persists across restarts | ↑ |

**TC-HOME-016 removed 2026-07-30** — it exercised a Statements quick action that no longer
exists.

## 8. Stale-artifact fixes applied 2026-07-30

| Artifact | Was | Now |
|---|---|---|
| `ui.yaml` | 119-line `quick_actions_card` (Pay/Transactions/Statements/Consents) | removed — none ships |
| `ui.yaml` | `account_switcher` as a horizontal `chip_row` | `account_selector_sheet` (bottom_sheet), hero card is the trigger |
| `docs.yaml#description` | claimed quick-action row, spending snapshot, route to consent-list | corrected to what ships |
| `docs.yaml#state_model` | flat fields + `spendThisMonth`, `topCategoryName`, `activeConsentId` | verbatim `HomeState` from `HomeViewModel.kt:81-88` |
| `docs.yaml#vm_actions` | 5 dead `Navigate*` actions | `OpenAccountSelector` / `DismissAccountSelector` |
| `tests.yaml` | TC-HOME-016 statements quick action | removed |

All six predate the 2026-07-28 reverse sync, which pruned `HomeData` but left these behind.

`docs.yaml` declares no `flow_ref` despite `flows/home-dashboard.yaml` existing.
