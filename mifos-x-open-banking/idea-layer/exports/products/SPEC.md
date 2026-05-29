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

The Products screen is a vertically-scrollable catalog that lets Consumer persona users browse, filter, and apply for banking products offered via Open Bank Project v5.0.0. A horizontal filter chip row at the top (All / Savings / Loans / Cards / Mortgages) lets users scope the list by category. Below it, four real OBP product cards are displayed:

1. **Instant Access Savings** — 4.5% AER, withdraw anytime, no minimum deposit, no notice period.
2. **Fixed Rate Bond 1yr** — 5.1% AER, 12-month lock-in, minimum £1,000 deposit, FSCS protected.
3. **Personal Loan** — from 6.9% APR, borrow £1,000–£25,000, flexible 1–7 year repayment terms.
4. **Platinum Credit Card** — 0% interest for 20 months on purchases, no annual fee, contactless + Apple Pay / Google Pay.

Each product card displays the headline rate in Display Small (`#4C662B`), a category badge, a description, horizontally-scrollable feature chips, and two action buttons — "Details" (outlined) and "Apply Now" (filled) — both navigating to `application-detail`. A promotional refer-a-friend banner (`#4C662B` fill) closes the list, offering £50 cashback when a friend opens any account before 30 June 2026. The screen supports four UI states: loading (4 skeleton cards), populated (all products + promo), empty (no matches for selected category), and error (network failure with retry).

---

## Screens

| ID       | Name     | Route     | Layout | Scroll   |
|----------|----------|-----------|--------|----------|
| products | Products | /products | Column | Vertical |

**Shell:** Top app bar (title "Products", back arrow → `navigate_back`, search action → `search_products`) + 5-tab bottom navigation bar (Products active).

| Nav Item | ID           | Icon            | Target     | Active |
|----------|--------------|-----------------|------------|--------|
| Home     | nav_home     | home            | home       | false  |
| Accounts | nav_accounts | account_balance | accounts   | false  |
| Products | nav_products | store           | products   | true   |
| Send     | nav_send     | send            | send-money | false  |
| More     | nav_more     | more_horiz      | settings   | false  |

---

## Components

| ID                             | Type   | Description                                                                                                              |
|--------------------------------|--------|--------------------------------------------------------------------------------------------------------------------------|
| products_title                 | text   | "Products" — Outfit/headline_large, #4C662B, bold; 16dp horizontal + top padding                                        |
| products_subtitle              | text   | "Explore accounts, savings, loans and cards tailored for you." — Outfit/body_medium, #44483D; 16dp horizontal padding    |
| category_tabs_row              | stack  | Horizontal scroll row of 5 filter buttons; role=tablist; fires `filter_products` action                                  |
| tab_all                        | button | "All" — filled variant, bg #4C662B, text #FFFFFF, border_radius 20, label_medium; selected=true                         |
| tab_savings                    | button | "Savings" — outlined variant, border #E1E4D5, text #44483D, border_radius 20, label_medium                               |
| tab_loans                      | button | "Loans" — outlined variant, border #E1E4D5, text #44483D, border_radius 20, label_medium                                 |
| tab_cards                      | button | "Cards" — outlined variant, border #E1E4D5, text #44483D, border_radius 20, label_medium                                 |
| tab_mortgages                  | button | "Mortgages" — outlined variant, border #E1E4D5, text #44483D, border_radius 20, label_medium                             |
| product_instant_access_savings | box    | White card (radius 16, elevation 2, border #F9FAEF 1dp, margin_h 20, margin_b 12); navigates to application-detail      |
| ias_name                       | text   | "Instant Access Savings" — Outfit/title_medium, #1A1C16, semibold                                                       |
| ias_category_badge             | box    | "Savings" — bg #CDEDA3, radius 6, text #4C662B, label_small; fires filter_products(savings)                             |
| ias_rate                       | text   | "4.5% AER" — Outfit/display_small (32sp/600), #4C662B, bold                                                             |
| ias_description                | text   | "Earn 4.5% AER on every pound you save. Withdraw at any time with no notice period or penalties." — body_medium, #44483D |
| ias_feat_aer                   | box    | Feature chip "4.5% AER" — bg #CDEDA3, radius 8, text #4C662B, label_small                                               |
| ias_feat_access                | box    | Feature chip "Instant access" — bg #DCE7C8, radius 8, text #386663, label_small                                         |
| ias_feat_no_min                | box    | Feature chip "No minimum deposit" — bg #CDEDA3, radius 8, text #4C662B, label_small                                      |
| ias_learn_more                 | button | "Details" — outlined, border+text #4C662B, radius 8, label_medium; navigates to application-detail                      |
| ias_apply                      | button | "Apply Now" — filled, bg #4C662B, text #FFFFFF, radius 8, label_medium; navigates to application-detail                 |
| product_fixed_rate_bond        | box    | White card (radius 16, elevation 2, border #F9FAEF 1dp, margin_h 20, margin_b 12); navigates to application-detail      |
| frb_name                       | text   | "Fixed Rate Bond 1yr" — Outfit/title_medium, #1A1C16, semibold                                                          |
| frb_category_badge             | box    | "Savings" — bg #CDEDA3, radius 6, text #4C662B, label_small; fires filter_products(savings)                             |
| frb_rate                       | text   | "5.1% AER" — Outfit/display_small (32sp/600), #4C662B, bold                                                             |
| frb_description                | text   | "Lock in a market-leading 5.1% AER for 12 months. Minimum deposit £1,000. Interest paid at maturity." — body_medium, #44483D |
| frb_feat_aer                   | box    | Feature chip "5.1% AER" — bg #CDEDA3, radius 8, text #4C662B, label_small                                               |
| frb_feat_term                  | box    | Feature chip "12-month term" — bg #CDEDA3, radius 8, text #44483D, label_small (A11Y fix: was #E8A317 ≤2.17:1 FAIL → #44483D ≥7.25:1 PASS) |
| frb_feat_fscs                  | box    | Feature chip "FSCS protected" — bg #CDEDA3, radius 8, text #4C662B, label_small                                         |
| frb_learn_more                 | button | "Details" — outlined, border+text #4C662B, radius 8, label_medium; navigates to application-detail                      |
| frb_apply                      | button | "Apply Now" — filled, bg #4C662B, text #FFFFFF, radius 8, label_medium; navigates to application-detail                 |
| product_personal_loan          | box    | White card (radius 16, elevation 2, border #F9FAEF 1dp, margin_h 20, margin_b 12); navigates to application-detail      |
| personal_loan_name             | text   | "Personal Loan" — Outfit/title_medium, #1A1C16, semibold                                                                |
| pl_category_badge              | box    | "Loans" — bg #CDEDA3, radius 6, text #44483D, label_small (A11Y fix: was #E8A317 FAIL → #44483D PASS); fires filter_products(loans) |
| pl_rate                        | text   | "From 6.9% APR" — Outfit/display_small (32sp/600), #4C662B, bold                                                        |
| personal_loan_description      | text   | "Borrow from £1,000 to £25,000 at a representative 6.9% APR. Flexible repayment terms from 1 to 7 years." — body_medium, #44483D |
| personal_loan_feat_apr         | box    | Feature chip "From 6.9% APR" — bg #CDEDA3, radius 8, text #44483D, label_small (A11Y fix)                               |
| personal_loan_feat_amount      | box    | Feature chip "Up to £25,000" — bg #CDEDA3, radius 8, text #4C662B, label_small                                          |
| personal_loan_feat_terms       | box    | Feature chip "1–7 year terms" — bg #DCE7C8, radius 8, text #386663, label_small                                         |
| personal_loan_learn_more       | button | "Details" — outlined, border+text #4C662B, radius 8, label_medium; navigates to application-detail                      |
| personal_loan_apply            | button | "Apply Now" — filled, bg #4C662B, text #FFFFFF, radius 8, label_medium; navigates to application-detail                 |
| product_platinum_credit_card   | box    | White card (radius 16, elevation 2, border #F9FAEF 1dp, margin_h 20, margin_b 12); navigates to application-detail      |
| pcc_name                       | text   | "Platinum Credit Card" — Outfit/title_medium, #1A1C16, semibold                                                         |
| pcc_category_badge             | box    | "Cards" — bg #DCE7C8, radius 6, text #386663, label_small; fires filter_products(cards)                                 |
| pcc_rate                       | text   | "0% for 20 months" — Outfit/display_small (32sp/600), #4C662B, bold                                                     |
| pcc_description                | text   | "0% interest on purchases for 20 months. No annual fee. Contactless and Apple Pay / Google Pay enabled." — body_medium, #44483D |
| pcc_feat_zero_pct              | box    | Feature chip "0% for 20 months" — bg #DCE7C8, radius 8, text #386663, label_small                                       |
| pcc_feat_no_annual_fee         | box    | Feature chip "No annual fee" — bg #CDEDA3, radius 8, text #4C662B, label_small                                          |
| pcc_feat_contactless           | box    | Feature chip "Contactless & Apple/Google Pay" — bg #CDEDA3, radius 8, text #4C662B, label_small                         |
| pcc_learn_more                 | button | "Details" — outlined, border+text #4C662B, radius 8, label_medium; navigates to application-detail                      |
| pcc_apply                      | button | "Apply Now" — filled, bg #4C662B, text #FFFFFF, radius 8, label_medium; navigates to application-detail                 |
| promotions_banner              | box    | #4C662B fill, radius 12, pad_h 16, pad_v 14, margin_h 20, margin_b 16; navigates to home                               |
| promo_banner_text              | text   | "Refer a friend — earn £50" — Outfit/title_small, #FFFFFF, semibold                                                     |
| promo_banner_detail            | text   | "When your friend opens any account before 30 June 2026" — Outfit/body_small, #CDEDA3                                   |

---

## States

| ID        | Trigger                                | Description                                                                          |
|-----------|----------------------------------------|--------------------------------------------------------------------------------------|
| loading   | Screen entry / `RetryLoad` event       | Title + subtitle + 5 category tabs visible; 4 skeleton product cards shimmer         |
| populated | OBP products load success              | All 4 product cards (IAS, FRB, PL, PCC) + promotions banner visible                 |
| empty     | Category filter returns no results     | Title + subtitle + tabs + empty state (store_outlined icon, "No products available") |
| error     | Network / API failure                  | Title + subtitle + tabs + error state (cloud_off icon, "Unable to load products", Retry button) |

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

**Events:** `ProductsLoaded(products: List<BankProduct>)`, `CategoryFilterChanged(category: ProductCategory)`, `ApplyNowClicked(productCode: String)`, `ProductDetailClicked(productCode: String)`, `RetryLoad`, `SearchOpened`

**Actions:** `filter_products`, `search_products`, `navigate_to_application_detail`

**DI Dependencies:** `ProductRepository`, `BankRepository`

**Errors:**
- `LOAD_FAILED`: "Unable to load products. Please try again."
- `NETWORK_TIMEOUT`: "Connection timed out. Check your internet connection."

---

## Navigation

| From     | To                 | Trigger                                        | Type  |
|----------|--------------------|------------------------------------------------|-------|
| products | application-detail | "Apply Now" button tap (any product card)      | push  |
| products | application-detail | "Details" button tap (any product card)        | push  |
| products | home               | nav_home tab tap                               | tab   |
| products | home               | Promotions banner tap                          | push  |
| products | home               | Top bar back arrow (`navigate_back`)           | pop   |
| products | accounts           | nav_accounts tab tap                           | tab   |
| products | send-money         | nav_send tab tap                               | tab   |
| products | settings           | nav_more tab tap                               | tab   |
| products | products           | Category tab tap (filter in-place)             | —     |
| products | —                  | Search icon tap (overlay opens)                | sheet |

---

## API Endpoints

| Endpoint                                        | Auth        | Tag     | Purpose                                   |
|-------------------------------------------------|-------------|---------|-------------------------------------------|
| GET /obp/v5.0.0/banks/{bankId}/products         | DirectLogin | Product | List available banking products from OBP  |

---

## Design Tokens

| Token                              | Value   | Usage                                                                    |
|------------------------------------|---------|--------------------------------------------------------------------------|
| colors.light.primary               | #4C662B | Page title, headline rates, "All" tab fill, "Apply Now" button bg, promo banner fill |
| colors.light.on_primary            | #FFFFFF | "All" tab text, "Apply Now" button text, promo banner title text          |
| colors.light.primary_container     | #CDEDA3 | Savings/Loans category badge bg, feature chips (IAS AER, IAS no-min, FRB AER/FSCS, PL amount, PCC no-fee, PCC contactless) |
| colors.light.on_primary_container  | #102000 | (dark-on-container reference — not rendered on this screen)               |
| colors.light.secondary             | #386663 | "Instant access" chip text, "1–7 year terms" chip text, Cards badge text  |
| colors.light.nav_active_indicator  | #DCE7C8 | Cards category badge bg, "Instant access" chip bg, "0% for 20 months" chip bg, "1–7 year terms" chip bg |
| colors.light.surface               | #FFFFFF | Product card backgrounds                                                  |
| colors.light.on_surface            | #1A1C16 | Product names (title_medium)                                              |
| colors.light.on_surface_variant    | #44483D | Subtitle, product descriptions, inactive filter tab text; A11Y-fixed chip text (FRB term, Loans badge, PL APR chip) |
| colors.light.surface_variant       | #E1E4D5 | Inactive filter tab border                                                |
| colors.light.background            | #F9FAEF | Screen background; product card border tint (#F9FAEF at 1dp)              |
| colors.light.secondary_container   | #BCEBE7 | (referenced — not directly rendered on this screen)                       |
| typography.headline_large          | Outfit 32sp/400 | Page title "Products"                                              |
| typography.display_small           | Outfit 32sp/600 | Headline rates (4.5% AER, 5.1% AER, From 6.9% APR, 0% for 20 months) |
| typography.title_medium            | Outfit 16sp/500 | Product names                                                      |
| typography.title_small             | Outfit 14sp/500 | Promotions banner heading                                          |
| typography.body_medium             | Outfit 14sp/400 | Subtitle, product descriptions                                     |
| typography.body_small              | Outfit 12sp/400 | Promotions banner detail text                                      |
| typography.label_medium            | Outfit 12sp/500 | Filter tab labels, action button labels                            |
| typography.label_small             | Outfit 11sp/500 | Category badges, feature chips                                     |
| radius.lg                          | 16dp    | Product cards                                                            |
| radius.md                          | 12dp    | Promotions banner                                                        |
| radius.sm                          | 8dp     | Feature chips, action buttons (Details / Apply Now)                      |
| radius.pill (≈20dp)                | 20dp    | Category filter tab buttons                                              |
| radius.xs                          | 6dp     | Category badge inside product card                                       |
| elevation.level2                   | 3dp     | Product cards (source declares elevation: 2 = level2)                    |
| spacing.md                         | 16dp    | Horizontal padding, content gaps                                         |
| spacing.sm                         | 8dp     | Tab row spacing, feature chip spacing                                    |
| spacing.xs                         | 4dp     | Promo banner subtitle top padding                                        |
| motion.duration.short4             | 200ms   | Skeleton shimmer duration (loading state)                                |

---

_Generated by /idea export | 2026-05-30_
