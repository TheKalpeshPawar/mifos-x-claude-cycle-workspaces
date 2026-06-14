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

The Business Insights screen gives the Consumer persona a cash-flow dashboard for a single **business** account (AccountCategory: Business, resolved client-side from the OBIE account list). It frames activity for a selected reporting period as Money In / Money Out / Net, breaks expenses across an 8-category business taxonomy (Payroll & Contractors, Tax, Rent & Facilities, Software & Subscriptions, Insurance, Treasury & Transfers, Income, Other) as a donut chart + legend, and lists top counterparties by spend.

An assist chip at the top switches between the user's business accounts; the picker is restricted client-side to BUSINESS-classified accounts from the OBIE `GET /accounts` response (`Data.Account[].AccountCategory`). A horizontally-scrolling period selector (Week / Month / Quarter / Year / Custom) drives the reporting window; the selected period maps to `fromBookingDateTime`/`toBookingDateTime` query params on `GET /accounts/{AccountId}/transactions`. All cash-flow aggregation, the 8-category expense breakdown, and top-counterparty ranking run **client-side** from the transaction list — OBIE v4.0 has no analytics endpoint. The Income category absorbs credit keywords but is excluded from the expenses-only donut. There are no budgets by design — business accounts are tracked purely by cash flow.

Five states are declared: `loading` (skeleton shimmer while data is fetched), `populated` (full dashboard), `empty` (no Business-scoped account in the authorised list), `no_activity` (account connected but zero transactions in the selected period), and `error` (fetch failed — retry available).

---

## Screens

| ID                | Name              | Route               | Layout | Scroll   |
|-------------------|-------------------|---------------------|--------|----------|
| business-insights | Business Insights | /business-insights  | Column | Vertical |

**Shell:** Top app bar — title "Business Insights", navigation icon `arrow_back` (navigate_back). No bottom navigation bar.

| Bar Item    | Icon       | Action        |
|-------------|------------|---------------|
| Back arrow  | arrow_back | navigate_back |

---

## Components

| ID                       | Type              | Description                                                                                                                        |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| biz_account_selector     | chip (assist)     | "TechStart — Business Current GBP"; trailing `expand_more`; tap → `open_account_picker` (BUSINESS accounts only); role button       |
| biz_period_selector_row  | stack (row)       | Horizontal scroll; period tabs (Week / Month / Quarter / Year / Custom); 8dp spacing; tap → `state_change(selected_period)`; role tablist |
| biz_period_label         | text              | "June 2026" — Outfit/body_medium, #5C6057; reflects selected period                                                                |
| biz_cash_flow_card       | card              | surface_container_low; 16dp radius; 16dp padding; 20dp horizontal margin; groups the cash-flow row; role group                      |
| biz_cash_flow_row        | stack (row)       | Equal-distribution 3-column row: Money In / Money Out / Net                                                                        |
| biz_money_in             | text              | "£75000.00" — Outfit/title_small, bold; sum of CreditDebitIndicator=Credit transactions for the period                             |
| biz_money_out            | text              | "-£26300.00" — Outfit/title_small, bold; sum of CreditDebitIndicator=Debit transactions                                            |
| biz_net                  | text              | "£48700.00" — Outfit/title_small, bold, #4C662B; Net = Money In + Money Out                                                        |
| biz_expenses_title       | text              | "Expenses by Category" — Outfit/title_small, semibold; role heading level 2                                                        |
| biz_expense_donut_card   | card              | surface_container_low; 16dp radius; 16dp padding; 20dp horizontal margin; donut chart + legend rows; role img                      |
| biz_category_payroll     | list_item         | "Payroll & Contractors — -£15516.01"; a11y label "Payroll and Contractors: 15,516 pounds"                                          |
| biz_category_tax         | list_item         | "Tax — -£8000.00"; a11y label "Tax: 8,000 pounds"                                                                                 |
| biz_category_rent        | list_item         | "Rent & Facilities — -£2500.00"; a11y label "Rent and Facilities: 2,500 pounds"                                                    |
| biz_category_software    | list_item         | "Software & Subscriptions — -£450.00"; a11y label "Software and Subscriptions: 450 pounds"                                         |
| biz_category_insurance   | list_item         | "Insurance — -£350.00"; a11y label "Insurance: 350 pounds"                                                                        |
| biz_merchants_title      | text              | "Top Counterparties" — Outfit/title_small, semibold; role heading level 2                                                          |
| biz_merchants_card       | card              | surface_container_low; 16dp radius; 20dp horizontal margin; top-counterparty rows                                                   |
| biz_merchant_payroll     | list_item         | "Mifos-X-Open-Bank — 1 payment — -£15000.00"                                                                                       |

---

## States

| ID          | Trigger                                                              | Description                                                                                                                                |
|-------------|----------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| loading     | Screen entry / account or period change — fetch in flight            | Account selector + period row + period label visible. 3 skeleton cards (height 120, shimmer, reduced-motion fallback = static placeholder). |
| populated   | Accounts + transactions loaded, ≥1 transaction in the period window | Full dashboard: account selector, period selector, cash-flow card, expense donut + legend, top counterparties.                              |
| empty       | No Business-scoped account in the authorised account list            | `storefront` icon + "No business accounts" + "Business insights appear once a business account is connected to your profile."               |
| no_activity | Business account in scope, zero transactions in the period           | Account selector + period selector + period label visible. `storefront` icon + "No activity in this period" + supporting detail text.       |
| error       | `get_accounts`, `get_balances`, or `get_transactions` fails          | "Could not load business insights" + "Check your connection and try again." + Retry (`retry_load` intent).                                 |

---

## State Model

**ViewModel:** `BusinessInsightsViewModel`
**Screen State Type:** `BusinessInsightsUiState`
**Pattern:** MVI

| Field             | Type                            | Default        | Notes                                                                                                    |
|-------------------|---------------------------------|----------------|----------------------------------------------------------------------------------------------------------|
| phase             | Enum (loading/populated/empty/no_activity/error) | loading | Drives which declared state renders                                                           |
| selectedAccount   | OBReadAccount6?                 | null           | Account in scope (`Data.Account[]`); null until `get_accounts` resolves                                   |
| businessAccounts  | List\<OBReadAccount6\>          | emptyList()    | Authorised accounts filtered client-side to Business `AccountCategory`                                    |
| selectedPeriod    | Period                          | currentMonth   | Maps to `fromBookingDateTime`/`toBookingDateTime` query params on `get_transactions`                      |
| moneyIn           | OBActiveOrHistoricCurrencyAndAmount | 0           | Client-side sum of CreditDebitIndicator=Credit; DERIVED                                                  |
| moneyOut          | OBActiveOrHistoricCurrencyAndAmount | 0           | Client-side sum of CreditDebitIndicator=Debit; DERIVED                                                   |
| net               | OBActiveOrHistoricCurrencyAndAmount | 0           | moneyIn − moneyOut; DERIVED                                                                              |
| expenseCategories | List\<CategoryBreakdown\>       | emptyList()    | Debit totals over 8-category taxonomy; Income excluded from donut; DERIVED                               |
| topCounterparties | List\<Counterparty\>            | emptyList()    | Client-side aggregation by resolved display name; DERIVED — never a raw login username                   |

**Intents:** `LoadInsights`, `SelectAccount`, `SelectPeriod`, `Retry`

**DI:** `AccountsRepository`, `TransactionsRepository`

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

The account picker (`open_account_picker`) and period selector (`state_change`) are in-screen state actions — they do not navigate. Custom range picker opens as a bottom sheet within the same screen.

---

## API Endpoints

| Endpoint                                                      | Method | Auth                  | Tag  | Purpose                                                                                           |
|---------------------------------------------------------------|--------|-----------------------|------|---------------------------------------------------------------------------------------------------|
| GET /obie/open-banking/v4.0/aisp/accounts                     | GET    | Authorization Code    | AISP | Authorised account list — filtered client-side to Business AccountCategory for the account picker  |
| GET /obie/open-banking/v4.0/aisp/accounts/{AccountId}/balances| GET    | Authorization Code    | AISP | Current balance context (e.g. InterimAvailable) for the in-scope account (OBReadBalance1)         |
| GET /obie/open-banking/v4.0/aisp/accounts/{AccountId}/transactions | GET | Authorization Code | AISP | Transaction list for the period window; all cash-flow + categorisation derived client-side         |

All three endpoints require an authorised account-access consent (Status AUTH) with appropriate permissions (`ReadAccounts`, `ReadBalances`, `ReadTransactionsDetail`) and a scoped authorization-code token.

---

## Design Tokens

| Token                                | Value           | Usage                                                                          |
|--------------------------------------|-----------------|--------------------------------------------------------------------------------|
| colors.light.primary                 | #4C662B         | `biz_net` positive value; account selector chip active state                  |
| colors.light.on_surface_variant      | #5C6057         | `biz_period_label`; category legend secondary text                             |
| colors.light.background              | #F9FAEF         | Screen root background                                                         |
| colors.light.surface_container_low   | M3 token        | `biz_cash_flow_card`, `biz_expense_donut_card`, `biz_merchants_card` fill      |
| typography.title_small               | Outfit 14sp/500 | Cash-flow values (Money In / Money Out / Net); section headings                |
| typography.body_medium               | Outfit 14sp/400 | `biz_period_label`                                                             |
| radius.lg                            | 16dp            | All card corner radii                                                          |
| spacing.md                           | 16dp            | Card internal padding                                                          |
| spacing.lg (horizontal)              | 20dp            | Card horizontal margin                                                         |
| motion.shimmer                       | short4 (200ms)  | Skeleton shimmer in loading state                                              |

---

_Generated by /idea export | 2026-06-14_
