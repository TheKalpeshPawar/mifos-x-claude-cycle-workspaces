# SPEC — Business Insights

| Field         | Value                       |
|---------------|-----------------------------|
| Feature       | business-insights           |
| Flavor        | consumer                    |
| Status        | approved                    |
| Quality Score | 95                          |
| ViewModel     | BusinessInsightsViewModel   |

---

## Overview

The Business Insights screen gives the Consumer persona a cash-flow view of a single **business** account (product_code BUSINESS). It frames activity for a selected reporting period as Money In / Money Out / Net, breaks expenses down across an 8-category business taxonomy (Payroll & Contractors, Tax, Rent & Facilities, Software & Subscriptions, Insurance, Treasury & Transfers, Income, Other) as a donut + legend, and lists the top counterparties by spend. An assist chip at the top switches between the user's business accounts (the picker is restricted to BUSINESS-classified accounts, resolved via per-account detail fetch since the account-list endpoint returns `product_code: null`); a horizontally-scrolling period selector with a custom-range option drives the reporting window. There are no budgets by design — business accounts are independent books tracked purely by cash flow. The selected business account's transactions are fetched and all period filtering plus categorisation runs client-side (the OBP sandbox caps the transaction window at the 50 newest and ignores date params). The Income category absorbs credit keywords but is filtered out of the expenses-only donut.

---

## Screens

| ID                | Name              | Route               | Layout | Scroll   |
|-------------------|-------------------|---------------------|--------|----------|
| business-insights | Business Insights | /business-insights  | Column | Vertical |

**Shell:** Top app bar — title "Business Insights", navigation icon `arrow_back` (navigate_back action). No bottom navigation bar.

| Bar Item   | Icon       | Action        |
|------------|------------|---------------|
| Back arrow | arrow_back | navigate_back |

---

## Components

| ID                       | Type           | Description                                                                                                       |
|--------------------------|----------------|-------------------------------------------------------------------------------------------------------------------|
| biz_account_selector     | chip (assist)  | "TechStart — Business Current GBP"; trailing `expand_more`; tap → open_account_picker (BUSINESS accounts only)     |
| biz_period_selector_row  | stack (row)    | Horizontal scroll; reporting-period tabs; spacing 8dp; on tap → state_change(selected_period); role tablist        |
| biz_period_label         | text           | "June 2026" — Outfit/body_medium, #5C6057; reflects the selected period                                            |
| biz_cash_flow_card       | card           | Surface_container_low; radius 16dp; padding 16dp; margin_horizontal 20dp; groups the cash-flow row                 |
| biz_cash_flow_row        | stack (row)    | Equal-distribution row: Money In / Money Out / Net                                                                 |
| biz_money_in             | text           | "£75000.00" — Outfit/title_small, bold (period credits total)                                                      |
| biz_money_out            | text           | "-£26300.00" — Outfit/title_small, bold (period debits total)                                                      |
| biz_net                  | text           | "£48700.00" — Outfit/title_small, bold, #4C662B (net = in − out)                                                   |
| biz_expenses_title       | text           | "Expenses by Category" — Outfit/title_small, semibold                                                              |
| biz_expense_donut_card   | card           | Surface_container_low; radius 16dp; padding 16dp; donut chart + category legend; role img                          |
| biz_category_payroll     | list_item      | "Payroll & Contractors — -£15516.01"                                                                               |
| biz_category_tax         | list_item      | "Tax — -£8000.00"                                                                                                  |
| biz_category_rent        | list_item      | "Rent & Facilities — -£2500.00"                                                                                    |
| biz_category_software    | list_item      | "Software & Subscriptions — -£450.00"                                                                              |
| biz_category_insurance   | list_item      | "Insurance — -£350.00"                                                                                             |
| biz_merchants_title      | text           | "Top Counterparties" — Outfit/title_small, semibold                                                                |
| biz_merchants_card       | card           | Surface_container_low; radius 16dp; margin_horizontal 20dp; top-counterparty rows                                  |
| biz_merchant_payroll     | list_item      | "Mifos-X-Open-Bank — 1 payment — -£15000.00"                                                                       |

---

## States

| ID          | Trigger                                                     | Description                                                                                         |
|-------------|------------------------------------------------------------|-----------------------------------------------------------------------------------------------------|
| loading     | Screen entry / account or period change — fetch in flight  | Account selector + period row + period label visible; 3 skeleton cards (height 120) below           |
| populated   | Transactions loaded for the selected business account      | All components visible: account selector, period selector, cash-flow card, expense donut + legend, top counterparties |
| empty       | No business accounts connected to the profile              | "No business accounts" + "Business insights appear once a business account is connected to your profile." (`storefront` icon) |
| no_activity | Business account selected but no transactions in period    | Account selector + period row + label visible; "No activity in this period" + detail (`storefront` icon) |
| error       | Transaction / account-detail fetch failed                  | "Could not load business insights" + "Check your connection and try again." + retry_load            |

---

## State Model

**ViewModel:** `BusinessInsightsViewModel`
**Screen State Type:** `BusinessInsightsUiState`

| Field            | Type                         | Default        |
|------------------|------------------------------|----------------|
| selectedAccount  | BusinessAccount?             | null           |
| businessAccounts | List<BusinessAccount>        | emptyList()    |
| selectedPeriod   | ReportingPeriod              | currentMonth   |
| moneyIn          | BigDecimal                   | ZERO           |
| moneyOut         | BigDecimal                   | ZERO           |
| net              | BigDecimal                   | ZERO           |
| categories       | List<ExpenseCategory>        | emptyList()    |
| topCounterparties| List<Counterparty>           | emptyList()    |
| uiState          | BusinessInsightsUiState      | Loading        |

**Screen State Members:** `Loading`, `Populated`, `Empty`, `NoActivity`, `Error`

**Events:** `OnAccountSelected`, `OnPeriodSelected`, `OnOpenAccountPicker`, `OnRetry`, `NavigateBack`

**Actions:**

| Action                       | Trigger             | Description                                                                 |
|------------------------------|---------------------|-----------------------------------------------------------------------------|
| `loadBusinessAccounts()`     | ScreenOpened        | Resolves BUSINESS accounts via per-account detail fetch (list returns null product_code) |
| `selectAccount(account)`     | OnAccountSelected   | Switches account; refetches transactions for the active period             |
| `selectPeriod(period)`       | OnPeriodSelected    | Updates the reporting window; re-runs client-side filtering + categorisation |
| `computeCashFlow()`          | after fetch         | Sums credits/debits → Money In / Out / Net for the period                  |
| `categoriseExpenses()`       | after fetch         | Buckets debits into the 8-category taxonomy; Income excluded from the donut |
| `retry()`                    | OnRetry             | Re-dispatches the transaction fetch on error                               |

**DI Dependencies:** `AccountsRepository`, `TransactionsRepository`

**Errors:**

| ID            | Message                                            |
|---------------|----------------------------------------------------|
| load_failed   | "Could not load business insights"                 |
| network_error | "Check your connection and try again."             |
| not_logged_in | "Your session expired. Please sign in again."      |

---

## Navigation

| ID       | From              | To       | Trigger                  | Type |
|----------|-------------------|----------|--------------------------|------|
| nav_back | business-insights | (caller) | top app bar back arrow   | pop  |

The account picker (`open_account_picker`) and period selector (`state_change`) are in-screen state actions — they do not navigate.

---

## API Endpoints

| Endpoint                                                            | Method | Auth        | Tag          | Purpose                                                            |
|--------------------------------------------------------------------|--------|-------------|--------------|-------------------------------------------------------------------|
| GET /obp/v5.1.0/my/banks/{bank_id}/accounts/{account_id}/account   | GET    | DirectLogin | Accounts     | Per-account detail — `product_code` for BUSINESS scope classification |
| GET /obp/v6.0.0/my/accounts/{account_id}/transactions              | GET    | DirectLogin | Transactions | Business account transactions for cash-flow analysis (sandbox caps 50 newest) |

---

## Design Tokens

| Token                            | Value           | Usage                                                        |
|----------------------------------|-----------------|-------------------------------------------------------------|
| colors.light.primary             | #4C662B         | biz_net positive value                                       |
| colors.light.on_surface_variant  | #5C6057         | biz_period_label; category secondary text                   |
| colors.light.surface_container_low| (M3 token)     | biz_cash_flow_card / biz_expense_donut_card / biz_merchants_card fill |
| typography.title_small           | Outfit          | cash-flow values; section titles                            |
| typography.body_medium           | Outfit          | period label                                                |
| radius.lg                        | 16dp            | card corner radius                                          |
| spacing.md                       | 16dp            | card padding                                                |
| spacing.lg (20dp)                | 20dp            | card horizontal margin                                      |

---

_Generated by /idea export | 2026-06-11_
