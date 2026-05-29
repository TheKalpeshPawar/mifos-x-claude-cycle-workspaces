# SPEC — Spending Insights (PFM Dashboard)

| Field         | Value                    |
|---------------|--------------------------|
| Feature       | pfm-dashboard            |
| Flavor        | consumer                 |
| Status        | approved                 |
| Quality Score | 100                      |
| ViewModel     | PfmDashboardViewModel    |

---

## Overview

The Spending Insights screen is the personal finance management (PFM) hub for the consumer persona. It surfaces a full income-vs-expense summary, per-category spending breakdown with a pie chart and colour-coded legend, overall monthly budget progress, per-category budget progress bars, and a top-merchants list — all scoped to a user-selected reporting period (This Month / Last Month / Last 3 Months / Custom).

The screen resolves to six states driven by `PfmDashboardUiState`: **loading** (skeleton placeholders), **populated** / **content** (full data with budgets), **empty** (no transactions in period), **no_budget_set** (transactions present but no budget configured), and **error** (network or auth failure). It navigates back to `home`, forward to `transactions` (with optional category or merchant filter), and to `accounts`. Budget management is handled via a bottom sheet (not a separate route).

Data comes from two OBP endpoints: `GET /obp/v6.0.0/my/personal-data-fields` for budget limits (stored under convention `pfm_budget_<categoryId>`) and `GET /obp/v6.0.0/my/accounts/{account_id}/transactions` filtered by the selected period's date range.

---

## Screens

| ID            | Name               | Route           | Layout | Scroll   |
|---------------|--------------------|-----------------|--------|----------|
| pfm-dashboard | Spending Insights  | /pfm-dashboard  | Column | Vertical |

**Shell:** Top app bar ("Spending Insights", navigation_icon: arrow_back → navigate_back, tune action → open_pfm_settings). Bottom navigation bar with 5 items, Insights tab active.

| Nav Item  | ID            | Icon            | Target        | Active |
|-----------|---------------|-----------------|---------------|--------|
| Home      | nav_home      | home            | home          | false  |
| Accounts  | nav_accounts  | account_balance | accounts      | false  |
| Insights  | nav_insights  | insights        | pfm-dashboard | true   |
| Cards     | nav_cards     | credit_card     | cards         | false  |
| More      | nav_more      | more_horiz      | settings      | false  |

---

## Components

| ID                          | Type      | Description                                                                                                         |
|-----------------------------|-----------|---------------------------------------------------------------------------------------------------------------------|
| pfm_title                   | text      | "Spending Insights" — Outfit/headline_large, #4C662B, bold, 20dp horizontal padding, 16dp top, 4dp bottom          |
| period_selector_row         | stack     | Horizontal scrolling chip row, 8dp spacing, 20dp horizontal padding, 16dp bottom padding, scroll_indicator enabled  |
| period_chip_this_month      | chip      | "This Month" — filter variant, selected by default; selected: #4C662B fill + #FFFFFF text; unselected: #CDEDA3 + #4C662B; 20dp radius, 16dp/8dp padding |
| period_chip_last_month      | chip      | "Last Month" — same variant/colours, unselected default                                                             |
| period_chip_last_3_months   | chip      | "Last 3 Months" — same variant/colours, unselected default                                                          |
| period_chip_custom          | chip      | "Custom" — same variant; tap opens custom date range picker bottom sheet                                            |
| pfm_period_label            | text      | "May 2026" — Outfit/body_medium, #44483D, 20dp horizontal padding, 16dp bottom padding                             |
| this_month_summary_card     | box       | #FFFFFF fill, 20dp radius, 2dp elevation, 20dp padding, 20dp horizontal + bottom margin; bound to obp_transactions_list (totalSpent, totalReceived, netBalance) |
| summary_section_label       | text      | "This Month" — Outfit/title_medium, #1A1C16, semibold, 16dp bottom padding; heading level 2                        |
| summary_metrics_row         | stack     | Horizontal, space_between, 3 equal flex columns                                                                     |
| spent_label                 | text      | "Total Spent" — Outfit/label_small, #44483D, 0.4 letter spacing                                                    |
| spent_amount                | text      | "£1,029.80" — Outfit/title_large, #BA1A1A, bold                                                                    |
| received_label              | text      | "Total Received" — Outfit/label_small, #44483D                                                                      |
| received_amount             | text      | "£3,200.00" — Outfit/title_large, #4C662B, bold                                                                     |
| net_label                   | text      | "Net" — Outfit/label_small, #44483D                                                                                 |
| net_amount                  | text      | "+£2,170.20" — Outfit/title_large, #4C662B, bold                                                                   |
| overall_budget_card         | box       | #CDEDA3 fill, 20dp radius, 1dp elevation, 20dp padding, 20dp horizontal + bottom margin; bound to obp_personal_data_fields (overallBudgetLimit, budgets) |
| overall_budget_title        | text      | "Monthly Budget" — Outfit/title_small, #4C662B, semibold; heading level 2                                          |
| overall_budget_percent      | text      | "68% used" — Outfit/label_medium, #44483D, semibold (a11y: #44483D ≥7.25:1; was #E8A317 — FAIL)                  |
| overall_budget_spent        | text      | "£1,029.80 spent" — Outfit/body_medium, #1A1C16, semibold                                                          |
| overall_budget_remaining    | text      | "£470.20 left" — Outfit/body_medium, #4C662B, semibold                                                             |
| overall_budget_progress_track | box     | #E1E4D5 track, 6dp radius, 10dp height, full width; role: progressbar                                              |
| overall_budget_progress_fill  | box     | #E8A317 fill, 6dp radius, 10dp height, width "68%"                                                                 |
| overall_budget_of_total     | text      | "of £1,500.00 monthly budget" — Outfit/label_small, #44483D, 4dp top padding                                       |
| category_section_label      | text      | "Spending by Category" — Outfit/title_medium, #1A1C16, semibold, 20dp horizontal padding; heading level 2          |
| category_pie_chart          | box       | #FFFFFF fill, 20dp radius, 2dp elevation, 220dp height, 20dp horizontal margin; pie chart of 5 categories; bound to obp_transactions_list (categoryBreakdown) |
| category_legend_col         | stack     | Vertical list, 8dp spacing, 20dp horizontal + 12dp vertical padding; 5 colour-dot + label + amount rows            |
| category_row_food           | stack     | "Food & Dining": #BA1A1A dot (12×12dp) + label (body_medium #1A1C16) + "£320.50" (body_medium semibold) — 31.1%  |
| category_row_transport      | stack     | "Transport": #386663 dot + label + "£125.00" — 12.1%                                                               |
| category_row_shopping       | stack     | "Shopping": #CDEDA3 dot + label + "£89.30" — 8.7%                                                                  |
| category_row_bills          | stack     | "Bills": #4C662B dot + label + "£450.00" — 43.7%                                                                   |
| category_row_entertainment  | stack     | "Entertainment": #E8A317 dot + label + "£45.00" — 4.4%                                                             |
| budgets_section_label       | text      | "Budget Progress" — Outfit/title_medium, #1A1C16, semibold, 20dp horizontal padding; heading level 2               |
| budget_food_dining          | box       | #FFFFFF, 16dp radius, 1dp elevation, 16dp padding, 20dp horizontal margin, 10dp bottom margin; Food & Dining budget card (92% — near limit) |
| food_dining_amounts         | text      | "£320.50 / £350.00" — Outfit/body_medium, #BA1A1A, semibold (near limit colour)                                   |
| food_dining_progress_fill   | box       | #BA1A1A fill, 4dp radius, 8dp height, width "92%"                                                                  |
| budget_transport            | box       | #FFFFFF, 16dp radius, 10dp bottom margin; Transport — £125.00 / £200.00, 63%                                       |
| transport_amounts           | text      | "£125.00 / £200.00" — Outfit/body_medium, #44483D                                                                  |
| transport_progress_fill     | box       | #E8A317 fill, "63%"                                                                                                 |
| budget_shopping             | box       | #FFFFFF, 16dp radius; Shopping — £89.30 / £150.00, 60%                                                             |
| shopping_amounts            | text      | "£89.30 / £150.00" — Outfit/body_medium, #44483D                                                                   |
| shopping_progress_fill      | box       | #4C662B fill, "60%"                                                                                                 |
| budget_bills                | box       | #FFFFFF, 16dp radius; Bills — £450.00 / £500.00, 90% (near limit)                                                  |
| bills_amounts               | text      | "£450.00 / £500.00" — Outfit/body_medium, #BA1A1A, semibold                                                        |
| bills_progress_fill         | box       | #BA1A1A fill, "90%"                                                                                                 |
| budget_entertainment        | box       | #FFFFFF, 16dp radius; Entertainment — £45.00 / £100.00, 45%                                                        |
| entertainment_amounts       | text      | "£45.00 / £100.00" — Outfit/body_medium, #44483D                                                                   |
| entertainment_progress_fill | box       | #4C662B fill, "45%"                                                                                                 |
| manage_budgets_button       | button    | "Manage Budgets" — outlined, #4C662B border + text, 12dp radius, 24dp horizontal + 14dp vertical padding, centered |
| merchants_section_label     | text      | "Top Merchants" — Outfit/title_medium, #1A1C16, semibold, 20dp horizontal padding; heading level 2                 |
| merchants_card              | box       | #FFFFFF, 20dp radius, 2dp elevation, 16dp horizontal + 8dp vertical padding, 20dp horizontal + 24dp bottom margin  |
| merchant_row_tesco          | list_item | "Tesco" — storefront icon, #4C662B on #CDEDA3 circle (40dp); "8 transactions"; "£142.30" (#BA1A1A bold)           |
| merchant_row_netflix        | list_item | "Netflix" — play_circle icon, #BA1A1A on #CDEDA3 circle; "1 transaction"; "£17.99" (#BA1A1A bold)                 |
| merchant_row_spotify        | list_item | "Spotify" — music_note icon, #4C662B on #CDEDA3 circle; "1 transaction"; "£11.99" (#BA1A1A bold)                  |
| merchant_row_tfl            | list_item | "Transport for London" — directions_subway icon, #386663 on #DCE7C8 circle; "23 transactions"; "£78.50" (#BA1A1A bold) |
| view_all_transactions_button| button    | "View All Transactions" — text variant, #4C662B, Outfit/label_large, centered, 32dp bottom margin                  |
| no_budget_set_banner        | box       | #CDEDA3 fill, 16dp radius, #E8A317 1dp border, 20dp padding, 20dp horizontal + 16dp bottom margin; visible in no_budget_set state only |
| no_budget_banner_title      | text      | "No budget set" — Outfit/title_small, #44483D, semibold (a11y: ≥7.25:1; was #E8A317 — FAIL)                      |
| no_budget_banner_body       | text      | "Set a monthly budget to track how much you spend against your target." — Outfit/body_small, #44483D               |
| set_budget_cta_button       | button    | "Set Budget Now" — filled, #4C662B bg + #FFFFFF text, 12dp radius, 24dp/14dp padding, centered, 12dp top margin    |

---

## States

| ID             | Trigger                                           | Description                                                                                                               |
|----------------|---------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| loading        | Screen entry / RetryLoad                          | Title + period chip row + period label visible; 5 skeleton cards (120dp, #E1E4D5) replace data sections; 200ms shimmer    |
| populated      | Data loaded, budget configured                    | Full screen: summary card, overall budget card, category chart + legend, 5 budget progress cards, merchant card, View All |
| content        | Alias for populated (Kotlin sealed class branch)  | Identical visible components to populated                                                                                 |
| empty          | No transactions in selected period                | Title + period selector; receipt_long icon + "No transaction history yet" + "View Accounts" CTA                           |
| no_budget_set  | Transactions present, no budget configured        | Summary card + category chart + no_budget_set_banner ("No budget set" + "Set Budget Now" CTA) + merchant card             |
| error          | Network or auth failure                           | Title + period selector; "Could not load spending insights. Please try again." + Retry action                             |

---

## State Model

**ViewModel:** `PfmDashboardViewModel`
**Screen State Type:** `PfmDashboardUiState`

| Name               | Type                      | Default               |
|--------------------|---------------------------|-----------------------|
| totalSpent         | BigDecimal                | BigDecimal.ZERO       |
| totalReceived      | BigDecimal                | BigDecimal.ZERO       |
| categoryBreakdown  | List\<CategorySpend\>     | emptyList()           |
| budgets            | List\<BudgetEntry\>       | emptyList()           |
| overallBudgetLimit | BigDecimal?               | null                  |
| topMerchants       | List\<MerchantSpend\>     | emptyList()           |
| selectedPeriod     | PfmPeriod                 | PfmPeriod.THIS_MONTH  |
| reportingPeriod    | String                    | ""                    |
| uiState            | PfmDashboardUiState       | Loading               |
| error              | UiError?                  | null                  |

**Events:** `DataLoaded`, `BudgetEditClicked(categoryId: String)`, `ManageBudgetsClicked`, `ChartDetailClicked(categoryId: String?)`, `PeriodSelected(period: PfmPeriod)`, `CategoryFilterClicked(categoryId: String)`, `MerchantClicked(merchantName: String)`, `RetryLoad`, `NavigateToTransactions`, `NavigateToAccounts`

**Actions:** `edit_budget`, `manage_budgets`, `open_chart_detail`, `open_pfm_settings`, `select_period`, `open_custom_date_picker`, `filter_by_category`, `view_merchant_transactions`, `navigate_to_transactions`, `navigate_to_accounts`

**DI Dependencies:** `PersonalDataFieldsRepository`, `TransactionsRepository`

**Errors:**
- `LOAD_FAILED` (global): "Unable to load spending insights. Please try again."
- `SAVE_FAILED` (budget_save): "Could not save budget. Please try again."

---

## Navigation

| From          | To             | Trigger                                                          | Type   |
|---------------|----------------|------------------------------------------------------------------|--------|
| pfm-dashboard | home           | navigate_back (top app bar arrow_back)                           | pop    |
| pfm-dashboard | transactions   | navigate_to_transactions (summary card tap, View All button)     | push   |
| pfm-dashboard | transactions   | filter_by_category (category legend row tap)                     | push   |
| pfm-dashboard | transactions   | view_merchant_transactions (merchant row tap)                    | push   |
| pfm-dashboard | accounts       | navigate_to_accounts (empty state "View Accounts" CTA)           | push   |
| pfm-dashboard | —              | manage_budgets (overall budget card, Manage Budgets btn, Set Budget Now) | sheet |
| pfm-dashboard | —              | open_chart_detail (category pie chart tap)                       | sheet  |
| pfm-dashboard | —              | open_custom_date_picker (Custom period chip tap)                 | sheet  |
| pfm-dashboard | —              | open_pfm_settings (tune icon in top app bar)                     | sheet  |
| pfm-dashboard | —              | select_period (This Month / Last Month / Last 3 Months chip tap) | none   |
| pfm-dashboard | —              | edit_budget (per-category budget card tap)                       | sheet  |

---

## API Endpoints

| Endpoint                                                          | Auth        | Tag          | Purpose                                          |
|-------------------------------------------------------------------|-------------|--------------|--------------------------------------------------|
| GET /obp/v6.0.0/my/personal-data-fields                          | DirectLogin | User         | Read budget limits stored as personal data fields |
| POST /obp/v6.0.0/my/personal-data-fields                         | DirectLogin | User         | Create or update a category budget limit          |
| GET /obp/v6.0.0/my/accounts/{account_id}/transactions            | DirectLogin | Transactions | Fetch transactions for PFM aggregation, period-filtered |

---

## Design Tokens

| Token                              | Value    | Usage                                                                                       |
|------------------------------------|----------|---------------------------------------------------------------------------------------------|
| colors.light.primary               | #4C662B  | Page title, period chip selected fill, overall budget title, received/net amounts, budget remaining, shopping/entertainment progress fill, "Manage Budgets" + "View All" text |
| colors.light.primary_container     | #CDEDA3  | Overall budget card fill, period chip unselected bg, Tesco/Spotify merchant icon bg, no_budget_set_banner fill |
| colors.light.secondary             | #386663  | Transport category dot, TfL merchant icon colour                                            |
| colors.light.nav_active_indicator  | #DCE7C8  | TfL merchant icon background container                                                      |
| colors.light.error                 | #BA1A1A  | Total Spent amount, Food & Dining / Bills budget amounts + progress fill, Netflix icon colour, all merchant amounts |
| colors.light.surface               | #FFFFFF  | Summary card, per-category budget cards, merchants card                                     |
| colors.light.background            | #F9FAEF  | Screen background                                                                           |
| colors.light.on_background         | #1A1C16  | Section headers, category/merchant/budget category names, summary section label             |
| colors.light.on_surface_variant    | #44483D  | Period label, metric sub-labels, Transport/Shopping/Entertainment budget amounts            |
| colors.light.pending               | #E8A317  | Overall budget progress fill, transport budget progress fill, entertainment category dot, no_budget_set_banner border |
| colors.light.surface_variant       | #E1E4D5  | Budget progress track backgrounds                                                           |
| typography.headline_large          | Outfit 32sp      | Page title "Spending Insights"                                                    |
| typography.title_medium            | Outfit 16sp/500  | Section headers (This Month, Spending by Category, Budget Progress, Top Merchants)|
| typography.title_large             | Outfit 22sp/400  | Metric amounts (£1,029.80, £3,200.00, +£2,170.20)                                |
| typography.title_small             | Outfit 14sp/500  | "Monthly Budget", per-category budget title, "No budget set" banner title         |
| typography.body_medium             | Outfit 14sp/400  | Period label, budget amounts, category amounts                                    |
| typography.body_small              | Outfit 12sp/400  | "No budget set" banner body text                                                  |
| typography.label_large             | Outfit 14sp/500  | "Manage Budgets" + "View All Transactions" button labels                          |
| typography.label_medium            | Outfit 12sp/500  | Period chip labels, "68% used" budget percent                                     |
| typography.label_small             | Outfit 11sp/500  | Metric sub-labels (Total Spent, Total Received, Net), "of £1,500.00 monthly budget"|
| radius.pill                        | 20dp     | Period filter chips                                                                         |
| radius.xl (~20dp)                  | 20dp     | Summary card, overall budget card, pie chart card, merchants card                           |
| radius.lg (16dp)                   | 16dp     | Per-category budget cards, no_budget_set_banner                                             |
| radius.md (12dp)                   | 12dp     | Manage Budgets + Set Budget Now button radius                                               |
| radius.xs (4dp)                    | 4dp      | Budget progress fills and tracks                                                            |
| elevation.level1                   | 1dp      | Overall budget card, per-category budget cards                                              |
| elevation.level2                   | 3dp      | Summary card, pie chart card, merchants card                                                |
| iconography.icon-xl                | 40dp     | Merchant icon circles (Tesco, Netflix, Spotify, TfL)                                       |

---

_Generated by /idea export | 2026-05-30_
