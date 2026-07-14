# Standing Orders — Visual Mockup

> Auto-generated from `screens/standing-orders/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-14T00:00:00Z

---

## Screen: Standing Orders

Canvas: 393×852dp · Top app bar with back · Bottom nav · Material 3 light theme

---

### State: loading

```
┌─────────────────────────────────────────────┐
│ ← Standing Orders                           │  ← top_app_bar
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
│ ← Standing Orders                           │
├─────────────────────────────────────────────┤
│                                              │
│  3 Active · 1 Inactive                      │  ← summary_row labelMedium #41474D
│                                              │
│ ┌─────────────────────────────────────────┐ │
│ │  ↻  Rent — Landlord Properties Ltd      │ │  ← standing_order_card elevation 1
│ │     [Active]     Monthly                │ │    status badge primary tonal "Active"
│ │     Next: £975.00 on 01 Aug 2026        │ │    frequency decoded from ISO 20022
│ │     Account: 60-83-71 12345678          │ │    CreditorAccount.Identification
│ │     Ref: RENT/JULY                      │ │    reference bodySmall #41474D
│ └─────────────────────────────────────────┘ │
│ ┌─────────────────────────────────────────┐ │
│ │  ↻  HSBC Regular Saver                  │ │
│ │     [Active]     Monthly                │ │
│ │     Next: £300.00 on 15 Aug 2026        │ │
│ │     Account: 40-05-15 87654321          │ │
│ └─────────────────────────────────────────┘ │
│ ┌─────────────────────────────────────────┐ │
│ │  ↻  Charity Direct Debit — Oxfam        │ │
│ │     [Active]     Monthly                │ │
│ │     Next: £10.00 on 28 Aug 2026         │ │
│ │     Final: 28 Oct 2027                  │ │  ← final_payment_row (hasFinalPayment)
│ │     Account: 72-22-15 99887766          │ │
│ └─────────────────────────────────────────┘ │
│ ┌─────────────────────────────────────────┐ │
│ │  ↻  Old broadband — BT                  │ │
│ │     [Inactive]   Monthly                │ │  ← status badge secondary tonal "Inactive"
│ │     Last: £35.00                        │ │
│ └─────────────────────────────────────────┘ │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
top_app_bar/ (title "Standing Orders", leading back → account-detail)
back_button/ (icon_button arrow_back always visible)
summary_row/ (text labelMedium #41474D, padding h 16dp): "3 Active · 1 Inactive"
standing_orders_list/ (list vertical gap 8dp padding h 16dp)
└── standing_order_card × N (card elevation 1 radius 12dp padding 16dp)
     ├── status_badge         (chip tonal, Active=primary, Inactive=secondary)
     ├── frequency_label      (labelSmall #41474D): "Monthly" / "Weekly" / "Annual"
     ├── creditor_name        (titleMedium #181C20): "Rent — Landlord Properties Ltd"
     ├── next_payment_row     (bodyMedium #181C20): "Next: £975.00 on 01 Aug 2026"
     ├── final_payment_row    (bodySmall #41474D, visible_when hasFinalPayment)
     ├── creditor_account     (bodySmall Roboto Mono #41474D): "60-83-71 12345678"
     └── reference            (bodySmall #41474D): "Ref: RENT/JULY"
BottomNav (always)
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│ ← Standing Orders                           │
├─────────────────────────────────────────────┤
│            [autorenew]                       │  ← icon 48dp #41474D
│    No standing orders                       │  ← title headlineSmall #181C20
│  No standing orders are set up for         │  ← body bodyMedium #41474D
│  this account.                             │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│ ← Standing Orders                           │
├─────────────────────────────────────────────┤
│            [error_outline]                   │  ← icon 48dp #BA1A1A
│    Unable to load standing orders          │
│         [  Try again  ]                     │  ← retry_button filled #266489
└─────────────────────────────────────────────┘
```

---

### Interaction Summary

| Component | Action | Target |
|---|---|---|
| back_button | navigate_back | account-detail |
| standing_order_card | (read-only display, AIS) | — |
| retry_button | retry_load | in-place retry |

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| standing_order_card | match_parent − 32dp | ~120dp | 12dp |
| status_badge | wrap | 24dp | 9999 |
| summary_row | match_parent | 32dp | 0 |
