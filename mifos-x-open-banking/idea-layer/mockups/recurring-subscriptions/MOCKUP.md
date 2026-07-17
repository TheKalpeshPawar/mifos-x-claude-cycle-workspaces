# Recurring Payments — Visual Mockup

> Auto-generated from `screens/recurring-subscriptions/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-16T00:00:00Z

---

## Screen: Recurring Payments

Canvas: 393×852dp (Pixel 5) · Top app bar visible (title: "Recurring Payments", leading: back) · Bottom nav visible · No FAB · Roboto font · Material 3 light theme · bg #F7F9FF

Shell resolved from `app-shell.yaml` + `ui.yaml#shell` overrides:
- Top app bar: visible, variant: small, h 64dp, bg #F7F9FF, title "Recurring Payments" (titleLarge 22sp #181C20), leading: arrow_back icon 24dp #181C20
- Bottom navigation: Home (home) | Accounts (account_balance) | Transactions (receipt_long) | More (more_horiz) — none selected on this sub-screen
- FAB: hidden (`fab_visible: false`)

---

### State: loading

```
┌─────────────────────────────────────────────┐
│ ←  Recurring Payments                       │  ← top_app_bar bg #F7F9FF h 64dp
│                                             │    back_button arrow_back 24dp #181C20
├─────────────────────────────────────────────┤    title titleLarge 22sp/28sp w400 #181C20
│                                             │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │  ← shimmer_row_1 72dp h, radius 8dp
│                                             │    bg #DDE3EA → #E5E8ED pulse 1.5s ease
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │  ← shimmer_row_2 72dp h, radius 8dp
│                                             │    margin horizontal 16dp, gap 8dp
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │  ← shimmer_row_3 72dp h, radius 8dp
│                                             │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │  ← shimmer_row_4 72dp h, radius 8dp
│                                             │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │  ← shimmer_row_5 72dp h, radius 8dp
│                                             │
│                                             │
│                                             │
│                                             │
│                                             │
│                                             │
│                                             │
│                                             │
│                                             │
│                                             │
├─────────────────────────────────────────────┤
│ ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More │  ← bottom_nav bg #F7F9FF h 80dp
└─────────────────────────────────────────────┘
```

### Component Hierarchy — loading

```
Screen: Recurring Payments (UiState.Loading)
│
TopAppBar/ (variant:small bg #F7F9FF elevation 0 h 64dp)
├── leading: back_button (icon arrow_back 24dp #181C20 min-touch 48dp)
│   accessibility_label: "Navigate back"
└── title: "Recurring Payments" (titleLarge 22sp/28sp w400 #181C20)

loading_skeleton/ (stack vertical gap 8dp padding top 16dp horizontal 16dp bottom 16dp)
│   accessibility_label: "Loading recurring payments"  [sr-only]
│   reduce-motion: static fill #DDE3EA, no pulse animation
│
├── shimmer_row_1 (shimmer variant:list_item 72dp h radius 8dp bg #DDE3EA pulse 1.5s)
├── shimmer_row_2 (shimmer variant:list_item 72dp h radius 8dp bg #DDE3EA pulse 1.5s)
├── shimmer_row_3 (shimmer variant:list_item 72dp h radius 8dp bg #DDE3EA pulse 1.5s)
├── shimmer_row_4 (shimmer variant:list_item 72dp h radius 8dp bg #DDE3EA pulse 1.5s)
└── shimmer_row_5 (shimmer variant:list_item 72dp h radius 8dp bg #DDE3EA pulse 1.5s)
    each row: width match_parent (361dp at 16dp margins), gap 8dp between rows

BottomNav/ (persistent, h 80dp bg #F7F9FF)
├── tab Home         (icon:home,          label:"Home",         default tint #41474D)
├── tab Accounts     (icon:account_balance,label:"Accounts",    default tint #41474D)
├── tab Transactions (icon:receipt_long,  label:"Transactions", default tint #41474D)
└── tab More         (icon:more_horiz,    label:"More",         default tint #41474D)
```

---

### State: content

```
┌─────────────────────────────────────────────┐
│ ←  Recurring Payments                       │  ← top_app_bar bg #F7F9FF h 64dp
├─────────────────────────────────────────────┤
│                                             │
│ ┌─────────────────────────────────────────┐ │  ← detected_notice banner bg #DDE3EA
│ │ ℹ  Detected by analysing your past     │ │    icon info_outline 20dp #41474D
│ │    transactions. Not from the bank.    │ │    bodyMedium 14sp #41474D padding 12dp
│ └─────────────────────────────────────────┘ │    radius 12dp margin h 16dp v 8dp
│                                             │
│ ┌─────────────────────────────────────────┐ │  ← summary_card bg #F7F9FF elev 1
│ │  Estimated monthly spend                │ │    radius 12dp padding 16dp
│ │                                         │ │    margin h 16dp b 8dp
│ │  £85.93                                 │ │  ← summary_amount headlineMedium 28sp #BA1A1A
│ │  7 subscriptions detected              │ │  ← summary_count bodySmall 12sp #41474D
│ └─────────────────────────────────────────┘ │    summary_label labelMedium 12sp #50606E
│                                             │
│  ↻  PureGym                     £24.99     │  ← subscription_row[0]
│     Monthly · Next 15 Jul 2026              │    icon autorenew 24dp #266489
│     [Detected]                             │    detected_badge chip #EBEEF3
│  ↻  Spotify                     £11.99     │  ← subscription_row[1]
│     Monthly · Next 12 Jul 2026              │    label titleMedium 16sp #181C20
│     [Detected]                             │    supporting bodySmall 12sp #41474D
│  ↻  Adobe Lightroom            £143.88     │  ← subscription_row[2] Annual cadence
│     Annual · Next 14 Dec 2026              │    amount = full annual charge
│     [Detected]                             │
│  ↻  Netflix                     £10.99     │  ← subscription_row[3]
│     Monthly · Next 8 Jul 2026              │
│     [Detected]                             │
│  ↻  Amazon Prime                 £8.99     │  ← subscription_row[4]
│     Monthly · Next 20 Jul 2026             │
│     [Detected]                             │
│  ↻  Apple TV+                    £8.99     │  ← subscription_row[5]
│     Monthly · Next 1 Jul 2026              │
│     [Detected]                             │
│  ↻  Disney+                      £7.99     │  ← subscription_row[6]
│     Monthly · Next 3 Jul 2026              │    trailing bodyMedium 14sp #181C20
│     [Detected]                             │
├─────────────────────────────────────────────┤
│ ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
Screen: Recurring Payments (UiState.Content — 7 subscriptions, total £85.93/mo)
│
TopAppBar/ (variant:small bg #F7F9FF elevation 0 h 64dp)
├── leading: back_button (icon arrow_back 24dp #181C20 min-touch 48dp)
└── title: "Recurring Payments" (titleLarge 22sp/28sp w400 #181C20)

LazyColumn/ (scrollable content body padding top 8dp bottom 24dp)
│
├── detected_notice/ (banner, horizontal stack padding 12dp gap 8dp,
│   │                 bg #DDE3EA radius 12dp margin h 16dp b 8dp width 361dp)
│   │   accessibility_label: "These payments were detected by analysing your transaction
│   │                         history. They are not bank-registered mandates."
│   ├── icon info_outline (20dp #41474D decorative)
│   └── message (bodyMedium 14sp/20sp w400 #41474D wrap):
│               "Detected by analysing your past transactions. Not from the bank."
│
├── summary_card/ (card bg #F7F9FF elevation 1 radius 12dp padding 16dp
│   │              margin h 16dp b 8dp width 361dp)
│   │  stack vertical gap 4dp:
│   ├── summary_label  (labelMedium 12sp/16sp w500 #50606E): "Estimated monthly spend"
│   ├── summary_amount (headlineMedium 28sp/36sp w400 #BA1A1A): "£85.93"
│   │   accessibility_label: "Total estimated monthly spend: £85.93 across 7 subscriptions"
│   └── summary_count  (bodySmall 12sp/16sp w400 #41474D): "7 subscriptions detected"
│
└── subscriptions_list/ (list vertical items_source:subscriptions sorted monthly_equivalent DESC)
    │
    ├── subscription_row[0]/ (list_item min-touch 72dp full-width
    │   │   on_click → navigateTransactions(merchant:"PureGym") effect:navigate target:transactions)
    │   ├── icon: autorenew (24dp #266489 leading)
    │   ├── stack vertical gap 2dp weight 1:
    │   │   ├── label (titleMedium 16sp/24sp w500 #181C20 maxLines:1 ellipsis): "PureGym"
    │   │   ├── supporting (bodySmall 12sp/16sp w400 #41474D): "Monthly · Next 15 Jul 2026"
    │   │   └── detected_badge (chip variant:assist bg #EBEEF3 radius 9999dp
    │   │                        padding h 8dp v 4dp h 24dp
    │   │                        label "Detected" labelSmall 11sp/16sp w500 #181C20
    │   │                        accessibility_label: "Detected by in-app analysis")
    │   └── trailing: "£24.99" (bodyMedium 14sp/20sp w400 #181C20 align:end)
    │   accessibility_label: "PureGym: £24.99 Monthly, next 15 Jul 2026"
    │
    ├── subscription_row[1]/ (on_click → navigateTransactions(merchant:"Spotify") effect:navigate)
    │   ├── icon: autorenew (24dp #266489)
    │   ├── label: "Spotify" / supporting: "Monthly · Next 12 Jul 2026" / detected_badge
    │   └── trailing: "£11.99" (#181C20)
    │   accessibility_label: "Spotify: £11.99 Monthly, next 12 Jul 2026"
    │
    ├── subscription_row[2]/ (on_click → navigateTransactions(merchant:"Adobe Lightroom") effect:navigate)
    │   ├── icon: autorenew (24dp #266489)
    │   ├── label: "Adobe Lightroom" / supporting: "Annual · Next 14 Dec 2026" / detected_badge
    │   └── trailing: "£143.88" (#181C20)   [full annual charge; "Annual" cadence provides context]
    │   accessibility_label: "Adobe Lightroom: £143.88 Annual, next 14 Dec 2026"
    │
    ├── subscription_row[3]/ (on_click → navigateTransactions(merchant:"Netflix") effect:navigate)
    │   ├── icon: autorenew (24dp #266489)
    │   ├── label: "Netflix" / supporting: "Monthly · Next 8 Jul 2026" / detected_badge
    │   └── trailing: "£10.99" (#181C20)
    │   accessibility_label: "Netflix: £10.99 Monthly, next 8 Jul 2026"
    │
    ├── subscription_row[4]/ (on_click → navigateTransactions(merchant:"Amazon Prime") effect:navigate)
    │   ├── icon: autorenew (24dp #266489)
    │   ├── label: "Amazon Prime" / supporting: "Monthly · Next 20 Jul 2026" / detected_badge
    │   └── trailing: "£8.99" (#181C20)
    │   accessibility_label: "Amazon Prime: £8.99 Monthly, next 20 Jul 2026"
    │
    ├── subscription_row[5]/ (on_click → navigateTransactions(merchant:"Apple TV+") effect:navigate)
    │   ├── icon: autorenew (24dp #266489)
    │   ├── label: "Apple TV+" / supporting: "Monthly · Next 1 Jul 2026" / detected_badge
    │   └── trailing: "£8.99" (#181C20)
    │   accessibility_label: "Apple TV+: £8.99 Monthly, next 1 Jul 2026"
    │
    └── subscription_row[6]/ (on_click → navigateTransactions(merchant:"Disney+") effect:navigate)
        ├── icon: autorenew (24dp #266489)
        ├── label: "Disney+" / supporting: "Monthly · Next 3 Jul 2026" / detected_badge
        └── trailing: "£7.99" (#181C20)
        accessibility_label: "Disney+: £7.99 Monthly, next 3 Jul 2026"

BottomNav/ (persistent h 80dp bg #F7F9FF)
├── tab Home         (icon:home,          label:"Home",         default tint #41474D)
├── tab Accounts     (icon:account_balance,label:"Accounts",    default tint #41474D)
├── tab Transactions (icon:receipt_long,  label:"Transactions", default tint #41474D)
└── tab More         (icon:more_horiz,    label:"More",         default tint #41474D)
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│ ←  Recurring Payments                       │  ← top_app_bar bg #F7F9FF h 64dp
├─────────────────────────────────────────────┤
│                                             │
│                                             │
│                                             │
│                                             │
│              [↻ autorenew]                 │  ← icon 48dp #41474D centred
│                                             │    contentDescription: "No recurring payments found"
│       No recurring payments                │  ← title headlineSmall 24sp/32sp #181C20
│           found                            │    centred, padding h 32dp
│                                             │
│  We didn't detect any recurring payment    │  ← body bodyMedium 14sp/20sp #41474D
│  patterns in your transactions. Once you   │    centred, padding h 32dp, max 6 lines
│  have more history, patterns such as       │
│  streaming, gym, and software              │
│  subscriptions will appear here.           │
│                                             │
│                                             │
│                                             │
│                                             │
├─────────────────────────────────────────────┤
│ ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — empty

```
Screen: Recurring Payments (UiState.Empty — EC-RS-001/EC-RS-002: insufficient recurrence patterns)
│
TopAppBar/ (variant:small bg #F7F9FF elevation 0 h 64dp)
├── leading: back_button (icon arrow_back 24dp #181C20 min-touch 48dp)
└── title: "Recurring Payments" (titleLarge 22sp/28sp w400 #181C20)

empty_state/ (stack vertical center_both padding h 32dp)
│   accessibility_label: "No recurring payments found. We didn't detect any recurring payment
│                         patterns in your transactions."
├── icon  (autorenew 48dp #41474D decorative:false
│          contentDescription: "No recurring payments found"
│          margin bottom 16dp)
├── title (headlineSmall 24sp/32sp w400 #181C20 align:center):
│         "No recurring payments found"
└── body  (bodyMedium 14sp/20sp w400 #41474D align:center margin top 8dp):
          "We didn't detect any recurring payment patterns in your transactions.
           Once you have more history, patterns such as streaming, gym, and software
           subscriptions will appear here."

BottomNav/ (persistent h 80dp bg #F7F9FF)
├── tab Home         (icon:home,          label:"Home",         default tint #41474D)
├── tab Accounts     (icon:account_balance,label:"Accounts",    default tint #41474D)
├── tab Transactions (icon:receipt_long,  label:"Transactions", default tint #41474D)
└── tab More         (icon:more_horiz,    label:"More",         default tint #41474D)
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│ ←  Recurring Payments                       │  ← top_app_bar bg #F7F9FF h 64dp
├─────────────────────────────────────────────┤
│                                             │
│                                             │
│                                             │
│                                             │
│            [error_outline]                 │  ← icon 48dp #BA1A1A centred
│                                             │    contentDescription: "Error loading"
│  Unable to load recurring payments        │  ← title headlineSmall 24sp/32sp #181C20
│                                             │    centred, padding h 32dp
│  We couldn't read your cached              │  ← body bodyMedium 14sp/20sp #41474D
│  transaction data. This may be a           │    centred, padding h 32dp
│  temporary issue — please try again.       │
│                                             │
│     [        Try again        ]            │  ← retry_button outlined 48dp h
│                                             │    border #72787E text #266489 radius 9999
│                                             │    min-touch 48dp width match_parent − 64dp
│                                             │    margin h 32dp top 24dp
│                                             │
├─────────────────────────────────────────────┤
│ ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — error

```
Screen: Recurring Payments (UiState.Error — EC-RS-003: DataStore IOException / deserialisation failure)
│
TopAppBar/ (variant:small bg #F7F9FF elevation 0 h 64dp)
├── leading: back_button (icon arrow_back 24dp #181C20 min-touch 48dp)
└── title: "Recurring Payments" (titleLarge 22sp/28sp w400 #181C20)

error_state/ (stack vertical center_both padding h 32dp)
│   accessibility_label: "Unable to load recurring payments. We couldn't read your
│                         cached transaction data."
├── icon  (error_outline 48dp #BA1A1A decorative:false
│          contentDescription: "Error loading recurring payments"
│          margin bottom 16dp)
├── title (headlineSmall 24sp/32sp w400 #181C20 align:center):
│         "Unable to load recurring payments"
└── body  (bodyMedium 14sp/20sp w400 #41474D align:center margin top 8dp):
          "We couldn't read your cached transaction data. This may be a temporary
           issue — please try again."

retry_button/ (button variant:outlined min-touch 48dp h match_parent − 64dp w
│              border 1dp #72787E text #266489 radius 9999
│              margin h 32dp top 24dp)
│   label: "Try again" (labelLarge 14sp/20sp w500 #266489)
│   accessibility_label: "Retry loading recurring payments"
│   on_click → retryLoadSubscriptions()
│     action: retry_load_subscriptions
│     effect: transform_state
│     description: "Re-runs recurring-payment detection over locally cached DataStore
│                   transactions; UiState resets to Loading → resolves to Content | Empty | Error.
│                   No network request issued."

BottomNav/ (persistent h 80dp bg #F7F9FF)
├── tab Home         (icon:home,          label:"Home",         default tint #41474D)
├── tab Accounts     (icon:account_balance,label:"Accounts",    default tint #41474D)
├── tab Transactions (icon:receipt_long,  label:"Transactions", default tint #41474D)
└── tab More         (icon:more_horiz,    label:"More",         default tint #41474D)
```

---

### Interaction Summary

| Component | Action | Effect | Target / Behaviour |
|---|---|---|---|
| back_button (all states) | navigate_back | navigate | Previous screen in back stack (e.g. pfm-dashboard) |
| subscription_row[0] PureGym | navigate_transactions | navigate | transactions screen — params: merchant="PureGym"; TransactionsViewModel applies case-insensitive contains filter |
| subscription_row[1] Spotify | navigate_transactions | navigate | transactions screen — params: merchant="Spotify" |
| subscription_row[2] Adobe Lightroom | navigate_transactions | navigate | transactions screen — params: merchant="Adobe Lightroom" |
| subscription_row[3] Netflix | navigate_transactions | navigate | transactions screen — params: merchant="Netflix" |
| subscription_row[4] Amazon Prime | navigate_transactions | navigate | transactions screen — params: merchant="Amazon Prime" |
| subscription_row[5] Apple TV+ | navigate_transactions | navigate | transactions screen — params: merchant="Apple TV+" |
| subscription_row[6] Disney+ | navigate_transactions | navigate | transactions screen — params: merchant="Disney+" |
| retry_button (error state) | retry_load_subscriptions | transform_state | In-place: UiState resets to Loading → re-runs recurring-payment detection algorithm over cached DataStore transactions → resolves to Content \| Empty \| Error. No network call. |

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| top_app_bar | match_parent (393dp) | 64dp | 0 |
| detected_notice banner | match_parent − 32dp (361dp) | ~56dp (hug) | 12dp |
| summary_card | match_parent − 32dp (361dp) | ~84dp (hug) | 12dp |
| subscription_row (× 7) | match_parent (393dp) | 72dp min | 0 |
| detected_badge chip | hug content (~72dp) | 24dp | 9999dp (full pill) |
| autorenew icon (list leading) | 24dp | 24dp | — |
| shimmer_row (× 5) | match_parent − 32dp (361dp) | 72dp | 8dp |
| autorenew icon (empty state) | 48dp | 48dp | — |
| error_outline icon | 48dp | 48dp | — |
| retry_button | match_parent − 64dp (265dp) | 48dp | 9999dp (full pill) |
| bottom_nav | match_parent (393dp) | 80dp | 0 |
