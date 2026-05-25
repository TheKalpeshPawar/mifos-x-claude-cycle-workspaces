# Feature Specification — Products

| Field | Value |
|---|---|
| Feature | products |
| Name | Products |
| Flavor | consumer |
| Status | designed |
| Quality Score | 88 |
| Contract Version | 1.1.0 |

---

## Overview

The Products screen is the bank product catalogue for Mifos X Open Banking consumers. It presents four real OBP-backed products in scrollable cards organised by horizontally-scrollable category filter chips (All, Savings, Loans, Cards, Mortgages). Each card shows the product name, prominent rate badge, category label, a concise description, colour-coded feature badge chips, and two action buttons — "Details" (outlined) and "Apply Now" (filled) — both navigating to the `application-detail` screen. A promotional banner ("Refer a friend — earn £50", expires 30 June 2026) sits below the product list.

The screen handles four states: **loading** (4 skeleton cards), **populated** (full product list), **empty** (category filter has no matches), and **error** (network failure with retry). Navigation connects to home, accounts, and send-money via the bottom navigation bar, and to `application-detail` via product CTAs.

---

## Screens

| Screen ID | Name | Route | Archetype | Scroll |
|---|---|---|---|---|
| products | Products | /products | index_list | vertical |

---

## Shell

| Element | Config |
|---|---|
| Top app bar | Title "Products", back arrow (navigate_back to home), search action (search_products) |
| Bottom navigation | 5 items: Home (home), Accounts (accounts), Products (products, active), Send (send-money), More (more) |

---

## Components

| ID | Type | Description |
|---|---|---|
| products_title | text | "Products" — headline_large, #1800B1, bold, padding_horizontal 20, padding_top 16 |
| products_subtitle | text | "Explore accounts, savings, loans and cards tailored for you." — body_medium, #555555, padding_horizontal 20 |
| category_tabs_row | stack | Horizontally scrollable row of 5 category filter chips |
| tab_all | button | "All" — filled #1800B1 (active); action: filter_products |
| tab_savings | button | "Savings" — outlined #CCCCCC border, #666666 text; action: filter_products |
| tab_loans | button | "Loans" — outlined; action: filter_products |
| tab_cards | button | "Cards" — outlined; action: filter_products |
| tab_mortgages | button | "Mortgages" — outlined; action: filter_products |
| product_instant_access_savings | box | Card container for Instant Access Savings; corner_radius 16, elevation 2; on_click → application-detail |
| ias_name | text | "Instant Access Savings" — title_medium, #111111, semi-bold |
| ias_category_badge | box | "Savings" — #E8F5E9 bg, #2E7D32 text, label_small |
| ias_rate | text | "4.5% AER" — display_small, #1800B1, bold |
| ias_description | text | "Earn 4.5% AER on every pound you save. Withdraw at any time with no notice period or penalties." — body_medium, #555555 |
| ias_feat_aer | box | Feature badge "4.5% AER" — #E8F5E9 bg, #2E7D32 text |
| ias_feat_access | box | Feature badge "Instant access" — #E3F2FD bg, #1565C0 text |
| ias_feat_no_min | box | Feature badge "No minimum deposit" — #EDE7F6 bg, #4527A0 text |
| ias_learn_more | button | "Details" — outlined #1800B1; navigates to application-detail |
| ias_apply | button | "Apply Now" — filled #1800B1 white text; navigates to application-detail |
| product_fixed_rate_bond | box | Card container for Fixed Rate Bond 1yr; on_click → application-detail |
| frb_name | text | "Fixed Rate Bond 1yr" — title_medium, #111111, semi-bold |
| frb_category_badge | box | "Savings" — #E8F5E9 bg, #2E7D32 text |
| frb_rate | text | "5.1% AER" — display_small, #1800B1, bold |
| frb_description | text | "Lock in a market-leading 5.1% AER for 12 months. Minimum deposit £1,000. Interest paid at maturity." — body_medium, #555555 |
| frb_feat_aer | box | Feature badge "5.1% AER" — #E8F5E9 bg, #2E7D32 text |
| frb_feat_term | box | Feature badge "12-month term" — #FFF3E0 bg, #E65100 text |
| frb_feat_fscs | box | Feature badge "FSCS protected" — #EDE7F6 bg, #4527A0 text |
| frb_learn_more | button | "Details" — outlined #1800B1; navigates to application-detail |
| frb_apply | button | "Apply Now" — filled #1800B1; navigates to application-detail |
| product_personal_loan | box | Card container for Personal Loan; on_click → application-detail |
| personal_loan_name | text | "Personal Loan" — title_medium, #111111, semi-bold |
| pl_category_badge | box | "Loans" — #FFF3E0 bg, #E65100 text |
| pl_rate | text | "From 6.9% APR" — display_small, #1800B1, bold |
| personal_loan_description | text | "Borrow from £1,000 to £25,000 at a representative 6.9% APR. Flexible repayment terms from 1 to 7 years." — body_medium, #555555 |
| personal_loan_feat_apr | box | Feature badge "From 6.9% APR" — #FFF3E0 bg, #E65100 text |
| personal_loan_feat_amount | box | Feature badge "Up to £25,000" — #EDE7F6 bg, #4527A0 text |
| personal_loan_feat_terms | box | Feature badge "1–7 year terms" — #E3F2FD bg, #1565C0 text |
| personal_loan_learn_more | button | "Details" — outlined #1800B1; navigates to application-detail |
| personal_loan_apply | button | "Apply Now" — filled #1800B1; navigates to application-detail |
| product_platinum_credit_card | box | Card container for Platinum Credit Card; on_click → application-detail |
| pcc_name | text | "Platinum Credit Card" — title_medium, #111111, semi-bold |
| pcc_category_badge | box | "Cards" — #E3F2FD bg, #1565C0 text |
| pcc_rate | text | "0% for 20 months" — display_small, #1800B1, bold |
| pcc_description | text | "0% interest on purchases for 20 months. No annual fee. Contactless and Apple Pay / Google Pay enabled." — body_medium, #555555 |
| pcc_feat_zero_pct | box | Feature badge "0% for 20 months" — #E3F2FD bg, #1565C0 text |
| pcc_feat_no_annual_fee | box | Feature badge "No annual fee" — #E8F5E9 bg, #2E7D32 text |
| pcc_feat_contactless | box | Feature badge "Contactless & Apple/Google Pay" — #EDE7F6 bg, #4527A0 text |
| pcc_learn_more | button | "Details" — outlined #1800B1; navigates to application-detail |
| pcc_apply | button | "Apply Now" — filled #1800B1; navigates to application-detail |
| promotions_banner | box | Promotional banner — #1800B1 bg, corner_radius 12; on_click → home |
| promo_banner_text | text | "Refer a friend — earn £50" — title_small, #FFFFFF, semi-bold |
| promo_banner_detail | text | "When your friend opens any account before 30 June 2026" — body_small, #C5C0FF |

---

## States

| ID | Trigger | Description |
|---|---|---|
| loading | Screen enters; OBP API call in flight | Title, subtitle, and category tabs shown; skeleton list of 4 cards |
| populated | API returns product list | Full product cards: Instant Access Savings, Fixed Rate Bond 1yr, Personal Loan, Platinum Credit Card; promotional banner below |
| empty | Category filter returns no matching products | Title, subtitle, and tabs shown; empty-state with store_outlined icon, title "No products available", message inviting filter change |
| error | Network or OBP API failure | Title, subtitle, and tabs shown; error state with cloud_off icon, title "Unable to load products", message with offline hint, Retry button |

---

## State Model

**ViewModel:** `ProductsViewModel`

### State Fields

| Name | Type | Default |
|---|---|---|
| products | List\<BankProduct\> | emptyList() |
| selectedCategory | ProductCategory | ProductCategory.ALL |
| uiState | ProductsUiState | Loading |
| error | UiError? | null |

### Events

`ProductsLoaded(products: List<BankProduct>)`, `CategoryFilterChanged(category: ProductCategory)`, `ApplyNowClicked(productCode: String)`, `ProductDetailClicked(productCode: String)`, `RetryLoad`, `SearchOpened`

### Actions

`filter_products`, `search_products`, `navigate_to_application_detail`

### DI Dependencies

`ProductRepository`, `BankRepository`

### Error Codes

| Field | Code | Message |
|---|---|---|
| global | LOAD_FAILED | Unable to load products. Please try again. |
| global | NETWORK_TIMEOUT | Connection timed out. Check your internet connection. |

---

## Navigation

| From | To | Trigger | Type |
|---|---|---|---|
| ias_learn_more / ias_apply | application-detail | Tap | push |
| frb_learn_more / frb_apply | application-detail | Tap | push |
| personal_loan_learn_more / personal_loan_apply | application-detail | Tap | push |
| pcc_learn_more / pcc_apply | application-detail | Tap | push |
| product card body (any) | application-detail | Tap card | push |
| promotions_banner | home | Tap banner | push |
| bottom nav — Home | home | Tap | replace |
| bottom nav — Accounts | accounts | Tap | replace |
| bottom nav — Send | send-money | Tap | replace |
| top app bar back arrow | home | Tap | pop |

---

## Products Catalogue

| Product | Category | Rate / Offer | Key Features |
|---|---|---|---|
| Instant Access Savings | Savings | 4.5% AER | Instant access, No minimum deposit |
| Fixed Rate Bond 1yr | Savings | 5.1% AER | 12-month term, FSCS protected |
| Personal Loan | Loans | From 6.9% APR | Up to £25,000, 1–7 year terms |
| Platinum Credit Card | Cards | 0% for 20 months | No annual fee, Contactless & Apple/Google Pay |

---

## Promotional Banner

| Field | Value |
|---|---|
| Headline | Refer a friend — earn £50 |
| Detail | When your friend opens any account before 30 June 2026 |
| Background | #1800B1 |
| CTA | Navigates to home (referral flow) |
| Expiry | 30 June 2026 |

---

## Design Tokens

| Token | Value | Usage |
|---|---|---|
| primary | #1800B1 | Title, active tab, Apply Now buttons, Details borders, promo banner bg |
| on_primary | #FFFFFF | Apply Now text, active tab text |
| surface | #FFFFFF | Product card background |
| background | #FCF8FF | Screen background |
| error | #BA1A1A | Error state |
| green_badge | #E8F5E9 / #2E7D32 | Savings category, AER rate badges |
| blue_badge | #E3F2FD / #1565C0 | Cards category, instant access, contactless badges |
| orange_badge | #FFF3E0 / #E65100 | Loans category, APR, term badges |
| purple_badge | #EDE7F6 / #4527A0 | FSCS protected, amount, no-minimum badges |
| promo_accent | #C5C0FF | Promo banner secondary text |

---

*Generated by /idea export | 2026-05-25*
