# Transactions — Visual Mockup

> Auto-generated from `screens/transactions/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-14T00:00:00Z

---

## Screen: Transactions

Canvas: 393×852dp · Top app bar with back arrow · Bottom nav · Material 3 light theme

---

### State: loading

```
┌─────────────────────────────────────────────┐
│ ← Transactions                              │  ← top_app_bar
├─────────────────────────────────────────────┤
│                                              │
│                   ◌                          │  ← loading_spinner circular #266489 centred
│               (spinning)                     │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: content

```
┌─────────────────────────────────────────────┐
│ ← Transactions                              │
├─────────────────────────────────────────────┤
│                                              │
│  Money in  +£2,850.00  │  Money out  -£891.12 │ ← period_summary stat_block
│            #266489     │            #BA1A1A    │   two stats side by side
│                                              │
│  ┌────────────────────────────────────────┐ │
│  │ 🔍 Search transactions                 │ │  ← search_field text_field
│  └────────────────────────────────────────┘ │
│                                              │
│ (All) (Money in) (Money out) (Pending)      │  ← filter chips h-scroll
│                                              │
│  14 Jul 2026                                 │  ← date_group_header labelSmall #41474D
│  ┌──────────────────────────────────────┐   │
│  │ 🛒  Sainsbury's           -£24.80   │   │  ← tx_card elevation 0 radius 8dp
│  │     category: Groceries  14 Jul     │   │    amount error #BA1A1A
│  └──────────────────────────────────────┘   │
│  ┌──────────────────────────────────────┐   │
│  │ ☕  Costa Coffee           -£4.35   │   │
│  │     category: Eating out  14 Jul    │   │
│  └──────────────────────────────────────┘   │
│                                              │
│  13 Jul 2026                                 │
│  ┌──────────────────────────────────────┐   │
│  │ ⛽  Shell Garage           -£62.00  │   │
│  │     category: Transport   13 Jul    │   │
│  └──────────────────────────────────────┘   │
│  ┌──────────────────────────────────────┐   │
│  │  !  Amazon.co.uk          -£18.50   │   │  ← pending badge
│  │     category: Shopping    Pending   │   │    badge chip tonal labelSmall
│  └──────────────────────────────────────┘   │
│                                              │
│  10 Jul 2026                                 │
│  ┌──────────────────────────────────────┐   │
│  │ 💷  Salary — Acme Ltd    +£2,850    │   │  ← credit amount primary #266489
│  │     category: Income      10 Jul    │   │
│  └──────────────────────────────────────┘   │
│                                              │
│         [  Load more transactions  ]         │  ← load_more_button outlined
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
top_app_bar/ (title "Transactions", leading back → accounts or home)
period_summary/ (stat_block two columns, padding h 16dp)
│  ├── total_credit (label "Money in", value "+£2,850.00" primary #266489)
│  └── total_debit  (label "Money out", value "-£891.12" error #BA1A1A)
search_field/ (text_field, icon search leading, placeholder "Search transactions")
filter_chips/ (chip_group h-scroll, padding h 16dp)
│  ├── filter_all       "All" (selected)
│  ├── filter_credit    "Money in"
│  ├── filter_debit     "Money out"
│  └── filter_pending   "Pending"
transactions_list/ (lazy list, grouped by BookingDateTime date)
│  ├── date_group_header × N (labelSmall #41474D, sticky)
│  └── tx_card × M per group (card elevation 0 radius 8dp padding v 12dp h 16dp)
│       ├── tx_category_icon   (icon categoryIcon, md, #50606E)
│       ├── tx_merchant_name   (bodyMedium #181C20, maxLines 1 ellipsis)
│       ├── tx_category_label  (bodySmall #41474D)
│       ├── tx_date            (bodySmall #41474D)
│       ├── pending_badge      (badge tonal labelSmall, visible_when Status=Pending)
│       └── tx_amount          (bodyMedium, credit=#266489, debit=#BA1A1A)
load_more_button/ (button outlined, visible_when nextPageAvailable)
BottomNav (always)
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│ ← Transactions                              │
├─────────────────────────────────────────────┤
│  [period_summary and filters still shown]   │
│                                              │
│            [receipt_long]                    │  ← icon 48dp #41474D centred
│                                              │
│    No transactions found                    │  ← title headlineSmall #181C20
│  No transactions match your current         │  ← body bodyMedium #41474D
│  filters for this period.                   │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│ ← Transactions                              │
├─────────────────────────────────────────────┤
│                                              │
│            [error_outline]                   │  ← icon 48dp #BA1A1A
│                                              │
│    Unable to load transactions              │  ← title headlineSmall #181C20
│  Please check your connection.              │  ← body bodyMedium #41474D
│                                              │
│         [  Try again  ]                     │  ← retry_button filled #266489
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### Interaction Summary

| Component | Action | Target |
|---|---|---|
| back arrow | navigate_back | account-detail or home |
| filter chips | filter_transactions | in-place list filter |
| search_field | search_transactions | in-place search filter |
| tx_card | navigate_transaction_detail | transaction-detail (transactionId, accountId) |
| load_more_button | load_more_transactions | paginate (Links.Next cursor) |
| retry_button (error) | retry_load | in-place retry |

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| period_summary | match_parent | 56dp | 0 |
| search_field | match_parent − 32dp | 48dp | 28dp |
| filter chip (each) | wrap | 32dp | 9999 |
| tx_card | match_parent − 32dp | 64dp min | 8dp |
| date_group_header | match_parent | 24dp | 0 |
| load_more_button | match_parent − 32dp | 40dp | 12dp |
