# Feature Specification — Products

| Field | Value |
|---|---|
| Feature | products |
| Name | Products |
| Flavor | consumer |
| Status | enriched |
| Quality Score | 78 |

---

## Overview

The Products screen presents the Mifos product catalogue to consumers in a browseable list organised by category. Horizontally scrollable filter tabs (All, Current, Savings, Loans, Cards) allow quick category switching. Each product card displays the product name, a concise description, colour-coded feature badges, and two actions: "Learn More" to expand inline detail and "Apply" to navigate to the account application form. Three products are shown in the enriched state: Current Plus Account (no monthly fee, free UK transfers), Flex Saver (4.5% AER, instant access), and Personal Loan (from 6.9% APR, up to £25,000). The screen uses a top app bar with back navigation and a search shortcut, and connects to the main bottom navigation.

---

## Screens

| Screen ID | Name | Route | Archetype | Scroll |
|---|---|---|---|---|
| products | Products | /products | index_list | vertical |

---

## Components

| ID | Type | Description |
|---|---|---|
| products_title | text | Page heading "Products" headline_large, #1800B1, bold |
| category_tabs_row | stack | Horizontally scrollable tab bar with 5 category buttons |
| tab_all | button | "All" — filled #1800B1 (active default) |
| tab_current | button | "Current" — outlined, unselected |
| tab_savings | button | "Savings" — outlined, unselected |
| tab_loans | button | "Loans" — outlined, unselected |
| tab_cards | button | "Cards" — outlined, unselected |
| product_current_plus | box | Card for Current Plus Account |
| current_plus_name | text | "Current Plus Account" title_medium, semi-bold |
| current_plus_description | text | "A flexible everyday current account with no monthly fee and free transfers across the UK." |
| current_plus_feat_no_fee | box | Feature badge "No monthly fee" — purple-tinted (#EDE7F6 bg, #4527A0 text) |
| current_plus_feat_transfers | box | Feature badge "Free UK transfers" — green-tinted (#E8F5E9 bg, #2E7D32 text) |
| current_plus_learn_more | button | "Learn More" outlined #1800B1 |
| current_plus_apply | button | "Apply" filled #1800B1; navigates to account-applications |
| product_savings_flex | box | Card for Flex Saver |
| savings_flex_name | text | "Flex Saver" title_medium, semi-bold |
| savings_flex_description | text | "Earn 4.5% AER on your savings with instant access. No minimum deposit required." |
| savings_flex_feat_aer | box | Feature badge "4.5% AER" — green-tinted |
| savings_flex_feat_access | box | Feature badge "Instant access" — blue-tinted (#E3F2FD bg, #1565C0 text) |
| savings_flex_learn_more | button | "Learn More" outlined #1800B1 |
| savings_flex_apply | button | "Apply" filled #1800B1 |
| product_personal_loan | box | Card for Personal Loan |
| personal_loan_name | text | "Personal Loan" title_medium, semi-bold |
| personal_loan_description | text | "Borrow from £1,000 to £25,000 at a representative 6.9% APR over 1–7 years." |
| personal_loan_feat_apr | box | Feature badge "From 6.9% APR" — orange-tinted (#FFF3E0 bg, #E65100 text) |
| personal_loan_feat_amount | box | Feature badge "Up to £25,000" — purple-tinted |
| personal_loan_learn_more | button | "Learn More" outlined #1800B1 |
| personal_loan_apply | button | "Apply" filled #1800B1 |

---

## States

| ID | Trigger | Description |
|---|---|---|
| loading | Screen enters; API call in flight | Title and category tabs shown; skeleton list of 3 cards |
| content | API returns product list | Full product cards rendered |
| empty | Filter returns no products | Title and tabs; empty state with store_outlined icon and message |
| error | Network or API failure | Title and tabs; error state with cloud_off icon and retry button |

---

## State Model

**ViewModel:** `ProductsViewModel`

### State Fields

| Name | Type | Default |
|---|---|---|
| products | List\<BankProduct\> | emptyList() |
| selectedCategory | ProductCategory | ProductCategory.ALL |
| expandedProductCode | String? | null |
| uiState | ProductsUiState | Loading |
| error | UiError? | null |

### Events
`ProductsLoaded`, `CategoryFilterChanged(category: ProductCategory)`, `ProductDetailExpanded(productCode: String)`, `ApplyClicked(productCode: String)`, `LearnMoreClicked(productCode: String)`, `RetryLoad`

### Actions
`filter_products`, `expand_product_detail`, `search_products`, `navigate_to_applications`

### DI Dependencies
`ProductRepository`, `BankRepository`

---

## Navigation

| From | To | Trigger | Type |
|---|---|---|---|
| current_plus_apply | account-applications | Apply button tap | push |
| savings_flex_apply | account-applications | Apply button tap | push |
| personal_loan_apply | account-applications | Apply button tap | push |
| top_app_bar back | home | navigation_icon tap | pop |

---

## API Endpoints

| Endpoint | Auth | Purpose |
|---|---|---|
| GET /obp/v3.1.0/banks/{bankId}/products | DirectLogin | Fetch all bank products for catalogue display |

---

## Design Tokens

| Token | Value | Usage |
|---|---|---|
| primary | #1800B1 | Title, active tab, apply buttons, learn-more border |
| on_primary | #FFFFFF | Apply button text, active tab text |
| surface | #FFFFFF | Product cards |
| background | #FCF8FF | Screen background |
| error | #BA1A1A | Error state |
| purple_badge | #EDE7F6 / #4527A0 | No monthly fee, Up to £25,000 badges |
| green_badge | #E8F5E9 / #2E7D32 | Free transfers, 4.5% AER badges |
| blue_badge | #E3F2FD / #1565C0 | Instant access badge |
| orange_badge | #FFF3E0 / #E65100 | From 6.9% APR badge |

---

*Generated by /idea export | 2026-05-25*
