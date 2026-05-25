# Feature Specification — Spending Insights (PFM Dashboard)

| Field | Value |
|---|---|
| Feature | pfm-dashboard |
| Name | Spending Insights |
| Flavor | consumer |
| Status | designed |
| Quality Score | 88 |
| Contract Version | 1.1.0 |

---

## Overview

The Spending Insights dashboard gives consumers a full personal financial management (PFM) view for a chosen reporting period. A scrollable period chip selector (This Month / Last Month / Last 3 Months / Custom) drives the active data window. A summary card shows Total Spent (£1,029.80), Total Received (£3,200.00), and Net (+£2,170.20) for the period side-by-side. An overall budget progress card tracks £1,029.80 of a £1,500.00 monthly budget at 68% consumed (amber indicator). A pie chart with a category legend breaks spending into five categories: Bills £450.00, Food & Dining £320.50, Transport £125.00, Shopping £89.30, Entertainment £45.00. Per-category budget progress cards show individual category budgets with colour-coded fill bars (red = critical ≥90%, amber = approaching ≥60%, green = healthy). A Top Merchants section lists the four highest-spend merchants (Tesco £142.30, Transport for London £78.50, Netflix £17.99, Spotify £11.99) with transaction counts. Budget entries are persisted via OBP's personal data fields API; transaction totals are derived by locally aggregating the OBP transactions feed filtered by the selected date range.

---

## Screens

| Screen ID | Name | Route | Archetype | Scroll |
|---|---|---|---|---|
| pfm-dashboard | Spending Insights | /pfm-dashboard | dashboard | vertical |

---

## Shell

| Zone | Configuration |
|---|---|
| Top app bar | Title "Spending Insights", back arrow (navigate_back → home), tune icon (open_pfm_settings) |
| Bottom nav | Home / Accounts / Insights (active) / Cards / More |

---

## Components

| ID | Type | Description |
|---|---|---|
| pfm_title | text | "Spending Insights" headline_large, #1800B1, bold, padding H20 T16 |
| period_selector_row | stack | Horizontal scrollable chip row, padding H20, B16 |
| period_chip_this_month | chip | Filter chip "This Month" — selected state: bg #1800B1 text #FFFFFF; unselected: bg #F0EDFF text #1800B1 |
| period_chip_last_month | chip | Filter chip "Last Month" — same style, unselected by default |
| period_chip_last_3_months | chip | Filter chip "Last 3 Months" — unselected by default |
| period_chip_custom | chip | Filter chip "Custom" — opens date range picker on tap |
| pfm_period_label | text | Active period label "May 2026" body_medium, #888888 |
| this_month_summary_card | box | White card (radius 20, elevation 2, border #F0F0F0); tappable → transactions |
| summary_section_label | text | "This Month" title_medium semi-bold |
| spent_amount | text | "£1,029.80" title_large bold #FF5252 |
| received_amount | text | "£3,200.00" title_large bold #4CAF50 |
| net_amount | text | "+£2,170.20" title_large bold #1800B1 |
| overall_budget_card | box | Lavender card (bg #F8F4FF, border #E8E0FF, radius 20, elevation 1); tappable → manage_budgets |
| overall_budget_title | text | "Monthly Budget" title_small semi-bold #1800B1 |
| overall_budget_percent | text | "68% used" label_medium semi-bold #FF9800 |
| overall_budget_spent | text | "£1,029.80 spent" body_medium semi-bold |
| overall_budget_remaining | text | "£470.20 left" body_medium semi-bold #4CAF50 |
| overall_budget_progress_track | box | Progress track: bg #E0E0E0, height 10, radius 6 |
| overall_budget_progress_fill | box | Progress fill: bg #FF9800 (amber), width 68%, height 10 |
| overall_budget_of_total | text | "of £1,500.00 monthly budget" label_small #888888 |
| category_section_label | text | "Spending by Category" title_medium semi-bold, padding H20 |
| category_pie_chart | box | Pie chart card (white, radius 20, elevation 2, height 220); tappable → open_chart_detail |
| category_legend_col | stack | Vertical legend list; each row tappable → filter_by_category → transactions |
| category_row_food | stack | Food & Dining row — dot #FF6B6B, amount £320.50 |
| category_row_transport | stack | Transport row — dot #4ECDC4, amount £125.00 |
| category_row_shopping | stack | Shopping row — dot #A8E6CF, amount £89.30 |
| category_row_bills | stack | Bills row — dot #1800B1, amount £450.00 |
| category_row_entertainment | stack | Entertainment row — dot #FFD93D, amount £45.00 |
| budgets_section_label | text | "Budget Progress" title_medium semi-bold, padding H20 |
| budget_food_dining | box | Food & Dining: £320.50 / £350.00, 92% fill #FF5252 (critical) |
| budget_transport | box | Transport: £125.00 / £200.00, 63% fill #FF9800 (approaching) |
| budget_shopping | box | Shopping: £89.30 / £150.00, 60% fill #FF9800 (approaching) |
| budget_bills | box | Bills: £450.00 / £500.00, 90% fill #FF5252 (critical) |
| budget_entertainment | box | Entertainment: £45.00 / £100.00, 45% fill #4CAF50 (healthy) |
| manage_budgets_button | button | "Manage Budgets" outlined #1800B1, radius 12, centered |
| merchants_section_label | text | "Top Merchants" title_medium semi-bold, padding H20 |
| merchants_card | box | White card (radius 20, elevation 2, border #F0F0F0) containing merchant rows |
| merchant_row_tesco | list_item | Tesco — storefront icon #1800B1, £142.30, 8 transactions → transactions |
| merchant_row_tfl | list_item | Transport for London — subway icon #003688, £78.50, 23 transactions → transactions |
| merchant_row_netflix | list_item | Netflix — play_circle icon #E50914, £17.99, 1 transaction → transactions |
| merchant_row_spotify | list_item | Spotify — music_note icon #1DB954, £11.99, 1 transaction → transactions |
| view_all_transactions_button | button | "View All Transactions" text variant #1800B1 → transactions |
| no_budget_set_banner | box | Amber banner (bg #FFF8E1, border #FFE082) shown when no budget defined |
| set_budget_cta_button | button | "Set Budget Now" filled #1800B1 → manage_budgets |

---

## States

| ID | Trigger | Description |
|---|---|---|
| loading | Screen enters; API calls in-flight | Period chips and title visible; 5 skeleton cards shown |
| populated | Data loaded; budgets set | Full dashboard: summary card, overall budget, category chart, per-category budgets, top merchants |
| empty | No transactions in selected period | Period chips + title; empty state with receipt_long icon, "No transaction history yet", "View Accounts" CTA |
| no_budget_set | Transactions loaded but no budget entries found | Summary card + category breakdown shown; amber "No budget set" banner with "Set Budget Now" CTA replaces budget progress section; top merchants still shown |

---

## State Model

**ViewModel:** `PfmDashboardViewModel`

### State Fields

| Name | Type | Default |
|---|---|---|
| totalSpent | BigDecimal | BigDecimal.ZERO |
| totalReceived | BigDecimal | BigDecimal.ZERO |
| categoryBreakdown | List\<CategorySpend\> | emptyList() |
| budgets | List\<BudgetEntry\> | emptyList() |
| overallBudgetLimit | BigDecimal? | null |
| topMerchants | List\<MerchantSpend\> | emptyList() |
| selectedPeriod | PfmPeriod | PfmPeriod.THIS_MONTH |
| reportingPeriod | String | "" |
| uiState | PfmDashboardUiState | Loading |
| error | UiError? | null |

### Error Codes

| Field | Code | Message |
|---|---|---|
| global | LOAD_FAILED | Unable to load spending insights. Please try again. |
| budget_save | SAVE_FAILED | Could not save budget. Please try again. |

### Events

`DataLoaded`, `BudgetEditClicked(categoryId: String)`, `ManageBudgetsClicked`, `ChartDetailClicked(categoryId: String?)`, `PeriodSelected(period: PfmPeriod)`, `CategoryFilterClicked(categoryId: String)`, `MerchantClicked(merchantName: String)`, `RetryLoad`, `NavigateToTransactions`, `NavigateToAccounts`

### Actions

`edit_budget`, `manage_budgets`, `open_chart_detail`, `open_pfm_settings`, `select_period`, `open_custom_date_picker`, `filter_by_category`, `view_merchant_transactions`, `navigate_to_transactions`, `navigate_to_accounts`

### DI Dependencies

`PersonalDataFieldsRepository`, `TransactionsRepository`

---

## Navigation

| Action | Target | Type | Description |
|---|---|---|---|
| navigate_back | home | pop | Top app bar back arrow |
| open_pfm_settings | — | bottom sheet | Top app bar tune icon |
| navigate_to_transactions | transactions | push | Summary card tap / view all button |
| filter_by_category | transactions | push | Category legend row tap; passes categoryId filter |
| view_merchant_transactions | transactions | push | Merchant row tap; passes merchantName filter |
| manage_budgets | — | bottom sheet | Overall budget card tap / Manage Budgets button |
| open_chart_detail | — | full-screen modal | Pie chart tap |
| open_custom_date_picker | — | bottom sheet | "Custom" period chip tap |
| select_period | — | in-place reload | This Month / Last Month / Last 3 Months chip tap |
| navigate_to_accounts | accounts | push | Empty state "View Accounts" CTA |
| edit_budget | — | bottom sheet | Per-category budget card tap |

---

## Category Breakdown (populated state)

| Category | Color | Amount | % |
|---|---|---|---|
| Bills | #1800B1 | £450.00 | 43.7% |
| Food & Dining | #FF6B6B | £320.50 | 31.1% |
| Transport | #4ECDC4 | £125.00 | 12.1% |
| Shopping | #A8E6CF | £89.30 | 8.7% |
| Entertainment | #FFD93D | £45.00 | 4.4% |
| **Total** | | **£1,029.80** | 100% |

## Per-Category Budgets

| Category | Spent | Budget | % | Color |
|---|---|---|---|---|
| Food & Dining | £320.50 | £350.00 | 92% | #FF5252 (critical) |
| Transport | £125.00 | £200.00 | 63% | #FF9800 (approaching) |
| Shopping | £89.30 | £150.00 | 60% | #FF9800 (approaching) |
| Bills | £450.00 | £500.00 | 90% | #FF5252 (critical) |
| Entertainment | £45.00 | £100.00 | 45% | #4CAF50 (healthy) |

## Top Merchants

| Merchant | Icon | Amount | Transactions |
|---|---|---|---|
| Tesco | storefront | £142.30 | 8 |
| Transport for London | directions_subway | £78.50 | 23 |
| Netflix | play_circle | £17.99 | 1 |
| Spotify | music_note | £11.99 | 1 |

---

## Design Tokens

| Token | Value | Usage |
|---|---|---|
| primary | #1800B1 | Title, net amount, buttons, Bills category dot |
| on_primary | #FFFFFF | Button text |
| surface | #FFFFFF | Summary card, budget cards, merchants card |
| surface_variant | #F8F4FF | Overall budget card background (lavender tint) |
| error | #FF5252 | Spent amount, critical budget fills and amounts |
| success | #4CAF50 | Received amount, remaining budget label, healthy fill |
| warning | #FF9800 | Overall budget progress fill, approaching budget fills |
| on_surface_variant | #888888 | Period label, metric sub-labels, merchant transaction count |
| border_default | #F0F0F0 | Card borders |
| border_budget | #E8E0FF | Overall budget card border |

---

*Generated by /idea export | 2026-05-25*
