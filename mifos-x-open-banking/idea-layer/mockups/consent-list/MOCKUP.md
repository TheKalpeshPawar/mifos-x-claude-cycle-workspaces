# Consent List — Visual Mockup

> Auto-generated from `screens/consent-list/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-16T00:00:00Z

---

## Screen: Data Sharing Consents

Canvas: 393×852dp (Pixel 5) · Top app bar visible (back arrow) · Bottom nav visible · No FAB · Roboto font · Material 3 light theme · bg #F7F9FF

Shell (from `app-shell.yaml` + `ui.yaml#shell`):
- Top app bar enabled · small variant · title "Data Sharing Consents" (strings.consent_list_title) · back arrow leading icon · bg #F7F9FF
- Bottom navigation — Home | Accounts | Transactions | More · More tab selected (screen reached via Settings → Manage consents)
- FAB disabled per `ui.yaml#shell.fab_visible: false`

---

### State: loading

```
┌─────────────────────────────────────────────┐
│ ← Data Sharing Consents                    │  ← top_app_bar small, titleMedium 16sp #181C20
│                                              │    bg #F7F9FF, leading back-arrow #41474D
├─────────────────────────────────────────────┤
│                                              │
│                                              │
│                                              │
│                   ◌                          │  ← progress_indicator circular
│               (spinning)                     │    tint primary #266489, size 48dp
│                                              │    vertically centered in safe area
│                                              │
│                                              │
│                                              │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions ⊕ More │  ← bottom_nav bg #F7F9FF h 80dp
│           (14sp/20sp) (14sp/20sp)  ← More  │    More selected tint #266489
└─────────────────────────────────────────────┘   others tint #41474D
```

### Component Hierarchy — loading

```
Screen: Data Sharing Consents (ConsentListUiState.Loading)
│
top_app_bar/ (small, bg #F7F9FF, elevation 0)
│   ├── leading back_arrow  (icon arrow_back 24dp #41474D)
│   └── title "Data Sharing Consents" (titleLarge 22sp/28sp #181C20)
│
loading_body/ (fill parent, vertically centered)
│   accessibility_label: "Loading your consents" (strings.consent_list_loading)
│
└── progress_indicator (circular, tint #266489, 48dp×48dp, centred)
    accessibility_label: "Loading consent status from HSBC" (strings.consent_list_loading)

BottomNav/ (persistent)
├── tab Home         (icon home,          label "Home",         tint #41474D)
├── tab Accounts     (icon account_balance,label "Accounts",    tint #41474D)
├── tab Transactions (icon receipt_long,  label "Transactions", tint #41474D)
└── tab More         (icon more_horiz,    label "More",         selected tint #266489)
```

---

### State: content

Demo data: has_near_expiry_consents=true → reconfirm_banner visible. Two active consents (aac-fb2c4e8a: 89 days; aac-d4e5f6a7: 7 days). One history consent (aac-a1b2c3d4: Expired 26 Jun 2026).

```
┌─────────────────────────────────────────────┐
│ ← Data Sharing Consents                    │  ← top_app_bar small bg #F7F9FF
│                                              │
├─────────────────────────────────────────────┤
│                                              │
│ ┌─────────────────────────────────────────┐ │  ← reconfirm_banner bg errorContainer #FFDAD6
│ │ ⚠  Reconfirmation required             │ │    icon warning_amber tint #BA1A1A
│ │    A consent expires in 7 days.        │ │    title bodyLarge #93000A
│ │    Reconfirm to maintain access.       │ │    body bodyMedium #93000A
│ └─────────────────────────────────────────┘ │    visible_when has_near_expiry_consents
│                                              │
│  Active                                      │  ← active_section_label labelLarge 14sp/20sp w500
│                                              │    color onSurfaceVariant #41474D
│                                              │    padding h 16dp top 8dp bottom 4dp
│ ┌─────────────────────────────────────────┐ │  ← consent_card[0] elevation 1 radius 12dp
│ │ [HSBC]          ✓ Authorised            │ │    bg surfaceContainerLow #F1F4F9
│ │ ─────────────────────────────────────── │ │    bank_logo 40×20dp, status_chip:
│ │                                          │ │      primaryContainer #C9E6FF text #004B6F
│ │  10 data types shared                   │ │  ← permission_summary bodyMedium 14sp #181C20
│ │  Expires in 89 days · 26 Sep 2026       │ │  ← expiry_countdown labelMedium 12sp #41474D
│ │  Connected 28 Jun 2026                  │ │  ← granted_since labelSmall 11sp #41474D
│ └─────────────────────────────────────────┘ │    on_click → consent-detail (aac-fb2c4e8a)
│                                              │
│ ┌─────────────────────────────────────────┐ │  ← consent_card[1] elevation 1 radius 12dp
│ │ [HSBC]          ✓ Authorised            │ │    bg surfaceContainerLow #F1F4F9
│ │                                          │ │    status_chip primaryContainer #C9E6FF
│ │ [⚠ Reconfirm soon]                     │ │  ← reconfirm_urgency_chip
│ │                                          │ │    bg errorContainer #FFDAD6 text #93000A
│ │                                          │ │    icon warning_amber, visible_when
│ │  4 data types shared                    │ │    days_until_expiry(7) ≤ 14 → true
│ │  Expires in 7 days  · 6 Jul 2026        │ │  ← expiry_countdown labelMedium 12sp error #BA1A1A
│ │  Connected 7 Apr 2026                   │ │  ← granted_since labelSmall 11sp #41474D
│ └─────────────────────────────────────────┘ │    on_click → consent-detail (aac-d4e5f6a7)
│                                              │
│  ─────────────────────────────────────────  │  ← section_divider outlineVariant #C1C7CE
│                                              │    visible_when has_active && has_history
│  History                                     │  ← history_section_label labelLarge #41474D
│                                              │
│ ┌─────────────────────────────────────────┐ │  ← history_consent_card elevation 0 radius 12dp
│ │ [HSBC]          ○ Expired               │ │    bg surface #F7F9FF
│ │                                          │ │    border outlineVariant #C1C7CE 1dp
│ │                                          │ │    history_status_chip:
│ │  Expired 26 Jun 2026                    │ │      surfaceVariant #DDE3EA text #41474D
│ │  Connected 12 Mar 2026                  │ │  ← history_expiry_label labelMedium #41474D
│ └─────────────────────────────────────────┘ │  ← history_connected_on labelSmall #41474D
│                                              │    on_click → consent-detail (aac-a1b2c3d4)
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions ⊕ More │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
Screen: Data Sharing Consents (ConsentListUiState.Content)
│
top_app_bar/ (small, bg #F7F9FF, elevation 0)
│   ├── leading back_arrow (icon arrow_back 24dp #41474D)
│   └── title "Data Sharing Consents" (titleLarge 22sp #181C20)
│
scroll_column/ (vertical scroll, padding h 16dp bottom 16dp)
│
├── reconfirm_banner/ (visible_when=has_near_expiry_consents → true)
│   │  bg errorContainer #FFDAD6, radius 8dp, padding 16dp, margin bottom 8dp
│   ├── icon  warning_amber (24dp tint #BA1A1A)
│   ├── title "Reconfirmation required" (bodyLarge 16sp/24sp w400 #93000A)
│   └── body  "A consent expires in 7 days. Reconfirm to maintain access." (bodyMedium 14sp #93000A)
│
├── active_section_label (text labelLarge 14sp/20sp w500 #41474D, padding top 8dp bottom 4dp)
│     "Active"
│
├── active_consents_list/ (list vertical gap 8dp, visible_when=has_active_consents → true)
│   │   items_source: active_consents [aac-fb2c4e8a, aac-d4e5f6a7]
│   │
│   ├── consent_card[aac-fb2c4e8a]/ (card elevation 1 radius 12dp padding 16dp
│   │   │  bg #F1F4F9, on_click → navigate consent-detail(consentId=aac-fb2c4e8a))
│   │   ├── consent_card_header_row/ (stack horizontal, alignment center_vertical, gap 8dp)
│   │   │   ├── bank_logo (image ic_hsbc_logo 40×20dp, contentDescription "HSBC")
│   │   │   └── status_chip (chip assist, label "Authorised", icon check_circle 16dp,
│   │   │                     bg primaryContainer #C9E6FF, text onPrimaryContainer #004B6F)
│   │   │   [reconfirm_urgency_chip: hidden — days_until_expiry(89) > 14]
│   │   ├── permission_summary (text bodyMedium 14sp #181C20): "10 data types shared"
│   │   ├── expiry_countdown  (text labelMedium 12sp #41474D): "Expires in 89 days · 26 Sep 2026"
│   │   └── granted_since     (text labelSmall 11sp #41474D): "Connected 28 Jun 2026"
│   │
│   └── consent_card[aac-d4e5f6a7]/ (card elevation 1 radius 12dp padding 16dp
│       │  bg #F1F4F9, on_click → navigate consent-detail(consentId=aac-d4e5f6a7))
│       ├── consent_card_header_row/ (stack horizontal gap 8dp)
│       │   ├── bank_logo (image ic_hsbc_logo 40×20dp, contentDescription "HSBC")
│       │   └── status_chip (chip assist, label "Authorised", icon check_circle 16dp,
│       │                     bg primaryContainer #C9E6FF, text onPrimaryContainer #004B6F)
│       ├── reconfirm_urgency_chip (chip assist VISIBLE — days_until_expiry(7) ≤ 14
│       │     label "Reconfirm soon", icon warning_amber 16dp,
│       │     bg errorContainer #FFDAD6, text onErrorContainer #93000A)
│       ├── permission_summary (text bodyMedium 14sp #181C20): "4 data types shared"
│       ├── expiry_countdown  (text labelMedium 12sp #BA1A1A): "Expires in 7 days · 6 Jul 2026"
│       └── granted_since     (text labelSmall 11sp #41474D): "Connected 7 Apr 2026"
│
├── section_divider (divider, height 1dp, color outlineVariant #C1C7CE,
│     margin v 8dp, visible_when=has_active && has_history → true)
│
├── history_section_label (text labelLarge 14sp/20sp w500 #41474D, padding top 8dp bottom 4dp)
│     "History"
│
└── history_consents_list/ (list vertical gap 8dp, visible_when=has_history_consents → true)
    │   items_source: history_consents [aac-a1b2c3d4]
    │
    └── history_consent_card[aac-a1b2c3d4]/ (card elevation 0 radius 12dp padding 16dp
        │  bg surface #F7F9FF, border outlineVariant #C1C7CE 1dp,
        │  on_click → navigate consent-detail(consentId=aac-a1b2c3d4))
        ├── history_card_header_row/ (stack horizontal gap 8dp)
        │   ├── bank_logo_history (image ic_hsbc_logo 40×20dp, contentDescription "HSBC")
        │   └── history_status_chip (chip assist, label "Expired", icon schedule 16dp,
        │                            bg surfaceVariant #DDE3EA, text onSurfaceVariant #41474D)
        ├── history_expiry_label  (text labelMedium 12sp #41474D): "Expired 26 Jun 2026"
        └── history_connected_on  (text labelSmall 11sp #41474D): "Connected 12 Mar 2026"

BottomNav/ (persistent)
├── tab Home         (icon home,           label "Home",         tint #41474D)
├── tab Accounts     (icon account_balance, label "Accounts",    tint #41474D)
├── tab Transactions (icon receipt_long,   label "Transactions", tint #41474D)
└── tab More         (icon more_horiz,     label "More",         selected tint #266489)
```

---

### State: empty

No ConsentIds stored locally — active and history lists are both empty.

```
┌─────────────────────────────────────────────┐
│ ← Data Sharing Consents                    │  ← top_app_bar bg #F7F9FF
│                                              │
├─────────────────────────────────────────────┤
│                                              │
│                                              │
│                                              │
│            [link_off]                        │  ← empty_state icon link_off
│                                              │    size 48dp, tint #41474D, centred
│                                              │
│       No consents yet                       │  ← title headlineSmall 24sp/32sp #181C20 centred
│                                              │
│   You haven't connected any bank            │
│   accounts via Open Banking yet.            │  ← body bodyMedium 14sp/20sp #41474D centred
│                                              │
│       [  Connect a bank  ]                  │  ← connect_button filled, 56dp h
│                                              │    bg primary #266489 text onPrimary #FFFFFF
│                                              │    radius 9999, min touch 56dp
│                                              │    on_click → user-onboarding
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions ⊕ More │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — empty

```
Screen: Data Sharing Consents (ConsentListUiState.Empty)
│
top_app_bar/ (small, bg #F7F9FF, elevation 0, leading back_arrow #41474D)
│
empty_state/ (state_binding: empty, vertically centred, padding horizontal 32dp)
│   accessibility_label: "No consents yet" (strings.consent_list_empty_a11y)
│
├── icon  (link_off 48dp tint #41474D, decorative: false,
│          contentDescription: "No bank accounts connected")
├── title (headlineSmall 24sp/32sp w400 #181C20 center):
│         "No consents yet"
├── body  (bodyMedium 14sp/20sp w400 #41474D center):
│         "You haven't connected any bank accounts via Open Banking yet."
└── connect_button (button variant:filled, 56dp h, bg #266489, label-color #FFFFFF,
                    radius 9999, min touch 56dp)
    label: "Connect a bank"
    accessibility_label: "Connect your bank account via Open Banking" (strings.consent_list_connect_a11y)
    on_click → navigate_connect → user-onboarding (RULE action_contract effect:navigate)

BottomNav/ (persistent — More tab selected)
```

---

### State: error

NetworkError or HTTP 500 from GET /account-access-consents/{ConsentId}.

```
┌─────────────────────────────────────────────┐
│ ← Data Sharing Consents                    │  ← top_app_bar bg #F7F9FF
│                                              │
├─────────────────────────────────────────────┤
│                                              │
│                                              │
│                                              │
│           [error_outline]                    │  ← error_state icon error_outline
│                                              │    size 48dp, tint error #BA1A1A, centred
│                                              │
│     Unable to load consents                 │  ← title headlineSmall 24sp/32sp #181C20 centred
│                                              │
│   No internet connection.                   │
│   Please try again.                         │  ← body bodyMedium 14sp #41474D centred
│                                              │    content from {error.message}
│                                              │
│         [  Try again  ]                     │  ← retry_button filled 56dp h
│                                              │    bg primary #266489 text #FFFFFF
│                                              │    radius 9999
│                                              │    on_click → retry_load (call_api)
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions ⊕ More │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — error

```
Screen: Data Sharing Consents (ConsentListUiState.Error — NetworkError)
│
top_app_bar/ (small, bg #F7F9FF, elevation 0, leading back_arrow #41474D)
│
error_state/ (variant:error, state_binding: error, vertically centred, padding horizontal 32dp)
│   accessibility_label: "Unable to load consents" (strings.consent_list_error_a11y)
│
├── icon  (error_outline 48dp tint #BA1A1A, decorative: false,
│          contentDescription: "Error loading consent status")
├── title (headlineSmall 24sp/32sp w400 #181C20 center):
│         "Unable to load consents"
├── body  (bodyMedium 14sp/20sp w400 #41474D center):
│         "{error.message}" — demo: "No internet connection. Please try again."
└── retry_button (button variant:filled, 56dp h, bg #266489, label-color #FFFFFF, radius 9999)
    label: "Try again"
    accessibility_label: "Retry loading consents" (strings.consent_list_retry_a11y)
    on_click → retry_load — effect: call_api — re-fetches all stored ConsentIds from
                             GET /account-access-consents/{ConsentId} via ktorfit

BottomNav/ (persistent — More tab selected)
```

---

### State: error_auth

HTTP 401 Unauthorized from consent-status fetch — PSU access token expired. Dedicated re-auth CTA instead of generic retry.

```
┌─────────────────────────────────────────────┐
│ ← Data Sharing Consents                    │  ← top_app_bar bg #F7F9FF
│                                              │
├─────────────────────────────────────────────┤
│                                              │
│                                              │
│                                              │
│             [lock_open]                      │  ← auth_error_state icon lock_open
│                                              │    size 48dp, tint error #BA1A1A, centred
│                                              │
│       Session expired                       │  ← title headlineSmall 24sp/32sp #181C20 centred
│                                              │
│   Your access has expired.                  │
│   Sign in again to view your               │  ← body bodyMedium 14sp #41474D centred
│   consent status.                           │
│                                              │
│         [  Sign in again  ]                 │  ← reauth_button filled 56dp h
│                                              │    bg primary #266489 text #FFFFFF radius 9999
│                                              │    on_click → navigate_reauth → login
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions ⊕ More │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — error_auth

```
Screen: Data Sharing Consents (ConsentListUiState.ErrorAuth — TokenExpiredSession HTTP 401)
│
top_app_bar/ (small, bg #F7F9FF, elevation 0, leading back_arrow #41474D)
│
auth_error_state/ (variant:error, state_binding: error_auth, vertically centred, padding h 32dp)
│   accessibility_label: "Session expired" (strings.consent_list_auth_error_a11y)
│
├── icon  (lock_open 48dp tint #BA1A1A, decorative: false,
│          contentDescription: "Session expired")
├── title (headlineSmall 24sp/32sp w400 #181C20 center):
│         "Session expired"
├── body  (bodyMedium 14sp/20sp w400 #41474D center):
│         "Your access has expired. Sign in again to view your consent status."
└── reauth_button (button variant:filled, 56dp h, bg #266489, label-color #FFFFFF, radius 9999)
    label: "Sign in again"
    accessibility_label: "Sign in again to renew your session" (strings.consent_list_reauth_a11y)
    on_click → navigate_reauth — effect: navigate — target: login
               (re-initiates FAPI OAuth flow to renew PSU access token)

BottomNav/ (persistent — More tab selected)
```

---

### Interaction Summary

| Component | Action | Effect | Target / Behaviour |
|---|---|---|---|
| consent_card (active list, any) | navigate_consent_detail | navigate | consent-detail screen · param consentId="{item.Data.ConsentId}" · pastes OBIE ConsentId as route param for status/permissions/expiry display |
| history_consent_card (history list, any) | navigate_consent_detail | navigate | consent-detail screen · param consentId="{item.Data.ConsentId}" · shows historical record for Expired or Revoked consent |
| connect_button (empty state) | navigate_connect | navigate | user-onboarding screen · begins fresh FAPI account-access consent flow |
| retry_button (error state) | retry_load | call_api | Re-fetches status for all locally stored ConsentIds via GET /account-access-consents/{ConsentId} through ktorfit · transitions back to loading then content \| error |
| reauth_button (error_auth state) | navigate_reauth | navigate | login screen · re-initiates FAPI OAuth flow to renew expired PSU access token (HTTP 401 recovery path) |

---

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| top_app_bar | match_parent | 56dp | 0 |
| reconfirm_banner | match_parent − 32dp | wrap (≈72dp) | 8dp |
| active_section_label | match_parent − 32dp | 20dp | 0 |
| consent_card (active) | match_parent − 32dp | wrap (≈116dp) | 12dp |
| bank_logo (ic_hsbc_logo) | 40dp | 20dp | 0 |
| status_chip (Authorised / Expired) | hug content | 28dp | 9999dp (full pill) |
| reconfirm_urgency_chip | hug content | 28dp | 9999dp (full pill) |
| section_divider | match_parent − 32dp | 1dp | 0 |
| history_section_label | match_parent − 32dp | 20dp | 0 |
| history_consent_card | match_parent − 32dp | wrap (≈88dp) | 12dp |
| empty_state icon (link_off) | 48dp | 48dp | 0 |
| connect_button | match_parent − 64dp | 56dp | 9999dp (full pill) |
| retry_button | match_parent − 64dp | 56dp | 9999dp (full pill) |
| reauth_button | match_parent − 64dp | 56dp | 9999dp (full pill) |
| bottom_nav | match_parent | 80dp | 0 |
