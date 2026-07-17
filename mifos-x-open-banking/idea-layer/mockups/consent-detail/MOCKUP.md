# Consent Detail — Visual Mockup

> Auto-generated from `screens/consent-detail/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-17T00:00:00Z

---

## Screen: HSBC Connection Detail

Canvas: 393×852dp (Pixel 5) · Top app bar visible (back + "Connection Detail") · Bottom nav visible · No FAB · Roboto font · Material 3 light theme · bg #F7F9FF

Shell (from `app-shell.yaml` + `ui.yaml#shell` override):
- Top app bar: small variant, leading = back arrow (24dp icon, 48dp touch target), title = "Connection Detail" (titleLarge 22sp), bg #F7F9FF (surface), onSurface #181C20.
- Bottom navigation: Home (home) | Accounts (account_balance) | Transactions (receipt_long) | More (more_horiz → settings). "More" tab active #266489 (consent-detail reached via Settings → Manage consents). Unselected tabs #41474D. Nav bg #F7F9FF, 80dp height.
- FAB: hidden per `ui.yaml#shell.fab_visible: false`.
- Scrollable content area: 393×716dp (852 − 56dp top app bar − 80dp bottom nav). Horizontal screen padding 16dp.

---

### State: loading

```
┌─────────────────────────────────────────────┐
│ [←]  Connection Detail                      │  ← top_app_bar 56dp, bg #F7F9FF
│      back arrow 24dp onSurface #181C20      │    title titleLarge 22sp #181C20
├─────────────────────────────────────────────┤
│                                              │
│                                              │
│                                              │
│                                              │
│                    ( ◯ )                    │  ← load_progress circular 48dp
│                                              │    indicator color #266489 (primary)
│                                              │    centered in content area 393×716dp
│                                              │
│                                              │
│                                              │
│                                              │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│  ← bottom_nav 80dp, bg #F7F9FF
│  #41474D  #41474D    #41474D        #266489 │    More tab selected #266489
└─────────────────────────────────────────────┘
```

### Component Hierarchy — loading

```
Screen: Consent Detail (ConsentDetailUiState.Loading)
│
├── TopAppBar/ (56dp, bg #F7F9FF)
│   ├── leading: back arrow icon 24dp, tint #181C20, touch target 48×48dp
│   └── title: "Connection Detail" titleLarge 22sp #181C20
│
├── ContentArea/ (393×716dp, bg #F7F9FF, center alignment)
│   └── load_progress  (CircularProgressIndicator, 48dp, trackColor #C9E6FF, color #266489)
│       accessibility_label: "Loading consent details"
│
└── BottomNav/ (80dp, bg #F7F9FF)
    ├── tab Home         (icon:home,          label:"Home",         tint #41474D)
    ├── tab Accounts     (icon:account_balance,label:"Accounts",    tint #41474D)
    ├── tab Transactions (icon:receipt_long,  label:"Transactions", tint #41474D)
    └── tab More         (icon:more_horiz,    label:"More",         tint #266489, selected)
```

---

### State: content

> Content is scrollable. Virtual content height ≈ 1 340dp. Wireframe shows the full virtual scroll.
> `expiry_warning_banner` is **HIDDEN** — `expiryWarningDays` is null (ExpirationDateTime 2026-09-26, ~71 days out).

```
┌─────────────────────────────────────────────┐
│ [←]  Connection Detail                      │  ← top_app_bar 56dp, bg #F7F9FF
├─────────────────────────────────────────────┤  ── SCROLLABLE CONTENT BEGINS ──
│                                              │  16dp top padding
│ ┌─────────────────────────────────────────┐ │  ← status_header_card
│ │                                          │ │    ElevatedCard, bg #F1F4F9
│ │  [HSBC]           ◉ Authorised           │ │    elevation 2 (3dp shadow), radius 16dp
│ │  48×24dp          bg #C9E6FF txt #004B6F │ │    padding 16dp, margin h 16dp
│ │                   icon check_circle 16dp  │ │
│ │                                          │ │  ← bank_identity_row: row, gap 12dp, fill
│ │  ID: aac-fb2c4e8a-7d31-4c9e-9f2a-1b3c5d7e9f01   │ │  ← consent_id_label labelSmall 11sp #41474D
│ └─────────────────────────────────────────┘ │    marginTop 8dp inside card
│                                              │  [expiry_warning_banner HIDDEN — expiryWarningDays null]
│  ACCESS PERIOD                               │  ← dates_header labelLarge 14sp 500w #41474D
│                                              │    padding h 16dp, top 16dp, bottom 8dp
│  ┌─────────────────────────────────────────┐ │
│  │ 📅  Connected on                         │ │  ← created_date_row list_item 72dp
│  │     2026-06-28T18:25:00Z                 │ │    icon:event 24dp #41474D
│  └─────────────────────────────────────────┘ │    headline bodyLarge 16sp #181C20
│  ┌─────────────────────────────────────────┐ │    supporting bodyMedium 14sp #41474D
│  │ 🗓  Expires on                           │ │  ← expiry_date_row 72dp
│  │     2026-09-26T00:00:00Z                 │ │    icon:event_busy 24dp #41474D
│  └─────────────────────────────────────────┘ │
│  ┌─────────────────────────────────────────┐ │  ← transaction_from_row 72dp
│  │ 🕐  Transaction history from             │ │    icon:history 24dp #41474D
│  │     2026-03-30T00:00:00Z                 │ │
│  └─────────────────────────────────────────┘ │
│  ┌─────────────────────────────────────────┐ │  ← transaction_to_row 72dp
│  │ 📆  Transaction history to               │ │    icon:event_available 24dp #41474D
│  │     2026-06-28T23:59:59Z                 │ │
│  └─────────────────────────────────────────┘ │
│                                              │  16dp gap
│  ┌─── [↺]  Reconfirm access ──────────────┐ │  ← reconfirm_button FilledTonal
│  └─────────────────────────────────────────┘ │    bg #D3E5F5, txt #384956, radius 100dp
│                                              │    width 361dp, height 40dp, icon refresh 18dp
│  DATA SHARED                                 │  ← permissions_header labelLarge 14sp #41474D
│                                              │    padding h 16dp, top 16dp, bottom 8dp
│  ┌─────────────────────────────────────────┐ │
│  │ ✓  Account details                       │ │  ← permission_row[0] list_item 72dp
│  │    Account identifiers, sort code,        │ │    icon:check_circle_outline 24dp #266489
│  │    account number, nickname               │ │    headline bodyLarge 16sp #181C20
│  └─────────────────────────────────────────┘ │    supporting bodyMedium 14sp #41474D
│  ┌─────────────────────────────────────────┐ │
│  │ ✓  Balances                              │ │  ← permission_row[1] list_item 72dp
│  │    Current and available balances         │ │
│  │    for each account                       │ │
│  └─────────────────────────────────────────┘ │
│  ┌─────────────────────────────────────────┐ │
│  │ ✓  Transaction history                   │ │  ← permission_row[2] list_item 72dp
│  │    Debits and credits with merchant,      │ │
│  │    amount, and date                       │ │
│  └─────────────────────────────────────────┘ │
│  ┌─────────────────────────────────────────┐ │
│  │ ✓  Beneficiaries                         │ │  ← permission_row[3]
│  │    Saved payees on your account           │ │
│  └─────────────────────────────────────────┘ │
│  ┌─────────────────────────────────────────┐ │
│  │ ✓  Standing orders                       │ │  ← permission_row[4]
│  │    Scheduled recurring payment            │ │
│  │    instructions                           │ │
│  └─────────────────────────────────────────┘ │
│  ┌─────────────────────────────────────────┐ │
│  │ ✓  Direct debits                         │ │  ← permission_row[5]
│  │    Active direct debit mandates           │ │
│  │    and their status                       │ │
│  └─────────────────────────────────────────┘ │
│  ┌─────────────────────────────────────────┐ │
│  │ ✓  Scheduled payments                    │ │  ← permission_row[6]
│  │    One-off future-dated payment           │ │
│  │    instructions                           │ │
│  └─────────────────────────────────────────┘ │
│  ┌─────────────────────────────────────────┐ │
│  │ ✓  Statements                            │ │  ← permission_row[7]
│  │    Monthly statement metadata             │ │
│  │    and PDF references                     │ │
│  └─────────────────────────────────────────┘ │
│  ┌─────────────────────────────────────────┐ │
│  │ ✓  Product information                   │ │  ← permission_row[8]
│  │    Interest rates and product features    │ │
│  │    attached to your accounts              │ │
│  └─────────────────────────────────────────┘ │
│  ┌─────────────────────────────────────────┐ │
│  │ ✓  Account holder name                   │ │  ← permission_row[9]
│  │    Full legal name registered             │ │
│  │    on the account                         │ │
│  └─────────────────────────────────────────┘ │
│                                              │  24dp gap
│  ┌─── [✕]  Revoke access ─────────────────┐ │  ← revoke_button Outlined
│  └─────────────────────────────────────────┘ │    border 1dp #BA1A1A, txt #BA1A1A
│                                              │    radius 100dp, width 361dp, height 40dp
│                                              │  24dp bottom padding
├─────────────────────────────────────────────┤  ── SCROLLABLE CONTENT ENDS ──
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│  ← bottom_nav 80dp
│  #41474D  #41474D    #41474D        #266489 │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
Screen: Consent Detail (ConsentDetailUiState.Content)
│
├── TopAppBar/ (56dp, bg #F7F9FF)
│   ├── leading: back arrow 24dp #181C20
│   └── title: "Connection Detail" titleLarge 22sp #181C20
│
├── ContentArea/ (393dp wide, vertical scroll)
│   │   padding: top 16dp, horizontal 16dp, bottom 24dp
│   │
│   ├── status_header_card  (ElevatedCard, bg #F1F4F9, radius 16dp, elev 2, margin h 0)
│   │   padding 16dp inside
│   │   ├── bank_identity_row  (Row, fill width, horizontalArrangement=SpaceBetween, height 32dp)
│   │   │   ├── bank_logo    (Image asset:ic_hsbc_logo, 48×24dp, contentDesc: "HSBC logo")
│   │   │   └── status_chip  (AssistChip, bg #C9E6FF, text #004B6F "Authorised", icon check_circle 18dp #004B6F)
│   │   └── consent_id_label (Text, labelSmall 11sp #41474D, marginTop 8dp)
│   │       "ID: aac-fb2c4e8a-7d31-4c9e-9f2a-1b3c5d7e9f01"
│   │
│   │   [expiry_warning_banner — HIDDEN, visible_when expiryWarningDays != null, currently null]
│   │
│   ├── dates_header  (Text, labelLarge 14sp 500w #41474D, padding top 16dp bottom 8dp)
│   │   "ACCESS PERIOD"
│   │
│   ├── dates_list  (Column, vertical, divider outlineVariant #C1C7CE 0.5dp)
│   │   ├── created_date_row    (ListItem, icon:event 24dp #41474D, headline "Connected on" bodyLarge #181C20, supporting "2026-06-28T18:25:00Z" bodyMedium #41474D)
│   │   ├── expiry_date_row     (ListItem, icon:event_busy 24dp #41474D, headline "Expires on" bodyLarge #181C20, supporting "2026-09-26T00:00:00Z" bodyMedium #41474D)
│   │   ├── transaction_from_row (ListItem, icon:history 24dp #41474D, headline "Transaction history from" bodyLarge #181C20, supporting "2026-03-30T00:00:00Z" bodyMedium #41474D)
│   │   └── transaction_to_row  (ListItem, icon:event_available 24dp #41474D, headline "Transaction history to" bodyLarge #181C20, supporting "2026-06-28T23:59:59Z" bodyMedium #41474D)
│   │
│   ├── reconfirm_button  (FilledTonalButton, bg #D3E5F5, text #384956 labelLarge 14sp 500w)
│   │   icon:refresh 18dp, label "Reconfirm access", width fill 361dp, height 40dp, radius 100dp
│   │   state_binding: [content] only
│   │
│   ├── permissions_header  (Text, labelLarge 14sp 500w #41474D, padding top 16dp bottom 8dp)
│   │   "DATA SHARED"
│   │
│   ├── permissions_list  (Column, vertical, items_source: consent.permissions_detail × 10)
│   │   ├── permission_row[0]   (ListItem, icon:check_circle_outline 24dp #266489, "Account details" / "Account identifiers, sort code, account number, nickname")
│   │   ├── permission_row[1]   (ListItem, icon:check_circle_outline 24dp #266489, "Balances" / "Current and available balances for each account")
│   │   ├── permission_row[2]   (ListItem, icon:check_circle_outline 24dp #266489, "Transaction history" / "Debits and credits with merchant, amount, and date")
│   │   ├── permission_row[3]   (ListItem, icon:check_circle_outline 24dp #266489, "Beneficiaries" / "Saved payees on your account")
│   │   ├── permission_row[4]   (ListItem, icon:check_circle_outline 24dp #266489, "Standing orders" / "Scheduled recurring payment instructions")
│   │   ├── permission_row[5]   (ListItem, icon:check_circle_outline 24dp #266489, "Direct debits" / "Active direct debit mandates and their status")
│   │   ├── permission_row[6]   (ListItem, icon:check_circle_outline 24dp #266489, "Scheduled payments" / "One-off future-dated payment instructions")
│   │   ├── permission_row[7]   (ListItem, icon:check_circle_outline 24dp #266489, "Statements" / "Monthly statement metadata and PDF references")
│   │   ├── permission_row[8]   (ListItem, icon:check_circle_outline 24dp #266489, "Product information" / "Interest rates and product features attached to your accounts")
│   │   └── permission_row[9]   (ListItem, icon:check_circle_outline 24dp #266489, "Account holder name" / "Full legal name registered on the account")
│   │
│   └── revoke_button  (OutlinedButton, border 1dp #BA1A1A, text #BA1A1A labelLarge 14sp 500w)
│       icon:link_off 18dp, label "Revoke access", width fill 361dp, height 40dp, radius 100dp
│       state_binding: [content] only
│
└── BottomNav/ (80dp, bg #F7F9FF)
    ├── Home (home #41474D), Accounts (account_balance #41474D), Transactions (receipt_long #41474D)
    └── More (more_horiz #266489, selected indicator bg #C9E6FF radius 16dp)
```

---

### State: revoke_confirm

> Same scroll content as `content` (status_header_card, dates_list, permissions_list visible behind scrim). `reconfirm_button` and `revoke_button` are hidden (state_binding:[content] only). The `revoke_confirm_dialog` overlays with scrim.

```
┌─────────────────────────────────────────────┐
│ [←]  Connection Detail                      │  ← top_app_bar 56dp
├─────────────────────────────────────────────┤
│▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒│  ← scrim #000000 at 32% opacity
│▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒│    dimmed consent content behind
│▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒│
│▒▒▒ ┌────────────────────────────────┐ ▒▒▒│
│▒▒▒ │                                │ ▒▒▒│  ← revoke_confirm_dialog
│▒▒▒ │  Revoke HSBC access?           │ ▒▒▒│    bg #EBEEF3 (surfaceContainer)
│▒▒▒ │                                │ ▒▒▒│    radius 28dp (extra_large), width 280dp
│▒▒▒ │  Removing this connection will │ ▒▒▒│    title: headlineSmall 24sp #181C20
│▒▒▒ │  stop Mifos from reading your  │ ▒▒▒│    body: bodyMedium 14sp #41474D
│▒▒▒ │  HSBC account data. You can    │ ▒▒▒│    padding 24dp all sides
│▒▒▒ │  reconnect at any time.        │ ▒▒▒│
│▒▒▒ │                                │ ▒▒▒│
│▒▒▒ │           [Cancel]  [Revoke]   │ ▒▒▒│  ← dialog_cancel_button: Text, #266489
│▒▒▒ └────────────────────────────────┘ ▒▒▒│    dialog_confirm_button: Filled, bg #BA1A1A
│▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒│    txt #FFFFFF, radius 100dp, h 40dp
│▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒▒│
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│  ← bottom_nav 80dp
└─────────────────────────────────────────────┘
```

### Component Hierarchy — revoke_confirm

```
Screen: Consent Detail (ConsentDetailUiState.RevokeConfirm)
│
├── TopAppBar/ (56dp, back + "Connection Detail")
│
├── ContentArea/ (scrimmed: #000000 at 32% over the scrolled consent content)
│   ├── status_header_card   (visible — state_binding includes revoke_confirm)
│   ├── dates_header / dates_list  (visible)
│   ├── permissions_header / permissions_list  (visible, behind scrim)
│   │   [reconfirm_button — HIDDEN, state_binding:[content] only]
│   │   [revoke_button    — HIDDEN, state_binding:[content] only]
│   │
│   └── revoke_confirm_dialog  (AlertDialog, centered in viewport)
│       bg #EBEEF3, radius 28dp, padding 24dp, width 280dp
│       title: "Revoke HSBC access?" headlineSmall 24sp #181C20
│       body:  "Removing this connection will stop Mifos from reading your HSBC account data. You can reconnect at any time." bodyMedium 14sp #41474D
│       actions row (horizontalArrangement=End, gap 8dp):
│       ├── dialog_cancel_button  (TextButton, label "Cancel" labelLarge #266489, h 40dp, radius 100dp)
│       └── dialog_confirm_button (FilledButton, bg #BA1A1A, text "Revoke" labelLarge #FFFFFF, h 40dp, radius 100dp)
│
└── BottomNav/ (80dp, More active #266489)
```

---

### State: revoking

```
┌─────────────────────────────────────────────┐
│ [←]  Connection Detail                      │  ← top_app_bar 56dp, bg #F7F9FF
│      back arrow disabled (alpha 38%) #181C20│    back unavailable during API call
├─────────────────────────────────────────────┤
│                                              │
│                                              │
│                                              │
│                    ( ◯ )                    │  ← revoke_progress circular 48dp
│                                              │    color #266489 (primary), animating
│                Revoking access…              │  ← revoke_progress label
│                                              │    bodyMedium 14sp #41474D
│                                              │    centered below progress, marginTop 16dp
│                                              │
│                                              │
│                                              │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│  ← bottom_nav 80dp
└─────────────────────────────────────────────┘
```

### Component Hierarchy — revoking

```
Screen: Consent Detail (ConsentDetailUiState.Revoking)
│
├── TopAppBar/ (56dp, bg #F7F9FF)
│   ├── leading: back arrow icon 24dp, tint #181C20 at 38% opacity (disabled during DELETE in-flight)
│   └── title: "Connection Detail" titleLarge 22sp #181C20
│
├── ContentArea/ (393×716dp, bg #F7F9FF, vertical + horizontal center alignment)
│   └── revoke_progress  (CircularProgressIndicator + label Column, centerHorizontally)
│       ├── CircularProgressIndicator 48dp, color #266489, trackColor #C9E6FF
│       └── label Text "Revoking access…" bodyMedium 14sp #41474D, marginTop 16dp
│           accessibility_label: "Revoking connection, please wait"
│           (prevents double-tap; no consent content shown in this state)
│
└── BottomNav/ (80dp)
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│ [←]  Connection Detail                      │  ← top_app_bar 56dp, bg #F7F9FF
├─────────────────────────────────────────────┤
│                                              │
│                                              │
│                   ⚠                         │  ← error_state icon:error_outline 48dp
│                                              │    tint #BA1A1A (error)
│            Something went wrong             │  ← error_state title headlineMedium 28sp #181C20
│                                              │
│      We couldn't load your connection        │  ← error_state body bodyLarge 16sp #41474D
│      details. Please check your network      │    derived from ConsentDetailErrorCode
│      connection and try again.               │    (e.g. NetworkError message)
│                                              │
│   ┌─── Try again ─────────────────────────┐ │  ← retry_button FilledButton
│   └───────────────────────────────────────┘ │    bg #266489, txt #FFFFFF labelLarge
│                                              │    radius 100dp, width 280dp, h 40dp
│                                              │    marginTop 24dp
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│  ← bottom_nav 80dp
└─────────────────────────────────────────────┘
```

### Component Hierarchy — error

```
Screen: Consent Detail (ConsentDetailUiState.Error)
│
├── TopAppBar/ (56dp, back + "Connection Detail")
│
├── ContentArea/ (393×716dp, bg #F7F9FF, vertical + horizontal center, padding h 32dp)
│   └── error_state  (variant:error, column, centerHorizontally, gap 8dp)
│       ├── icon:error_outline  48dp, tint #BA1A1A (error)
│       │   contentDescription "" (decorative, title provides context)
│       ├── title Text  "Something went wrong" headlineMedium 28sp #181C20, textAlign Center
│       ├── body Text   "{error.message}" bodyLarge 16sp #41474D, textAlign Center
│       │   (e.g. "We couldn't load your connection details. Please check your network connection and try again.")
│       │   Mapped from ConsentDetailErrorCode enum (ConsentNotFound|NetworkError|TokenExpired|RevokeServerError…)
│       └── retry_button  (FilledButton, bg #266489, text "Try again" labelLarge #FFFFFF)
│           radius 100dp, width 280dp, height 40dp, marginTop 24dp
│           on_click → retry_load → GET /account-access-consents/{ConsentId}
│
└── BottomNav/ (80dp)
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│ [←]  Connection Detail                      │  ← top_app_bar 56dp, bg #F7F9FF
├─────────────────────────────────────────────┤
│                                              │
│                                              │
│                   ✕                         │  ← empty_state icon:link_off 48dp
│                                              │    tint #41474D (onSurfaceVariant)
│            No connection found               │  ← empty_state title headlineMedium 28sp #181C20
│                                              │
│    The selected connection returned no       │  ← empty_state body bodyLarge 16sp #41474D
│    data. It may have already been removed.   │
│    Return to your connections list.          │
│                                              │
│   ┌─── Go back ────────────────────────────┐ │  ← empty_go_back_button FilledButton
│   └───────────────────────────────────────┘ │    bg #266489, txt #FFFFFF, radius 100dp
│                                              │    width 280dp, h 40dp, marginTop 24dp
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│  ← bottom_nav 80dp
└─────────────────────────────────────────────┘
```

### Component Hierarchy — empty

```
Screen: Consent Detail (ConsentDetailUiState.Empty — no Data block in GET 200 response)
│
├── TopAppBar/ (56dp, back + "Connection Detail")
│
├── ContentArea/ (393×716dp, bg #F7F9FF, vertical + horizontal center, padding h 32dp)
│   └── empty_state  (variant:neutral, column, centerHorizontally, gap 8dp)
│       ├── icon:link_off  48dp, tint #41474D (onSurfaceVariant)
│       ├── title Text  "No connection found" headlineMedium 28sp #181C20, textAlign Center
│       ├── body Text   "The selected connection returned no data. It may have already been removed. Return to your connections list." bodyLarge 16sp #41474D, textAlign Center
│       └── empty_go_back_button  (FilledButton, bg #266489, text "Go back" labelLarge #FFFFFF)
│           radius 100dp, width 280dp, height 40dp, marginTop 24dp
│           on_click → navigate_back → consent-list
│
└── BottomNav/ (80dp)
```

---

### Conditional Variant: content (expiry warning visible)

> **Figma frame name: "consent-detail / content / expiry_warning"**
> This variant exists for testing and Figma component coverage. In production, it is shown only when `expiryWarningDays != null` (i.e., ExpirationDateTime ≤ 7 days away). For the primary demo data (ExpirationDateTime 2026-09-26, ~71 days out), this variant is **not rendered**. Document a hypothetical date of 2026-09-29 (3 days away) to trigger it.

```
┌─────────────────────────────────────────────┐
│ [←]  Connection Detail                      │  ← top_app_bar 56dp
├─────────────────────────────────────────────┤
│ ┌─────────────────────────────────────────┐ │  ← status_header_card (same as content state)
│ │ [HSBC]           ◉ Authorised            │ │
│ │ ID: aac-fb2c4e8a-7d31-4c9e-9f2a-1b3c…  │ │
│ └─────────────────────────────────────────┘ │
│ ┌─────────────────────────────────────────┐ │  ← expiry_warning_banner VISIBLE
│ │  ⏰  Expires in 3 days. Reconfirm your   │ │    bg #EADDFF (tertiaryContainer — closest
│ │      connection before 2026-09-26.        │ │    M3 analog for custom "warning-container")
│ └─────────────────────────────────────────┘ │    icon:access_time 24dp #4C4162 (onTertiaryContainer)
│  ··· (rest of content state below) ···      │    text bodySmall 12sp #4C4162
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│
└─────────────────────────────────────────────┘
```

> **Token note:** `warning-container` / `on-warning-container` are semantic role aliases in ui.yaml that are NOT defined as hex values in design-tokens.yaml. For rendering, map to the closest M3 warm-neutral role: `warning-container → tertiaryContainer #EADDFF`, `on-warning-container → onTertiaryContainer #4C4162`. Both hexes are legal tokens. The Compose implementation should define these as custom MaterialTheme color extensions.

---

### Interaction Summary

| Component ID | Action | Effect | Target / Result |
|---|---|---|---|
| `reconfirm_button` | `navigate_reconfirm` | `navigate` | → `login` (re-runs FAPI authorize flow, 90-day reconfirmation) |
| `revoke_button` | `confirm_revoke` | `transform_state` | `Content` → `RevokeConfirm` (no API call, state transition only) |
| `dialog_cancel_button` | `dismiss_revoke_confirm` | `transform_state` | `RevokeConfirm` → `Content` (dismisses dialog, no API call) |
| `dialog_confirm_button` | `execute_revoke` | `call_api` | DELETE /account-access-consents/{ConsentId}; 204/404 → clear PSU token + ConsentId → navigate to `consent-list` |
| `retry_button` | `retry_load` | `call_api` | Re-issues GET /account-access-consents/{ConsentId}; success → `Content`, failure → `Error` |
| `empty_go_back_button` | `navigate_back` | `navigate` | → `consent-list` |

Non-interactive components (display only): `load_progress`, `revoke_progress`, `status_header_card`, `bank_identity_row`, `bank_logo`, `status_chip`, `consent_id_label`, `expiry_warning_banner`, `expiry_warning_row`, `expiry_warning_icon`, `expiry_warning_text`, `dates_header`, `dates_list`, `created_date_row`, `expiry_date_row`, `transaction_from_row`, `transaction_to_row`, `permissions_header`, `permissions_list`, `permission_row`, `error_state`, `empty_state`.

ViewModel lifecycle actions (not on-click; fired on screen entry): `loadConsentDetail` — GET /account-access-consents/{consentId}.

---

### Dimensions Table

| Component | Width | Height | Corner Radius | Notes |
|---|---|---|---|---|
| **Screen canvas** | 393dp | 852dp | — | Pixel 5 baseline |
| **top_app_bar** | 393dp | 56dp | 0 | Small M3, bg #F7F9FF |
| **bottom_nav** | 393dp | 80dp | 0 | bg #F7F9FF, 4 tabs |
| **bottom_nav tab indicator** | 64dp | 32dp | 16dp (full) | bg #C9E6FF, selected only |
| **content_area** | 393dp | 716dp | — | scrollable, padding h 16dp |
| `status_header_card` | 361dp | 80dp | 16dp (large) | ElevatedCard bg #F1F4F9, elev 2 |
| `bank_logo` | 48dp | 24dp | 0 | asset ic_hsbc_logo |
| `status_chip` | wrap | 32dp | 100dp (full) | AssistChip, bg #C9E6FF |
| `consent_id_label` | fill | 16dp | — | labelSmall 11sp |
| `expiry_warning_banner` | 361dp | 56dp | 12dp (medium) | bg #EADDFF (conditional variant) |
| `dates_header` | 361dp | 36dp | — | labelLarge, padding top 16dp |
| `created_date_row` | 393dp | 72dp | 0 | ListItem, divider below |
| `expiry_date_row` | 393dp | 72dp | 0 | ListItem |
| `transaction_from_row` | 393dp | 72dp | 0 | ListItem |
| `transaction_to_row` | 393dp | 72dp | 0 | ListItem |
| `reconfirm_button` | 361dp | 40dp | 100dp (full) | FilledTonal, bg #D3E5F5 |
| `permissions_header` | 361dp | 36dp | — | labelLarge, padding top 16dp |
| `permission_row` (×10) | 393dp | 72dp | 0 | ListItem, 10 rows |
| `revoke_button` | 361dp | 40dp | 100dp (full) | Outlined, border #BA1A1A |
| `revoke_confirm_dialog` | 280dp | auto (~220dp) | 28dp (extra_large) | AlertDialog bg #EBEEF3 |
| `dialog_cancel_button` | wrap | 40dp | 100dp (full) | TextButton label #266489 |
| `dialog_confirm_button` | wrap | 40dp | 100dp (full) | Filled bg #BA1A1A txt #FFFFFF |
| `error_state` icon | 48dp | 48dp | — | tint #BA1A1A |
| `retry_button` | 280dp | 40dp | 100dp (full) | Filled bg #266489 |
| `empty_state` icon | 48dp | 48dp | — | tint #41474D |
| `empty_go_back_button` | 280dp | 40dp | 100dp (full) | Filled bg #266489 |
| List item leading icon | 24dp | 24dp | 0 | touch target 48×48dp |
