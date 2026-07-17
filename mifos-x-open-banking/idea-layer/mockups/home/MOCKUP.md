# Home — Visual Mockup

> Auto-generated from `screens/home/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-16T00:00:00Z

---

## Screen: Home Dashboard

Canvas: 393×852dp (Pixel 5) · Bottom nav visible · No top app bar · No FAB · Roboto font · Material 3 light theme

Shell (from `app-shell.yaml`): Bottom navigation — Home | Accounts | Transactions | More.
Top app bar disabled per `ui.yaml#shell.top_app_bar_visible: false`.
FAB disabled per `ui.yaml#shell.fab_visible: false`.

---

### State: loading

```
┌─────────────────────────────────────────────┐
│                                              │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │  ← skeleton_hero: 361×180dp, radius 16dp
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │    shimmer surfaceVariant #DDE3EA pulse 1.5s
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │    margin horizontal 16dp
│                                              │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │  ← skeleton_actions: 361×80dp, radius 12dp
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │    margin horizontal 16dp
│                                              │
│  ░░░░░░░░░░░░░░░░░░                         │  ← skeleton_tx_header: 140dp×20dp text shimmer
│                                              │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │  ← skeleton_tx_1: match_parent×64dp, radius 8dp
│                                              │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │  ← skeleton_tx_2: match_parent×64dp, radius 8dp
│                                              │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │  ← skeleton_tx_3: match_parent×64dp, radius 8dp
│                                              │
│   [gap 12dp between each skeleton block]    │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│  ← bottom_nav bg #F7F9FF h 80dp
└─────────────────────────────────────────────┘
```

### Component Hierarchy — loading

```
Screen: Home (UiState.Loading)
│
loading_skeleton/ (stack vertical, gap 12dp, padding top 32dp horizontal 16dp bottom 16dp)
│   accessibility_label: "Loading your account" (#DDE3EA shimmer, reduce-motion: static fill)
│
├── skeleton_hero        (shimmer variant:card, 180dp h, radius 16dp, #DDE3EA pulse)
├── skeleton_actions     (shimmer variant:card,  80dp h, radius 12dp, #DDE3EA pulse)
├── skeleton_tx_header   (shimmer variant:text,  20dp h × 140dp w)
├── skeleton_tx_1        (shimmer variant:card,  64dp h, radius 8dp)
├── skeleton_tx_2        (shimmer variant:card,  64dp h, radius 8dp)
└── skeleton_tx_3        (shimmer variant:card,  64dp h, radius 8dp)

BottomNav/ (persistent, always rendered)
├── tab Home         (icon:home,          label:"Home",         selected, tint #266489)
├── tab Accounts     (icon:account_balance,label:"Accounts",    default,  tint #41474D)
├── tab Transactions (icon:receipt_long,  label:"Transactions", default,  tint #41474D)
└── tab More         (icon:more_horiz,    label:"More",         default,  tint #41474D)
```

---

### State: content

```
┌─────────────────────────────────────────────┐
│                                              │
│ ┌─ Everyday Current ─┐  ISA Saver  Platinum │  ← account_switcher chip_row horizontal scroll
│                                              │    selected chip: bg #C9E6FF text #004B6F
│                                              │    unselected chip: outline #72787E text #41474D
│ ┌─────────────────────────────────────────┐ │  ← padding top 16dp horizontal 16dp bottom 8dp
│ │  CurrentAccount       [account_balance] │ │
│ │                                          │ │  ← hero_balance_card bg #C9E6FF
│ │  Everyday Current                        │ │    elevation 2, radius 16dp, padding 24dp
│ │                                          │ │    margin horizontal 16dp bottom 16dp
│ │  £2,847.63                               │ │  ← hero_balance displaySmall 36sp #004B6F
│ │  Available  £2,847.63                   │ │  ← hero_available_label/amount bodySmall 12sp
│ │  40-05-15 12345678                       │ │  ← hero_identification bodySmall 12sp #004B6F
│ └─────────────────────────────────────────┘ │
│                                              │
│ ┌─────────────────────────────────────────┐ │  ← quick_actions_card elevation 1
│ │  ⊘       ≡         ≡         🛡         │ │    radius 12dp, padding 16dp
│ │  Pay   Trans..  Statements  Consents    │ │    margin horizontal 16dp bottom 16dp
│ │ [off]  [tonal]  [tonal]    [tonal]      │ │    pay_button disabled (PISP stub)
│ └─────────────────────────────────────────┘ │
│                                              │
│  Recent transactions          View all →    │  ← recent_tx_header titleSmall 14sp #181C20
│                                              │    view_all_transactions_link text_button #266489
│  ┌───────────────────────────────────────┐  │
│  │ 🛒  AMAZON UK MARKETPLACE  -£31.99   │  │  ← recent_tx_row[0] card elev 0 radius 8dp
│  │     27 Jun                            │  │    icon shopping_cart 24dp #50606E
│  └───────────────────────────────────────┘  │    amount bodyMedium #BA1A1A
│  ┌───────────────────────────────────────┐  │
│  │ 🍽  PRET A MANGER 083 LONDON -£8.45  │  │  ← recent_tx_row[1]  icon restaurant #50606E
│  │     27 Jun                            │  │
│  └───────────────────────────────────────┘  │
│  ┌───────────────────────────────────────┐  │
│  │ 🛒  TESCO STORES 3476 LONDON -£42.17 │  │  ← recent_tx_row[2]  icon local_grocery_store
│  │     26 Jun                            │  │
│  └───────────────────────────────────────┘  │
│  ┌───────────────────────────────────────┐  │
│  │ 🚌  TFL TRAVEL CHARGE        -£6.80  │  │  ← recent_tx_row[3]  icon directions_bus
│  │     26 Jun                            │  │
│  └───────────────────────────────────────┘  │
│  ┌───────────────────────────────────────┐  │
│  │ 💼  SALARY ACME LTD      +£2,400.00  │  │  ← recent_tx_row[4]  icon work
│  │     25 Jun                            │  │    amount bodyMedium #266489 (credit)
│  └───────────────────────────────────────┘  │
│                                              │
│ ┌─────────────────────────────────────────┐ │  ← spending_snapshot_card elevation 1
│ │  Spending this month                 ›  │ │    radius 12dp, padding 16dp
│ │  This month                             │ │    margin horizontal 16dp bottom 32dp
│ │  £167.41                       [›]      │ │  ← spending_amount headlineMedium 28sp #BA1A1A
│ │  Top category: Groceries                │ │    spending_chevron chevron_right 24dp #41474D
│ └─────────────────────────────────────────┘ │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
Screen: Home (UiState.Content)
│
account_switcher/ (chip_row h-scroll, padding top 16dp horizontal 16dp bottom 8dp)
├── account_chip[0] "Everyday Current"    (selected:  bg #C9E6FF text #004B6F radius 9999)
├── account_chip[1] "ISA Saver"           (unselected: outline #72787E text #41474D radius 9999)
└── account_chip[2] "Platinum Mastercard" (unselected: outline #72787E text #41474D radius 9999)
    on_click → selectAccount(accountId) — persists to DataStore, re-fetches balances+transactions

hero_balance_card/ (card bg #C9E6FF, elevation 2, radius 16dp, padding 24dp,
│                   margin h 16dp b 16dp; tappable → navigateToAccountDetail)
│  stack vertical gap 12dp:
├── row[type_icon] (stack horizontal alignment center_vertical):
│   ├── hero_account_subtype  (labelMedium 12sp/16sp w500 #004B6F): "CurrentAccount"
│   └── hero_account_icon     (icon account_balance 24dp #004B6F decorative)
├── hero_nickname     (titleLarge 22sp/28sp w400 #004B6F): "Everyday Current"
├── hero_balance      (displaySmall 36sp/44sp w400 #004B6F): "£2,847.63"
├── row[available] (stack horizontal gap 8dp alignment center_vertical):
│   ├── hero_available_label  (bodySmall 12sp/16sp w400 #004B6F): "Available"
│   └── hero_available_amount (bodySmall 12sp/16sp w400 #004B6F): "£2,847.63"
└── hero_identification (bodySmall 12sp/16sp w400 #004B6F): "40-05-15 12345678"

quick_actions_card/ (card bg surface #F7F9FF, elevation 1, radius 12dp, padding 16dp,
│                    margin h 16dp b 16dp)
│  stack horizontal gap 8dp alignment center_vertical:
├── action_pay/ (stack vertical center_horizontal gap 4dp weight 1, disabled)
│   ├── pay_button (icon_button send tonal 48dp×48dp disabled, bg #D3E5F5 dimmed alpha)
│   └── label "Pay" (labelSmall 11sp/16sp #41474D center) — PISP stub, taps silently ignored
├── action_transactions/ (stack vertical center_horizontal gap 4dp weight 1)
│   ├── transactions_button (icon_button receipt_long tonal 48dp×48dp bg #D3E5F5)
│   └── label "Transactions" (labelSmall 11sp/16sp #41474D center)
├── action_statements/ (stack vertical center_horizontal gap 4dp weight 1)
│   ├── statements_button (icon_button description tonal 48dp×48dp bg #D3E5F5)
│   └── label "Statements" (labelSmall 11sp/16sp #41474D center)
└── action_consents/ (stack vertical center_horizontal gap 4dp weight 1)
    ├── consents_button (icon_button shield tonal 48dp×48dp bg #D3E5F5)
    └── label "Consents" (labelSmall 11sp/16sp #41474D center)

recent_transactions_section/ (stack vertical gap 8dp, padding h 16dp b 16dp)
│
├── row[section_header] (stack horizontal alignment center_vertical):
│   ├── recent_tx_header (section_header titleSmall 14sp/20sp w500 #181C20 weight 1):
│   │                     "Recent transactions"
│   └── view_all_transactions_link (text_button labelMedium 12sp #266489): "View all"
│       on_click → navigateToTransactions(selectedAccountId)
│
└── recent_transactions_list/ (list no-scroll gap 4dp, items source: recentTransactions)
    ├── recent_tx_row[0] (card elev 0 radius 8dp padding v 12dp h 16dp)
    │   stack horizontal gap 16dp alignment center_vertical:
    │   ├── tx_category_icon (icon shopping_cart 24dp #50606E decorative)
    │   ├── stack vertical gap 4dp weight 1:
    │   │   ├── tx_description "AMAZON UK MARKETPLACE" (bodyMedium 14sp #181C20 maxLines 1 ellipsis)
    │   │   └── tx_date "27 Jun" (bodySmall 12sp #41474D)
    │   └── tx_amount "- £31.99" (bodyMedium 14sp #BA1A1A align end)
    │   on_click → navigateToTransactionDetail(TX-20260627-0002, 40051512345678)
    │
    ├── recent_tx_row[1] (card elev 0 radius 8dp)
    │   ├── tx_category_icon (icon restaurant 24dp #50606E)
    │   ├── tx_description "PRET A MANGER 083 LONDON" + tx_date "27 Jun"
    │   └── tx_amount "- £8.45" (#BA1A1A)
    │   on_click → navigateToTransactionDetail(TX-20260627-0001, 40051512345678)
    │
    ├── recent_tx_row[2] (card elev 0 radius 8dp)
    │   ├── tx_category_icon (icon local_grocery_store 24dp #50606E)
    │   ├── tx_description "TESCO STORES 3476 LONDON" + tx_date "26 Jun"
    │   └── tx_amount "- £42.17" (#BA1A1A)
    │   on_click → navigateToTransactionDetail(TX-20260626-0001, 40051512345678)
    │
    ├── recent_tx_row[3] (card elev 0 radius 8dp)
    │   ├── tx_category_icon (icon directions_bus 24dp #50606E)
    │   ├── tx_description "TFL TRAVEL CHARGE" + tx_date "26 Jun"
    │   └── tx_amount "- £6.80" (#BA1A1A)
    │   on_click → navigateToTransactionDetail(TX-20260626-0002, 40051512345678)
    │
    └── recent_tx_row[4] (card elev 0 radius 8dp)
        ├── tx_category_icon (icon work 24dp #50606E)
        ├── tx_description "SALARY ACME LTD" + tx_date "25 Jun"
        └── tx_amount "+ £2,400.00" (bodyMedium 14sp #266489 align end — credit colour)
        on_click → navigateToTransactionDetail(TX-20260625-0001, 40051512345678)

spending_snapshot_card/ (card bg #F7F9FF, elevation 1, radius 12dp, padding 16dp,
│                         margin h 16dp b 32dp; tappable → navigateToPfm)
│  stack horizontal gap 16dp alignment center_vertical:
├── stack vertical gap 4dp weight 1:
│   ├── spending_snapshot_header (titleSmall 14sp/20sp w500 #181C20): "Spending this month"
│   ├── spending_this_month (bodySmall 12sp/16sp w400 #41474D): "This month"
│   ├── spending_amount (headlineMedium 28sp/36sp w400 #BA1A1A): "£167.41"
│   └── spending_top_category (bodySmall 12sp/16sp w400 #41474D): "Top category: Groceries"
└── spending_chevron (icon chevron_right 24dp #41474D, accessibility: "View spending breakdown")

BottomNav/ (persistent)
├── Home         (selected, tint #266489)
├── Accounts     (default,  tint #41474D)
├── Transactions (default,  tint #41474D)
└── More         (default,  tint #41474D)
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│                                              │
│                                              │
│                                              │
│          [account_balance_wallet]            │  ← icon 48dp #41474D centred
│                                              │
│      No accounts connected yet              │  ← title headlineSmall 24sp #181C20 centred
│                                              │
│   Connect your bank via Open Banking        │
│   to see your balances and recent           │  ← body bodyMedium 14sp #41474D centred
│   transactions.                             │
│                                              │
│       [ Connect with Open Banking ]         │  ← connect_bank_button filled 56dp h
│                                              │    bg #266489 text #FFFFFF radius 9999
│                                              │
│                                              │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│
└─────────────────────────────────────────────┘
```

### Component Hierarchy — empty

```
Screen: Home (UiState.Empty — reason: no_accounts / no_consent)
│
empty_home/ (empty_state, vertically centered, padding horizontal 32dp)
│   accessibility_label: "No accounts connected yet"
│
├── icon  (account_balance_wallet 48dp #41474D, decorative: false,
│          contentDescription: "No accounts connected")
├── title (headlineSmall 24sp/32sp w400 #181C20 center):
│         "No accounts connected yet"
├── body  (bodyMedium 14sp/20sp w400 #41474D center):
│         "Connect your bank via Open Banking to see your balances and recent transactions."
└── connect_bank_button (button variant:filled, 56dp h, bg #266489 label-color #FFFFFF,
                         radius 9999, min touch 56dp)
    label: "Connect with Open Banking"
    accessibility_label: "Connect your bank account via Open Banking"
    on_click → navigateToLogin()

BottomNav/ (persistent — Home tab selected)
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│                                              │
│                                              │
│              [error_outline]                 │  ← icon 48dp #BA1A1A centred
│                                              │
│     Unable to load your accounts            │  ← title headlineSmall 24sp #181C20 centred
│                                              │
│   Your session has expired.                 │
│   Please sign in again.                     │  ← body bodyMedium 14sp #41474D centred
│                                             │     (dynamic: error.userMessage)
│                                              │    EC-HOME-001 demo: 401 token expired
│                                              │
│         [      Try again      ]              │  ← retry_button filled 56dp h #266489
│                                              │    visible_when: error.recoverable == true
│                                              │    (EC-HOME-001 401: shown)
│                                              │    (EC-HOME-002 403 non-recoverable: hidden)
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│
└─────────────────────────────────────────────┘
```

### Component Hierarchy — error

```
Screen: Home (UiState.Error — EC-HOME-001: code 401, recoverable: true)
│
error_home/ (error_state, vertically centered, padding horizontal 32dp)
│   accessibility_label: "Unable to load your accounts"
│
├── icon  (error_outline 48dp #BA1A1A, decorative: false,
│          contentDescription: "Error loading accounts")
├── title (headlineSmall 24sp/32sp w400 #181C20 center):
│         "Unable to load your accounts"
├── body  (bodyMedium 14sp/20sp w400 #41474D center):
│         "{error.userMessage}"
│         Demo render: "Your session has expired. Please sign in again."
│         EC-HOME-002 render: "Your consent doesn't include balance access. Manage consents to fix this."
└── retry_button (button variant:filled, 56dp h, bg #266489 label-color #FFFFFF,
                  radius 9999, visible_when: error.recoverable == true)
    label: "Try again"
    accessibility_label: "Retry loading your accounts"
    on_click → retryLoad() — re-issues GET /accounts + parallel GET /balances + GET /transactions

BottomNav/ (persistent — Home tab selected)
```

---

### Interaction Summary

| Component | Action | Effect | Target / Behaviour |
|---|---|---|---|
| account_chip | select_account | call_api | Persists chosen AccountId to DataStore; parallel re-fetch of balances + recent transactions for new account; transitions loading → content \| error |
| hero_balance_card | navigate_account_detail | navigate | account-detail screen (param: accountId = selectedAccountId) |
| pay_button | noop | none | Disabled PISP stub — tap produces no observable effect; shown greyed-out to signal future capability |
| transactions_button | navigate_transactions | navigate | transactions screen (param: accountId = selectedAccountId) |
| statements_button | navigate_statements | navigate | statements screen (param: accountId = selectedAccountId) |
| consents_button | navigate_consent_list | navigate | consent-list screen (no params) |
| recent_tx_row | navigate_transaction_detail | navigate | transaction-detail screen (params: transactionId, accountId) |
| view_all_transactions_link | navigate_transactions | navigate | transactions screen (param: accountId = selectedAccountId) |
| spending_snapshot_card | navigate_pfm | navigate | pfm-dashboard screen (no params — uses cached Room PFM data) |
| connect_bank_button (empty) | navigate_login | navigate | login screen — initiates FAPI Open Banking consent flow |
| retry_button (error) | retry_load | call_api | Re-issues full home load: GET /accounts then parallel GET /balances + GET /transactions; shown only when error.recoverable = true |

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| account_chip | hug content | 32dp | 9999dp (full pill) |
| hero_balance_card | match_parent − 32dp | wrap (~156dp) | 16dp |
| quick_actions_card | match_parent − 32dp | 80dp | 12dp |
| pay_button / action icon_buttons | 48dp | 48dp | 9999dp (circular tonal) |
| recent_tx_row | match_parent | 64dp | 8dp |
| spending_snapshot_card | match_parent − 32dp | wrap (~96dp) | 12dp |
| connect_bank_button | match_parent − 64dp | 56dp | 9999dp (full pill) |
| retry_button | match_parent − 64dp | 56dp | 9999dp (full pill) |
| skeleton_hero | match_parent − 32dp | 180dp | 16dp |
| skeleton_actions | match_parent − 32dp | 80dp | 12dp |
| skeleton_tx_{1,2,3} | match_parent | 64dp | 8dp |
| bottom_nav | match_parent | 80dp | 0 |
