# Scheduled Payments — Visual Mockup

> Auto-generated from `screens/scheduled-payments/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-16T00:00:00Z

---

## Screen: Scheduled Payments

Canvas: 393×852dp (Pixel 5) · Top app bar (small, 64dp, back leading) visible · Bottom nav visible · No FAB · Roboto / Roboto Mono · Material 3 light theme · Background #F7F9FF

Shell (from `ui.yaml#shell` + `app-shell.yaml`):
Top app bar (small, 64dp) — title "Scheduled Payments" (resolved from `strings.sp_screen_title`), leading: arrow_back icon button → navigate to `account-detail`. Top bar bg `surfaceContainer` #EBEEF3.
Bottom navigation — **Home | Accounts | Transactions | More** (icons: home / account_balance / receipt_long / more_horiz; "More" targets settings). Accounts tab active (selected tint #266489) — this screen is a sub-screen of the accounts flow.
FAB disabled per `ui.yaml#shell.fab_visible: false`.

---

### State: loading

```
┌─────────────────────────────────────────────┐
│ ←  Scheduled Payments                       │  ← top_app_bar bg #EBEEF3 h 64dp
│                                             │    title titleLarge 22sp #181C20 w400
│                                             │    back_button arrow_back 48dp tint #266489
├─────────────────────────────────────────────┤
│                                             │
│                                             │
│                                             │
│                                             │
│                     ◌                       │  ← progress_indicator circular 48dp
│                                             │    indeterminate, tint primary #266489
│                                             │    centred in content area (393×708dp)
│                                             │    reduce-motion: static fill, no animation
│                                             │
│                                             │
│                                             │
│                                             │
│                                             │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│  ← bottom_nav bg #F7F9FF h 80dp
│           ─────────                         │    Accounts: selected indicator tint #266489
└─────────────────────────────────────────────┘
```

### Component Hierarchy — loading

```
Screen: Scheduled Payments (ScheduledPaymentsUiState.Loading)
│
TopAppBar/ (small variant, h 64dp, bg #EBEEF3 surfaceContainer, elevation 0)
├── back_button  (icon_button arrow_back, 48dp×48dp touch-target, tint primary #266489)
│               accessibility_label: "Navigate back"
│               on_click → navigate_back: pops scheduled-payments → account-detail
└── title        (titleLarge 22sp/28sp w400 #181C20): "Scheduled Payments"
│
progress_indicator/ (circular, indeterminate, centred both axes in content area)
│   diameter 48dp, stroke 4dp, tint primary #266489
│   accessibility_label: "Loading scheduled payments" (strings.sp_loading_a11y)
│   (reduce-motion override: static fill, no rotation animation)
│
BottomNav/ (persistent, h 80dp, bg surfaceBright #F7F9FF)
├── tab Home         (icon: home 24dp,          label: "Home",         default,  tint onSurfaceVariant #41474D)
├── tab Accounts     (icon: account_balance 24dp,label: "Accounts",    selected, tint primary #266489, active indicator)
├── tab Transactions (icon: receipt_long 24dp,  label: "Transactions", default,  tint onSurfaceVariant #41474D)
└── tab More         (icon: more_horiz 24dp,    label: "More",         default,  tint onSurfaceVariant #41474D)
```

---

### State: content

```
┌─────────────────────────────────────────────┐
│ ←  Scheduled Payments                       │  ← top_app_bar bg #EBEEF3 h 64dp
├─────────────────────────────────────────────┤  (scrollable list below; 4 cards > 708dp)
│                                             │
│ ┌─────────────────────────────────────────┐ │  ── scheduled_payment_card [SP-001] ──
│ │  HMRC Self Assessment                   │ │  ← sp_payee_name: titleMedium 16sp/24sp
│ │                                         │ │    w500 onSurface #181C20
│ │  GBP 842.00                             │ │  ← sp_amount: headlineSmall 24sp/32sp
│ │                                         │ │    w400 error #BA1A1A  Roboto Mono
│ │  Due: Fri 31 Jul 2026                   │ │  ← sp_scheduled_date: bodySmall 12sp/16sp
│ │                                         │ │    w400 onSurfaceVariant #41474D
│ │  [🗓  Execution date         ]          │ │  ← sp_type_chip (assist): bg secondaryContainer
│ │                                         │ │    #D3E5F5 text onSecondaryContainer #384956
│ │  To: 08-32-00 12001039                  │ │    icon calendar_today 18dp, h 32dp r 9999
│ │  Ref: HMRC-SA-2526                      │ │  ← sp_account_id labelSmall 11sp #41474D Mono
│ └─────────────────────────────────────────┘ │  ← sp_reference labelSmall 11sp #41474D
│   card: bg surfaceContainerLow #F1F4F9     │    elevation 1, radius 12dp, padding 16dp
│         margin h 16dp, gap-below 8dp       │
│ ┌─────────────────────────────────────────┐ │  ── scheduled_payment_card [SP-002] ──
│ │  Westminster Council Tax                │ │  ← sp_payee_name #181C20
│ │                                         │ │
│ │  GBP 198.00                             │ │  ← sp_amount #BA1A1A Roboto Mono
│ │                                         │ │
│ │  Due: Sun 5 Jul 2026                    │ │
│ │                                         │ │
│ │  [🗓  Execution date         ]          │ │  ← chip calendar_today, bg #D3E5F5
│ │                                         │ │
│ │  To: 60-23-05 20490017                  │ │  ← Roboto Mono #41474D
│ │  Ref: CTAX-JUL                          │ │
│ └─────────────────────────────────────────┘ │
│                                             │
│ ┌─────────────────────────────────────────┐ │  ── scheduled_payment_card [SP-003] ──
│ │  Direct Line Insurance                  │ │  ← sp_payee_name #181C20
│ │                                         │ │
│ │  GBP 412.50                             │ │  ← sp_amount #BA1A1A Roboto Mono
│ │                                         │ │
│ │  Due: Sat 15 Aug 2026                   │ │
│ │                                         │ │
│ │  [↓  Arrival date            ]          │ │  ← chip arrow_downward (Arrival type)
│ │                                         │ │    bg #D3E5F5, text #384956
│ │  To: 20-00-00 73428901                  │ │  ← Roboto Mono #41474D
│ │  Ref: DL-HOME-INS-26                    │ │
│ └─────────────────────────────────────────┘ │
│                                             │
│ ┌─────────────────────────────────────────┐ │  ── scheduled_payment_card [SP-004] ──
│ │  Amazon Payments UK                     │ │
│ │                                         │ │
│ │  GBP 95.00                              │ │  ← sp_amount #BA1A1A Roboto Mono
│ │                                         │ │
│ │  Due: Tue 14 Jul 2026                   │ │
│ │                                         │ │
│ │  [🗓  Execution date         ]          │ │  ← chip calendar_today, bg #D3E5F5
│ │                                         │ │
│ │  To: 23-69-72 10001289                  │ │  ← Roboto Mono #41474D
│ │  Ref: PRIME-ANN-26                      │ │
│ └─────────────────────────────────────────┘ │
│   [list scrolls; 4 cards total — 792dp]    │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│
│           ─────────                         │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
Screen: Scheduled Payments (ScheduledPaymentsUiState.Content — 4 ScheduledPaymentUiModel items)
│
TopAppBar/ (small, h 64dp, bg #EBEEF3)
├── back_button  (icon_button arrow_back, 48dp×48dp, tint primary #266489)
│               on_click → navigate_back → account-detail
└── title        (titleLarge 22sp/28sp w400 #181C20): "Scheduled Payments"
│
scheduled_payments_list/ (LazyColumn vertical scroll, gap 8dp, padding h 16dp, top 8dp, bottom 16dp)
│   items_source: scheduledPayments (OBReadScheduledPayment3.Data.ScheduledPayment[])
│
├── scheduled_payment_card[SP-001]
│       bg surfaceContainerLow #F1F4F9, elevation 1, radius 12dp, padding 16dp
│       layout: Column vertical gap 4dp
│       accessibility_label: "Payment of 842.00 GBP to HMRC Self Assessment"
│   ├── sp_payee_name   (titleMedium 16sp/24sp w500 onSurface #181C20)
│   │                   "HMRC Self Assessment"
│   ├── sp_amount       (headlineSmall 24sp/32sp w400 error #BA1A1A, Roboto Mono)
│   │                   "GBP 842.00"
│   │                   accessibility_label: "842.00 GBP scheduled"
│   ├── sp_scheduled_date (bodySmall 12sp/16sp w400 onSurfaceVariant #41474D)
│   │                   "Due: Fri 31 Jul 2026"
│   ├── sp_type_chip    (AssistChip: bg secondaryContainer #D3E5F5, label onSecondaryContainer #384956)
│   │                   icon: calendar_today 18dp #384956, label: "Execution date"
│   │                   h 32dp, radius 9999, labelLarge 14sp/20sp w500
│   │                   accessibility_label: "Money leaves your account on 31 Jul 2026"
│   ├── sp_account_id   (labelSmall 11sp/16sp w500 onSurfaceVariant #41474D, Roboto Mono)
│   │                   "To: 08-32-00 12001039"
│   └── sp_reference    (labelSmall 11sp/16sp w500 onSurfaceVariant #41474D)
│                       "Ref: HMRC-SA-2526"
│
├── scheduled_payment_card[SP-002]
│       bg surfaceContainerLow #F1F4F9, elevation 1, radius 12dp, padding 16dp
│   ├── sp_payee_name   "Westminster Council Tax"       (titleMedium 16sp w500 #181C20)
│   ├── sp_amount       "GBP 198.00"                   (headlineSmall 24sp #BA1A1A Roboto Mono)
│   ├── sp_scheduled_date "Due: Sun 5 Jul 2026"         (bodySmall 12sp #41474D)
│   ├── sp_type_chip    icon: calendar_today, label: "Execution date"
│   │                   bg #D3E5F5, text #384956
│   │                   accessibility_label: "Money leaves your account on 5 Jul 2026"
│   ├── sp_account_id   "To: 60-23-05 20490017"        (labelSmall 11sp #41474D Roboto Mono)
│   └── sp_reference    "Ref: CTAX-JUL"                (labelSmall 11sp #41474D)
│
├── scheduled_payment_card[SP-003]
│       bg surfaceContainerLow #F1F4F9, elevation 1, radius 12dp, padding 16dp
│   ├── sp_payee_name   "Direct Line Insurance"         (titleMedium 16sp w500 #181C20)
│   ├── sp_amount       "GBP 412.50"                   (headlineSmall 24sp #BA1A1A Roboto Mono)
│   ├── sp_scheduled_date "Due: Sat 15 Aug 2026"        (bodySmall 12sp #41474D)
│   ├── sp_type_chip    icon: arrow_downward, label: "Arrival date"
│   │                   bg #D3E5F5, text #384956
│   │                   accessibility_label: "Funds arrive at Direct Line Insurance on 15 Aug 2026"
│   ├── sp_account_id   "To: 20-00-00 73428901"        (labelSmall 11sp #41474D Roboto Mono)
│   └── sp_reference    "Ref: DL-HOME-INS-26"          (labelSmall 11sp #41474D)
│
└── scheduled_payment_card[SP-004]
        bg surfaceContainerLow #F1F4F9, elevation 1, radius 12dp, padding 16dp
    ├── sp_payee_name   "Amazon Payments UK"            (titleMedium 16sp w500 #181C20)
    ├── sp_amount       "GBP 95.00"                    (headlineSmall 24sp #BA1A1A Roboto Mono)
    ├── sp_scheduled_date "Due: Tue 14 Jul 2026"        (bodySmall 12sp #41474D)
    ├── sp_type_chip    icon: calendar_today, label: "Execution date"
    │                   bg #D3E5F5, text #384956
    │                   accessibility_label: "Money leaves your account on 14 Jul 2026"
    ├── sp_account_id   "To: 23-69-72 10001289"        (labelSmall 11sp #41474D Roboto Mono)
    └── sp_reference    "Ref: PRIME-ANN-26"            (labelSmall 11sp #41474D)

BottomNav/ (persistent)
├── tab Home         (icon: home,          label: "Home",         default,  tint #41474D)
├── tab Accounts     (icon: account_balance,label: "Accounts",    selected, tint #266489)
├── tab Transactions (icon: receipt_long,  label: "Transactions", default,  tint #41474D)
└── tab More         (icon: more_horiz,    label: "More",         default,  tint #41474D)
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│ ←  Scheduled Payments                       │  ← top_app_bar bg #EBEEF3 h 64dp
├─────────────────────────────────────────────┤
│                                             │
│                                             │
│                                             │
│                  [schedule]                 │  ← icon schedule 48dp onSurfaceVariant #41474D
│                                             │    centred horizontally, upper-mid vertically
│                                             │
│          No scheduled payments              │  ← title headlineSmall 24sp/32sp w400
│                                             │    onSurface #181C20, centre aligned
│   No payments are scheduled for this       │  ← body bodyMedium 14sp/20sp w400
│   account.                                 │    onSurfaceVariant #41474D, centre aligned
│                                             │
│                                             │
│                                             │
│                                             │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│
│           ─────────                         │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — empty

```
Screen: Scheduled Payments (ScheduledPaymentsUiState.Empty)
│
TopAppBar/ (small, h 64dp, bg #EBEEF3)
├── back_button  (icon_button arrow_back, 48dp×48dp, tint #266489)
│               on_click → navigate_back → account-detail
└── title        (titleLarge 22sp/28sp w400 #181C20): "Scheduled Payments"
│
empty_scheduled_payments/ (empty_state, Column vertically centred in content area, padding h 32dp)
│   accessibility_label: "No scheduled payments found" (strings.sp_empty_a11y)
│   Column: gap 16dp, horizontalAlignment Center
│
├── icon  (Material icon: schedule, 48dp×48dp, tint onSurfaceVariant #41474D)
│         decorative: false, contentDescription: "No scheduled payments"
├── title (headlineSmall 24sp/32sp w400 onSurface #181C20, textAlign Center)
│         "No scheduled payments"
└── body  (bodyMedium 14sp/20sp w400 onSurfaceVariant #41474D, textAlign Center)
          "No payments are scheduled for this account."

BottomNav/ (persistent — Accounts tab selected, tint #266489)
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│ ←  Scheduled Payments                       │  ← top_app_bar bg #EBEEF3 h 64dp
├─────────────────────────────────────────────┤
│                                             │
│                                             │
│              [error_outline]                │  ← icon error_outline 48dp error #BA1A1A
│                                             │    centred horizontally, upper-mid vertically
│                                             │
│  Unable to load scheduled payments         │  ← title headlineSmall 24sp/32sp w400
│                                             │    onSurface #181C20, centre aligned
│  No network connection. Check your         │  ← body bodyMedium 14sp/20sp w400
│  connection and retry.                     │    onSurfaceVariant #41474D, centre aligned
│                                             │    [EC-SP-004 NetworkError demo render]
│                                             │    EC-SP-001 401: "Session expired. Please
│                                             │    log in again."
│                                             │    EC-SP-003 429: "Too many requests.
│                                             │    Please wait a moment and try again."
│                                             │
│       [      Try again       ]              │  ← retry_button filled h 56dp
│                                             │    bg primary #266489, text #FFFFFF
│                                             │    radius 9999, width match_parent − 64dp
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│
│           ─────────                         │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — error

```
Screen: Scheduled Payments (ScheduledPaymentsUiState.Error)
│
TopAppBar/ (small, h 64dp, bg #EBEEF3)
├── back_button  (icon_button arrow_back, 48dp×48dp, tint #266489)
│               on_click → navigate_back → account-detail
└── title        (titleLarge 22sp/28sp w400 #181C20): "Scheduled Payments"
│
error_state/ (error variant, Column vertically centred in content area, padding h 32dp)
│   accessibility_label: "Error loading scheduled payments" (strings.sp_error_a11y)
│   Column: gap 16dp, horizontalAlignment Center
│
├── icon  (Material icon: error_outline, 48dp×48dp, tint error #BA1A1A)
│         decorative: false, contentDescription: "Error loading scheduled payments"
├── title (headlineSmall 24sp/32sp w400 onSurface #181C20, textAlign Center)
│         "Unable to load scheduled payments"
├── body  (bodyMedium 14sp/20sp w400 onSurfaceVariant #41474D, textAlign Center)
│         "{error.message}" — resolved per error type:
│         EC-SP-001 (HTTP 401 TokenExpired):    "Session expired. Please log in again."
│         EC-SP-002 (HTTP 403 ConsentRevoked):  "Account access consent has been revoked."
│         EC-SP-003 (HTTP 429 RateLimited):     "Too many requests. Please wait a moment and try again."
│         EC-SP-004 (IOException NetworkError): "No network connection. Check your connection and retry."
└── retry_button (FilledButton, h 56dp, bg primary #266489, label onPrimary #FFFFFF)
        width: fillMaxWidth with horizontal padding 32dp → effective width match_parent − 64dp
        radius: 9999dp (full pill, M3 FilledButton default)
        min touch target: 56dp
        label: "Try again" (strings.action_retry, labelLarge 14sp/20sp w500 #FFFFFF)
        accessibility_label: "Retry loading scheduled payments" (strings.sp_retry_a11y)
        on_click → retry_load: action_contract effect=call_api
                   re-invokes LoadScheduledPayments(accountId)
                   GET /accounts/{AccountId}/scheduled-payments via Ktorfit AisApiService
                   transitions: Loading → Content | Empty | Error

BottomNav/ (persistent — Accounts tab selected, tint #266489)
```

---

### Interaction Summary

| Component | Action | Effect | Target / Behaviour |
|---|---|---|---|
| back_button | navigate_back | navigate | Pops scheduled-payments from back stack; returns user to account-detail screen. Visible in all states via top app bar leading slot. |
| retry_button | retry_load | call_api | Re-invokes `LoadScheduledPayments(accountId)` ViewModel action; issues GET `/accounts/{AccountId}/scheduled-payments` via Ktorfit; transitions through Loading → Content \| Empty \| Error. Visible in error state only. |

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| top_app_bar | match_parent (393dp) | 64dp | 0 |
| back_button (touch target) | 48dp | 48dp | 9999dp (circular) |
| progress_indicator (loading) | 48dp | 48dp | 9999dp (circular) |
| scheduled_payments_list | match_parent | fill remaining (~708dp, scrolls) | 0 |
| scheduled_payment_card | match_parent − 32dp (361dp) | ~192dp (hug content) | 12dp |
| sp_payee_name text row | match_parent | 24dp (line height) | 0 |
| sp_amount text row | match_parent | 32dp (line height) | 0 |
| sp_scheduled_date text row | match_parent | 16dp (line height) | 0 |
| sp_type_chip | wrap content (~140dp) | 32dp | 9999dp (full pill) |
| sp_type_chip icon | 18dp | 18dp | 0 |
| sp_account_id text row | match_parent | 16dp (line height) | 0 |
| sp_reference text row | match_parent | 16dp (line height) | 0 |
| empty state icon (schedule) | 48dp | 48dp | 0 |
| error state icon (error_outline) | 48dp | 48dp | 0 |
| retry_button | match_parent − 64dp (329dp) | 56dp | 9999dp (full pill) |
| bottom_nav | match_parent (393dp) | 80dp | 0 |
