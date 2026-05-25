# Feature Specification — Transaction History
**Feature:** transactions | **Flavor:** consumer | **Status:** enriched | **Quality Score:** 80

---

## Overview

The Transaction History screen presents a paginated, filterable, and searchable list of bank transactions for a given account. A prominent monthly summary card shows total spent vs total received for the current period. Users can narrow results via a search bar (by merchant, amount, or date), a date-range picker (defaulting to Last 30 Days), and type-filter chips (All / Debit / Credit / Pending). Transactions are grouped by date and each row is tappable to open the transaction detail screen. A "Load More" button at the bottom handles pagination.

---

## Screens

| Screen ID | Label | Route | Layout | Scroll |
|---|---|---|---|---|
| transactions_content | Transaction History | /transactions | Vertical scroll, top app bar with back + filter action | vertical |

---

## Components

| ID | Type | Description |
|---|---|---|
| search_bar | input | Full-width search: variant=search, placeholder "Search by merchant, amount, date...", leading_icon search, trailing_icon mic |
| date_range_picker | box | Tappable row showing current date range ("Last 30 Days") + date_range icon + expand_more chevron |
| filter_chips_row | stack | Horizontal scrollable filter chips: All (active), Debit, Credit, Pending |
| filter_all / filter_debit / filter_credit / filter_pending | button | Filter selection chips; active = filled #1800B1; inactive = outlined #CCCCCC |
| monthly_summary_card | box | Two-column summary: "Spent this month £1,240.30" (red) / "Received £3,200.00" (green) |
| spent_amount | text | "£1,240.30" — title_large, #FF5252, weight 700 |
| received_amount | text | "£3,200.00" — title_large, #4CAF50, weight 700 |
| transactions_date_group_header | text | Date group label "25 May 2026" — label_medium, #666666 |
| txn_list_row_1 | box | Tesco Supermarket / Groceries / -£42.50 / 25 May 2026 |
| txn_list_row_2 | box | Salary Payment / Income / +£3,200.00 / 24 May 2026 |
| txn_list_row_3 | box | EDF Energy / Utilities / -£94.20 / 23 May 2026 |
| load_more_button | button | Text variant, "Load More Transactions", centered, #1800B1 |

---

## States

| ID | Trigger | Description |
|---|---|---|
| loading | ScreenOpened / RetryLoad | Search bar + filter chips visible; skeleton: 1 summary card (80px) + 3 row skeletons (68px) |
| content | Transactions loaded | All filters + summary card + date group + transaction rows + load more |
| empty | No transactions match filters | Search + date picker + filters visible; empty card: "No transactions found", CTA "Clear Filters" |
| error | Network / auth failure | Search bar visible; error card: "Could not load transactions", CTA "Retry" |
| searching | User typed in search_bar | Search bar + filter chips; skeleton rows while search executes |

---

## State Model

**ViewModel:** `TransactionsViewModel`
**ScreenState:** `TransactionsScreenState`

| Field | Type | Default |
|---|---|---|
| isLoading | Boolean | true |
| transactions | List\<TransactionSummary\> | emptyList() |
| activeFilter | TransactionTypeFilter | TransactionTypeFilter.ALL |
| dateRange | DateRange | DateRange.LAST_30_DAYS |
| searchQuery | String | "" |
| totalSpent | BigDecimal | BigDecimal.ZERO |
| totalReceived | BigDecimal | BigDecimal.ZERO |
| currentPage | Int | 0 |
| hasMore | Boolean | true |
| error | UiError? | null |
| isSearching | Boolean | false |

**Events:** RetryLoad · SearchQueryChanged(query: String) · FilterTypeChanged(filter: TransactionTypeFilter) · DateRangeChanged(range: DateRange) · LoadMore · TransactionSelected(transactionId: String) · ClearFilters

**Actions:** loadTransactions(triggers: ScreenOpened/RetryLoad/ClearFilters) · searchTransactions(query) · filterByType(TransactionTypeFilter) · filterByDateRange(DateRange) · loadNextPage · navigateToDetail(transactionId)

**DI:** TransactionsRepository · AccountsRepository

---

## Navigation

| From | To | Trigger | Type |
|---|---|---|---|
| transactions | transaction-detail | Tap any txn_list_row | push |
| transactions | account-detail | Top app bar back arrow | pop |
| transactions | send-money | Bottom nav "Pay" | replace |
| transactions | accounts | Bottom nav "Accounts" | replace |

---

## API Endpoints

| Endpoint | Auth | Purpose |
|---|---|---|
| GET /obp/v5.1.0/my/banks/{bankId}/accounts/{accountId}/transactions | DirectLogin | Fetch paginated transactions with date range, type filter, and sort |

---

## Design Tokens

| Token | Value | Usage |
|---|---|---|
| color.primary | #1800B1 | Active filter chip, Load More text, date_range icon |
| color.surface | #FFFFFF | Transaction row backgrounds |
| color.surface_variant | #F5F5F5 | Search bar + date picker backgrounds |
| color.summary_bg | #F8F4FF | Monthly summary card background (light purple tint) |
| color.debit | #FF5252 | Debit amounts, spent total |
| color.credit | #4CAF50 | Credit amounts, received total |
| color.groceries_badge | #E8F5E9 / #2E7D32 | Groceries category chip |
| color.utilities_badge | #FFF3E0 / #E65100 | Utilities category chip |
| color.income_badge | #E8F5E9 / #2E7D32 | Income category chip |
| typography.title_large | — | Summary amounts (£1,240.30 / £3,200.00) |
| typography.label_medium | — | Filter chip labels, date group header |
| typography.body_medium | — | Transaction merchant names |
| typography.body_small | — | Date + category badges |
| typography.body_large | — | Transaction amount column |

---

_Generated by /idea export | 2026-05-25_
