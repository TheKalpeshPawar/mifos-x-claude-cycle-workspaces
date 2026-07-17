# Direct Debits — Visual Mockup

> Auto-generated from `screens/direct-debits/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-16T00:00:00Z

---

## Screen: Direct Debits

Canvas: 393×852dp (Pixel 5) · Top app bar (back arrow + "Direct Debits") · Bottom nav visible · No FAB · Roboto font · Material 3 light theme · bg #F7F9FF

Shell (from `app-shell.yaml` + `ui.yaml#shell`): Top app bar enabled, variant small, leading: back (`back_button` component, arrow_back 24dp #181C20, 48dp touch target), title "Direct Debits". Bottom navigation — **Home | Accounts | Transactions | More** (icons: home / account_balance / receipt_long / more_horiz per `app-shell.yaml`; Accounts tab active at tint #266489 — screen is reached from account-detail). FAB hidden (`ui.yaml#shell.fab_visible: false`). No drawer.

---

### State: loading

```
┌─────────────────────────────────────────────┐
│ ← Direct Debits                             │  ← top_app_bar small h 64dp bg #F7F9FF
├─────────────────────────────────────────────┤   title titleLarge 22sp/28sp w400 #181C20
│                                             │   leading: back_button arrow_back 24dp #181C20
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │  ← skeleton card 1 of 4 (list_card variant)
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │    h 80dp, radius 12dp, margin h 16dp
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │    shimmer fill #DDE3EA pulse 1.5s
│                                             │    gap 8dp between skeleton cards
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │  ← skeleton card 2
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
│                                             │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │  ← skeleton card 3
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
│                                             │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │  ← skeleton card 4 (item_count 4 from ui.yaml)
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
│                                             │
│                                             │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions ⊕ More│  ← bottom_nav h 80dp bg #F7F9FF
└─────────────────────────────────────────────┘  Accounts icon tint #266489; others #41474D
```

### Component Hierarchy — loading

```
Screen: Direct Debits (UiState.Loading)
│
loading_skeleton/ (list_card variant, item_count 4, stack vertical gap 8dp,
│                  padding h 16dp top 16dp; state_binding: [loading])
│   accessibility_label: "Loading direct debits"
│   shimmer: fill #DDE3EA pulse 1.5s; reduce-motion: static fill, no animation
│
├── skeleton_card_1  (list_card, 361dp w, h 80dp, radius 12dp, fill #DDE3EA)
├── skeleton_card_2  (list_card, 361dp w, h 80dp, radius 12dp, fill #DDE3EA)
├── skeleton_card_3  (list_card, 361dp w, h 80dp, radius 12dp, fill #DDE3EA)
└── skeleton_card_4  (list_card, 361dp w, h 80dp, radius 12dp, fill #DDE3EA)

back_button/ (icon_button — top app bar leading slot, rendered in all states)
│   icon: arrow_back 24dp #181C20, touch target 48dp×48dp
│   accessibility_label: "Back to account details"
│   on_click → navigateBack() — emits NavigationEvent.Back → account-detail

BottomNav/ (persistent across all states)
├── tab Home         (icon: home,           label: "Home",         default, tint #41474D)
├── tab Accounts     (icon: account_balance, label: "Accounts",    selected, tint #266489)
├── tab Transactions (icon: receipt_long,   label: "Transactions", default, tint #41474D)
└── tab More         (icon: more_horiz,     label: "More",         default, tint #41474D)
```

---

### State: content

```
┌─────────────────────────────────────────────┐
│ ← Direct Debits                             │  ← top_app_bar small h 64dp bg #F7F9FF
├─────────────────────────────────────────────┤
│                                             │
│  ┌ Active (3) ┐  ┌ Inactive (1) ┐         │  ← mandate_summary_chips chip_group
│  └────────────┘  └──────────────┘         │    padding h 16dp top 16dp bottom 8dp
│                                             │    active_count_chip: tonal
│ ┌─────────────────────────────────────────┐ │      bg #C9E6FF text #004B6F radius 9999
│ │ British Gas                             │ │    inactive_count_chip: outline
│ │ ┌ Active ┐                              │ │      border #72787E text #41474D radius 9999
│ │ └────────┘                              │ │
│ │ £78.00                                  │ │  ← direct_debit_card [0: British Gas]
│ │ Last collected: 15 Jun 2026             │ │    bg #F1F4F9 (surfaceContainerLow)
│ │ Mandate: DD-BG-44120                   │ │    elevation 1, radius 12dp, padding 16dp
│ └─────────────────────────────────────────┘ │    margin h 16dp, gap between cards 8dp
│ ┌─────────────────────────────────────────┐ │
│ │ Vodafone                                │ │  ← direct_debit_card [1: Vodafone]
│ │ ┌ Active ┐                              │ │    dd_originator_name titleMedium 16sp w500 #181C20
│ │ £29.00                                  │ │    dd_status_badge tonal primary: bg #C9E6FF
│ │ Last collected: 20 Jun 2026             │ │      text #004B6F h 24dp radius 9999
│ │ Mandate: DD-VF-88301                   │ │    dd_previous_amount headlineSmall 24sp #181C20
│ └─────────────────────────────────────────┘ │    dd_previous_date bodySmall 12sp #41474D
│ ┌─────────────────────────────────────────┐ │    dd_mandate_id labelSmall 11sp #41474D
│ │ Aviva Insurance                         │ │
│ │ ┌ Active ┐                              │ │  ← direct_debit_card [2: Aviva Insurance]
│ │ £41.50                                  │ │
│ │ Last collected: 05 Jun 2026             │ │
│ │ Mandate: DD-AV-10293                   │ │
│ └─────────────────────────────────────────┘ │
│ ┌─────────────────────────────────────────┐ │  ← direct_debit_card [3: TV Licensing]
│ │ TV Licensing                            │ │    Inactive — outline badge variant
│ │ ┌ Inactive ┐                            │ │    dd_status_badge outline: border #72787E
│ │ £13.25                                  │ │      text #41474D h 24dp radius 9999
│ │ Last collected: 01 Mar 2026             │ │
│ │ Mandate: DD-TVL-55667                  │ │
│ └─────────────────────────────────────────┘ │
│                                             │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions ⊕ More│
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
Screen: Direct Debits (UiState.Content — 3 Active, 1 Inactive; sorted Active-first by ViewModel)
│
mandate_summary_chips/ (chip_group, row, padding h 16dp top 16dp bottom 8dp, gap 8dp)
│   accessibility_label: "3 active, 1 inactive direct debit mandates"
│   state_binding: [content] — display-only, no on_click interaction
│
├── active_count_chip  (chip tonal, bg #C9E6FF text #004B6F, h 32dp radius 9999)
│                       label: "Active (3)"
│                       accessibility_label: "3 Active direct debits"
└── inactive_count_chip (chip outline, border #72787E text #41474D, h 32dp radius 9999)
                         label: "Inactive (1)"
                         accessibility_label: "1 Inactive direct debit"

direct_debits_list/ (list, vertical scroll, items_source: directDebits, gap 8dp,
│                    padding h 16dp bottom 16dp; state_binding: [content])
│   accessibility_label: "Direct debit mandates"
│
├── direct_debit_card[0] — British Gas (Active)
│   (card bg #F1F4F9, elevation 1, radius 12dp, padding 16dp)
│   (accessibility_label: "British Gas, Active")
│   stack vertical gap 8dp:
│   ├── dd_originator_name  (titleMedium 16sp/24sp w500 #181C20): "British Gas"
│   │                        role: heading
│   ├── dd_status_badge     (tonal primary, bg #C9E6FF text #004B6F, h 24dp radius 9999)
│   │                        value: "Active"
│   │                        accessibility_label: "Status: Active"
│   ├── dd_previous_amount  (headlineSmall 24sp/32sp w400 #181C20): "£78.00"
│   │                        role: amount; color neutral onSurface #181C20 (NOT error)
│   ├── dd_previous_date    (bodySmall 12sp/16sp w400 #41474D): "Last collected: 15 Jun 2026"
│   └── dd_mandate_id       (labelSmall 11sp/16sp w500 #41474D): "Mandate: DD-BG-44120"
│
├── direct_debit_card[1] — Vodafone (Active)
│   (card bg #F1F4F9, elevation 1, radius 12dp, padding 16dp)
│   (accessibility_label: "Vodafone, Active")
│   ├── dd_originator_name: "Vodafone" (titleMedium #181C20)
│   ├── dd_status_badge: "Active" (tonal primary bg #C9E6FF text #004B6F h 24dp r 9999)
│   ├── dd_previous_amount: "£29.00" (headlineSmall #181C20)
│   ├── dd_previous_date: "Last collected: 20 Jun 2026" (bodySmall #41474D)
│   └── dd_mandate_id: "Mandate: DD-VF-88301" (labelSmall #41474D)
│
├── direct_debit_card[2] — Aviva Insurance (Active)
│   (card bg #F1F4F9, elevation 1, radius 12dp, padding 16dp)
│   (accessibility_label: "Aviva Insurance, Active")
│   ├── dd_originator_name: "Aviva Insurance" (titleMedium #181C20)
│   ├── dd_status_badge: "Active" (tonal primary bg #C9E6FF text #004B6F h 24dp r 9999)
│   ├── dd_previous_amount: "£41.50" (headlineSmall #181C20)
│   ├── dd_previous_date: "Last collected: 05 Jun 2026" (bodySmall #41474D)
│   └── dd_mandate_id: "Mandate: DD-AV-10293" (labelSmall #41474D)
│
└── direct_debit_card[3] — TV Licensing (Inactive)
    (card bg #F1F4F9, elevation 1, radius 12dp, padding 16dp)
    (accessibility_label: "TV Licensing, Inactive")
    ├── dd_originator_name: "TV Licensing" (titleMedium #181C20)
    ├── dd_status_badge: "Inactive" (outline, border #72787E text #41474D h 24dp r 9999)
    ├── dd_previous_amount: "£13.25" (headlineSmall #181C20)
    ├── dd_previous_date: "Last collected: 01 Mar 2026" (bodySmall #41474D)
    └── dd_mandate_id: "Mandate: DD-TVL-55667" (labelSmall #41474D)

back_button/ + BottomNav/ — identical to loading state
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│ ← Direct Debits                             │  ← top_app_bar small h 64dp bg #F7F9FF
├─────────────────────────────────────────────┤
│                                             │
│                                             │
│                                             │
│           [subscriptions]                   │  ← icon 48dp #41474D centred
│                                             │    Material symbol: subscriptions
│  No direct debit mandates registered       │  ← title headlineSmall 24sp w400 #181C20
│                                             │    centred; padding h 32dp
│  No direct debit mandates are registered   │  ← body bodyMedium 14sp w400 #41474D
│  for this account.                         │    centred; max 3 lines
│                                             │
│                                             │
│                                             │
│                                             │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions ⊕ More│
└─────────────────────────────────────────────┘
```

### Component Hierarchy — empty

```
Screen: Direct Debits (UiState.Empty — Data.DirectDebit[] is empty in OBIE 200 response)
│
empty_direct_debits/ (empty_state, vertically centred, padding h 32dp;
│                     state_binding: [empty])
│   accessibility_label: "No direct debit mandates registered"
│
├── icon  (subscriptions 48dp #41474D, decorative: false,
│          contentDescription: "No direct debit mandates")
├── title (headlineSmall 24sp/32sp w400 #181C20 center):
│         "No direct debit mandates registered"
└── body  (bodyMedium 14sp/20sp w400 #41474D center):
          "No direct debit mandates are registered for this account."

back_button/ + BottomNav/ — identical to loading state; no retry or action buttons present
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│ ← Direct Debits                             │  ← top_app_bar small h 64dp bg #F7F9FF
├─────────────────────────────────────────────┤
│                                             │
│                                             │
│            [error_outline]                  │  ← icon 48dp #BA1A1A centred
│                                             │    Material symbol: error_outline
│    Unable to load direct debits            │  ← title headlineSmall 24sp #181C20
│                                             │    centred; padding h 32dp
│  Session expired. Please log in again.     │  ← body bodyMedium 14sp #41474D centred
│                                             │    bound to error.userMessage
│                                             │    (demo: TokenExpired 401)
│        [      Try again      ]              │  ← retry_button filled h 56dp
│                                             │    bg #266489 label #FFFFFF radius 9999
│                                             │    visible_when: error.isRetriable = true
│                                             │    HIDDEN for 403 ConsentRevoked
│                                             │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions ⊕ More│
└─────────────────────────────────────────────┘
```

Error sub-variants — same state, dynamic body text and retry_button visibility:

| Error ID | HTTP | isRetriable | userMessage (demo-data.yaml) | retry_button |
|---|---|---|---|---|
| TokenExpired | 401 | true | "Session expired. Please log in again." | visible |
| ConsentRevoked | 403 | **false** | "Account access consent has been revoked. Re-authorise in Consents." | **hidden** |
| RateLimited | 429 | true | "Too many requests. Please wait a moment and try again." | visible |
| NetworkError | — | true | "No network connection. Check your connection and retry." | visible |

### Component Hierarchy — error

```
Screen: Direct Debits (UiState.Error — demo: TokenExpired 401, isRetriable: true)
│
error_state/ (empty_state variant: error, vertically centred, padding h 32dp;
│             state_binding: [error])
│   accessibility_label: "Unable to load direct debits"
│
├── icon  (error_outline 48dp #BA1A1A, decorative: false,
│          contentDescription: "Error loading direct debits")
├── title (headlineSmall 24sp/32sp w400 #181C20 center):
│         "Unable to load direct debits"
├── body  (bodyMedium 14sp/20sp w400 #41474D center):
│         bound to {error.userMessage}
│         401 render: "Session expired. Please log in again."
│         403 render: "Account access consent has been revoked. Re-authorise in Consents."
│         429 render: "Too many requests. Please wait a moment and try again."
│         network:    "No network connection. Check your connection and retry."
└── retry_button (button variant: filled, h 56dp, min-touch 56dp, bg #266489,
                  label color #FFFFFF, radius 9999,
                  visible_when: error.isRetriable == true;
                  hidden for ConsentRevoked 403 — retry would always fail)
    label: "Try again"
    accessibility_label: "Retry loading direct debits"
    on_click → retryLoad() — re-invokes loadDirectDebits(accountId);
               transitions UiState Loading → Content | Empty on success

back_button/ + BottomNav/ — identical to all other states
```

---

### Interaction Summary

| Component | Action | Effect | Target / Behaviour |
|---|---|---|---|
| back_button | navigate_back | navigate | Pops Direct Debits from back stack; returns user to account-detail |
| retry_button | retry_load | call_api | Re-issues GET /accounts/{AccountId}/direct-debits via Ktorfit; visible only when `error.isRetriable == true` (hidden for 403 ConsentRevoked); screen transitions Loading → Content \| Empty on success |
| mandate_summary_chips | — | none | Display-only chip group; shows activeCount and inactiveCount from ViewModel; no on_click |
| direct_debit_card | — | none | Display-only (AISP read-only; no row-tap or expand interaction declared in ui.yaml) |

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| direct_debit_card | match_parent − 32dp (361dp) | wrap (~168dp) | 12dp |
| dd_status_badge Active (primary tonal) | hug content | 24dp | 9999dp (pill) |
| dd_status_badge Inactive (outline) | hug content | 24dp | 9999dp (pill) |
| active_count_chip (tonal) | hug content | 32dp | 9999dp (pill) |
| inactive_count_chip (outline) | hug content | 32dp | 9999dp (pill) |
| retry_button (filled) | match_parent − 64dp (265dp) | 56dp | 9999dp (pill) |
| skeleton_card (loading) | match_parent − 32dp (361dp) | 80dp | 12dp |
| top_app_bar | match_parent (393dp) | 64dp | 0dp |
| bottom_nav | match_parent (393dp) | 80dp | 0dp |
