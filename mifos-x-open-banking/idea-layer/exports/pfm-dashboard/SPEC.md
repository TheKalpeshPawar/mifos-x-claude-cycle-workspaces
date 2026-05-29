# SPEC — Spending Insights

| Field         | Value                    |
|---------------|--------------------------|
| Feature       | pfm-dashboard            |
| Flavor        | consumer                 |
| Status        | approved                 |
| Quality Score | 100                      |
| ViewModel     | PfmDashboardViewModel    |

---

## Overview

Spending Insights is the personal finance management dashboard for Consumer persona users. It surfaces a full-period breakdown of income vs. spending, an overall monthly budget progress card, a category spending pie chart with legend (5 categories), per-category budget progress cards, and a top-merchants list. A horizontally-scrollable period selector (This Month / Last Month / Last 3 Months / Custom) drives all data.

Budget limits are stored as OBP personal data fields (`pfm_budget_<categoryId>`), enabling server-side persistence without a separate budget service. For May 2026: spent £1,029.80 against a £1,500.00 monthly budget (68%), received £3,200.00, net positive £2,170.20. Categories: Bills (£450.00, 43.7%), Food & Dining (£320.50, 31.1%), Transport (£125.00, 12.1%), Shopping (£89.30, 8.7%), Entertainment (£45.00, 4.4%). Top merchants: Tesco £142.30 (8 txns), TfL £78.50 (23 txns), Netflix £17.99, Spotify £11.99.

---

## Screens

| ID            | Name              | Route          | Layout | Scroll   |
|---------------|-------------------|----------------|--------|----------|
| pfm-dashboard | Spending Insights | /pfm-dashboard | Column | Vertical |

**Shell:** Top app bar ("Spending Insights", back arrow, tune filter action) + Bottom navigation bar with 5 items (Insights active)

| Nav Item | ID           | Icon            | Target        |
|----------|--------------|-----------------|---------------|
| Home     | nav_home     | home            | home          |
| Accounts | nav_accounts | account_balance | accounts      |
| Insights | nav_insights | insights        | pfm-dashboard |
| Cards    | nav_cards    | credit_card     | cards         |
| More     | nav_more     | more_horiz      | settings      |

---

## Components

| ID                           | Type      | Description                                                                                  |
|------------------------------|-----------|----------------------------------------------------------------------------------------------|
| pfm_title                    | text      | "Spending Insights" — Outfit/headline_large, #4C662B, bold                                  |
| period_selector_row          | stack     | Horizontal scroll row of 4 filter chips; fires select_period on tap                         |
| period_chip_this_month       | chip      | "This Month" — selected bg #4C662B text #FFFFFF; unselected bg #CDEDA3 text #4C662B         |
| period_chip_last_month       | chip      | "Last Month" — same chip token colors, unselected by default                                |
| period_chip_last_3_months    | chip      | "Last 3 Months" — same chip token colors, unselected by default                             |
| period_chip_custom           | chip      | "Custom" — opens date range picker bottom sheet on tap                                      |
| pfm_period_label             | text      | "May 2026" — Outfit/body_medium, #44483D                                                    |
| this_month_summary_card      | box       | White card (#FFFFFF, radius 20, elevation 2) — 3-column Spent/Received/Net metrics          |
| summary_section_label        | text      | "This Month" — Outfit/title_medium, #1A1C16, semibold                                       |
| spent_label                  | text      | "Total Spent" — Outfit/label_small, #44483D                                                 |
| spent_amount                 | text      | "£1,029.80" — Outfit/title_large, #BA1A1A, bold                                             |
| received_label               | text      | "Total Received" — Outfit/label_small, #44483D                                              |
| received_amount              | text      | "£3,200.00" — Outfit/title_large, #4C662B, bold                                             |
| net_label                    | text      | "Net" — Outfit/label_small, #44483D                                                         |
| net_amount                   | text      | "+£2,170.20" — Outfit/title_large, #4C662B, bold                                            |
| overall_budget_card          | box       | #CDEDA3 card (radius 20, elevation 1) — overall budget heading + progress bar               |
| overall_budget_title         | text      | "Monthly Budget" — Outfit/title_small, #4C662B, semibold                                    |
| overall_budget_percent       | text      | "68% used" — Outfit/label_medium, #44483D                                                   |
| overall_budget_spent         | text      | "£1,029.80 spent" — Outfit/body_medium, #1A1C16, semibold                                   |
| overall_budget_remaining     | text      | "£470.20 left" — Outfit/body_medium, #4C662B, semibold                                      |
| overall_budget_progress_track| box       | Progress track — #E1E4D5, radius 6, height 10dp, full width                                 |
| overall_budget_progress_fill | box       | Progress fill — #E8A317, width 68%, radius 6, height 10dp                                   |
| overall_budget_of_total      | text      | "of £1,500.00 monthly budget" — Outfit/label_small, #44483D                                 |
| category_section_label       | text      | "Spending by Category" — Outfit/title_medium, #1A1C16, semibold                             |
| category_pie_chart           | box       | White card (radius 20, h 220dp, elevation 2) — pie chart; a11y: Bills 43.7%, Food 31.1%…   |
| category_legend_col          | stack     | Vertical column of 5 category legend rows                                                    |
| category_row_food            | stack     | "Food & Dining" — dot #BA1A1A, amount "£320.50", Outfit/body_medium, #1A1C16               |
| category_row_transport       | stack     | "Transport" — dot #386663, amount "£125.00"                                                  |
| category_row_shopping        | stack     | "Shopping" — dot #CDEDA3, amount "£89.30"                                                   |
| category_row_bills           | stack     | "Bills" — dot #4C662B, amount "£450.00"                                                     |
| category_row_entertainment   | stack     | "Entertainment" — dot #E8A317, amount "£45.00"                                              |
| budgets_section_label        | text      | "Budget Progress" — Outfit/title_medium, #1A1C16, semibold                                  |
| budget_food_dining           | box       | White card (radius 16) — "Food & Dining £320.50 / £350.00", fill 92% #BA1A1A (near limit)   |
| budget_transport             | box       | White card — "Transport £125.00 / £200.00", fill 63% #E8A317                               |
| budget_shopping              | box       | White card — "Shopping £89.30 / £150.00", fill 60% #4C662B                                 |
| budget_bills                 | box       | White card — "Bills £450.00 / £500.00", fill 90% #BA1A1A (near limit)                      |
| budget_entertainment         | box       | White card — "Entertainment £45.00 / £100.00", fill 45% #4C662B                            |
| manage_budgets_button        | button    | "Manage Budgets" — outlined, border+text #4C662B, radius 12, centered                      |
| merchants_section_label      | text      | "Top Merchants" — Outfit/title_medium, #1A1C16, semibold                                   |
| merchants_card               | box       | White card (radius 20, elevation 2) — 4 merchant list rows                                  |
| merchant_row_tesco           | list_item | "Tesco" — storefront icon (bg #CDEDA3, color #4C662B), "8 transactions", "£142.30" error    |
| merchant_row_netflix         | list_item | "Netflix" — play_circle icon (bg #CDEDA3, color #BA1A1A), "1 transaction", "£17.99" error  |
| merchant_row_spotify         | list_item | "Spotify" — music_note icon (bg #CDEDA3, color #4C662B), "1 transaction", "£11.99" error   |
| merchant_row_tfl             | list_item | "Transport for London" — directions_subway icon (bg #DCE7C8, color #386663), "23 transactions", "£78.50" error |
| view_all_transactions_button | button    | "View All Transactions" — text variant, #4C662B, Outfit/label_large                        |
| no_budget_set_banner         | box       | #CDEDA3 card amber border — "No budget set" + body + "Set Budget Now" filled CTA #4C662B   |

---

## States

| ID            | Trigger                                 | Description                                                                      |
|---------------|-----------------------------------------|----------------------------------------------------------------------------------|
| loading       | Screen entry / RetryLoad                | Title + period selector visible; 5 skeleton cards shimmer; all data cards hidden |
| populated     | Transactions + budgets loaded           | All sections visible: summary, overall budget, pie, per-category budgets, merchants |
| empty         | No transactions in selected period      | Title + period selector; empty state (receipt_long icon, "View Accounts" CTA)    |
| no_budget_set | Transactions loaded, no budget set      | Summary + pie + merchants visible; budget section shows prompt banner            |
| content       | Alias for populated                     | Same as populated — default loaded state alias                                   |
| error         | Network / API failure                   | Title + period selector; error message + "Retry" action                          |

---

## State Model

**ViewModel:** `PfmDashboardViewModel`
**Screen State Type:** `PfmDashboardUiState`

| Name               | Type                  | Default              |
|--------------------|-----------------------|----------------------|
| totalSpent         | BigDecimal            | BigDecimal.ZERO      |
| totalReceived      | BigDecimal            | BigDecimal.ZERO      |
| categoryBreakdown  | List\<CategorySpend\> | emptyList()          |
| budgets            | List\<BudgetEntry\>   | emptyList()          |
| overallBudgetLimit | BigDecimal?           | null                 |
| topMerchants       | List\<MerchantSpend\> | emptyList()          |
| selectedPeriod     | PfmPeriod             | PfmPeriod.THIS_MONTH |
| reportingPeriod    | String                | ""                   |
| uiState            | PfmDashboardUiState   | Loading              |
| error              | UiError?              | null                 |

**Events:** `DataLoaded`, `BudgetEditClicked(categoryId)`, `ManageBudgetsClicked`, `ChartDetailClicked(categoryId?)`, `PeriodSelected(period)`, `CategoryFilterClicked(categoryId)`, `MerchantClicked(merchantName)`, `RetryLoad`, `NavigateToTransactions`, `NavigateToAccounts`

**DI Dependencies:** `PersonalDataFieldsRepository`, `TransactionsRepository`

**Errors:**
- `LOAD_FAILED`: "Unable to load spending insights. Please try again."
- `SAVE_FAILED`: "Could not save budget. Please try again."

---

## Navigation

| From          | To           | Trigger                              | Type  |
|---------------|--------------|--------------------------------------|-------|
| pfm-dashboard | transactions | summary card tap / View All tap      | push  |
| pfm-dashboard | transactions | category row tap (filtered)          | push  |
| pfm-dashboard | transactions | merchant row tap (filtered)          | push  |
| pfm-dashboard | accounts     | nav_accounts tab tap                 | tab   |
| pfm-dashboard | home         | nav_home tab tap / back arrow        | tab   |
| pfm-dashboard | cards        | nav_cards tab tap                    | tab   |
| pfm-dashboard | settings     | nav_more tab tap                     | tab   |
| pfm-dashboard | —            | manage_budgets_button                | sheet |
| pfm-dashboard | —            | category_pie_chart tap               | sheet |
| pfm-dashboard | —            | period_chip_custom tap               | sheet |

---

## API Endpoints

| Endpoint                                               | Auth        | Tag          | Purpose                                         |
|--------------------------------------------------------|-------------|--------------|-------------------------------------------------|
| GET /obp/v6.0.0/my/personal-data-fields               | DirectLogin | User         | Read PFM budgets stored as personal data fields |
| POST /obp/v6.0.0/my/personal-data-fields              | DirectLogin | User         | Create/update budget (pfm_budget_<categoryId>)  |
| GET /obp/v6.0.0/my/accounts/{account_id}/transactions | DirectLogin | Transactions | Fetch transactions for PFM analysis per period  |

---

## Design Tokens

| Token                           | Value   | Usage                                                              |
|---------------------------------|---------|--------------------------------------------------------------------|
| colors.light.primary            | #4C662B | Page title, received/net amounts, budget remaining, safe fills     |
| colors.light.primary_container  | #CDEDA3 | Overall budget card bg, chip unselected bg, merchant icon bg       |
| colors.light.on_primary         | #FFFFFF | Chip selected text                                                 |
| colors.light.error              | #BA1A1A | Spent amount, food & bills budget fills, merchant amounts, food dot|
| colors.light.pending            | #E8A317 | Overall progress fill (68%), transport fill, entertainment dot     |
| colors.light.secondary          | #386663 | Transport category dot, TfL icon                                  |
| colors.light.surface            | #FFFFFF | Summary card, budget cards, merchants card                         |
| colors.light.surface_variant    | #E1E4D5 | Progress track background                                          |
| colors.light.on_surface         | #1A1C16 | Section labels, category names, merchant names                     |
| colors.light.on_surface_variant | #44483D | Period label, budget percent, column labels                        |
| colors.light.background         | #F9FAEF | Screen background                                                  |
| colors.light.nav_active_indicator | #DCE7C8 | TfL merchant icon bg, active nav pill                            |
| typography.headline_large       | —       | Page title                                                         |
| typography.title_medium         | —       | Section headers (category, budget, merchants)                      |
| typography.title_large          | —       | Spent / received / net metric values                               |
| typography.body_medium          | —       | Period label, category/budget amounts, merchant names              |
| typography.label_medium         | —       | Budget percent, filter chip text                                   |
| typography.label_small          | —       | Metric column labels, budget-of-total text                         |
| radius.xl                       | 24dp    | Summary card, pie chart card, merchants card                       |
| radius.lg                       | 16dp    | Per-category budget cards                                          |
| radius.sm                       | 8dp     | Feature chips, badge dots                                          |
| elevation.level2                | 3dp     | Summary card, pie chart card, merchants card                       |

---

_Generated by /idea export | 2026-05-29_
