# Standing Orders — Visual Mockup

> Auto-generated from `screens/standing-orders/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-16T00:00:00Z

---

## Screen: Standing Orders

Canvas: 393×852dp (Pixel 5) · Top app bar (small, back leading) · Bottom nav visible · No FAB · Roboto font · Material 3 light theme · Background `surface` #F7F9FF

Shell (from `app-shell.yaml` + `ui.yaml#shell`):
- Top app bar: enabled, small variant, title "Standing Orders", leading icon `arrow_back` → pops to `account-detail`
- Bottom navigation: **Home | Accounts | Transactions | More** (icons: home / account_balance / receipt_long / more_horiz; "Accounts" tab in active hierarchy — this screen is a child of account-detail)
- FAB: disabled (`fab_visible: false` per `ui.yaml#shell`)
- Snackbar host: enabled, bottom position

---

### State: loading

```
┌─────────────────────────────────────────────┐
│ ← Standing Orders                            │  ← top_app_bar small, bg #F7F9FF elev 0
│                                              │    title titleLarge 22sp #181C20
├─────────────────────────────────────────────┤    back arrow_back 48dp tint #266489
│                                              │
│                                              │
│                                              │
│                    ◌                         │  ← progress_indicator circular
│                                              │    color primary #266489, size 40dp
│                                              │    anchored center of content area
│                                              │
│                                              │
│                                              │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More │  ← bottom_nav bg #F7F9FF h 80dp
└─────────────────────────────────────────────┘    ◫ Accounts tint #266489 (active context)
                                                    others tint #41474D
```

### Component Hierarchy — loading

```
Screen: Standing Orders (StandingOrdersUiState.Loading)
│
top_app_bar/ (small variant, bg surface #F7F9FF, elevation 0, h 64dp)
├── back_button (icon_button arrow_back, 48dp×48dp tint primary #266489)
│   on_click → navigateBack()  ─── pops to account-detail
└── title "Standing Orders" (titleLarge 22sp/28sp w400 #181C20, center)

progress_indicator/ (circular, size 40dp, color primary #266489, strokeWidth 4dp)
│   accessibility_label: "Loading standing orders"
│   layout: fillMaxSize, wrapContentSize(Alignment.Center)

BottomNav/ (persistent, bg #F7F9FF, elevation 3dp, h 80dp)
├── tab Home         (icon home          24dp, label "Home",         tint #41474D)
├── tab Accounts     (icon account_balance24dp, label "Accounts",    tint #266489 ← active context)
├── tab Transactions (icon receipt_long  24dp, label "Transactions", tint #41474D)
└── tab More         (icon more_horiz    24dp, label "More",         tint #41474D)
```

---

### State: content

```
┌─────────────────────────────────────────────┐
│ ← Standing Orders                            │  ← top_app_bar small, back #266489
├─────────────────────────────────────────────┤
│                                              │
│  4 Active · 1 Inactive                      │  ← summary_row labelMedium 12sp/16sp
│                                             │    #41474D, padding h 16dp v 8dp
│ ┌───────────────────────────────────────┐   │
│ │ Jameson Lettings           [Active]   │   │  ← SO-001 standing_order_card
│ │ £1,200.00 GBP                         │   │    elevation 1, radius 12dp, padding 16dp
│ │ Monthly on the 1st                    │   │    margin h 16dp, bottom 8dp
│ │ Next: 01 Jul 2026                     │   │    [Active] badge: bg #C9E6FF text #004B6F
│ │ 40-12-09 65872310                     │   │    headlineSmall 24sp on-surface #181C20
│ │ Ref: RENT-FLAT12                      │   │    bodySmall 12sp on-surface-variant #41474D
│ └───────────────────────────────────────┘   │    sort-code: Roboto Mono
│                                              │
│ ┌───────────────────────────────────────┐   │
│ │ ISA Saver                  [Active]   │   │  ← SO-002 standing_order_card
│ │ £200.00 GBP                           │   │
│ │ Monthly on the 1st                    │   │
│ │ Next: 01 Jul 2026                     │   │
│ │ 60-16-13 31926819                     │   │
│ │ Ref: ISA-TOPUP                        │   │
│ └───────────────────────────────────────┘   │
│                                              │
│ ┌───────────────────────────────────────┐   │
│ │ PureGym                    [Active]   │   │  ← SO-003 standing_order_card
│ │ £24.99 GBP                            │   │
│ │ Monthly on the 15th                   │   │
│ │ Next: 15 Jul 2026                     │   │
│ │ 20-00-00 55512345                     │   │
│ │ Ref: GYM-MBR                          │   │
│ └───────────────────────────────────────┘   │
│                                              │
│ ┌───────────────────────────────────────┐   │
│ │ Oxfam GB                 [Inactive]   │   │  ← SO-004 standing_order_card
│ │ £10.00 GBP                            │   │    [Inactive] badge: bg #D3E5F5 text #384956
│ │ Monthly on the 28th                   │   │    NextPaymentDateTime null → row omitted
│ │ Final: 28 Dec 2025                    │   │  ← so_final_date (hasFinalPayment=true)
│ │ 08-60-01 20321982                     │   │
│ │ Ref: CHARITY-DON                      │   │
│ └───────────────────────────────────────┘   │
│                                              │
│ ┌───────────────────────────────────────┐   │
│ │ Marcus Savings             [Active]   │   │  ← SO-005 standing_order_card
│ │ £50.00 GBP                            │   │
│ │ Weekly every Friday                   │   │
│ │ Next: 04 Jul 2026                     │   │
│ │ Final: 25 Dec 2026                    │   │  ← so_final_date (hasFinalPayment=true)
│ │ 30-96-22 41227714                     │   │
│ │ Ref: SAVINGS-SWEEP                    │   │
│ └───────────────────────────────────────┘   │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More │
└─────────────────────────────────────────────┘
  ↑ pull-to-refresh gesture on list triggers retry_load (LoadStandingOrders re-issued)
```

### Component Hierarchy — content

```
Screen: Standing Orders (StandingOrdersUiState.Content)
│   summaryLabel = "4 Active · 1 Inactive"
│
top_app_bar/ (small, bg #F7F9FF, elevation 0, h 64dp)
├── back_button (icon_button arrow_back 48dp×48dp tint #266489)
└── title "Standing Orders" (titleLarge 22sp #181C20)

summary_row/ (text labelMedium 12sp/16sp w500 #41474D)
│   value: "4 Active · 1 Inactive"
│   padding: horizontal 16dp, vertical 8dp
│   accessibility_label: "4 Active · 1 Inactive"

standing_orders_list/ (LazyColumn vertical, gap 8dp, padding h 16dp b 16dp)
│   pull_to_refresh: enabled, indicator color #266489
│   accessibility_label: "Standing orders list"
│
├── standing_order_card[SO-001] (Card elevation 1, radius 12dp, bg #FFFFFF)
│   │   padding 16dp, margin bottom 8dp
│   │   accessibility_label: "Standing order for Jameson Lettings"
│   │   stack vertical gap 4dp:
│   ├── row[name+badge] (stack horizontal, alignment center_vertical, gap 8dp)
│   │   ├── so_payee_name "Jameson Lettings" (titleMedium 16sp/24sp w500 #181C20, weight 1)
│   │   └── so_status_badge "Active" (AssistChip/Badge, bg #C9E6FF text #004B6F radius 9999 h 24dp)
│   ├── so_amount "£1,200.00 GBP" (headlineSmall 24sp/32sp w400 #181C20)
│   ├── so_frequency "Monthly on the 1st" (bodySmall 12sp/16sp w400 #41474D)
│   ├── so_next_date "Next: 01 Jul 2026" (bodySmall 12sp/16sp w400 #41474D)
│   │   [so_final_date hidden: hasFinalPayment=false]
│   ├── so_sort_code "40-12-09 65872310" (bodySmall 12sp/16sp w400 #41474D, Roboto Mono)
│   └── so_payment_ref "Ref: RENT-FLAT12" (bodySmall 12sp/16sp w400 #41474D)
│
├── standing_order_card[SO-002] (Card elevation 1, radius 12dp, bg #FFFFFF)
│   │   padding 16dp
│   ├── so_payee_name "ISA Saver" + so_status_badge "Active" (#C9E6FF / #004B6F)
│   ├── so_amount "£200.00 GBP"
│   ├── so_frequency "Monthly on the 1st"
│   ├── so_next_date "Next: 01 Jul 2026"
│   │   [so_final_date hidden: hasFinalPayment=false]
│   ├── so_sort_code "60-16-13 31926819"
│   └── so_payment_ref "Ref: ISA-TOPUP"
│
├── standing_order_card[SO-003] (Card elevation 1, radius 12dp, bg #FFFFFF)
│   │   padding 16dp
│   ├── so_payee_name "PureGym" + so_status_badge "Active" (#C9E6FF / #004B6F)
│   ├── so_amount "£24.99 GBP"
│   ├── so_frequency "Monthly on the 15th"
│   ├── so_next_date "Next: 15 Jul 2026"
│   │   [so_final_date hidden: hasFinalPayment=false]
│   ├── so_sort_code "20-00-00 55512345"
│   └── so_payment_ref "Ref: GYM-MBR"
│
├── standing_order_card[SO-004] (Card elevation 1, radius 12dp, bg #FFFFFF)
│   │   padding 16dp
│   ├── so_payee_name "Oxfam GB" + so_status_badge "Inactive" (#D3E5F5 / #384956)
│   ├── so_amount "£10.00 GBP"
│   ├── so_frequency "Monthly on the 28th"
│   │   [so_next_date omitted: NextPaymentDateTime=null]
│   ├── so_final_date "Final: 28 Dec 2025" (bodySmall #41474D, VISIBLE: hasFinalPayment=true)
│   ├── so_sort_code "08-60-01 20321982"
│   └── so_payment_ref "Ref: CHARITY-DON"
│
└── standing_order_card[SO-005] (Card elevation 1, radius 12dp, bg #FFFFFF)
    │   padding 16dp
    ├── so_payee_name "Marcus Savings" + so_status_badge "Active" (#C9E6FF / #004B6F)
    ├── so_amount "£50.00 GBP"
    ├── so_frequency "Weekly every Friday"
    ├── so_next_date "Next: 04 Jul 2026"
    ├── so_final_date "Final: 25 Dec 2026" (bodySmall #41474D, VISIBLE: hasFinalPayment=true)
    ├── so_sort_code "30-96-22 41227714"
    └── so_payment_ref "Ref: SAVINGS-SWEEP"

BottomNav/ (persistent, bg #F7F9FF, h 80dp)
├── Home         (icon home,           tint #41474D)
├── Accounts     (icon account_balance, tint #266489 ← active context)
├── Transactions (icon receipt_long,   tint #41474D)
└── More         (icon more_horiz,     tint #41474D)
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│ ← Standing Orders                            │  ← top_app_bar small, back #266489
├─────────────────────────────────────────────┤
│                                              │
│                                              │
│                                              │
│               [autorenew]                    │  ← icon autorenew 48dp #41474D centred
│                                              │    contentDescription: "No standing orders"
│       No standing orders                    │  ← title headlineSmall 24sp/32sp #181C20
│                                              │    centred, padding h 32dp
│  No standing orders are set up for          │  ← body bodyMedium 14sp/20sp #41474D
│  this account.                              │    centred, padding h 32dp
│                                              │
│                                              │
│                                              │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — empty

```
Screen: Standing Orders (StandingOrdersUiState.Empty)
│
top_app_bar/ (small, bg #F7F9FF, elevation 0, h 64dp)
├── back_button (icon_button arrow_back 48dp×48dp tint #266489)
└── title "Standing Orders" (titleLarge 22sp #181C20)

empty_standing_orders/ (empty_state, fillMaxSize, vertically centered, padding h 32dp)
│   accessibility_label: "No standing orders are set up for this account"
│   stack vertical gap 16dp, alignment center_horizontal:
│
├── icon  (autorenew 48dp, tint #41474D, decorative: false)
│         contentDescription: "No standing orders"
├── title (headlineSmall 24sp/32sp w400 #181C20, textAlign Center):
│         "No standing orders"
└── body  (bodyMedium 14sp/20sp w400 #41474D, textAlign Center):
          "No standing orders are set up for this account."

BottomNav/ (persistent, bg #F7F9FF, h 80dp)
├── Home         (icon home,           tint #41474D)
├── Accounts     (icon account_balance, tint #266489 ← active context)
├── Transactions (icon receipt_long,   tint #41474D)
└── More         (icon more_horiz,     tint #41474D)
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│ ← Standing Orders                            │  ← top_app_bar small, back #266489
├─────────────────────────────────────────────┤
│                                              │
│                                              │
│             [error_outline]                  │  ← icon error_outline 48dp #BA1A1A
│                                              │    contentDescription: "Error loading orders"
│   Unable to load standing orders            │  ← title headlineSmall 24sp/32sp #181C20
│                                              │    centred, padding h 32dp
│  Session expired. Please log in again.      │  ← body bodyMedium 14sp/20sp #41474D
│  (demo: TokenExpiredError — HTTP 401)       │    centred, padding h 32dp
│                                              │    actual: {error.message} from ViewModel
│                                              │
│       [        Try again         ]           │  ← retry_button filled, bg #266489
│                                              │    label text #FFFFFF labelLarge 14sp
│                                              │    h 48dp, radius 9999, padding h 24dp
│                                              │    min touch 48dp
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — error

```
Screen: Standing Orders (StandingOrdersUiState.Error — demo: TokenExpiredError, recoverable)
│
top_app_bar/ (small, bg #F7F9FF, elevation 0, h 64dp)
├── back_button (icon_button arrow_back 48dp×48dp tint #266489)
└── title "Standing Orders" (titleLarge 22sp #181C20)

error_state/ (empty_state variant:error, fillMaxSize, vertically centered, padding h 32dp)
│   accessibility_label: "Unable to load standing orders"
│   stack vertical gap 16dp, alignment center_horizontal:
│
├── icon  (error_outline 48dp, tint error #BA1A1A, decorative: false)
│         contentDescription: "Error loading standing orders"
├── title (headlineSmall 24sp/32sp w400 #181C20, textAlign Center):
│         "Unable to load standing orders"
├── body  (bodyMedium 14sp/20sp w400 #41474D, textAlign Center):
│         "{error.message}"
│         Demo (EC-SO-001 401): "Session expired. Please log in again."
│         EC-SO-002 403:        "Account access consent has been revoked."
│         EC-SO-003 429:        "Too many requests. Please wait a moment and try again."
│         EC-SO-004 network:    "No network connection. Check your connection and retry."
│         EC-SO-005 5xx:        "Something went wrong. Please try again later."
│
└── retry_button (Button variant:filled, bg #266489, label-color #FFFFFF)
    │   label "Try again", labelLarge 14sp/20sp w500
    │   h 48dp, radius 9999, padding h 24dp, min touch 48dp
    │   margin top 8dp
    on_click → retryLoad()  ─── re-invokes LoadStandingOrders(accountId)
                                 transitions to Loading then Content | Empty | Error

BottomNav/ (persistent, bg #F7F9FF, h 80dp)
├── Home         (icon home,           tint #41474D)
├── Accounts     (icon account_balance, tint #266489 ← active context)
├── Transactions (icon receipt_long,   tint #41474D)
└── More         (icon more_horiz,     tint #41474D)
```

---

### Interaction Summary

| Component | Action | Effect | Target / Behaviour |
|---|---|---|---|
| back_button | navigate_back | navigate | Pops standing-orders from back stack; returns to `account-detail` |
| standing_orders_list (pull-to-refresh) | retry_load | call_api | Re-issues GET /accounts/{AccountId}/standing-orders via ktorfit; transitions Loading → Content \| Empty \| Error |
| retry_button (error state) | retry_load | call_api | Re-invokes LoadStandingOrders with same accountId via ktorfit (hsbc-obie-ais-v4.0); transitions Loading → Content \| Empty \| Error |

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| top_app_bar | match_parent (393dp) | 64dp | 0dp |
| progress_indicator | 40dp | 40dp | 9999dp (circle) |
| summary_row | match_parent | 32dp | 0dp |
| standing_orders_list | match_parent | fill_remaining | 0dp (container) |
| standing_order_card | match_parent − 32dp (361dp) | wrap (~160dp standard / ~180dp with final_date row) | 12dp (medium) |
| so_status_badge | hug content | 24dp | 9999dp (pill) |
| so_amount text | match_parent | 32dp | 0dp |
| retry_button | match_parent − 64dp (~265dp) | 48dp | 9999dp (pill) |
| empty / error icon | 48dp | 48dp | — |
| bottom_nav | match_parent (393dp) | 80dp | 0dp |
