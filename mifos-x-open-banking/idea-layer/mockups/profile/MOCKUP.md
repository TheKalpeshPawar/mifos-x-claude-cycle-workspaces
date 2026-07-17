# Profile — Visual Mockup

> Auto-generated from `screens/profile/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-16T00:00:00Z

---

## Screen: Profile

Canvas: 393×852dp (Pixel 5) · Top app bar (small, leading ← back, title "Profile") · Bottom nav visible · No FAB · Roboto font · Material 3 light theme · bg #F7F9FF

Shell (from `app-shell.yaml` + `ui.yaml#shell`):
- Top app bar: small variant, title "Profile" (Roboto 22sp #181C20), leading back-arrow navigation icon (← #181C20).
- Bottom navigation: **Home** (home icon) | **Accounts** (account_balance) | **Transactions** (receipt_long) | **More** (more_horiz → settings screen). Profile is outside the primary rail so no tab is selected.
- FAB: disabled (`ui.yaml#shell.fab_visible: false`).

---

### State: loading

```
┌─────────────────────────────────────────────┐
│ ←  Profile                                  │  ← top_app_bar: h 56dp, bg #F7F9FF
│                                             │    title Roboto 22sp weight 400 #181C20
├─────────────────────────────────────────────┤
│                                             │
│                                             │
│                                             │
│                   ◌                         │  ← progress_indicator (circular)
│             (spinning arc)                  │    size 40dp, stroke 4dp
│                                             │    color: primary #266489
│                                             │    centered in available viewport area
│                                             │    accessibility: "Loading your profile"
│                                             │
│                                             │
├─────────────────────────────────────────────┤
│  ⌂      ◫       ≡       ⊕                  │  ← bottom_nav: h 80dp, bg #F7F9FF
│ Home Accounts Trans…  More                  │    icons 24dp, labels labelMedium 12sp
│                                             │    no tab selected, all icons #41474D
└─────────────────────────────────────────────┘
```

### Component Hierarchy — loading

```
Screen: Profile (ProfileUiState.Loading)
│
ContentArea/ (fills 393×(852-56-80)dp = 393×716dp)
│   gravity: center
│
└── progress_indicator  (CircularProgressIndicator, size 40dp, color #266489)
        accessibility_label: "Loading your profile"
        reduce-motion: static shimmer arc, no animation

BottomNav/ (persistent across all states)
├── tab Home         (icon:home,           label:"Home",         tint #41474D)
├── tab Accounts     (icon:account_balance, label:"Accounts",    tint #41474D)
├── tab Transactions (icon:receipt_long,   label:"Transactions", tint #41474D)
└── tab More         (icon:more_horiz,     label:"More",         tint #41474D)
```

---

### State: content

```
┌─────────────────────────────────────────────┐
│ ←  Profile                                  │  ← top_app_bar bg #F7F9FF
├─────────────────────────────────────────────┤
│                                             │
│ ┌─────────────────────────────────────────┐ │  ← identity_header_card
│ │                                         │ │    Card elevation 2 (shadow 3dp)
│ │            ┌────────┐                   │ │    bg #EBEEF3 (surfaceContainerHigh)
│ │            │   PS   │                   │ │    radius 12dp, padding 16dp
│ │            └────────┘                   │ │    items centered horizontally
│ │                                         │ │  ← user_avatar: 72×72dp, circle
│ │         Priya Sharma                    │ │    bg #C9E6FF, initials "PS"
│ │        Personal account                 │ │    initials text: labelLarge 14sp #004B6F
│ │                                         │ │  ← user_full_name: headlineMedium 28sp #181C20
│ └─────────────────────────────────────────┘ │  ← party_type: labelMedium 12sp #50606E
│                                             │
│  IDENTITY                                   │  ← identity_section_header: titleSmall
│                                             │    14sp w500 #41474D, paddingH 0dp paddingV 8dp
│  ✉  Email                                  │  ← email_row ListItem
│     priya.sharma@example.co.uk             │    icon:email 24dp #50606E
│                                             │    label: bodySmall 12sp #41474D "Email"
│  📱  Mobile                                │  ← mobile_row ListItem
│     +44 7700 900482                        │    icon:phone 24dp #50606E
│                                             │    label: bodySmall 12sp #41474D "Mobile"
│  🏠  Address                               │  ← address_row ListItem
│     12 Baker Street, London W1U 6TZ        │    icon:home 24dp #50606E
│                                             │    label: bodySmall 12sp #41474D "Address"
│  OPEN BANKING CONNECTION                   │  ← connection_section_header: titleSmall
│                                             │    14sp w500 #41474D
│ ┌─────────────────────────────────────────┐ │  ← consent_summary_card
│ │  🏛  HSBC Open Banking                  │ │    Card elevation 1 (shadow 1dp)
│ │                                         │ │    bg #F1F4F9 (surfaceContainerLow)
│ │  ✔  Status                              │ │    radius 12dp, padding 16dp
│ │      Authorised                         │ │  ← bank_label: icon account_balance #266489
│ │                                         │ │    titleMedium 16sp #181C20
│ │  ⏱  Expires                             │ │  ← consent_status_row: icon verified #266489
│ │      26 Sep 2026                        │ │    label bodySmall #41474D / supporting #266489
│ │                                         │ │  ← consent_expiry_row: icon schedule #50606E
│ │  Permissions                            │ │    label bodySmall #41474D / supporting #181C20
│ │  ✓  Account information                 │ │  ← permissions_section_header labelMedium #41474D
│ │  ✓  Balances                            │ │  ← perm_accounts_detail check_circle #266489
│ │  ✓  Transaction details                 │ │  ← perm_balances           check_circle #266489
│ │  ✓  Personal identity                   │ │  ← perm_transactions       check_circle #266489
│ │                                         │ │  ← perm_party              check_circle #266489
│ │        ┌────────────────────┐           │ │
│ │        │  Manage consent   │           │ │  ← manage_consent_button: tonal
│ │        └────────────────────┘           │ │    bg #C9E6FF, text #004B6F
│ └─────────────────────────────────────────┘ │    radius 20dp, h 40dp, minW 160dp
│                                             │
│  ┌───────────────────────────────────────┐  │  ← sign_out_button: outlined
│  │           Sign out                    │  │    border #BA1A1A (1dp), label #BA1A1A
│  └───────────────────────────────────────┘  │    fill 361dp w, h 40dp, radius 20dp
│                                             │
├─────────────────────────────────────────────┤
│  ⌂      ◫       ≡       ⊕                  │  ← bottom_nav
│ Home Accounts Trans…  More                  │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
Screen: Profile (ProfileUiState.Content)
│
LazyColumn/ (vertical scroll, paddingH 16dp, paddingTop 16dp, paddingBottom 96dp, gap 16dp)
│
├── identity_header_card/ (Card elevation 2, radius 12dp, bg #EBEEF3)
│   │   padding 16dp, Column centered horizontally, gap 8dp
│   ├── user_avatar        (Box 72×72dp, shape Circle, bg #C9E6FF)
│   │   └── initials text  ("PS", labelLarge 14sp #004B6F, centered)
│   ├── user_full_name     (Text headlineMedium 28sp #181C20, "Priya Sharma")
│   └── party_type         (Text labelMedium 12sp #50606E, "Personal account")
│
├── identity_section_header (Text titleSmall 14sp w500 #41474D uppercase, "IDENTITY")
│
├── identity_list/ (Column, divider outlineVariant #C1C7CE, startPadding 56dp)
│   ├── email_row    (ListItem icon:email #50606E, label:"Email",
│   │                  supporting:"priya.sharma@example.co.uk" bodyMedium #181C20)
│   ├── mobile_row   (ListItem icon:phone #50606E, label:"Mobile",
│   │                  supporting:"+44 7700 900482" bodyMedium #181C20)
│   └── address_row  (ListItem icon:home #50606E, label:"Address",
│                       supporting:"12 Baker Street, London W1U 6TZ" bodyMedium #181C20)
│
├── connection_section_header (Text titleSmall 14sp w500 #41474D, "OPEN BANKING CONNECTION")
│
├── consent_summary_card/ (Card elevation 1, radius 12dp, bg #F1F4F9)
│   │   padding 16dp, Column gap 8dp
│   ├── bank_label           (Row: Icon account_balance 20dp #266489, Text titleMedium 16sp #181C20
│   │                           "HSBC Open Banking")
│   ├── consent_status_row   (ListItem icon:verified #266489 label:"Status"
│   │                           supporting:"Authorised" bodyMedium #266489)
│   ├── consent_expiry_row   (ListItem icon:schedule #50606E label:"Expires"
│   │                           supporting:"26 Sep 2026" bodyMedium #181C20)
│   ├── permissions_section_header (Text labelMedium 12sp w500 #41474D, "Permissions")
│   ├── permissions_list/
│   │   ├── perm_accounts_detail (ListItem icon:check_circle #266489 "Account information")
│   │   ├── perm_balances        (ListItem icon:check_circle #266489 "Balances")
│   │   ├── perm_transactions    (ListItem icon:check_circle #266489 "Transaction details")
│   │   └── perm_party           (ListItem icon:check_circle #266489 "Personal identity")
│   └── manage_consent_button (FilledTonalButton bg #C9E6FF text #004B6F "Manage consent"
│                                radius 20dp, h 40dp, onClick→navigate consent-detail)
│
├── sign_out_button (OutlinedButton border #BA1A1A label #BA1A1A "Sign out"
│                    fillWidth true, h 40dp, radius 20dp)
│
BottomNav/ (persistent)
├── tab Home (icon:home, tint #41474D) · tab Accounts · tab Transactions · tab More
```

---

### State: content_expiring

```
┌─────────────────────────────────────────────┐
│ ←  Profile                                  │  ← top_app_bar bg #F7F9FF
├─────────────────────────────────────────────┤
│                                             │
│ ┌─────────────────────────────────────────┐ │  ← identity_header_card (same as content)
│ │            ┌────────┐                   │ │
│ │            │   PS   │                   │ │  ← user_avatar #C9E6FF "PS" #004B6F
│ │            └────────┘                   │ │
│ │         Priya Sharma                    │ │  ← user_full_name headlineMedium #181C20
│ │        Personal account                 │ │  ← party_type labelMedium #50606E
│ └─────────────────────────────────────────┘ │
│                                             │
│  IDENTITY                                   │  ← identity_section_header
│  ✉  Email                                  │
│     priya.sharma@example.co.uk             │  ← email_row (real data)
│  📱  Mobile                                │
│     +44 7700 900482                        │  ← mobile_row (real data)
│  🏠  Address                               │
│     12 Baker Street, London W1U 6TZ        │  ← address_row (real data)
│                                             │
│ ┌─────────────────────────────────────────┐ │  ← expiry_warning_banner
│ │ ⚠  Your consent expires in 5 days.     │ │    Card elevation 0, variant:advisory
│ │    Please renew to keep access.         │ │    bg #EADDFF (tertiaryContainer)
│ │                                         │ │    radius 12dp, padding 12dp
│ │    ┌────────────────────┐               │ │  ← warning_icon: warning_amber 24dp #4C4162
│ │    │  Renew Consent    │               │ │  ← expiry_warning_text: bodyMedium #4C4162
│ │    └────────────────────┘               │ │  ← renew_consent_button: tonal
│ └─────────────────────────────────────────┘ │    bg #DDE3EA text #41474D radius 20dp
│                                             │
│  OPEN BANKING CONNECTION                   │  ← connection_section_header
│ ┌─────────────────────────────────────────┐ │  ← consent_summary_card elevation 1
│ │  🏛  HSBC Open Banking                  │ │
│ │  ✔  Status       Authorised             │ │  ← consent_status_row verified #266489
│ │  ⏱  Expires      04 Jul 2026            │ │  ← consent_expiry_row (expiring fixture)
│ │                                         │ │
│ │  Permissions                            │ │
│ │  ✓  Account information                 │ │  ← 4 permissions (expiring fixture subset)
│ │  ✓  Balances                            │ │
│ │  ✓  Transaction details                 │ │
│ │  ✓  Personal identity                   │ │
│ │                                         │ │
│ │        ┌────────────────────┐           │ │
│ │        │  Manage consent   │           │ │  ← manage_consent_button tonal #C9E6FF
│ │        └────────────────────┘           │ │
│ └─────────────────────────────────────────┘ │
│                                             │
│  ┌───────────────────────────────────────┐  │  ← sign_out_button outlined #BA1A1A
│  │           Sign out                    │  │    (visible in content_expiring)
│  └───────────────────────────────────────┘  │
│                                             │
├─────────────────────────────────────────────┤
│  ⌂      ◫       ≡       ⊕                  │  ← bottom_nav
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content_expiring

```
Screen: Profile (ProfileUiState.ContentExpiring)
│
LazyColumn/ (same padding as content state, gap 16dp)
│
├── identity_header_card/ (Card elevation 2, radius 12dp — identical to content state)
│   ├── user_avatar ("PS", #C9E6FF / #004B6F, 72dp)
│   ├── user_full_name ("Priya Sharma", headlineMedium #181C20)
│   └── party_type ("Personal account", labelMedium #50606E)
│
├── identity_section_header ("IDENTITY", titleSmall #41474D)
│
├── identity_list/ (email_row + mobile_row + address_row — same real data as content)
│
├── expiry_warning_banner/ (Card elevation 0, radius 12dp, bg #EADDFF, padding 12dp)
│   │   Row layout: icon leading, Column (text + button) trailing
│   ├── warning_icon         (Icon warning_amber 24dp, tint #4C4162, contentDescription "")
│   ├── expiry_warning_text  (Text bodyMedium 14sp #4C4162,
│   │                          "Your consent expires in 5 days. Please renew to keep access.")
│   └── renew_consent_button (FilledTonalButton bg #DDE3EA text #41474D "Renew Consent"
│                               radius 20dp h 40dp, onClick→navigate_consent_renew)
│
├── connection_section_header ("OPEN BANKING CONNECTION", titleSmall #41474D)
│
├── consent_summary_card/ (elevation 1, radius 12dp — expiring fixture data)
│   ├── bank_label           ("HSBC Open Banking", account_balance icon #266489)
│   ├── consent_status_row   (supporting:"Authorised", verified icon #266489)
│   ├── consent_expiry_row   (supporting:"04 Jul 2026", schedule icon #50606E)
│   ├── permissions_list/ (4 items: Account information, Balances, Transaction details, Personal identity)
│   └── manage_consent_button (tonal #C9E6FF/#004B6F)
│
├── sign_out_button (OutlinedButton #BA1A1A — state_binding includes content_expiring)
│
BottomNav/
```

---

### State: confirm_sign_out

```
┌─────────────────────────────────────────────┐
│ ←  Profile                                  │  ← top_app_bar bg #F7F9FF
├─────────────────────────────────────────────┤
│  (content beneath — scrollable but dimmed)  │
│ ┌─────────────────────────────────────────┐ │  ← identity_header_card
│ │  [PS]   Priya Sharma                   │ │    (rendered under scrim)
│ │         Personal account               │ │
│ └─────────────────────────────────────────┘ │
│  IDENTITY                                   │
│  ✉  priya.sharma@example.co.uk             │
│  📱  +44 7700 900482                        │
│  🏠  12 Baker Street, London W1U 6TZ        │
│  OPEN BANKING CONNECTION                   │
│ ┌─────────────────────────────────────────┐ │  ← consent_summary_card (under scrim)
│ │  HSBC Open Banking · Authorised         │ │
│ │  Expires 26 Sep 2026                    │ │
│ └─────────────────────────────────────────┘ │
│                  ░░░░░░░░░░░░░░░░            │  ← scrim #00000066 (40% alpha)
│          ╔════════════════════════╗          │  ← sign_out_dialog
│          ║   Sign out?            ║          │    bg #FFFFFF, radius 28dp
│          ║                        ║          │    elevation level4 (8dp)
│          ║ You will be signed out ║          │    width 280dp, paddingH 24dp, paddingV 24dp
│          ║ and your session       ║          │
│          ║ will end.              ║          │  ← title: titleLarge 22sp #181C20
│          ║                        ║          │  ← body: bodyMedium 14sp #41474D
│          ║  [Cancel]  [Sign out]  ║          │
│          ╚════════════════════════╝          │  ← cancel_sign_out_button: TextButton #266489
│                  ░░░░░░░░░░░░░░░░            │  ← confirm_sign_out_button: FilledButton
│                                             │    bg #BA1A1A text #FFFFFF
├─────────────────────────────────────────────┤
│  ⌂      ◫       ≡       ⊕                  │  ← bottom_nav (behind scrim)
└─────────────────────────────────────────────┘
```

### Component Hierarchy — confirm_sign_out

```
Screen: Profile (ProfileUiState.ConfirmSignOut)
│
LazyColumn/ (same content as content state — identity_header_card + identity_list
│   + consent_summary_card — rendered beneath modal scrim; sign_out_button HIDDEN,
│   state_binding:[content, content_expiring] does NOT include confirm_sign_out)
│
Scrim/ (Box fill, bg #00000066, non-dismissable on outside tap for destructive confirm)
│
sign_out_dialog/ (AlertDialog, radius 28dp, bg #FFFFFF, elevation 8dp, width 280dp)
│   │   padding 24dp, Column gap 16dp
│   ├── title text          (Text titleLarge 22sp #181C20, "Sign out?")
│   ├── body text           (Text bodyMedium 14sp #41474D,
│   │                         "You will be signed out and your session will end.")
│   └── action_row/ (Row gap 8dp, end-aligned)
│       ├── cancel_sign_out_button  (TextButton label:"Cancel" text #266489,
│       │                             onClick→dismiss_sign_out_dialog → previous state)
│       └── confirm_sign_out_button (FilledButton label:"Sign out" bg #BA1A1A text #FFFFFF,
│                                     onClick→execute_sign_out → delete tokens → login)
│
BottomNav/ (visible behind scrim, not interactive while dialog open)
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│ ←  Profile                                  │  ← top_app_bar bg #F7F9FF
├─────────────────────────────────────────────┤
│                                             │
│                                             │
│                                             │
│                  ⊗                          │  ← error_outline icon 48dp, tint #BA1A1A
│                                             │    centered horizontally at ~38% height
│         Couldn't load your profile         │  ← error_state.title: titleLarge 22sp #181C20
│                                             │    centered, paddingH 32dp
│   Consent does not include profile access.  │  ← error.message: bodyMedium 14sp #41474D
│   The ReadParty permission was not granted  │    (EC-PROF-002 — 403 fixture)
│   when you authorised this app.             │    centered, paddingH 32dp
│                                             │
│              ┌─────────┐                   │
│              │  Retry  │                   │  ← retry_button: FilledButton
│              └─────────┘                   │    bg #266489 text #FFFFFF
│                                             │    minWidth 120dp h 40dp radius 20dp
│                                             │    centered horizontally
│                                             │
├─────────────────────────────────────────────┤
│  ⌂      ◫       ≡       ⊕                  │  ← bottom_nav
└─────────────────────────────────────────────┘
```

### Component Hierarchy — error

```
Screen: Profile (ProfileUiState.Error)
│
EmptyStateLayout/ (Box fill, gravity center, paddingH 32dp, gap 16dp Column)
│
error_state/ (EmptyState variant:error)
│   ├── error_outline icon  (Icon 48dp, tint #BA1A1A, contentDescription "Error")
│   ├── title text          (Text titleLarge 22sp #181C20, "Couldn't load your profile"
│   │                          centered, paddingH 32dp)
│   ├── body text           (Text bodyMedium 14sp #41474D, error.message
│   │                          "Consent does not include profile access. The ReadParty
│   │                           permission was not granted when you authorised this app."
│   │                          centered, paddingH 32dp)
│   └── retry_button (FilledButton bg #266489 text #FFFFFF "Retry"
│                       minWidth 120dp h 40dp radius 20dp centered,
│                       onClick→retry_load: call_api GET /accounts/{AccountId}/party)
│
BottomNav/
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│ ←  Profile                                  │  ← top_app_bar bg #F7F9FF
├─────────────────────────────────────────────┤
│                                             │
│                                             │
│                                             │
│                 ○×                          │  ← account_circle_off icon 48dp, tint #50606E
│                                             │    centered horizontally at ~38% height
│       No profile data available             │  ← profile_empty_state.title: titleLarge
│                                             │    22sp #181C20, centered, paddingH 32dp
│  We couldn't retrieve your identity from    │  ← profile_empty_state.body: bodyMedium
│  HSBC. Your consent may not include         │    14sp #41474D, centered, paddingH 32dp
│  identity access. Re-authorise to           │
│  regain access.                             │
│                                             │
│          ┌────────────────┐                │
│          │  Re-authorise  │                │  ← profile_empty_reauth_button: FilledButton
│          └────────────────┘                │    bg #266489 text #FFFFFF
│                                             │    minWidth 160dp h 40dp radius 20dp
│                                             │    centered horizontally
├─────────────────────────────────────────────┤
│  ⌂      ◫       ≡       ⊕                  │  ← bottom_nav
└─────────────────────────────────────────────┘
```

### Component Hierarchy — empty

```
Screen: Profile (ProfileUiState.Empty)
│
EmptyStateLayout/ (Box fill, gravity center, paddingH 32dp, gap 16dp Column)
│
profile_empty_state/ (EmptyState variant:neutral)
│   ├── account_circle_off icon (Icon 48dp, tint #50606E,
│   │                             contentDescription "No profile data")
│   ├── title text              (Text titleLarge 22sp #181C20,
│   │                             "No profile data available", centered, paddingH 32dp)
│   ├── body text               (Text bodyMedium 14sp #41474D,
│   │                             "We couldn't retrieve your identity from HSBC. Your consent
│   │                              may not include identity access. Re-authorise to regain access."
│   │                             centered, paddingH 32dp)
│   └── profile_empty_reauth_button (FilledButton bg #266489 text #FFFFFF "Re-authorise"
│                                      minWidth 160dp h 40dp radius 20dp centered,
│                                      onClick→navigate_reauth → login screen,
│                                      re-initiates FAPI authorization flow with ReadParty scope)
│
BottomNav/
```

---

### Interaction Summary

| Component | Action | Effect | Target / Outcome |
|---|---|---|---|
| renew_consent_button | navigate_consent_renew | navigate | `consent-detail` (with renew=true param) |
| manage_consent_button | navigate_consent_detail | navigate | `consent-detail` |
| sign_out_button | confirm_sign_out | transform_state | transitions to `confirm_sign_out`; saves `previousState` |
| cancel_sign_out_button | dismiss_sign_out_dialog | transform_state | restores `previousState` (content or content_expiring) |
| confirm_sign_out_button | execute_sign_out | delete | clears access token + refresh token + ConsentId from EncryptedSharedPreferences; navigates to `login` |
| retry_button | retry_load | call_api | re-invokes `loadProfile()` via GET /accounts/{AccountId}/party (ktorfit); transitions loading → content / error |
| profile_empty_reauth_button | navigate_reauth | navigate | `login` (re-initiates FAPI authorization flow to grant ReadParty scope) |

---

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| top_app_bar | 393dp (fill) | 56dp | 0dp |
| identity_header_card | 361dp (fill − 2×16dp) | 130dp | 12dp |
| user_avatar | 72dp | 72dp | 36dp (full circle) |
| expiry_warning_banner | 361dp (fill − 2×16dp) | 88dp | 12dp |
| consent_summary_card | 361dp (fill − 2×16dp) | 280dp | 12dp |
| manage_consent_button | 180dp (wrap) | 40dp | 20dp (stadium) |
| sign_out_button | 361dp (fill) | 40dp | 20dp (stadium) |
| sign_out_dialog | 280dp | 200dp | 28dp |
| cancel_sign_out_button | 80dp (wrap) | 40dp | 20dp (stadium) |
| confirm_sign_out_button | 100dp (wrap) | 40dp | 20dp (stadium) |
| renew_consent_button | 160dp (wrap) | 40dp | 20dp (stadium) |
| retry_button | 120dp (wrap) | 40dp | 20dp (stadium) |
| profile_empty_reauth_button | 160dp (wrap) | 40dp | 20dp (stadium) |
| bottom_navigation | 393dp (fill) | 80dp | 0dp |
| bottom_nav icon touch target | 48dp | 48dp | 24dp (circular) |
