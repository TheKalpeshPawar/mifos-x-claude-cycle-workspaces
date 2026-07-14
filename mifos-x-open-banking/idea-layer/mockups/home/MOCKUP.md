# Home — Visual Mockup

> Auto-generated from `screens/home/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-14T00:00:00Z

---

## Screen: Home Dashboard

Canvas: 393×852dp (Pixel 5) · Bottom nav visible · No top app bar · Roboto font · Material 3 light theme

---

### State: loading

```
┌─────────────────────────────────────────────┐
│                                              │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░     │  ← skeleton_hero 393×180dp radius 16dp
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░     │    surfaceVariant #DDE3EA pulse 1.5s
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░     │
│                                              │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░     │  ← skeleton_actions 393×80dp radius 12dp
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░     │
│                                              │
│  ░░░░░░░░░░░░░░░░░             ·             │  ← skeleton_tx_header 140dp text line
│                                              │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░     │  ← skeleton_tx_1 393×64dp radius 8dp
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░     │  ← skeleton_tx_2 393×64dp
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░     │  ← skeleton_tx_3 393×64dp
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │  ← bottom navigation #F7F9FF
└─────────────────────────────────────────────┘
```

### Component Hierarchy — loading

```
loading_skeleton/ (stack vertical, gap 12dp, padding top 24dp h 16dp)
├── skeleton_hero       (shimmer card, 180dp, radius 16dp, surfaceVariant)
├── skeleton_actions    (shimmer card, 80dp, radius 12dp, surfaceVariant)
├── skeleton_tx_header  (shimmer text, 20dp h, 140dp w)
├── skeleton_tx_1       (shimmer card, 64dp, radius 8dp)
├── skeleton_tx_2       (shimmer card, 64dp)
└── skeleton_tx_3       (shimmer card, 64dp)
BottomNav (always)
```

---

### State: content

```
┌─────────────────────────────────────────────┐
│ ( HSBC Current )  ( HSBC Savings )  ( →     │  ← account_switcher chip row h-scroll
│                                              │    chip bg #C9E6FF selected, radius 9999
│ ┌─────────────────────────────────────────┐ │
│ │  CurrentAccount            [account]    │ │  ← hero_balance_card bg #C9E6FF
│ │  HSBC Advance Current                   │ │    elevation 2, radius 16dp, padding 16dp
│ │                                          │ │
│ │  £4,281.55                               │ │  ← hero_balance displaySmall #004B6F
│ │  Available  £4,190.22                   │ │  ← available bodySmall #004B6F
│ │  40-05-15 12345678                       │ │  ← identification bodySmall
│ └─────────────────────────────────────────┘ │
│                                              │
│ ┌─────────────────────────────────────────┐ │
│ │  ⊘ Pay    ◫ Transactions  ≡ Statements │ │  ← quick_actions_card elevation 1
│ │  [tonal]  [tonal]         [tonal]  [🛡] │ │    radius 12dp, horizontal stack
│ └─────────────────────────────────────────┘ │
│                                              │
│  Recent transactions                View all →  ← section_header titleSmall #181C20
│                                              │
│  ┌───────────────────────────────────────┐  │
│  │ 🛒  Sainsbury's            -£24.80    │  │  ← recent_tx_row card elev 0 radius 8dp
│  │     12 Jul                            │  │    icon secondary #50606E
│  └───────────────────────────────────────┘  │
│  ┌───────────────────────────────────────┐  │
│  │ ☕  Costa Coffee             -£4.35   │  │
│  │     11 Jul                            │  │
│  └───────────────────────────────────────┘  │
│  ┌───────────────────────────────────────┐  │
│  │ 💷  Salary — Acme Ltd       +£2,850   │  │
│  │     10 Jul                            │  │
│  └───────────────────────────────────────┘  │
│  ┌───────────────────────────────────────┐  │
│  │ ⛽  Shell Garage             -£62.00  │  │
│  │     09 Jul                            │  │
│  └───────────────────────────────────────┘  │
│  ┌───────────────────────────────────────┐  │
│  │ 🎵  Spotify                  -£9.99   │  │
│  │     08 Jul                            │  │
│  └───────────────────────────────────────┘  │
│                                              │
│ ┌─────────────────────────────────────────┐ │
│ │  Spending this month    >               │ │  ← spending_snapshot_card elevation 1
│ │  This month                             │ │    radius 12dp, margin h 16dp
│ │  £1,240.88              [›]             │ │    amount headlineMedium color error
│ │  Top category: Groceries                │ │    chevron_right icon #41474D
│ └─────────────────────────────────────────┘ │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
account_switcher/ (chip_row h-scroll, padding top 12dp h 16dp)
│  └── account_chip × N  (selected: bg #C9E6FF text #004B6F; unselected: outline)
hero_balance_card/ (card bg #C9E6FF elevation 2 radius 16dp margin h 16dp)
│  ├── hero_account_subtype  (labelMedium #004B6F): "CurrentAccount"
│  ├── hero_account_icon     (icon account_balance, md, #004B6F, decorative)
│  ├── hero_nickname         (titleLarge #004B6F): "HSBC Advance Current"
│  ├── hero_balance          (displaySmall #004B6F): "£4,281.55"
│  ├── hero_available_label  (bodySmall #004B6F): "Available"
│  ├── hero_available_amount (bodySmall #004B6F): "£4,190.22"
│  └── hero_identification   (bodySmall #004B6F): "40-05-15 12345678"
quick_actions_card/ (card elevation 1 radius 12dp margin h 16dp)
│  ├── action_pay/       (icon_button send tonal disabled, labelSmall "Pay")
│  ├── action_transactions/ (icon_button receipt_long tonal → transactions)
│  ├── action_statements/   (icon_button description tonal → statements)
│  └── action_consents/     (icon_button shield tonal → consent-list)
recent_transactions_section/ (stack vertical gap 4dp padding h 16dp)
│  ├── recent_tx_header (section_header titleSmall): "Recent transactions"
│  ├── view_all_transactions_link (text_button → transactions)
│  └── recent_transactions_list/ (list items=recentTransactions)
│       └── recent_tx_row × 5  (card elev 0 radius 8dp)
│            ├── tx_category_icon  (icon categoryIcon, md, #50606E)
│            ├── tx_description    (bodyMedium #181C20, maxLines 1 ellipsis)
│            ├── tx_date           (bodySmall #41474D)
│            └── tx_amount         (bodyMedium, credit=#266489 / debit=#BA1A1A)
spending_snapshot_card/ (card elevation 1 radius 12dp margin h 16dp)
│  ├── spending_snapshot_header (titleSmall #181C20): "Spending this month"
│  ├── spending_this_month (bodySmall #41474D): "This month"
│  ├── spending_amount     (headlineMedium #BA1A1A): "£1,240.88"
│  ├── spending_top_category (bodySmall #41474D): "Top category: Groceries"
│  └── spending_chevron   (icon chevron_right md #41474D)
BottomNav (always)
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│                                              │
│                                              │
│              [account_balance_wallet]        │  ← icon 48dp #41474D
│                                              │
│         No accounts connected yet           │  ← headlineSmall #181C20
│    Connect your HSBC account via Open       │
│    Banking to see your balances and         │  ← bodyMedium #41474D centred
│    recent transactions.                     │
│                                              │
│         [  Connect with HSBC  ]             │  ← button filled 56dp #266489
│                                              │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│                                              │
│              [error_outline]                 │  ← icon 48dp #BA1A1A centred
│                                              │
│         Unable to load your accounts        │  ← headlineSmall #181C20
│    We couldn't retrieve your balance.       │  ← bodyMedium #41474D
│    Please check your connection and         │
│    try again.                               │
│                                              │
│         [  Try again  ]                     │  ← button filled (visible_when recoverable)
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### Interaction Summary

| Component | Action | Target |
|---|---|---|
| account_chip | select_account | in-place account switch |
| hero_balance_card | navigate_account_detail | account-detail (accountId) |
| transactions_button | navigate_transactions | transactions (accountId) |
| statements_button | navigate_statements | statements (accountId) |
| consents_button | navigate_consent_list | consent-list |
| recent_tx_row | navigate_transaction_detail | transaction-detail (transactionId, accountId) |
| view_all_transactions_link | navigate_transactions | transactions (accountId) |
| spending_snapshot_card | navigate_spending | spending-by-category |
| connect_bank_button (empty) | navigate_login | login |
| retry_button (error) | retry_load | in-place retry |

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| hero_balance_card | match_parent − 32dp | wrap (~140dp) | 16dp |
| quick_actions_card | match_parent − 32dp | 80dp | 12dp |
| recent_tx_row | match_parent | 64dp | 8dp |
| spending_snapshot_card | match_parent − 32dp | ~96dp | 12dp |
| skeleton_hero | match_parent − 32dp | 180dp | 16dp |
| bottom_nav | match_parent | 80dp | 0 |
