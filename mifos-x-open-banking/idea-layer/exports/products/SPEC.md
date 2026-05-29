# SPEC — Products

| Field         | Value              |
|---------------|--------------------|
| Feature       | products           |
| Flavor        | consumer           |
| Status        | approved           |
| Quality Score | 95                 |
| ViewModel     | ProductsViewModel  |

---

## Overview

The Products screen is a scrollable catalog that lets Consumer persona users browse, filter, and apply for banking products offered via Open Bank Project v5.0.0. It displays four real OBP products grouped by category with a horizontally-scrollable filter chip row (All / Savings / Loans / Cards / Mortgages) and a promotional refer-a-friend banner at the bottom.

Products listed: Instant Access Savings (4.5% AER — withdraw anytime, no minimum deposit), Fixed Rate Bond 1yr (5.1% AER — 12-month lock-in, min £1,000, FSCS protected), Personal Loan (from 6.9% APR — £1,000–£25,000, 1–7 year terms), Platinum Credit Card (0% for 20 months — no annual fee, contactless + Apple/Google Pay). Each card shows the headline rate in Display Small and has "Details" (outlined) and "Apply Now" (filled) action buttons navigating to application-detail.

---

## Screens

| ID       | Name     | Route     | Layout | Scroll   |
|----------|----------|-----------|--------|----------|
| products | Products | /products | Column | Vertical |

**Shell:** Top app bar ("Products", back arrow, search action) + Bottom navigation bar with 5 items (Products active)

| Nav Item | ID           | Icon            | Target      |
|----------|--------------|-----------------|-------------|
| Home     | nav_home     | home            | home        |
| Accounts | nav_accounts | account_balance | accounts    |
| Products | nav_products | store           | products    |
| Send     | nav_send     | send            | send-money  |
| More     | nav_more     | more_horiz      | settings    |

---

## Components

| ID                          | Type    | Description                                                                                     |
|-----------------------------|---------|-------------------------------------------------------------------------------------------------|
| products_title              | text    | "Products" — Outfit/headline_large, #4C662B, bold                                             |
| products_subtitle           | text    | "Explore accounts, savings, loans and cards tailored for you." — Outfit/body_medium, #44483D   |
| category_tabs_row           | stack   | Horizontal scroll row of 5 filter buttons; fires filter_products                               |
| tab_all                     | button  | "All" — filled, bg #4C662B, text #FFFFFF, radius 20; currently selected                       |
| tab_savings                 | button  | "Savings" — outlined, border #E1E4D5, text #44483D, radius 20                                 |
| tab_loans                   | button  | "Loans" — outlined, border #E1E4D5, text #44483D, radius 20                                   |
| tab_cards                   | button  | "Cards" — outlined, border #E1E4D5, text #44483D, radius 20                                   |
| tab_mortgages               | button  | "Mortgages" — outlined, border #E1E4D5, text #44483D, radius 20                               |
| product_instant_access_savings | box  | White card (radius 16, elevation 2) — Instant Access Savings product card                     |
| ias_name                    | text    | "Instant Access Savings" — Outfit/title_medium, #1A1C16, semibold                              |
| ias_category_badge          | box     | "Savings" — bg #CDEDA3, radius 6, text #4C662B, Outfit/label_small                            |
| ias_rate                    | text    | "4.5% AER" — Outfit/display_small, #4C662B, bold                                              |
| ias_description             | text    | "Earn 4.5% AER on every pound you save. Withdraw at any time with no notice period or penalties." — body_medium, #44483D |
| ias_feat_aer                | box     | Feature chip "4.5% AER" — bg #CDEDA3, radius 8, text #4C662B                                  |
| ias_feat_access             | box     | Feature chip "Instant access" — bg #DCE7C8, radius 8, text #386663                            |
| ias_feat_no_min             | box     | Feature chip "No minimum deposit" — bg #CDEDA3, radius 8, text #4C662B                        |
| ias_learn_more              | button  | "Details" — outlined, border+text #4C662B, radius 8; navigates to application-detail          |
| ias_apply                   | button  | "Apply Now" — filled, bg #4C662B, text #FFFFFF, radius 8; navigates to application-detail     |
| product_fixed_rate_bond     | box     | White card (radius 16, elevation 2) — Fixed Rate Bond 1yr product card                        |
| frb_name                    | text    | "Fixed Rate Bond 1yr" — Outfit/title_medium, #1A1C16, semibold                                |
| frb_category_badge          | box     | "Savings" — bg #CDEDA3, radius 6, text #4C662B                                                |
| frb_rate                    | text    | "5.1% AER" — Outfit/display_small, #4C662B, bold                                              |
| frb_description             | text    | "Lock in a market-leading 5.1% AER for 12 months. Minimum deposit £1,000. Interest paid at maturity." — body_medium, #44483D |
| frb_feat_aer                | box     | Feature chip "5.1% AER" — bg #CDEDA3, text #4C662B                                            |
| frb_feat_term               | box     | Feature chip "12-month term" — bg #CDEDA3, text #44483D                                       |
| frb_feat_fscs               | box     | Feature chip "FSCS protected" — bg #CDEDA3, text #4C662B                                      |
| frb_learn_more              | button  | "Details" — outlined, #4C662B                                                                  |
| frb_apply                   | button  | "Apply Now" — filled, #4C662B                                                                  |
| product_personal_loan       | box     | White card (radius 16, elevation 2) — Personal Loan product card                              |
| personal_loan_name          | text    | "Personal Loan" — Outfit/title_medium, #1A1C16, semibold                                      |
| pl_category_badge           | box     | "Loans" — bg #CDEDA3, radius 6, text #44483D                                                  |
| pl_rate                     | text    | "From 6.9% APR" — Outfit/display_small, #4C662B, bold                                         |
| personal_loan_description   | text    | "Borrow from £1,000 to £25,000 at a representative 6.9% APR. Flexible 1 to 7 year terms." — body_medium, #44483D |
| personal_loan_feat_apr      | box     | Feature chip "From 6.9% APR" — bg #CDEDA3, text #44483D                                       |
| personal_loan_feat_amount   | box     | Feature chip "Up to £25,000" — bg #CDEDA3, text #4C662B                                       |
| personal_loan_feat_terms    | box     | Feature chip "1–7 year terms" — bg #DCE7C8, text #386663                                      |
| personal_loan_learn_more    | button  | "Details" — outlined, #4C662B                                                                  |
| personal_loan_apply         | button  | "Apply Now" — filled, #4C662B                                                                  |
| product_platinum_credit_card| box     | White card (radius 16, elevation 2) — Platinum Credit Card product card                       |
| pcc_name                    | text    | "Platinum Credit Card" — Outfit/title_medium, #1A1C16, semibold                               |
| pcc_category_badge          | box     | "Cards" — bg #DCE7C8, radius 6, text #386663                                                  |
| pcc_rate                    | text    | "0% for 20 months" — Outfit/display_small, #4C662B, bold                                      |
| pcc_description             | text    | "0% interest on purchases for 20 months. No annual fee. Contactless and Apple Pay / Google Pay enabled." — body_medium, #44483D |
| pcc_feat_zero_pct           | box     | Feature chip "0% for 20 months" — bg #DCE7C8, text #386663                                    |
| pcc_feat_no_annual_fee      | box     | Feature chip "No annual fee" — bg #CDEDA3, text #4C662B                                       |
| pcc_feat_contactless        | box     | Feature chip "Contactless & Apple/Google Pay" — bg #CDEDA3, text #4C662B                      |
| pcc_learn_more              | button  | "Details" — outlined, #4C662B                                                                  |
| pcc_apply                   | button  | "Apply Now" — filled, #4C662B                                                                  |
| promotions_banner           | box     | #4C662B filled banner (radius 12) — referral promotion                                        |
| promo_banner_text           | text    | "Refer a friend — earn £50" — Outfit/title_small, #FFFFFF, semibold                           |
| promo_banner_detail         | text    | "When your friend opens any account before 30 June 2026" — Outfit/body_small, #CDEDA3         |

---

## States

| ID        | Trigger                               | Description                                                                    |
|-----------|---------------------------------------|--------------------------------------------------------------------------------|
| loading   | Screen entry / RetryLoad              | Title + subtitle + category tabs visible; 4 skeleton product cards shimmer     |
| populated | Products loaded from OBP v5.0.0       | All 4 product cards + promotions banner visible                                |
| empty     | Category filter returns no results    | Title + subtitle + tabs; empty state (store icon, "No products available")     |
| error     | Network / API failure                 | Title + subtitle + tabs; error state (cloud_off icon, Retry button)            |

---

## State Model

**ViewModel:** `ProductsViewModel`
**Screen State Type:** `ProductsUiState`

| Name             | Type                  | Default              |
|------------------|-----------------------|----------------------|
| products         | List\<BankProduct\>   | emptyList()          |
| selectedCategory | ProductCategory       | ProductCategory.ALL  |
| uiState          | ProductsUiState       | Loading              |
| error            | UiError?              | null                 |

**Events:** `ProductsLoaded(products)`, `CategoryFilterChanged(category)`, `ApplyNowClicked(productCode)`, `ProductDetailClicked(productCode)`, `RetryLoad`, `SearchOpened`

**DI Dependencies:** `ProductRepository`, `BankRepository`

**Errors:**
- `LOAD_FAILED`: "Unable to load products. Please try again."
- `NETWORK_TIMEOUT`: "Connection timed out. Check your internet connection."

---

## Navigation

| From     | To                 | Trigger                          | Type  |
|----------|--------------------|----------------------------------|-------|
| products | application-detail | "Apply Now" or "Details" tap     | push  |
| products | home               | nav_home tab tap / back arrow    | tab   |
| products | accounts           | nav_accounts tab tap             | tab   |
| products | send-money         | nav_send tab tap                 | tab   |
| products | settings           | nav_more tab tap                 | tab   |
| products | products           | category tab tap (filter in-place)| —   |
| products | —                  | search icon tap (overlay)        | sheet |

---

## API Endpoints

| Endpoint                                            | Auth        | Tag     | Purpose                                 |
|-----------------------------------------------------|-------------|---------|------------------------------------------|
| GET /obp/v5.0.0/banks/{bankId}/products             | DirectLogin | Product | List available banking products from OBP |

---

## Design Tokens

| Token                           | Value   | Usage                                                              |
|---------------------------------|---------|--------------------------------------------------------------------|
| colors.light.primary            | #4C662B | Page title, headline rates, filled buttons, active filter tab bg   |
| colors.light.primary_container  | #CDEDA3 | Feature chip bg (Savings/Loans), category badge bg (Savings)       |
| colors.light.secondary          | #386663 | Cards category badge text+bg (DCE7C8), loan terms chip text        |
| colors.light.secondary_container | #BCEBE7 | — (referenced for teal feature chips)                             |
| colors.light.nav_active_indicator | #DCE7C8 | Cards category badge bg, "0% for 20 months" chip bg              |
| colors.light.surface            | #FFFFFF | Product cards background                                           |
| colors.light.on_surface         | #1A1C16 | Product names                                                      |
| colors.light.on_surface_variant | #44483D | Subtitle, product descriptions, inactive filter tab text           |
| colors.light.surface_variant    | #E1E4D5 | Inactive filter tab border                                         |
| colors.light.background         | #F9FAEF | Screen background                                                  |
| colors.light.on_primary         | #FFFFFF | Active filter tab text, filled button text, promotions banner text |
| typography.headline_large       | —       | Page title                                                         |
| typography.display_small        | —       | Headline rates (4.5% AER, 5.1% AER, etc.)                        |
| typography.title_medium         | —       | Product names                                                      |
| typography.title_small          | —       | Promotions banner title                                            |
| typography.body_medium          | —       | Product descriptions, subtitle                                     |
| typography.body_small           | —       | Promotions banner detail text                                      |
| typography.label_medium         | —       | Filter tab labels                                                  |
| typography.label_small          | —       | Category badges, feature chips                                     |
| radius.lg                       | 16dp    | Product cards                                                      |
| radius.md                       | 12dp    | Promotions banner                                                  |
| radius.sm                       | 8dp     | Feature chips, action buttons                                      |
| radius.pill                     | 20dp    | Category filter tabs                                               |
| elevation.level2                | 3dp     | Product cards                                                      |

---

_Generated by /idea export | 2026-05-29_
