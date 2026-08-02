# Transactions — Feature Specification

> Generated from `screens/transactions/ui.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Source hash: `8fbdc3a139a1`
> Endpoints: 1 · DTOs: 1 · Components: 9 · Test scenarios: 12

## Lossless Export Contract

Lossless per RULE-EXPORT-ROUNDTRIP-001 — State Defaults, Error Matrix, Test Mapping and
Nav Origins below let the generators consume this file alone.

## 1. Overview

Full transaction history for one authorised account. Credit/debit filter chips, a date-range
chip with **server-side re-fetch**, free-text search by merchant or reference, and rows grouped
by booking date.

| Attribute | Value |
|---|---|
| Feature ID | `transactions` · Flow `transaction-review` · Cluster transactions |
| Priority | must (FR-005, FR-011) · Status approved · quality 95 |
| Archetype | index_list · Route `TransactionsRoute(accountId: String)` |
| Source module | `feature/transactions` — **implemented** |

## 2. Do not copy this as a stream template

**`transactions` is a suspend cursor-pager, not a `ScreenDataStream` feature.**
`TransactionsRepository` exposes `suspend firstPage(accountId)` / `nextPage(nextLink)`
returning `NetworkResult<TransactionsPage, NetworkError>`, hitting `Aisp` directly and
**bypassing Store5**. It is the only cursor-paging pattern in the repo.

Its fake stubs the stream out entirely (`FakeTransactionsRepository.kt:42-46` returns
`ScreenDataStream(state = emptyFlow(), …)`), so copying it for a new account-scoped screen
inherits none of the stream-ownership pattern. Copy `direct-debits` or `scheduled-payments`
instead.

`TransactionsRepository.transactionsStream` *does* exist and uses the `keyFlow` overload — but
its only production consumer is `feature/home`, not this screen.

## 3. Screen inventory

`loading_spinner` · `period_summary` (stat_block) · `filter_chips` (chip_row) ·
`search_field` (search_bar) · `transactions_list` · `load_more_button` ·
`pagination_loader` · `empty_transactions` · `error_state`.

## 4. State model — `TransactionsViewModel`

**Nine state fields** — the widest in the app: `accountId` · `uiState` · `activeFilter` ·
`query` · `dateFrom` · `dateTo` · `showDateRangePicker` · `hasNextPage` · `isPaginating`.
**Default:** `uiState = Loading`

**UiState:** `Loading` · `Content` · `Empty` · `Error`
**Actions (9):** `LoadTransactions` · `RetryLoad` · `LoadMore` · `FilterTransactions` ·
`SearchTransactions` · `OpenDateRangePicker` · `SetDateRange` · `DismissDateRangePicker` ·
`ClearFilters`
**Events:** none · **DI:** `SavedStateHandle` · `TransactionsRepository`

### Filter semantics differ by kind

| Filter | Where it runs |
|---|---|
| credit / debit chips | **in-memory** over the resident list |
| free-text search | **in-memory** over `TransactionInformation` + `MerchantDetails.MerchantName` |
| **date range** | **server-side re-fetch** with ISO-8601 bounds; resets the pagination cursor |

Mixing these up is the easy mistake — a date change must re-request, a chip must not.

## 5. Navigation

| Origin | Trigger | Target |
|---|---|---|
| `account-detail` | Transactions Explore option | `transactions` (accountId) |
| Home "View all" | tap | `transactions` (accountId) |
| transaction row | tap | `transaction-detail` (transactionId, accountId) |
| back | top-app-bar leading | `account-detail` |

There is **no Transactions tab** — the bottom-nav slot that once held one is now `Pay`, and
that tab was only ever a placeholder.

## 6. API dependencies

| ID | Method | Path | Permission | Response DTO |
|---|---|---|---|---|
| `transactions` | GET | `/accounts/{AccountId}/transactions` | ReadTransactionsDetail | `OBReadTransaction6` |

Full contract in `API.md`.

## 7. Design tokens

`list_item`, `chip_row` filters, `search_bar` search, `amount` (mono; credit `primary`,
debit `error`), `stat_block` period summary. Canonical brand spec: `design-system/DESIGN.md` 1.1.0.

## 8. Test mapping

TC-TXN-001 10 transactions render · 002 loading · 003 401 + Retry · **004 403 without Retry** ·
005 empty when no match · 006 Money-in filter · 007 Money-out filter · 008 search by
`TransactionInformation` · 009 row → transaction-detail · 010 Pending badge ·
**011 load-more appends the next page** · **012 date range re-fetches with ISO-8601 bounds**
→ `feature/transactions/src/commonTest/.../TransactionsViewModelTest.kt` + Robolectric +
instrumented.

## 9. Stale-artifact fix applied 2026-07-30

`data-flow.yaml` declared a `category` route param — "optional PFM category pre-filter from
pfm drill-down entry point". The pfm screens were deleted 2026-07-28 and source confirms
`TransactionsRoute(val accountId: String)` takes one argument. Removed, along with the
matching `source: pfm` entry point in `flow.yaml`.
