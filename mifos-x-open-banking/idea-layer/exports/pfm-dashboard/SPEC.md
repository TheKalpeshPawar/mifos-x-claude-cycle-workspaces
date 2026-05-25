# Feature Specification — Spending Insights (PFM Dashboard)

| Field | Value |
|---|---|
| Feature | pfm-dashboard |
| Name | Spending Insights |
| Flavor | consumer |
| Status | enriched |
| Quality Score | 78 |

---

## Overview

The Spending Insights dashboard provides consumers with a personal financial management (PFM) overview for the current reporting period (May 2026). A daily spending bar chart gives a visual summary of spending rhythm. Three summary metrics — Total Spent (£1,843.60), Total Received (£3,200.00), and Net (+£1,356.40) — are displayed side-by-side in a summary card. Below, budget progress bars for three categories (Groceries 78%, Transport 45%, Dining Out 97%) allow users to monitor their self-set budgets with colour-coded progress bars. A "Manage Budgets" button opens a budget management sheet. Budget data is persisted using OBP's personal data fields API, while transaction totals are derived from the transactions feed.

---

## Screens

| Screen ID | Name | Route | Archetype | Scroll |
|---|---|---|---|---|
| pfm-dashboard | Spending Insights | /pfm-dashboard | dashboard | vertical |

---

## Components

| ID | Type | Description |
|---|---|---|
| pfm_title | text | Page heading "Spending Insights" headline_large, #1800B1, bold |
| pfm_period_label | text | Reporting period "May 2026" body_medium, #888888 |
| monthly_chart_placeholder | box | 200dp tall chart card (#F8F4FF bg, radius 20, elevation 1) showing daily spending bar chart |
| chart_label | text | "Daily Spending — May" label_medium, #888888, centered |
| this_month_summary_card | box | Summary card (white, radius 20, elevation 2) with three side-by-side metrics |
| summary_section_label | text | "This Month" section heading title_medium, semi-bold |
| spent_amount | text | "£1,843.60" title_large, bold, #FF5252 (red — outgoing) |
| received_amount | text | "£3,200.00" title_large, bold, #4CAF50 (green — incoming) |
| net_amount | text | "+£1,356.40" title_large, bold, #1800B1 (primary — positive net) |
| budgets_section_label | text | "Budget Progress" section heading title_medium, semi-bold |
| budget_groceries | box | Groceries budget card — £312 / £400, 78% progress bar (#FF9800 orange fill) |
| budget_transport | box | Transport budget card — £68 / £150, 45% progress bar (#4CAF50 green fill) |
| budget_dining | box | Dining Out budget card — £195 / £200, 97% progress bar (#FF5252 red fill) |
| manage_budgets_button | button | "Manage Budgets" outlined #1800B1; opens budget management sheet |

---

## States

| ID | Trigger | Description |
|---|---|---|
| loading | Screen enters; API calls in flight | Title and period label visible; 4 skeleton cards shown |
| content | Data loaded from personal data fields and transactions | Full chart, summary metrics, and budget progress bars rendered |
| empty | No budgets exist; first-time user | Chart shown; empty state with "No budget data yet" and "Create First Budget" CTA |
| error | Network or API failure | Title and period label; error state with cloud_off icon and retry button |

---

## State Model

**ViewModel:** `PfmDashboardViewModel`

### State Fields

| Name | Type | Default |
|---|---|---|
| totalSpent | BigDecimal | BigDecimal.ZERO |
| totalReceived | BigDecimal | BigDecimal.ZERO |
| budgets | List\<BudgetEntry\> | emptyList() |
| dailySpending | List\<DailySpend\> | emptyList() |
| reportingPeriod | String | "" |
| uiState | PfmDashboardUiState | Loading |
| error | UiError? | null |

### Error Codes

| Field | Code | Message |
|---|---|---|
| global | LOAD_FAILED | Unable to load spending insights. Please try again. |
| budget_save | SAVE_FAILED | Could not save budget. Please try again. |

### Events
`DataLoaded`, `BudgetEditClicked(categoryId: String)`, `ManageBudgetsClicked`, `ChartDetailClicked`, `RetryLoad`

### Actions
`edit_budget`, `manage_budgets`, `open_chart_detail`, `open_pfm_settings`

### DI Dependencies
`PersonalDataFieldsRepository`, `TransactionsRepository`

---

## Navigation

| From | To | Trigger | Type |
|---|---|---|---|
| manage_budgets_button | (budget sheet) | Button tap | bottom sheet |
| monthly_chart_placeholder | (full-screen chart) | Chart tap | push/modal |
| top app bar back | home | navigation_icon tap | pop |

---

## API Endpoints

| Endpoint | Auth | Purpose |
|---|---|---|
| GET /obp/v6.0.0/my/personal-data-fields | DirectLogin | Read PFM budgets stored as pfm_budget_\<categoryId\> personal data fields |
| POST /obp/v6.0.0/my/personal-data-fields | DirectLogin | Create or update a budget entry for a category |

---

## Design Tokens

| Token | Value | Usage |
|---|---|---|
| primary | #1800B1 | Title, net amount, manage budgets button border |
| on_primary | #FFFFFF | Button text |
| surface | #FFFFFF | Summary card, budget cards |
| chart_background | #F8F4FF | Chart area background (soft lavender tint) |
| error | #FF5252 | Total spent amount, Dining Out budget bar (critical) |
| success | #4CAF50 | Total received amount, Transport budget bar (healthy) |
| warning | #FF9800 | Groceries budget bar (approaching) |
| on_surface_variant | #888888 | Period label, metric sub-labels |

---

*Generated by /idea export | 2026-05-25*
