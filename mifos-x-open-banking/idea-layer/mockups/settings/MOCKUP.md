# Settings — Visual Mockup

> Auto-generated from `screens/settings/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Source: DataStore preferences (kotlinx-serialization + Room/SQLDelight, no network)
> Generated: 2026-07-16T00:00:00Z

---

## Screen: Settings

Canvas: 393×852dp (Pixel 5) · Top app bar small (title "Settings", no leading icon) · Bottom nav active on "More" tab · Roboto font · Material 3 light theme · background #F7F9FF

---

### State: loading

```
┌─────────────────────────────────────────────────┐
│ Settings                                        │  ← top_app_bar small, bg #F7F9FF
│                                                 │    title titleLarge #181C20
├─────────────────────────────────────────────────┤
│                                                 │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │  ← settings_loading_skeleton
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │    list variant × 8 rows
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │    each row: 56dp h, radius 4dp
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │    shimmer surfaceVariant #DDE3EA
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │    pulse animation 1.5 s
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
│                                                 │
├─────────────────────────────────────────────────┤
│  ⌂ Home   ◫ Accounts  ▤ Transactions  ●More   │  ← bottom nav, More selected #266489
└─────────────────────────────────────────────────┘
```

### Component Hierarchy — loading

```
top_app_bar/ (title "Settings", no leading, no trailing)
settings_loading_skeleton/ (list variant, 8 shimmer rows)
├── skeleton_row_1 (56dp, radius 4dp, surfaceVariant #DDE3EA)
├── skeleton_row_2
├── skeleton_row_3
├── skeleton_row_4
├── skeleton_row_5
├── skeleton_row_6
├── skeleton_row_7
└── skeleton_row_8
BottomNav (Home | Accounts | Transactions | More●)
```

---

### State: content

```
┌─────────────────────────────────────────────────┐
│ Settings                                        │  ← top_app_bar small #F7F9FF
├─────────────────────────────────────────────────┤
│                                                 │  ← scrollable LazyColumn, padding 16dp
│  APPEARANCE                                     │  ← appearance_header section_header
│                                                 │    labelMedium #41474D, 40dp h
│  Theme                                          │  ← theme_row list_item 56dp
│  System default                   [▼ System ]   │    trailing: theme_dropdown
│                                                 │    dropdown bg #EBEEF3 radius 4dp
│  SECURITY                                       │  ← security_header section_header
│                                                 │
│  Biometric lock                                 │  ← biometric_row list_item
│  Require fingerprint or face ID on app open     │    supporting bodyMedium #41474D
│                                      [  ●  ]   │    biometric_switch ON → #266489
│                                                 │    track width 51dp h 28dp radius 14dp
│  Session timeout                                │  ← session_timeout_row list_item
│  Auto-lock after inactivity        [▼ 5 min ]   │    session_dropdown, 5 minutes selected
│                                                 │
│  PERMISSIONS                                    │  ← permissions_header section_header
│                                                 │    labelMedium #41474D
│  📍 Location                        ↗           │  ← location_permission_row info_row
│  Used for ATM distance sorting     granted      │    icon: location_on #266489
│                                                 │    status chip: granted #C9E6FF
│                                                 │    trailing: open_in_new #41474D
│  NOTIFICATIONS                                  │  ← notifications_header
│                                                 │
│  Consent expiry reminders                       │  ← consent_expiry_notif_row list_item
│  Alert before your Open Banking consent expires │
│                                      [  ●  ]   │    consent_expiry_switch ON → #266489
│  Security alerts                               │  ← security_alerts_notif_row list_item
│  Notify for unusual access or login events      │
│                                      [  ●  ]   │    security_alerts_switch ON → #266489
│                                                 │
│  STORAGE                                        │  ← storage_header section_header
│                                                 │
│  💾 PFM data                                    │  ← pfm_storage_location_row info_row
│  /data/data/org.mifosx.openbanking/files/       │    icon: storage #41474D
│  databases/pfm_cache                           │    display only, no trailing icon
│  Shared by dashboard & spending analysis        │    bodySmall #41474D
│                                                 │
│  🧹 Clear PFM cache                    >        │  ← clear_pfm_cache_row list_item
│  Remove aggregated spending & category data     │    icon: cleaning_services #41474D
│                                                 │    trailing: chevron_right #41474D
│  ACCOUNT                                        │  ← account_header
│                                                 │
│  🛡  Manage consents                    >       │  ← manage_consents_row list_item
│     View and revoke Open Banking access         │    icon: policy #41474D
│  👤  Profile                            >       │  ← profile_row list_item
│     Account holder identity details             │    icon: account_circle #41474D
│  🗑  Clear local data                   >       │  ← clear_local_data_row list_item
│     Erase cached account and transaction data   │    icon: delete_sweep #41474D
│                                                 │
│  ABOUT & LEGAL                                  │  ← about_header
│                                                 │
│  📄  Terms of service                   ↗       │  ← terms_row, icon: article
│  🔒  Privacy policy                     ↗       │  ← privacy_row, icon: privacy_tip
│  ℹ  Open source licences               >       │  ← licences_row, icon: info_outline
│  Version                    0.1.0 (build 1)    │  ← app_version_row (no tap target)
│                                                 │    supporting bodySmall #41474D
│                                                 │
├─────────────────────────────────────────────────┤
│  ⌂ Home   ◫ Accounts  ▤ Transactions  ●More   │
└─────────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
top_app_bar/ (title "Settings", no leading, no trailing)
[scrollable LazyColumn, padding h 16dp]
appearance_header/ (section_header): "APPEARANCE" (labelMedium #41474D, 40dp)
appearance_list/
└── theme_row (list_item 56dp, headlineLabel "Theme", supporting "System default")
    └── theme_dropdown (select, [Light / Dark / System], value "System", bg #EBEEF3 radius 4dp)
        on_click=update_theme → persist_db DataStore
security_header/ "SECURITY"
security_list/
├── biometric_row (list_item, "Biometric lock", supporting "Require fingerprint or face ID…")
│   └── biometric_switch (switch ON, #266489, 51×28dp radius 14dp)
│       on_click=toggle_biometric_lock → persist_db DataStore
└── session_timeout_row (list_item, "Session timeout", supporting "Auto-lock after inactivity")
    └── session_dropdown (select, [2 min / 5 min / 10 min / 30 min], value "5 minutes")
        on_click=update_session_timeout → persist_db DataStore
permissions_header/ "PERMISSIONS"
permissions_list/
└── location_permission_row (info_row, icon location_on #266489)
    label "Location", value "granted" (#C9E6FF chip), secondary "Used for ATM distance sorting"
    trailing: open_in_new #41474D, on_click=open_app_system_settings → share_external OS settings
notifications_header/ "NOTIFICATIONS"
notifications_list/
├── consent_expiry_notif_row (list_item, "Consent expiry reminders")
│   └── consent_expiry_switch (switch ON, #266489)
│       on_click=toggle_consent_expiry_notification → persist_db DataStore
└── security_alerts_notif_row (list_item, "Security alerts")
    └── security_alerts_switch (switch ON, #266489)
        on_click=toggle_security_alerts_notification → persist_db DataStore
storage_header/ "STORAGE"
storage_list/
├── pfm_storage_location_row (info_row, icon storage #41474D, display only)
│   label "PFM data", value "/data/data/org.mifosx.openbanking/files/databases/pfm_cache"
│   secondary "Shared by dashboard & spending analysis"
└── clear_pfm_cache_row (list_item, icon cleaning_services, "Clear PFM cache")
    trailing: chevron_right, on_click=clear_pfm_cache → delete Room pfm_cache
account_header/ "ACCOUNT"
account_links_list/
├── manage_consents_row (list_item, icon policy, trailing chevron_right)
│   on_click=navigate_consent_list → navigate consent-list
├── profile_row (list_item, icon account_circle, trailing chevron_right)
│   on_click=navigate_profile → navigate profile
└── clear_local_data_row (list_item, icon delete_sweep, trailing chevron_right)
    on_click=clear_local_data_confirm → transform_state → clear_confirm
about_header/ "ABOUT & LEGAL"
about_list/
├── terms_row (list_item, icon article, trailing open_in_new)
│   on_click=open_external_url(openbanking.org.uk/ToS) → share_external browser
├── privacy_row (list_item, icon privacy_tip, trailing open_in_new)
│   on_click=open_external_url(openbanking.org.uk/privacy) → share_external browser
├── licences_row (list_item, icon info_outline, trailing chevron_right)
│   on_click=open_oss_licences → share_external AboutLibraries
└── app_version_row (list_item display only): "0.1.0 (build 1)"
BottomNav (Home | Accounts | Transactions | More●)
```

---

### State: empty

```
┌─────────────────────────────────────────────────┐
│ Settings                                        │  ← top_app_bar small #F7F9FF
├─────────────────────────────────────────────────┤
│                                                 │
│                                                 │
│              [settings]                         │  ← settings_empty_state
│                                                 │    icon: settings 48dp #41474D
│         Settings unavailable                   │    title headlineSmall #181C20
│                                                 │
│   Loading your preferences…                    │  ← body bodyMedium #41474D
│   This should be instant.                       │
│                                                 │
│                                                 │
├─────────────────────────────────────────────────┤
│  ⌂ Home   ◫ Accounts  ▤ Transactions  ●More   │
└─────────────────────────────────────────────────┘
```

### Component Hierarchy — empty

```
top_app_bar/ (title "Settings", no leading)
settings_empty_state/ (variant: neutral, full-screen centred)
├── icon (settings, 48dp, #41474D)
├── title (headlineSmall #181C20): "Settings unavailable"
└── body (bodyMedium #41474D): "Loading your preferences…\nThis should be instant."
BottomNav (Home | Accounts | Transactions | More●)
```

---

### State: error

```
┌─────────────────────────────────────────────────┐
│ Settings                                        │  ← top_app_bar small #F7F9FF
├─────────────────────────────────────────────────┤
│                                                 │
│                                                 │
│           [error_outline]                       │  ← settings_error_state
│                                                 │    icon: error_outline 48dp #BA1A1A
│        Settings unavailable                    │    title headlineSmall #181C20
│                                                 │
│   Unable to read your preferences.             │  ← body bodyMedium #41474D
│   Storage may be full or corrupted.             │    DataStore IOException
│                                                 │
│          [    Try again    ]                    │  ← settings_error_retry_button
│                                                 │    variant: filled, bg #266489
│                                                 │    label labelLarge #FFFFFF 48dp h
│                                                 │
├─────────────────────────────────────────────────┤
│  ⌂ Home   ◫ Accounts  ▤ Transactions  ●More   │
└─────────────────────────────────────────────────┘
```

### Component Hierarchy — error

```
top_app_bar/ (title "Settings", no leading)
settings_error_state/ (variant: error, full-screen centred)
├── icon (error_outline, 48dp, #BA1A1A)
├── title (headlineSmall #181C20): "Settings unavailable"
├── body (bodyMedium #41474D): "Unable to read your preferences. Storage may be full or corrupted."
└── settings_error_retry_button (variant: filled, bg #266489, label "Try again")
    on_click=retry_load_settings → transform_state Loading→Content
BottomNav (Home | Accounts | Transactions | More●)
```

---

### State: clear_confirm

```
┌─────────────────────────────────────────────────┐
│ Settings                                        │  ← top_app_bar small #F7F9FF
├─────────────────────────────────────────────────┤
│  [dim scrim #000000 @ 32% opacity over content] │
│                                                 │
│  APPEARANCE        ↑ scrollable content visible │
│  Theme                       [▼ System ]        │
│  SECURITY                                       │
│  Biometric lock                    [  ●  ]      │
│  Session timeout               [▼ 5 min ]       │
│  PERMISSIONS                                    │
│  📍 Location               granted   ↗          │
│  …                                              │
│                                                 │
├────────── Bottom Sheet (modal) ─────────────────┤
│  ┌───────────────────────────────────────────┐  │
│  │ ▬▬▬  (drag handle)                        │  │  ← clear_local_data_sheet
│  │                                           │  │    bg: surfaceContainerLow #F1F4F9
│  │  Erase local data?                        │  │    radius top 28dp, elevation 2
│  │                                           │  │    title titleLarge #181C20
│  │  This will delete all cached account and  │  │
│  │  transaction data from your device.       │  │  ← body bodyMedium #41474D
│  │  Open Banking authorisations are NOT      │  │
│  │  affected.                                │  │
│  │                                           │  │
│  │  [ Cancel ]         [ Erase all ]         │  │  ← cancel_clear_local_data_button
│  │    text, #266489     filled, #BA1A1A      │  │    variant: text, labelLarge #266489
│  │    labelLarge         labelLarge #FFFFFF   │  │    confirm_clear_local_data_button
│  │                                           │  │    variant: filled, bg #BA1A1A (error)
│  └───────────────────────────────────────────┘  │    labelLarge #FFFFFF
├─────────────────────────────────────────────────┤
│  ⌂ Home   ◫ Accounts  ▤ Transactions  ●More   │
└─────────────────────────────────────────────────┘
```

### Component Hierarchy — clear_confirm

```
top_app_bar/ (title "Settings", no leading)
[content beneath scrim — same structure as content state]
scrim_overlay/ (#000000 @ 32% opacity)
clear_local_data_sheet/ (modal BottomSheet, bg #F1F4F9, top-corner radius 28dp, elevation 2)
├── drag_handle (centred, width 32dp, h 4dp, #C1C7CE, radius 2dp)
├── title (titleLarge #181C20): "Erase local data?"
├── body (bodyMedium #41474D):
│       "This will delete all cached account and transaction data from your device.
│        Open Banking authorisations are NOT affected."
├── cancel_clear_local_data_button (variant: text, labelLarge #266489): "Cancel"
│   on_click=dismiss_clear_local_data → transform_state → content
└── confirm_clear_local_data_button (variant: filled, bg #BA1A1A, labelLarge #FFFFFF): "Erase all"
    on_click=execute_clear_local_data → delete Room+SQLDelight + reset DataStore cached-at timestamps
BottomNav (Home | Accounts | Transactions | More●)
```

---

### Interaction Summary

| Component | Action | Effect | Target / Notes |
|---|---|---|---|
| theme_dropdown | update_theme | persist_db | DataStore: writes theme key atomically |
| biometric_switch | toggle_biometric_lock | persist_db | DataStore: flips biometric_lock_enabled; shows dialog if no hardware |
| session_dropdown | update_session_timeout | persist_db | DataStore: writes session_timeout key (whitelist 2/5/10/30 min) |
| location_permission_row | open_app_system_settings | share_external | OS App Settings deep-link; GPS used for ATM distance sort |
| consent_expiry_switch | toggle_consent_expiry_notification | persist_db | DataStore: flips notify_consent_expiry flag |
| security_alerts_switch | toggle_security_alerts_notification | persist_db | DataStore: flips notify_security_alerts flag |
| clear_pfm_cache_row | clear_pfm_cache | delete | Room: clears pfm_room_cache spending & category rows |
| manage_consents_row | navigate_consent_list | navigate | → consent-list screen |
| profile_row | navigate_profile | navigate | → profile screen |
| clear_local_data_row | clear_local_data_confirm | transform_state | → clear_confirm state; opens clear_local_data_sheet |
| terms_row | open_external_url | share_external | Browser: openbanking.org.uk/customer-hub/terms-and-conditions/ |
| privacy_row | open_external_url | share_external | Browser: openbanking.org.uk/privacy-policy/ |
| licences_row | open_oss_licences | share_external | AboutLibraries in-app OSS licences screen |
| app_version_row | (no action) | — | Display only: "0.1.0 (build 1)" |
| cancel_clear_local_data_button | dismiss_clear_local_data | transform_state | → content state; no data erased |
| confirm_clear_local_data_button | execute_clear_local_data | delete | Room/SQLDelight cache + DataStore cached-at reset; consent unaffected |
| settings_error_retry_button | retry_load_settings | transform_state | Loading → Content on success; Error on repeat IOException |

---

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| list_item row | match_parent | 56dp min | 0 |
| section_header label | match_parent | 40dp | 0 |
| switch (biometric, notif toggles) | 51dp | 28dp | 14dp (full) |
| dropdown selector (theme, session) | 120dp | 40dp | 4dp |
| info_row (location, pfm storage) | match_parent | 64dp min | 0 |
| bottom_sheet (clear_local_data_sheet) | match_parent | wrap (min 240dp) | 28dp top-start, 28dp top-end |
| drag_handle | 32dp | 4dp | 2dp |
| button (cancel_clear) | 120dp | 48dp | 9999dp (full) |
| button (confirm_clear / retry) | 140dp | 48dp | 9999dp (full) |
| empty/error icon | 48dp | 48dp | — |
| skeleton row | match_parent | 56dp | 4dp |
