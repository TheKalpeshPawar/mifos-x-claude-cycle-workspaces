# Scheduled Payments — Visual Mockup

> Auto-generated from `screens/scheduled-payments/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-14T00:00:00Z

---

## Screen: Scheduled Payments

Canvas: 393×852dp · Top app bar with back · Bottom nav · Material 3 light theme

---

### State: loading

```
┌─────────────────────────────────────────────┐
│ ← Scheduled Payments                        │  ← top_app_bar
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
│ ← Scheduled Payments                        │
├─────────────────────────────────────────────┤
│                                              │
│ ┌─────────────────────────────────────────┐ │
│ │  🗓  Monthly Rent Payment               │ │  ← payment_card elevation 1 radius 12dp
│ │     GBP 975.00                          │ │    InstructedAmount bodyLarge #181C20
│ │     Thu 31 Jul 2026                     │ │    ScheduledPaymentDateTime bodyMedium
│ │     [Execution date]                    │ │    ScheduledType chip labelSmall
│ │     To: 60-83-71 12345678               │ │    Mono bodySmall #41474D
│ │     Ref: RENT/AUG                       │ │    Reference bodySmall #41474D
│ └─────────────────────────────────────────┘ │
│ ┌─────────────────────────────────────────┐ │
│ │  ↓  Credit card payment — HSBC         │ │  ← icon arrow_downward (Arrival type)
│ │     GBP 842.00                          │ │
│ │     Mon 28 Jul 2026                     │ │
│ │     [Arrival date]                      │ │
│ │     To: 08-32-00 12001039               │ │
│ │     Ref: HSBC-CC-PYMT                   │ │
│ └─────────────────────────────────────────┘ │
│ ┌─────────────────────────────────────────┐ │
│ │  🗓  Car insurance renewal              │ │
│ │     GBP 450.00                          │ │
│ │     Fri 01 Aug 2026                     │ │
│ │     [Execution date]                    │ │
│ │     To: 20-60-53 43218765               │ │
│ └─────────────────────────────────────────┘ │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
top_app_bar/ (title "Scheduled Payments", leading back → account-detail)
back_button/ (icon_button arrow_back always visible)
scheduled_payments_list/ (list vertical gap 8dp padding h 16dp)
└── payment_card × N (card elevation 1 radius 12dp padding 16dp)
     ├── type_icon           (icon calendar_today=Execution / arrow_downward=Arrival, md #266489)
     ├── payee_name          (titleMedium #181C20): "Monthly Rent Payment"
     ├── amount              (bodyLarge #181C20): "GBP 975.00"
     ├── payment_date        (bodyMedium #41474D): "Thu 31 Jul 2026"
     ├── scheduled_type_chip (chip tonal labelSmall): "Execution date" / "Arrival date"
     ├── creditor_account    (bodySmall Roboto Mono #41474D): "To: 60-83-71 12345678"
     └── reference           (bodySmall #41474D): "Ref: RENT/AUG"
BottomNav (always)
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│ ← Scheduled Payments                        │
├─────────────────────────────────────────────┤
│             [schedule]                       │  ← icon 48dp #41474D
│    No scheduled payments                    │  ← title headlineSmall #181C20
│  No payments are scheduled for this        │  ← body bodyMedium #41474D
│  account.                                  │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│ ← Scheduled Payments                        │
├─────────────────────────────────────────────┤
│            [error_outline]                   │  ← icon 48dp #BA1A1A
│    Unable to load scheduled payments       │
│         [  Try again  ]                     │  ← retry_button filled #266489
└─────────────────────────────────────────────┘
```

---

### Interaction Summary

| Component | Action | Target |
|---|---|---|
| back_button | navigate_back | account-detail |
| payment_card | (display only, AIS read) | — |
| retry_button | retry_load | in-place retry |

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| payment_card | match_parent − 32dp | ~120dp | 12dp |
| scheduled_type_chip | wrap | 24dp | 9999 |
| type_icon | 24dp | 24dp | 0 |
