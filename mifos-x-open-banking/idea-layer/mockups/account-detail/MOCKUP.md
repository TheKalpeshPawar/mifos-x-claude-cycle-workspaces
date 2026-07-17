# Account Detail — Visual Mockup

> Auto-generated from `screens/account-detail/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-17T00:00:00Z

---

## Screen: Account Detail

Canvas: 393×852dp (Pixel 5) · Top app bar visible (small variant, back leading, title = account nickname) · Bottom nav visible (Accounts contextually active — drill-down from accounts list) · No FAB · Roboto font · Material 3 light theme · bg #F7F9FF

Shell resolution (`app-shell.yaml` + `ui.yaml#shell` overrides):
- `top_app_bar_visible: true` · variant: small · leading: back (arrow_back icon) · title: "{account.Nickname}"
- `bottom_navigation_visible: true` · rail: Home | Accounts | Transactions | More · Accounts tab tint #266489 (contextually active)
- `fab_visible: false`
- Screen background: `surface` #F7F9FF

---

### State: loading

```
┌─────────────────────────────────────────────┐
│ ←                                           │  ← top_app_bar bg #F7F9FF h 64dp elevation 0
│   (title deferred — Nickname not loaded)    │    back_button icon arrow_back 24dp tint #181C20
│                                             │    min touch target 48dp × 48dp
├─────────────────────────────────────────────┤
│                                             │
│                                             │
│                                             │
│                                             │
│                                             │
│                                             │
│                    ◉                        │  ← loading_spinner circular 40dp × 40dp
│                                             │    color primary #266489
│                                             │    horizontally + vertically centred in
│                                             │    remaining canvas (852 − 64 − 80 = 708dp)
│                                             │
│                                             │
│                                             │
│                                             │
│                                             │
│                                             │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│  ← bottom_nav bg #F7F9FF h 80dp
│           ▲ #266489                         │    Accounts: indicator bg #C9E6FF tint #266489
└─────────────────────────────────────────────┘
```

### Component Hierarchy — loading

```
Screen: AccountDetail (AccountDetailUiState.Loading)
│
TopAppBar/ (small variant, bg #F7F9FF, h 64dp, elevation 0)
│   padding start 4dp (for icon_button), end 16dp
├── back_button  (icon_button icon: arrow_back 24dp, tint #181C20, min-touch 48dp × 48dp)
│   on_click → navigateBack() — pop AccountDetail from nav stack → accounts
└── title_text   (none — {account.Nickname} not yet resolved during loading)

loading_spinner/ (progress_indicator variant: circular, centred in remaining viewport)
│   size: 40dp × 40dp
│   stroke_color: primary #266489
│   stroke_width: 4dp
│   accessibility_label: "Loading account details"
│   reduce_motion: static filled arc (no animation)

BottomNav/ (persistent, always rendered across all states)
├── tab Home         (icon: home 24dp,           label: "Home",         tint #41474D)
├── tab Accounts     (icon: account_balance 24dp, label: "Accounts",    tint #266489  ACTIVE
│                     indicator pill bg #C9E6FF, label-color #266489)
├── tab Transactions (icon: receipt_long 24dp,    label: "Transactions", tint #41474D)
└── tab More         (icon: more_horiz 24dp,      label: "More",         tint #41474D → settings)
```

---

### State: content

```
┌─────────────────────────────────────────────┐
│ ←  Everyday Current                         │  ← top_app_bar bg #F7F9FF h 64dp elevation 0
│                                             │    back_button arrow_back 24dp tint #181C20
│                                             │    title titleLarge 22sp w400 #181C20
├─────────────────────────────────────────────┤
│                                             │
│ ┌─────────────────────────────────────────┐ │  ← account_header_card bg #EBEEF3 elevation 2
│ │  CurrentAccount                         │ │    radius 12dp, padding 16dp
│ │  Everyday Current                       │ │    margin h 16dp top 16dp bottom 8dp
│ │                                         │ │
│ │  40-05-15 12345678                      │ │    account_subtype_label  labelMedium #50606E
│ │                                         │ │    account_nickname       headlineMedium #181C20
│ │  GBP · MIDLGB2105V                     │ │    account_identification bodyMedium #41474D
│ │  Last updated 28 Jun 2026 18:30         │ │    account_currency/servicer labelSmall #41474D
│ └─────────────────────────────────────────┘ │    account_last_updated  labelSmall #41474D
│                                             │
│ ┌ · · · · · · · · · · · · · · · · · · · ┐  │  ← open_banking_badge card variant:outlined
│ │  🔒 Connected via UK Open Banking      │  │    border #72787E bg #F7F9FF elevation 0
│ └ · · · · · · · · · · · · · · · · · · · ┘  │    radius 8dp padding h 12dp v 8dp
│                                             │    margin h 16dp bottom 16dp
│  Balances                                   │  ← balances_header titleSmall 14sp #181C20
│                                             │    margin h 16dp bottom 4dp
│  ┌───────────────────────────────────────┐  │  ← balance_row[0] list_item bg #F1F4F9
│  │  InterimAvailable       2847.63 GBP   │  │    h 64dp radius 8dp padding h 16dp v 12dp
│  └───────────────────────────────────────┘  │    supporting_text labelMedium #41474D
│  ┌───────────────────────────────────────┐  │    trailing titleMedium 16sp #181C20
│  │  InterimBooked          2810.04 GBP   │  │  ← balance_row[1] same spec
│  └───────────────────────────────────────┘  │    margin gap 4dp between rows
│  ┌───────────────────────────────────────┐  │  ← balance_row[2]
│  │  OpeningBooked          3150.00 GBP   │  │
│  └───────────────────────────────────────┘  │
│                                             │
│  Explore                                    │  ← actions_header titleSmall 14sp #181C20
│                                             │    margin h 16dp top 16dp bottom 4dp
│  ← [🧾 Transactions][📄 Statements] →      │  ← action_chips chip_row horizontal scroll
│     [🔄 Standing Orders][💳 Direct Debits] │    gap 8dp, padding h 16dp bottom 24dp
│     [📅 Scheduled][👥 Beneficiaries]       │    each chip: bg #F1F4F9 border #72787E
│     [🏧 ATM & Branches][📋 Product]        │    radius 9999dp h 32dp label labelMedium #41474D
│     [👤 Party]                             │    icon 18dp #41474D, padding h 8dp
│                                             │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│
│           ▲ #266489                         │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
Screen: AccountDetail (AccountDetailUiState.Content)
│   account: 40051512345678  "Everyday Current"  balances: 3 items
│
TopAppBar/ (small variant, bg #F7F9FF, h 64dp, elevation 0)
├── back_button  (icon_button arrow_back 24dp, tint #181C20, min-touch 48dp × 48dp)
│   on_click → navigateBack() → accounts
└── title_text   (titleLarge 22sp/28sp w400 #181C20): "Everyday Current"

ScrollColumn/ (fillMaxSize, padding top 16dp h 16dp bottom 24dp,
│              scrollable vertically — chip row handles own h-scroll)
│
account_header_card/ (card bg #EBEEF3, elevation 2, radius 12dp, padding 16dp,
│                     margin bottom 8dp; non-interactive display)
│   accessibility_label: "Account: Everyday Current, CurrentAccount, 40-05-15 12345678"
│   stack vertical gap 8dp:
├── account_subtype_label   (labelMedium 12sp/16sp w500 #50606E): "CurrentAccount"
├── account_nickname        (headlineMedium 28sp/36sp w400 #181C20): "Everyday Current"
├── account_identification  (bodyMedium 14sp/20sp w400 #41474D, font Roboto Mono):
│                           "40-05-15 12345678"
├── row[currency_servicer]  (stack horizontal gap 8dp alignment center_vertical):
│   ├── account_currency    (labelSmall 11sp/16sp w500 #41474D): "GBP"
│   └── account_servicer   (bodySmall 12sp/16sp w400 #41474D): "MIDLGB2105V"
└── account_last_updated    (labelSmall 11sp/16sp w500 #41474D):
                            "Last updated 28 Jun 2026 18:30"

open_banking_badge/ (card variant:outlined, bg #F7F9FF, border #72787E, elevation 0,
│                    radius 8dp, padding h 12dp v 8dp, margin bottom 16dp)
│   accessibility_label: "Data sourced via regulated UK Open Banking AIS consent"
│   stack horizontal gap 8dp alignment center_vertical:
├── badge_lock_icon         (icon lock 16dp tint #266489, decorative: false,
│                            contentDescription: "Open Banking lock")
└── open_banking_badge_text (labelSmall 11sp/16sp w500 #266489):
                            "Connected via UK Open Banking"

balances_header/ (section_header margin bottom 4dp)
└── label (titleSmall 14sp/20sp w500 #181C20): "Balances"

balances_list/ (list vertical no-v-scroll, gap 4dp, items: balances[3])
│   accessibility_label: "Account balances, 3 items"
├── balance_row[0] (list_item bg #F1F4F9, radius 8dp, padding h 16dp v 12dp, h 64dp,
│                  margin bottom 4dp)
│   ├── leading_text        (labelMedium 12sp/16sp w500 #41474D): "InterimAvailable"
│   └── trailing_content    (titleMedium 16sp/24sp w500 #181C20): "2847.63 GBP"
│   accessibility_label: "Interim Available balance: 2847.63 GBP"
├── balance_row[1] (list_item bg #F1F4F9, radius 8dp, padding h 16dp v 12dp, h 64dp)
│   ├── leading_text        (labelMedium 12sp/16sp w500 #41474D): "InterimBooked"
│   └── trailing_content    (titleMedium 16sp/24sp w500 #181C20): "2810.04 GBP"
│   accessibility_label: "Interim Booked balance: 2810.04 GBP"
└── balance_row[2] (list_item bg #F1F4F9, radius 8dp, padding h 16dp v 12dp, h 64dp)
    ├── leading_text        (labelMedium 12sp/16sp w500 #41474D): "OpeningBooked"
    └── trailing_content    (titleMedium 16sp/24sp w500 #181C20): "3150.00 GBP"
    accessibility_label: "Opening Booked balance: 3150.00 GBP"

actions_header/ (section_header margin top 16dp bottom 4dp)
└── label (titleSmall 14sp/20sp w500 #181C20): "Explore"

action_chips/ (chip_row horizontal scroll, LazyRow gap 8dp,
│             padding h 16dp bottom 24dp, clip to content width 361dp visible then scroll)
│   accessibility_label: "Account actions, 9 options"
│   Note: 9 chips waivered as a single interactive group per M3 accessibility spec
│         (density dial 5 → waiver for chip_row sub-items)
├── chip_transactions     (chip bg #F1F4F9 border #72787E radius 9999 h 32dp
│                          icon receipt_long 18dp #41474D padding h 8dp gap 4dp
│                          label labelMedium 12sp w500 #41474D: "Transactions")
│   on_click → navigateTransactions(accountId: "40051512345678") → transactions
├── chip_statements       (chip bg #F1F4F9 border #72787E radius 9999 h 32dp
│                          icon description 18dp #41474D
│                          label: "Statements")
│   on_click → navigateStatements(accountId: "40051512345678") → statements
├── chip_standing_orders  (chip bg #F1F4F9 border #72787E radius 9999 h 32dp
│                          icon autorenew 18dp #41474D
│                          label: "Standing Orders")
│   on_click → navigateStandingOrders(accountId: "40051512345678") → standing-orders
├── chip_direct_debits    (chip bg #F1F4F9 border #72787E radius 9999 h 32dp
│                          icon subscriptions 18dp #41474D
│                          label: "Direct Debits")
│   on_click → navigateDirectDebits(accountId: "40051512345678") → direct-debits
├── chip_scheduled_payments (chip bg #F1F4F9 border #72787E radius 9999 h 32dp
│                            icon schedule 18dp #41474D
│                            label: "Scheduled")
│   on_click → navigateScheduledPayments(accountId: "40051512345678") → scheduled-payments
├── chip_beneficiaries    (chip bg #F1F4F9 border #72787E radius 9999 h 32dp
│                          icon people 18dp #41474D
│                          label: "Beneficiaries")
│   on_click → navigateBeneficiaries(accountId: "40051512345678") → beneficiaries
├── chip_atm_locator      (chip bg #F1F4F9 border #72787E radius 9999 h 32dp
│                          icon atm 18dp #41474D
│                          label: "ATM & Branches")
│   on_click → navigateAtmLocator(accountId: "40051512345678") → atm-locator
├── chip_product          (chip bg #F1F4F9 border #72787E radius 9999 h 32dp
│                          icon description 18dp #41474D
│                          label: "Product")
│   on_click → navigateProduct(accountId: "40051512345678") → product
└── chip_party            (chip bg #F1F4F9 border #72787E radius 9999 h 32dp
                           icon person 18dp #41474D
                           label: "Party")
    on_click → navigateParty(accountId: "40051512345678") → party

BottomNav/ (persistent)
├── tab Home         (icon: home 24dp,           label: "Home",         tint #41474D)
├── tab Accounts     (icon: account_balance 24dp, label: "Accounts",    tint #266489 ACTIVE
│                     indicator pill bg #C9E6FF 64dp × 32dp, label #266489)
├── tab Transactions (icon: receipt_long 24dp,    label: "Transactions", tint #41474D)
└── tab More         (icon: more_horiz 24dp,      label: "More",         tint #41474D)
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│ ←  Euro Wallet                              │  ← top_app_bar bg #F7F9FF h 64dp
│                                             │    title "Euro Wallet" (empty_scenario.account)
│                                             │    back_button arrow_back 24dp tint #181C20
├─────────────────────────────────────────────┤
│                                             │
│ ┌─────────────────────────────────────────┐ │  ← account_header_card bg #EBEEF3 elevation 2
│ │  GlobalWallet                           │ │    radius 12dp, padding 16dp
│ │  Euro Wallet                            │ │    margin h 16dp top 16dp bottom 8dp
│ │                                         │ │    (same structure as content state
│ │  40-05-15 99999999                      │ │     but for the empty-scenario account)
│ │                                         │ │
│ │  EUR · MIDLGB2105V                     │ │    account_subtype_label  labelMedium #50606E
│ │  Last updated 28 Jun 2026 12:00         │ │    account_nickname       headlineMedium #181C20
│ └─────────────────────────────────────────┘ │    account_identification bodyMedium #41474D
│                                             │    account_last_updated   labelSmall #41474D
│ ┌ · · · · · · · · · · · · · · · · · · · ┐  │  ← open_banking_badge outlined
│ │  🔒 Connected via UK Open Banking      │  │    border #72787E bg #F7F9FF elevation 0
│ └ · · · · · · · · · · · · · · · · · · · ┘  │    margin h 16dp bottom 16dp
│                                             │
│                                             │
│         [account_balance_wallet]            │  ← balances_empty_state icon 48dp tint #41474D
│                                             │    variant: info, centred in remaining space
│    No balance data available                │  ← title headlineSmall 24sp #181C20 centred
│                                             │
│  No balance information is available        │
│  for this account. This may occur for       │  ← body bodyMedium 14sp #41474D centred
│  sub-accounts or wallet accounts.           │    padding h 32dp from screen edge
│                                             │
│                                             │
│                                             │
│                                             │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│
│           ▲ #266489                         │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — empty

```
Screen: AccountDetail (AccountDetailUiState.Empty)
│   account: 40051599999999  "Euro Wallet"  GlobalWallet  EUR  balances: []
│
TopAppBar/ (small variant, bg #F7F9FF, h 64dp, elevation 0)
├── back_button  (icon_button arrow_back 24dp, tint #181C20, min-touch 48dp × 48dp)
│   on_click → navigateBack() → accounts
└── title_text   (titleLarge 22sp/28sp w400 #181C20): "Euro Wallet"

ScrollColumn/ (padding top 16dp h 16dp bottom 24dp)
│
account_header_card/ (card bg #EBEEF3, elevation 2, radius 12dp, padding 16dp, margin bottom 8dp)
│   accessibility_label: "Account: Euro Wallet, GlobalWallet, 40-05-15 99999999"
│   stack vertical gap 8dp:
├── account_subtype_label   (labelMedium 12sp/16sp w500 #50606E): "GlobalWallet"
├── account_nickname        (headlineMedium 28sp/36sp w400 #181C20): "Euro Wallet"
├── account_identification  (bodyMedium 14sp/20sp w400 #41474D, Roboto Mono):
│                           "40-05-15 99999999"
├── row[currency_servicer]:
│   ├── account_currency    (labelSmall 11sp/16sp w500 #41474D): "EUR"
│   └── account_servicer   (bodySmall 12sp/16sp w400 #41474D): "MIDLGB2105V"
└── account_last_updated    (labelSmall 11sp/16sp w500 #41474D):
                            "Last updated 28 Jun 2026 12:00"

open_banking_badge/ (card outlined bg #F7F9FF border #72787E, elevation 0,
│                    radius 8dp, padding h 12dp v 8dp, margin bottom 16dp)
└── row (icon lock 16dp #266489 + labelSmall 11sp w500 #266489):
    "Connected via UK Open Banking"

balances_empty_state/ (empty_state variant:info, vertically centred in remaining viewport space,
│                      padding h 32dp from screen edge)
│   accessibility_label: "No balance data available for this account"
├── icon  (account_balance_wallet 48dp, tint #41474D, decorative: false,
│          contentDescription: "No balance information")
├── title (headlineSmall 24sp/32sp w400 #181C20 align center):
│         "No balance data available"
└── body  (bodyMedium 14sp/20sp w400 #41474D align center):
          "No balance information is available for this account.
           This may occur for sub-accounts or wallet accounts."

BottomNav/ (persistent — Accounts tab active #266489)
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│ ←                                           │  ← top_app_bar bg #F7F9FF h 64dp
│   (title absent — load failed pre-resolve)  │    back_button arrow_back 24dp tint #181C20
├─────────────────────────────────────────────┤
│                                             │
│                                             │
│                                             │
│              [error_outline]                │  ← error_state icon 48dp tint #BA1A1A centred
│                                             │    decorative: false
│                                             │
│    Something went wrong                     │  ← title headlineSmall 24sp #181C20 centred
│                                             │
│   Session expired. Please log in again.     │  ← body bodyMedium 14sp #41474D centred
│                                             │    demo: EC 401 TokenExpiredError recoverable
│                                             │
│                                             │
│       [     Try again      ]                │  ← retry_button filled h 56dp radius 9999
│                                             │    bg #266489 label-color #FFFFFF
│                                             │    visible_when: error.recoverable == true
│                                             │    hidden for 403 ConsentWithdrawn / 404 NotFound
│                                             │
│                                             │
│                                             │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│
│           ▲ #266489                         │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — error

```
Screen: AccountDetail (AccountDetailUiState.Error)
│   Demo: EC-401 TokenExpiredError — recoverable: true
│   EC-403 ConsentWithdrawnError   — recoverable: false (retry_button hidden)
│   EC-404 AccountNotFoundError    — recoverable: false (retry_button hidden)
│   EC-network NetworkError        — recoverable: true
│
TopAppBar/ (small variant, bg #F7F9FF, h 64dp, elevation 0)
├── back_button  (icon_button arrow_back 24dp, tint #181C20, min-touch 48dp × 48dp)
│   on_click → navigateBack() → accounts
└── title_text   (none — account.Nickname not resolved before error)

error_state/ (empty_state variant:error, vertically + horizontally centred in
│             remaining viewport 708dp, padding h 32dp)
│   accessibility_label: "Error loading account details"
├── icon  (error_outline 48dp, tint #BA1A1A, decorative: false,
│          contentDescription: "Error loading account")
├── title (headlineSmall 24sp/32sp w400 #181C20 align center):
│         "Something went wrong"
├── body  (bodyMedium 14sp/20sp w400 #41474D align center):
│         "{error.message}"
│         EC-401 render: "Session expired. Please log in again."
│         EC-403 render: "Access to this account has been withdrawn."
│         EC-404 render: "Account not found in your authorised account set."
│         EC-network render: "No network connection. Please check your connection and retry."
└── retry_button (button variant:filled, h 56dp, bg #266489, label #FFFFFF,
                  radius 9999, min-touch 56dp, width match_parent − 64dp = 265dp,
                  visible_when: error.recoverable == true)
    label: "Try again"
    accessibility_label: "Retry loading account details"
    on_click → retryLoad() — re-issues parallel GET /accounts/{id} + GET /accounts/{id}/balances;
               transitions Error → Loading → Content | Error

BottomNav/ (persistent — Accounts tab active #266489)
```

---

### Interaction Summary

| Component | Action | Effect | Target / Behaviour |
|---|---|---|---|
| back_button | navigate_back | navigate | Pop AccountDetail from nav stack; return to accounts list screen |
| chip_transactions | navigate_transactions | navigate | transactions screen, param accountId = 40051512345678 |
| chip_statements | navigate_statements | navigate | statements screen, param accountId = 40051512345678 |
| chip_standing_orders | navigate_standing_orders | navigate | standing-orders screen, param accountId = 40051512345678 |
| chip_direct_debits | navigate_direct_debits | navigate | direct-debits screen, param accountId = 40051512345678 |
| chip_scheduled_payments | navigate_scheduled_payments | navigate | scheduled-payments screen, param accountId = 40051512345678 |
| chip_beneficiaries | navigate_beneficiaries | navigate | beneficiaries screen, param accountId = 40051512345678 |
| chip_atm_locator | navigate_atm_locator | navigate | atm-locator screen, param accountId = 40051512345678 |
| chip_product | navigate_product | navigate | product screen, param accountId = 40051512345678 (triggers GET /accounts/{id}/product on product screen mount) |
| chip_party | navigate_party | navigate | party screen, param accountId = 40051512345678 (triggers GET /accounts/{id}/party on party screen mount) |
| retry_button (error, recoverable) | retry_load | call_api | Re-issues parallel GET /accounts/{id} + GET /accounts/{id}/balances; transitions Loading → Content \| Error; visible only when error.recoverable == true |

---

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| top_app_bar | match_parent 393dp | 64dp | 0 |
| bottom_nav | match_parent 393dp | 80dp | 0 |
| back_button (touch target) | 48dp | 48dp | 9999dp (circular) |
| account_header_card | match_parent − 32dp = 361dp | wrap ~160dp | 12dp |
| open_banking_badge | match_parent − 32dp = 361dp | wrap ~40dp | 8dp |
| balances_header | match_parent − 32dp = 361dp | 20dp | 0 |
| balance_row[0..2] | match_parent − 32dp = 361dp | 64dp | 8dp |
| actions_header | match_parent − 32dp = 361dp | 20dp | 0 |
| chip (each) | hug content min 80dp | 32dp | 9999dp (full pill) |
| chip icon | 18dp | 18dp | n/a |
| loading_spinner | 40dp | 40dp | n/a (circular) |
| balances_empty_state icon | 48dp | 48dp | n/a |
| error_state icon | 48dp | 48dp | n/a |
| retry_button | match_parent − 64dp = 265dp | 56dp | 9999dp (full pill) |
| action_chips chip_row (visible width) | match_parent − 32dp = 361dp | 32dp | n/a (h-scrollable) |
