# Consent List — Visual Mockup

> Auto-generated from `screens/consent-list/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-14T00:00:00Z

---

## Screen: Data Sharing Consents

Canvas: 393×852dp · Top app bar · Bottom nav · Material 3 light theme

---

### State: loading

```
┌─────────────────────────────────────────────┐
│  Data Sharing                               │  ← top_app_bar titleMedium #181C20
├─────────────────────────────────────────────┤
│                                              │
│                   ◌                          │  ← circular progress #266489 centred
│               (spinning)                     │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: content (with near-expiry consent)

```
┌─────────────────────────────────────────────┐
│  Data Sharing                               │
├─────────────────────────────────────────────┤
│ ⚠ Your consent expires in 12 days          │  ← reconfirm_banner bg #FFDAD6
│   Reconfirm to keep your accounts          │    icon warning_amber #BA1A1A
│   connected. [Reconfirm now]               │    CTA text button → consent-detail
│                                              │
│  ACTIVE                                      │  ← active_section_label labelLarge #41474D
│                                              │
│ ┌─────────────────────────────────────────┐ │
│ │  🛡  HSBC Open Banking Access            │ │  ← active consent card elevation 1
│ │     Authorised                           │ │    status badge tonal primary
│ │     Expires: 10 Oct 2026 · 12 days left │ │    urgency chip tonal error
│ │     ⚠ [Reconfirm soon]                 │ │
│ └─────────────────────────────────────────┘ │
│                                              │
│  ─────────────────────────────────────────  │  ← section divider
│                                              │
│  HISTORY                                     │  ← history_section_label labelLarge #41474D
│                                              │
│ ┌─────────────────────────────────────────┐ │
│ │  🛡  HSBC Open Banking Access            │ │  ← history consent card elevation 0 outlined
│ │     Expired                              │ │    status badge tonal secondary
│ │     Expired: 15 Apr 2026                │ │
│ └─────────────────────────────────────────┘ │
│ ┌─────────────────────────────────────────┐ │
│ │  🛡  HSBC Open Banking Access            │ │
│ │     Revoked                              │ │
│ │     Revoked: 01 Feb 2026                │ │
│ └─────────────────────────────────────────┘ │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
top_app_bar/ (title "Data Sharing", bg #F7F9FF)
reconfirm_banner/ (banner visible_when=has_near_expiry_consents)
│  ├── icon warning_amber #BA1A1A
│  ├── title: "Your consent expires in 12 days"
│  ├── body: "Reconfirm to keep your accounts connected."
│  └── CTA button text: "Reconfirm now" → consent-detail (consentId)
active_section_label/ (text labelLarge #41474D): "ACTIVE"
active_consents_list/ (list vertical, gap 8dp, padding h 16dp)
└── consent_card/ (card elevation 1 radius 12dp padding 16dp)
     ├── shield_icon        (icon shield lg #266489)
     ├── consent_title      (titleMedium #181C20): "HSBC Open Banking Access"
     ├── status_badge       (badge tonal): "Authorised" primary
     ├── expiry_line        (bodySmall #41474D): "Expires: 10 Oct 2026 · 12 days left"
     └── urgency_chip       (chip tonal error, visible_when days_until_expiry ≤ 14)
section_divider/ (divider)
history_section_label/ (text labelLarge #41474D): "HISTORY"
history_consents_list/ (list vertical, gap 8dp, padding h 16dp)
└── consent_card × N (card outlined elevation 0 radius 12dp)
     ├── consent_title  (titleMedium #41474D, muted for expired)
     ├── status_badge   (badge tonal secondary): "Expired" / "Revoked"
     └── date_line      (bodySmall #41474D): "Expired: 15 Apr 2026"
BottomNav (always)
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│  Data Sharing                               │
├─────────────────────────────────────────────┤
│                                              │
│               [shield]                       │  ← icon 48dp #41474D centred
│                                              │
│    No consents found                        │  ← title headlineSmall #181C20
│  You have not yet connected any bank        │  ← body bodyMedium #41474D
│  accounts via Open Banking.                 │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│  Data Sharing                               │
├─────────────────────────────────────────────┤
│                                              │
│            [error_outline]                   │  ← icon 48dp #BA1A1A
│                                              │
│    Unable to load consents                  │  ← title headlineSmall #181C20
│  Please check your connection.              │
│                                              │
│         [  Try again  ]                     │  ← retry_button filled #266489
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: error_auth

```
┌─────────────────────────────────────────────┐
│  Data Sharing                               │
├─────────────────────────────────────────────┤
│                                              │
│             [lock_outline]                   │  ← icon 48dp #BA1A1A
│                                              │
│    Session expired                          │  ← title headlineSmall #181C20
│  Please sign in again to view your          │  ← body bodyMedium #41474D
│  consent status.                            │
│                                              │
│         [  Sign in again  ]                 │  ← navigate → login
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### Interaction Summary

| Component | Action | Target |
|---|---|---|
| reconfirm_banner CTA | navigate_reconfirm_consent | consent-detail (consentId) |
| consent_card (active) | navigate_consent_detail | consent-detail (consentId) |
| consent_card (history) | navigate_consent_detail | consent-detail (consentId) |
| retry_button (error) | retry_load | in-place retry |
| sign_in_again_button (error_auth) | navigate_login | login |

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| reconfirm_banner | match_parent | ~72dp | 0 |
| consent_card (active) | match_parent − 32dp | ~100dp | 12dp |
| consent_card (history) | match_parent − 32dp | ~80dp | 12dp |
| status_badge | wrap | 24dp | 9999 |
| urgency_chip | wrap | 28dp | 9999 |
