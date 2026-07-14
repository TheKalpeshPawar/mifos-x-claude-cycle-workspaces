# Product Terms — Visual Mockup

> Auto-generated from `screens/product/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Source: OBReadProduct2 — GET /accounts/{AccountId}/product
> Generated: 2026-07-14T00:00:00Z

---

## Screen: Product Terms

Canvas: 393×852dp · Top app bar with back · Bottom nav · Material 3 light theme

---

### State: loading

```
┌─────────────────────────────────────────────┐
│ ← Product Terms                             │  ← top_app_bar
├─────────────────────────────────────────────┤
│                   ◌                          │  ← circular progress #266489 centred
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: content

```
┌─────────────────────────────────────────────┐
│ ← Product Terms                             │
├─────────────────────────────────────────────┤
│                                              │
│ ┌─────────────────────────────────────────┐ │
│ │  PCA                                    │ │  ← product_type_label labelMedium #50606E
│ │  HSBC Advance Account                   │ │  ← product_name headlineMedium #181C20
│ │  Product ID: PCA-ADVANCE-001            │ │  ← product_id labelSmall #41474D
│ └─────────────────────────────────────────┘ │    product_header_card elevation 2
│                                              │
│  FEES                                       │  ← fees_header section_header #41474D
│                                              │
│  Monthly maximum charge         £0.00       │  ← monthly_max_charge_row list_item
│                                              │    supporting_text label / trailing titleMedium
│                                              │
│  CREDIT INTEREST                            │  ← credit_interest_header
│                                              │
│  Up to £1,000 · paid monthly   0.10% AER   │  ← tier_band_row list_item
│  Up to £10,000 · paid monthly  0.15% AER   │    trailing titleMedium #181C20
│  Over £10,000 · paid monthly   0.25% AER   │
│                                              │
│  OVERDRAFT                                  │  ← overdraft_header section_header
│                                              │
│  Arranged overdraft            39.90% EAR   │  ← overdraft_tier_row list_item
│  Unarranged overdraft          39.90% EAR   │    trailing titleMedium #BA1A1A
│                                              │
│  FEATURES                                   │  ← features_header section_header
│                                              │
│  ✓  No monthly fee for account holders      │  ← feature_row list_item
│  ✓  Cashback on debit purchases             │    leading check_circle #266489
│  ✓  Global money transfers in 30 currencies │
│  ✓  Access to HSBC Premier Lounges         │
│  ✓  Preferential rates via HSBC Kinetic    │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
top_app_bar/ (title "Product Terms", leading back → account-detail)
product_header_card/ (card elevation 2 radius 12dp padding 16dp margin h 16dp)
│  ├── product_type_label (labelMedium #50606E): "PCA"  [OBProduct2.ProductType]
│  ├── product_name       (headlineMedium #181C20): "HSBC Advance Account"
│  └── product_id         (labelSmall #41474D): "Product ID: PCA-ADVANCE-001"
fees_header/ (section_header): "FEES" (padding h 16dp)
monthly_max_charge_row/ (list_item supporting="Monthly maximum charge" trailing="£0.00" titleMedium)
credit_interest_header/ (section_header): "CREDIT INTEREST"
credit_interest_list/ (list, items_source=product.PCA.CreditInterest.TierBandSet)
└── tier_band_list/ → tier_band_row × N (list_item)
     supporting: "Up to £{BandLimit} · paid {ApplicationFrequency}"
     trailing:   "{AER}% AER"  (titleMedium #181C20)
overdraft_header/ (section_header): "OVERDRAFT"
overdraft_list/ → overdraft_tier_list/ → overdraft_tier_row × N (list_item)
     supporting: "{OverdraftType} overdraft"
     trailing:   "{EAR}% EAR"  (titleMedium, Arranged=#181C20, Unarranged=#BA1A1A)
features_header/ (section_header): "FEATURES"
features_list/ (list, items_source=product.PCA.ProductDetails.Features)
└── feature_row × N (list_item leading_icon check_circle #266489, supporting_text=item)
BottomNav (always)
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│ ← Product Terms                             │
├─────────────────────────────────────────────┤
│            [info_outline]                    │  ← icon 48dp #41474D
│    No product information                  │  ← title headlineSmall #181C20
│  Product terms are not available for      │  ← body bodyMedium #41474D
│  this account type.                       │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│ ← Product Terms                             │
├─────────────────────────────────────────────┤
│            [error_outline]                   │  ← icon 48dp #BA1A1A
│    Unable to load product terms            │
│  body from error.message                   │
│         [  Try again  ]                     │  ← retry_button filled #266489
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### Interaction Summary

| Component | Action | Target |
|---|---|---|
| back_button | navigate_back | account-detail |
| feature_row / tier_band_row | (display only, read-only) | — |
| retry_button | retry_load | in-place retry |

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| product_header_card | match_parent − 32dp | ~80dp | 12dp |
| tier_band_row (list_item) | match_parent | 56dp | 0 |
| feature_row (list_item) | match_parent | 48dp | 0 |
| check_circle icon | 20dp | 20dp | circle |
