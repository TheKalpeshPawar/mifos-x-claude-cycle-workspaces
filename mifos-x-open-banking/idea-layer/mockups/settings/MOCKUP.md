# Settings — Visual Mockup

> Auto-generated from `screens/settings/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Source: DataStore preferences (kotlinx-serialization, no network)
> Generated: 2026-07-14T00:00:00Z

---

## Screen: Settings

Canvas: 393×852dp · Top app bar (no leading, no back) · Bottom nav · Material 3 light theme

---

### State: loading

```
┌─────────────────────────────────────────────┐
│ Settings                                    │  ← top_app_bar (no leading icon)
├─────────────────────────────────────────────┤
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │  ← settings_loading_skeleton shimmer
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │    list variant × 8 rows
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │    each 48dp radius 4dp
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: content

```
┌─────────────────────────────────────────────┐
│ Settings                                    │
├─────────────────────────────────────────────┤
│                                              │
│  APPEARANCE                                 │  ← appearance_header section_header
│                                              │
│  Theme                                      │  ← theme_row list_item
│  System default              [▼ System  ]   │    trailing theme_dropdown
│                                              │
│  SECURITY                                   │  ← security_header
│                                              │
│  Biometric lock                             │  ← biometric_row list_item
│  Require fingerprint or face ID on app open │
│                                    [  ●  ]  │  ← biometric_switch (ON = primary #266489)
│  Session timeout                            │  ← session_timeout_row list_item
│  Auto-lock after inactivity     [▼ 5 min ]  │    session_dropdown
│                                              │
│  NOTIFICATIONS                              │  ← notifications_header
│                                              │
│  Consent expiry reminders                  │  ← consent_expiry_notif_row
│  Alert before your Open Banking            │
│  consent expires                   [  ●  ]  │  ← consent_expiry_switch (ON)
│  Security alerts                           │  ← security_alerts_notif_row
│  Notify for unusual access         [  ●  ]  │  ← security_alerts_switch (ON)
│                                              │
│  ACCOUNT                                    │  ← account_header
│                                              │
│  🛡  Manage consents              >         │  ← manage_consents_row → consent-list
│     View and revoke Open Banking access     │
│  👤  Profile                      >         │  ← profile_row → profile
│     Account holder identity details         │
│  🗑  Clear local data             >         │  ← clear_local_data_row → bottom-sheet
│     Erase cached account and transaction    │
│     data (GDPR)                             │
│                                              │
│  ABOUT & LEGAL                             │  ← about_header
│                                              │
│  📄  Terms of service             ↗         │  ← terms_row icon article open_in_new
│  🔒  Privacy policy               ↗         │  ← privacy_row icon privacy_tip
│  ℹ  Open source licences         >         │  ← licences_row icon info_outline
│  Version                         1.0.0 (42) │  ← app_version_row (no tap target)
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
top_app_bar/ (title "Settings", no leading icon)
appearance_header/ (section_header): "APPEARANCE"
appearance_list/
└── theme_row (list_item, trailing dropdown [Light/Dark/System default])
    └── theme_dropdown (on_click=update_theme → DataStore atomic write)
security_header/ "SECURITY"
security_list/
├── biometric_row (list_item, trailing biometric_switch toggle, on_click=toggle_biometric_lock)
└── session_timeout_row (list_item, trailing session_dropdown [2m/5m/10m/30m])
    └── session_dropdown (on_click=update_session_timeout)
notifications_header/ "NOTIFICATIONS"
notifications_list/
├── consent_expiry_notif_row (list_item, trailing consent_expiry_switch)
└── security_alerts_notif_row (list_item, trailing security_alerts_switch)
account_header/ "ACCOUNT"
account_links_list/
├── manage_consents_row (list_item icon policy trailing chevron_right → consent-list)
├── profile_row (list_item icon account_circle trailing chevron_right → profile)
└── clear_local_data_row (list_item icon delete_sweep trailing chevron_right → bottom-sheet)
about_header/ "ABOUT & LEGAL"
about_list/
├── terms_row (list_item icon article trailing open_in_new → browser)
├── privacy_row (list_item icon privacy_tip trailing open_in_new → browser)
├── licences_row (list_item icon info_outline trailing chevron_right → oss licences)
└── app_version_row (list_item display only): "1.0.0 (42)"
BottomNav (always)
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│ Settings                                    │
├─────────────────────────────────────────────┤
│            [settings]                        │  ← icon 48dp #41474D
│    Settings unavailable                    │  ← title headlineSmall #181C20
│  Loading your preferences…                 │  ← body bodyMedium #41474D
│  This should be instant.                   │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│ Settings                                    │
├─────────────────────────────────────────────┤
│            [error_outline]                   │  ← icon 48dp #BA1A1A
│    Settings unavailable                    │
│  Unable to read your preferences.          │  ← I/O exception from DataStore
│         [  Try again  ]                     │  ← settings_error_retry_button filled
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### Interaction Summary

| Component | Action | Target |
|---|---|---|
| theme_dropdown | update_theme | DataStore atomic write |
| biometric_switch | toggle_biometric_lock | DataStore atomic write |
| session_dropdown | update_session_timeout | DataStore atomic write |
| consent_expiry_switch | toggle_consent_expiry_notification | DataStore |
| security_alerts_switch | toggle_security_alerts_notification | DataStore |
| manage_consents_row | navigate_consent_list | consent-list |
| profile_row | navigate_profile | profile |
| clear_local_data_row | clear_local_data_confirm | bottom-sheet → Room/DataStore wipe |
| terms_row | open_external_url | system browser (openbanking.org.uk/ToS) |
| privacy_row | open_external_url | system browser (openbanking.org.uk/privacy) |
| licences_row | open_oss_licences | AboutLibraries in-app |
| app_version_row | (no action) | — |
| settings_error_retry_button | retry_load_settings | DataStore re-read |

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| list_item row | match_parent | 56dp min | 0 |
| switch | 51dp | 28dp | 14dp |
| dropdown selector | 120dp | 40dp | 4dp |
| section_header label | match_parent | 40dp | 0 |
