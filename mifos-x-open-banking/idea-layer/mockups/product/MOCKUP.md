# Product Terms — Visual Mockup

> Auto-generated from `screens/product/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Source: OBReadProduct2 — GET /accounts/{AccountId}/product
> Generated: 2026-07-16T00:00:00Z

---

## Screen: Product Terms

Canvas: 393×852dp (Pixel 5) · Top app bar with back arrow · Bottom nav visible · No FAB · Roboto font · Material 3 light theme · bg #F7F9FF

Shell (from `app-shell.yaml` + `screens/product/ui.yaml#shell`):
- Top app bar: visible, small variant, title "Product Terms" (titleLarge #181C20), leading back arrow (48dp touch, #266489)
- Bottom navigation: Home | Accounts | Transactions | More — Accounts tab selected (product is nested under accounts flow)
- FAB: disabled (`fab_visible: false`)
- Initial state: `loading`

Bottom nav icon mapping (authoritative — `app-shell.yaml`):
- ⌂ Home (icon: home, tint #41474D when unselected)
- ◫ Accounts (icon: account_balance, tint #266489 — selected on this screen)
- ≡ Transactions (icon: receipt_long, tint #41474D)
- ⊕ More (icon: more_horiz, target: settings, tint #41474D)

---

### State: loading

_Initial state. Displayed while `productLoad(accountId)` issues GET /accounts/{AccountId}/product._

```
┌─────────────────────────────────────────────┐
│ ←  Product Terms                            │  ← top_app_bar bg #F7F9FF h 56dp
│                                              │    back arrow 24dp #266489, 48dp touch target
│                                              │    title titleLarge 22sp/28sp #181C20
│                                              │
│                                              │
│                                              │
│                    ◌                         │  ← progress_indicator circular #266489
│                                              │    strokeWidth 4dp, diameter 40dp
│                                              │    centered vertically in remaining space
│                                              │
│                                              │
│                                              │
│                                              │
│                                              │
│                                              │
│                                              │
│                                              │
├─────────────────────────────────────────────┤
│ ⌂ Home ◫ Accounts ≡ Transactions ⊕ More    │  ← bottom_nav bg #F7F9FF h 80dp
│                    ↑ selected #266489        │    unselected tint #41474D
└─────────────────────────────────────────────┘
```

### Component Hierarchy — loading

```
Screen: Product Terms (ProductUiState.Loading)
│
top_app_bar/ (small, bg #F7F9FF, elevation 0→2dp on scroll)
│   ├── leading: back_button (icon arrow_back 24dp #266489, 48dp×48dp touch, a11y "Go back")
│   │   on_click → NavigationController.navigateBack()
│   └── title "Product Terms" (titleLarge 22sp/28sp w400 #181C20)
│
loading_content/ (Box fill, contentAlignment=Center)
│   accessibility_label: "Loading product terms"
└── progress_indicator (CircularProgressIndicator, color #266489, strokeWidth 4dp, size 40dp)

BottomNav/ (persistent, always rendered)
├── tab Home         (icon: home,          label: "Home",         tint #41474D)
├── tab Accounts     (icon: account_balance,label: "Accounts",    tint #266489 — selected)
├── tab Transactions (icon: receipt_long,  label: "Transactions", tint #41474D)
└── tab More         (icon: more_horiz,    label: "More",         tint #41474D, target: settings)
```

---

### State: content

_Rendered when OBReadProduct2 returns a non-empty PCA entry (AccountId: 40051512345678, ProductId: HSBC-ADVANCE-PCA-001). Screen is scrollable — all sections visible on scroll._

```
┌─────────────────────────────────────────────┐
│ ←  Product Terms                            │  ← top_app_bar bg #F7F9FF
├─────────────────────────────────────────────┤
│                                              │  ← content padding top 16dp
│ ┌─────────────────────────────────────────┐ │  ← product_header_card
│ │  PCA                                    │ │    bg #EBEEF3 (surfaceContainer, elev 2)
│ │                           labelMedium → │ │    corner 12dp padding 16dp
│ │  HSBC Advance Account                   │ │    margin horizontal 16dp bottom 16dp
│ │                      headlineMedium  → │ │
│ │  Product ID: HSBC-ADVANCE-PCA-001      │ │  ← product_id labelSmall #41474D
│ └─────────────────────────────────────────┘ │
│                                              │
│  FEES                                       │  ← fees_header section_header
│  ─────────────────────────────────────────  │    labelSmall 11sp #41474D outlineVariant line
│  Monthly maximum charge         £0.00       │  ← monthly_max_charge_row list_item
│                                              │    supporting bodyMedium #181C20
│                                              │    trailing titleMedium 16sp/24sp #181C20
│                                              │
│  CREDIT INTEREST                            │  ← credit_interest_header section_header
│  ─────────────────────────────────────────  │
│  Up to £1,000 · paid Monthly   0.00% AER   │  ← tier_band_row[0] list_item
│                                              │    supporting bodyMedium #41474D
│  Up to £10,000 · paid Monthly  0.15% AER   │    trailing titleMedium #181C20
│                                              │  ← tier_band_row[1] list_item
│                                              │
│  OVERDRAFT                                  │  ← overdraft_header section_header
│  ─────────────────────────────────────────  │
│  Arranged overdraft           39.9% EAR    │  ← overdraft_tier_row[0] list_item
│                                              │    trailing titleMedium #BA1A1A (high rate)
│  Unarranged overdraft         49.9% EAR    │  ← overdraft_tier_row[1] list_item
│                                              │    trailing titleMedium #BA1A1A (high rate)
│                                              │
│  FEATURES                                   │  ← features_header section_header
│  ─────────────────────────────────────────  │
│  ✓  No monthly maintenance fee              │  ← feature_row[0] list_item
│                                              │    leading icon check_circle 20dp #266489
│  ✓  Mobile and online banking included     │  ← feature_row[1]
│  ✓  Arranged overdraft buffer up to £25    │  ← feature_row[2]
│  ✓  HSBC Rewards cashback on eligible spend│  ← feature_row[3]
│  ✓  Preferential rates on HSBC savings     │  ← feature_row[4]
│  ✓  24/7 telephone banking support         │  ← feature_row[5] bodyMedium #181C20
│                                              │  ← content padding bottom 32dp
├─────────────────────────────────────────────┤
│ ⌂ Home ◫ Accounts ≡ Transactions ⊕ More    │
│                    ↑ selected #266489        │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
Screen: Product Terms (ProductUiState.Content — product: HSBC Advance Account / PCA)
│
top_app_bar/ (small, bg #F7F9FF, elevation 2dp on scroll)
│   ├── leading: back_button (arrow_back 24dp #266489, navigates to account-detail)
│   └── title "Product Terms" (titleLarge 22sp/28sp w400 #181C20)
│
LazyColumn/ (scrollable, padding top 16dp horizontal 16dp bottom 32dp, gap 0dp between sections)
│
├── product_header_card/ (Card, bg #EBEEF3, elevation 2, cornerRadius 12dp,
│   │                     padding 16dp, margin horizontal 0dp bottom 16dp)
│   │   accessibility_label: "Product: HSBC Advance Account, type PCA, ID HSBC-ADVANCE-PCA-001"
│   │   stack vertical gap 4dp:
│   ├── product_type_label  (Text, labelMedium 12sp/16sp w500 color #50606E): "PCA"
│   │   [OBProduct2.ProductType — overline role]
│   ├── product_name        (Text, headlineMedium 28sp/36sp w400 color #181C20): "HSBC Advance Account"
│   │   [OBProduct2.ProductName — a11y role: heading]
│   └── product_id          (Text, labelSmall 11sp/16sp w500 color #41474D):
│                           "Product ID: HSBC-ADVANCE-PCA-001"
│
├── fees_header/ (section_header, padding vertical 8dp top 16dp,
│   label "FEES", style labelSmall #41474D, divider line outlineVariant #C1C7CE below)
│
├── monthly_max_charge_row/ (ListItem, minHeight 56dp, padding horizontal 0dp,
│   │   accessibility_label: "Monthly maximum charge: £0.00")
│   ├── supporting_text  (bodyMedium 14sp/20sp w400 #181C20): "Monthly maximum charge"
│   └── trailing_content (titleMedium 16sp/24sp w500 #181C20): "£0.00"
│
├── credit_interest_header/ (section_header, padding top 16dp,
│   label "CREDIT INTEREST", style labelSmall #41474D, divider line below)
│
├── credit_interest_list/ (items_source: TierBandSet, TierBandMethod: "Tiered",
│   │   accessibility_label: "Credit interest rates — tiered method")
│   │
│   ├── tier_band_row[0]/ (ListItem, minHeight 56dp,
│   │   │   accessibility_label: "Up to £1,000, paid Monthly: 0.00% AER")
│   │   ├── supporting_text  (bodyMedium 14sp/20sp #41474D): "Up to £1,000 · paid Monthly"
│   │   └── trailing_content (titleMedium 16sp/24sp w500 #181C20): "0.00% AER"
│   │
│   └── tier_band_row[1]/ (ListItem, minHeight 56dp,
│       │   accessibility_label: "Up to £10,000, paid Monthly: 0.15% AER")
│       ├── supporting_text  (bodyMedium 14sp/20sp #41474D): "Up to £10,000 · paid Monthly"
│       └── trailing_content (titleMedium 16sp/24sp w500 #181C20): "0.15% AER"
│
├── overdraft_header/ (section_header, padding top 16dp,
│   label "OVERDRAFT", style labelSmall #41474D, divider line below)
│
├── overdraft_list/ (items_source: OverdraftTierBandSet,
│   │   accessibility_label: "Overdraft interest rates")
│   │
│   ├── overdraft_tier_row[0]/ (ListItem, minHeight 56dp,
│   │   │   accessibility_label: "Arranged overdraft: 39.9% EAR")
│   │   ├── supporting_text  (bodyMedium 14sp/20sp #181C20): "Arranged overdraft"
│   │   └── trailing_content (titleMedium 16sp/24sp w500 #BA1A1A): "39.9% EAR"
│   │       [#BA1A1A signals high-cost credit — WCAG AA compliant on #F7F9FF bg]
│   │
│   └── overdraft_tier_row[1]/ (ListItem, minHeight 56dp,
│       │   accessibility_label: "Unarranged overdraft: 49.9% EAR")
│       ├── supporting_text  (bodyMedium 14sp/20sp #181C20): "Unarranged overdraft"
│       └── trailing_content (titleMedium 16sp/24sp w500 #BA1A1A): "49.9% EAR"
│
├── features_header/ (section_header, padding top 16dp,
│   label "FEATURES", style labelSmall #41474D, divider line below)
│
└── features_list/ (items_source: Features[6], accessibility_label: "Account features")
    ├── feature_row[0]/ (ListItem, minHeight 48dp,
    │   leading_icon: check_circle 20dp #266489, decorative false,
    │   contentDescription: "Feature: No monthly maintenance fee")
    │   supporting_text (bodyMedium 14sp/20sp #181C20): "No monthly maintenance fee"
    ├── feature_row[1]/ leading check_circle #266489
    │   supporting_text: "Mobile and online banking included"
    ├── feature_row[2]/ leading check_circle #266489
    │   supporting_text: "Arranged overdraft buffer up to £25"
    ├── feature_row[3]/ leading check_circle #266489
    │   supporting_text: "HSBC Rewards cashback on eligible spend"
    ├── feature_row[4]/ leading check_circle #266489
    │   supporting_text: "Preferential rates on HSBC savings and mortgages"
    └── feature_row[5]/ leading check_circle #266489
        supporting_text: "24/7 telephone banking support"

BottomNav/ (persistent)
├── tab Home         (icon: home,           label: "Home",         tint #41474D)
├── tab Accounts     (icon: account_balance, label: "Accounts",    tint #266489 — selected)
├── tab Transactions (icon: receipt_long,   label: "Transactions", tint #41474D)
└── tab More         (icon: more_horiz,     label: "More",         tint #41474D)
```

---

### State: empty

_Displayed when OBReadProduct2.Data is empty or account type (GlobalMoney, Savings, CreditCard) has no PCA/BCA entry. Informational — not an error; no Retry button._

```
┌─────────────────────────────────────────────┐
│ ←  Product Terms                            │  ← top_app_bar bg #F7F9FF
├─────────────────────────────────────────────┤
│                                              │
│                                              │
│                                              │
│                                              │
│              [info_outline]                  │  ← icon info_outline 48dp #41474D centred
│                                              │
│   No product information available          │  ← title headlineSmall 24sp/32sp #181C20 centred
│                                              │
│  Product terms are not available for       │  ← body bodyMedium 14sp/20sp #41474D centred
│  this account type.                        │
│                                              │
│  (no retry — informational, not recoverable)│  ← empty_product_state variant: informational
│                                              │
│                                              │
│                                              │
├─────────────────────────────────────────────┤
│ ⌂ Home ◫ Accounts ≡ Transactions ⊕ More    │
│                    ↑ selected #266489        │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — empty

```
Screen: Product Terms (ProductUiState.Empty — GlobalMoney / Savings / CreditCard account)
│
top_app_bar/ (bg #F7F9FF)
│   ├── leading: back_button (arrow_back 24dp #266489)
│   └── title "Product Terms" (titleLarge #181C20)
│
empty_product_state/ (Box, fill, contentAlignment=Center, padding horizontal 32dp)
│   accessibility_label: "No product information available for this account type"
│   variant: informational (info_outline icon, no action button)
│   stack vertical gap 16dp, horizontalAlignment=Center:
│
├── icon  (Icon info_outline, 48dp×48dp, tint #41474D,
│          contentDescription: "Information — no product terms available")
├── title (Text, headlineSmall 24sp/32sp w400 #181C20, textAlign=Center):
│         "No product information available"
└── body  (Text, bodyMedium 14sp/20sp w400 #41474D, textAlign=Center):
          "Product terms are not available for this account type."
          [No Retry button: informational empty is not a network failure;
           GlobalMoney/Savings/CreditCard accounts have no OBProduct2 PCA/BCA entry by design]

BottomNav/ (persistent — Accounts tab selected)
```

---

### State: error

_Displayed on HTTP 401 (token expired) / 403 (ReadProducts consent missing) / 404 (no product record) / network error. Dynamic body from error.message. Retry button always visible._

```
┌─────────────────────────────────────────────┐
│ ←  Product Terms                            │  ← top_app_bar bg #F7F9FF
├─────────────────────────────────────────────┤
│                                              │
│                                              │
│                                              │
│              [error_outline]                 │  ← icon error_outline 48dp #BA1A1A centred
│                                              │
│    Unable to load product terms             │  ← title headlineSmall 24sp/32sp #181C20 centred
│                                              │
│  Consent does not include ReadProducts.    │  ← body bodyMedium 14sp/20sp #41474D centred
│  (dynamic: error.message from ViewModel)   │    demo: HTTP 403 error message
│                                              │
│                                              │
│      [        Try again        ]             │  ← retry_button filled 56dp h
│                                              │    bg #266489 label #FFFFFF radius 9999
│                                              │    min touch target 56dp
│                                              │    on_click → retry_load → productLoad(accountId)
│                                              │
├─────────────────────────────────────────────┤
│ ⌂ Home ◫ Accounts ≡ Transactions ⊕ More    │
│                    ↑ selected #266489        │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — error

```
Screen: Product Terms (ProductUiState.Error — demo: HTTP 403 ReadProducts consent missing)
│
top_app_bar/ (bg #F7F9FF)
│   ├── leading: back_button (arrow_back 24dp #266489)
│   └── title "Product Terms" (titleLarge #181C20)
│
error_state/ (Box, fill, contentAlignment=Center, padding horizontal 32dp)
│   accessibility_label: "Unable to load product terms"
│   variant: error (error_outline icon, filled retry button)
│   stack vertical gap 16dp, horizontalAlignment=Center:
│
├── icon  (Icon error_outline, 48dp×48dp, tint #BA1A1A,
│          contentDescription: "Error loading product terms")
├── title (Text, headlineSmall 24sp/32sp w400 #181C20, textAlign=Center):
│         "Unable to load product terms"
├── body  (Text, bodyMedium 14sp/20sp w400 #41474D, textAlign=Center):
│         "{error.message}"   [dynamic from ViewModel error string]
│         HTTP 401 demo: "Session expired. Please re-authenticate."
│         HTTP 403 demo: "Consent does not include ReadProducts."
│         HTTP 404 demo: "No product data available for this account."
│         Network demo:  "Unable to connect. Check your internet connection."
└── retry_button (Button variant:filled, 56dp h, bg #266489, label-color #FFFFFF,
                  cornerRadius 9999, min touch 56dp, padding horizontal 24dp)
    label: "Try again"
    accessibility_label: "Retry loading product terms"
    on_click → action: retry_load (ProductAction.RetryLoad)
    action_contract:
      effect: call_api
      library_refs: [ktorfit, hsbc-obie-ais-v4.0:product]
      description: "Re-triggers productLoad(accountId) — re-issues GET /accounts/{AccountId}/product;
                    transitions Loading → Content | Empty | Error"

BottomNav/ (persistent — Accounts tab selected)
```

---

### Interaction Summary

_Mirrors current `action_contract` declarations in `screens/product/ui.yaml`. All other components are display-only._

| Component | Action | Effect | Target / Behaviour |
|---|---|---|---|
| back_button (top_app_bar leading) | navigate_back | navigate | NavigationController.navigateBack() — pops back to `account-detail` screen |
| retry_button (error state only) | retry_load | call_api | Re-triggers `productLoad(accountId)` via ktorfit GET /accounts/{AccountId}/product; transitions Loading → Content \| Empty \| Error |

_All other components (product_header_card, monthly_max_charge_row, tier_band_row × N, overdraft_tier_row × N, feature_row × N, empty_product_state) are display-only with no on_click contract._

---

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| top_app_bar | match_parent | 56dp | 0 |
| back_button touch target | 48dp | 48dp | 9999dp (circular ripple) |
| product_header_card | match_parent | wrap (~88dp) | 12dp |
| fees_header / section_headers | match_parent | 40dp (with divider) | 0 |
| monthly_max_charge_row (list_item) | match_parent | 56dp | 0 |
| tier_band_row[0] (list_item) | match_parent | 56dp | 0 |
| tier_band_row[1] (list_item) | match_parent | 56dp | 0 |
| overdraft_tier_row[0] (list_item) | match_parent | 56dp | 0 |
| overdraft_tier_row[1] (list_item) | match_parent | 56dp | 0 |
| feature_row × 6 (list_item with leading icon) | match_parent | 48dp | 0 |
| check_circle leading icon | 20dp | 20dp | circle |
| empty_product_state icon | 48dp | 48dp | circle (vector) |
| error_state icon | 48dp | 48dp | circle (vector) |
| retry_button | match_parent − 64dp | 56dp | 9999dp (full pill) |
| progress_indicator (loading) | 40dp | 40dp | circle |
| bottom_nav | match_parent | 80dp | 0 |
