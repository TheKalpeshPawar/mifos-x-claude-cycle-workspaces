# SPEC — Transaction History

| Field         | Value                    |
|---------------|--------------------------|
| Feature       | transactions             |
| Flavor        | consumer                 |
| Status        | approved                 |
| Quality Score | 95                       |
| ViewModel     | TransactionsViewModel    |

---

## Overview

The Transaction History screen is the Consumer persona's full ledger view for a selected account. It opens with a search bar and date range picker at the top, followed by horizontally-scrollable filter chips (All / Debit / Credit / Pending), a monthly summary card showing Spent (`£1,240.30`, red) and Received (`£3,200.00`, green) for the active period, and a date-grouped list of transaction rows. Each row displays a merchant logo, name, date, category chip, and signed amount. Rows are tappable and navigate to Transaction Detail. A "Load More Transactions" text button pages additional results. The screen has a bottom navigation bar — Accounts tab is active. Data is fetched from OBP with limit/offset/date/type query parameters.

---

## Screens

| ID                   | Name                | Route          | Layout | Scroll   |
|----------------------|---------------------|----------------|--------|----------|
| transactions_content | Transaction History | /transactions  | Column | Vertical |

**Shell:** Top app bar with back arrow + filter action. Bottom navigation bar (Accounts tab active).

| Element         | Value                          |
|-----------------|--------------------------------|
| Title           | "Transactions"                 |
| Navigation icon | arrow_back                     |
| Action 1        | filter_list → open_advanced_filter |

**Shell:** Bottom navigation bar with 5 items (Accounts active)

| Nav Item | ID           | Icon            | Target    | Active |
|----------|--------------|-----------------|-----------|--------|
| Home     | nav_home     | home            | home      | false  |
| Accounts | nav_accounts | account_balance | accounts  | true   |
| Pay      | nav_pay      | send            | send-money| false  |
| Cards    | nav_cards    | credit_card     | cards     | false  |
| More     | nav_more     | more_horiz      | settings  | false  |

---

## Components

| ID                         | Type   | Description                                                                                         |
|----------------------------|--------|-----------------------------------------------------------------------------------------------------|
| search_bar                 | input  | Search variant, background `#F9FAEF`, radius 12dp, leading icon search `#44483D`, trailing icon mic; placeholder "Search by merchant, amount, date…" |
| date_range_picker          | box    | Tappable date filter: background `#F9FAEF`, radius 12dp, date_range icon `#4C662B` + "Last 30 Days" label + expand_more chevron |
| filter_chips_row           | stack  | Horizontal scrollable row of 4 filter chips                                                         |
| filter_all                 | button | "All" — filled `#4C662B` bg / white text, radius 20, label_medium (selected state)                 |
| filter_debit               | button | "Debit" — outlined, border `#E1E4D5`, text `#44483D`, radius 20, label_medium                     |
| filter_credit              | button | "Credit" — outlined, border `#E1E4D5`, text `#44483D`, radius 20, label_medium                    |
| filter_pending             | button | "Pending" — outlined, border `#E1E4D5`, text `#44483D`, radius 20, label_medium                   |
| monthly_summary_card       | box    | `#CDEDA3` background, radius 16dp, padding 16dp, margin H 20dp. Spent + Received columns with vertical divider |
| spent_label                | text   | "Spent this month" — Outfit/label_small, `#44483D`, tracking 0.4                                  |
| spent_amount               | text   | "£1,240.30" — Outfit/title_large 700-weight, `#BA1A1A`                                            |
| received_label             | text   | "Received" — Outfit/label_small, `#44483D`                                                         |
| received_amount            | text   | "£3,200.00" — Outfit/title_large 700-weight, `#4C662B`                                            |
| summary_divider_v          | box    | 1×40dp vertical divider `#E1E4D5`, margin H 16dp                                                  |
| transactions_date_group_header | text | "25 May 2026" — Outfit/label_medium, `#44483D`, tracking 0.5, padding H 20dp                  |
| txn_list_row_1             | box    | Tesco Supermarket — white `#FFFFFF`, radius 12, elevation 1, padding 14dp; navigates to transaction-detail (txn_20260525_001) |
| txn1_merchant_logo         | image  | merchant_tesco 40×40dp, radius 20, bg `#CDEDA3`                                                    |
| txn1_name                  | text   | "Tesco Supermarket" — Outfit/body_medium 500w, `#1A1C16`                                          |
| txn1_date_meta             | text   | "25 May 2026" — Outfit/body_small, `#44483D`                                                      |
| txn1_category_badge        | box    | "Groceries" — `#CDEDA3` bg, radius 4dp; label_small `#4C662B`                                    |
| txn1_amount_col            | text   | "-£42.50" — Outfit/body_large 600w, `#BA1A1A`                                                    |
| txn_list_row_2             | box    | Salary Payment — white card; navigates to transaction-detail (txn_20260524_001)                    |
| txn2_merchant_logo         | image  | merchant_bank_transfer 40×40dp, bg `#CDEDA3`                                                       |
| txn2_name                  | text   | "Salary Payment" — Outfit/body_medium 500w, `#1A1C16`                                             |
| txn2_date_meta             | text   | "24 May 2026" — Outfit/body_small, `#44483D`                                                      |
| txn2_category_badge        | box    | "Income" — `#CDEDA3` bg; label_small `#4C662B`                                                    |
| txn2_amount_col            | text   | "+£3,200.00" — Outfit/body_large 600w, `#4C662B`                                                 |
| txn_list_row_3             | box    | EDF Energy — white card; navigates to transaction-detail (txn_20260523_001)                        |
| txn3_merchant_logo         | image  | merchant_edf 40×40dp, bg `#CDEDA3`                                                                 |
| txn3_name                  | text   | "EDF Energy" — Outfit/body_medium 500w, `#1A1C16`                                                |
| txn3_date_meta             | text   | "23 May 2026" — Outfit/body_small, `#44483D`                                                      |
| txn3_category_badge        | box    | "Utilities" — `#CDEDA3` bg; label_small `#44483D` (contrast fix A11Y-002)                        |
| txn3_amount_col            | text   | "-£94.20" — Outfit/body_large 600w, `#BA1A1A`                                                    |
| load_more_button           | button | "Load More Transactions" — text variant, `#4C662B`, label_medium, centered                        |

---

## States

| ID        | Trigger                                  | Description                                                                    |
|-----------|------------------------------------------|--------------------------------------------------------------------------------|
| loading   | ScreenOpened / RetryLoad / ClearFilters  | Search bar + filter chips visible; 3 skeleton rows + summary skeleton          |
| content   | loadTransactions success                 | Full layout: summary card + date header + 3 rows + load more button            |
| empty     | No transactions match filters            | Search + date picker + filters visible; empty card with "Clear Filters" action |
| error     | network_error / auth_error               | Search bar visible; error card with "Retry" action                             |
| searching | SearchQueryChanged event                 | Search bar + filters; 2 skeleton rows while search results load                |

---

## State Model

**ViewModel:** `TransactionsViewModel`
**Screen State Type:** `TransactionsScreenState`

| Name           | Type                  | Default                    |
|----------------|-----------------------|----------------------------|
| isLoading      | Boolean               | true                       |
| transactions   | List\<TransactionSummary\> | emptyList()           |
| activeFilter   | TransactionTypeFilter | TransactionTypeFilter.ALL  |
| dateRange      | DateRange             | DateRange.LAST_30_DAYS     |
| searchQuery    | String                | ""                         |
| totalSpent     | BigDecimal            | BigDecimal.ZERO            |
| totalReceived  | BigDecimal            | BigDecimal.ZERO            |
| currentPage    | Int                   | 0                          |
| hasMore        | Boolean               | true                       |
| error          | UiError?              | null                       |
| isSearching    | Boolean               | false                      |

**Events:** `RetryLoad`, `SearchQueryChanged(query)`, `FilterTypeChanged(filter)`, `DateRangeChanged(range)`, `LoadMore`, `TransactionSelected(transactionId)`, `ClearFilters`

**Actions:** `loadTransactions()`, `searchTransactions(query)`, `filterByType(filter)`, `filterByDateRange(range)`, `loadNextPage()`, `navigateToDetail(transactionId)`

**DI Dependencies:** `TransactionsRepository`, `AccountsRepository`

**Errors:**
- `network_error`: "Network unavailable. Please check your connection."
- `auth_error`: "Session expired. Please log in again."

---

## Navigation

| From         | To                 | Trigger                         | Type |
|--------------|--------------------|----------------------------------|------|
| transactions | transaction-detail | Tap any txn_list_row             | push |
| transactions | accounts           | Back arrow                       | pop  |
| transactions | home               | nav_home bottom tab              | tab  |
| transactions | send-money         | nav_pay bottom tab               | tab  |
| transactions | cards              | nav_cards bottom tab             | tab  |
| transactions | settings           | nav_more bottom tab              | tab  |

---

## API Endpoints

| Endpoint                                                                          | Auth        | Tag          | Purpose                                        |
|-----------------------------------------------------------------------------------|-------------|--------------|------------------------------------------------|
| GET /obp/v5.1.0/my/banks/{bankId}/accounts/{accountId}/transactions               | DirectLogin | Transactions | Fetch paginated transaction list with filters  |

---

## Design Tokens

| Token                          | Value   | Usage                                                             |
|--------------------------------|---------|-------------------------------------------------------------------|
| color.light.primary            | #4C662B | Filter "All" chip bg, received amount, load more button text, date icon |
| color.light.primary_container  | #CDEDA3 | Monthly summary card bg, merchant logo bg, category chip bg      |
| color.light.error              | #BA1A1A | Spent amount, debit transaction amounts                           |
| color.light.surface            | #FFFFFF | Transaction row card backgrounds                                  |
| color.light.background         | #F9FAEF | Screen background, search bar fill, date picker fill, skeleton   |
| color.light.surface_variant    | #E1E4D5 | Filter chip borders (unselected), vertical summary divider, skeleton |
| color.light.on_surface         | #1A1C16 | Merchant name, date range label                                   |
| color.light.on_surface_variant | #44483D | Date metadata, category labels, search icon, filter chip text    |
| color.light.on_primary         | #FFFFFF | "All" filter chip text (on `#4C662B`)                            |
| typography.title_large         | —       | Monthly totals (22sp/Regular but 700 weight override)             |
| typography.body_medium         | —       | Merchant name labels (14sp/500)                                   |
| typography.body_large          | —       | Transaction amount columns (16sp/600)                             |
| typography.body_small          | —       | Date metadata (12sp/400)                                          |
| typography.label_medium        | —       | Filter chips, "Load More" button text (12sp/500)                  |
| typography.label_small         | —       | Category chips, date group header labels (11sp/500)               |
| radius.md                      | 12dp    | Search bar, date picker, transaction row cards                    |
| radius.lg                      | 16dp    | Monthly summary card                                              |
| radius.pill                    | 20dp    | Filter chips                                                      |
| elevation.level1               | 1dp     | Transaction row card elevation                                    |
| spacing.md                     | 16dp    | Card padding, section margins                                     |
| spacing.sm                     | 8dp     | Between filter chips                                              |

---

_Generated by /idea export | 2026-05-29_
