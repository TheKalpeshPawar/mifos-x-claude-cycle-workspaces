# Consent Detail — Visual Mockup

> Auto-generated from `screens/consent-detail/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-14T00:00:00Z

---

## Screen: HSBC Connection Detail

Canvas: 393×852dp · Top app bar with back arrow · Bottom nav · Material 3 light theme

---

### State: loading

```
┌─────────────────────────────────────────────┐
│ ← HSBC Connection Detail                    │  ← top_app_bar
├─────────────────────────────────────────────┤
│                   ◌                          │  ← circular progress #266489 centred
└─────────────────────────────────────────────┘
```

---

### State: content

```
┌─────────────────────────────────────────────┐
│ ← HSBC Connection Detail                    │
├─────────────────────────────────────────────┤
│                                              │
│ ┌─────────────────────────────────────────┐ │
│ │  🛡  HSBC Open Banking Access           │ │  ← consent_header_card elevation 2
│ │                                          │ │    bg #F7F9FF radius 12dp padding 16dp
│ │  [Authorised]   Status                  │ │  ← status_badge: Authorised = primary tonal
│ │                                          │ │    Expired/AwaitingAuth = warning
│ │  Expires 10 Oct 2026                    │ │  ← expiry_date labelMedium #41474D
│ │  Created 10 Jul 2026                    │ │  ← created_date bodySmall #41474D
│ │  Consent ID: urn:ob:consent:abc123      │ │  ← consent_id bodySmall Roboto Mono #41474D
│ └─────────────────────────────────────────┘ │
│                                              │
│ ⚠ Expires in 7 days. Reconfirm to keep     │  ← expiry_warning_banner (visible_when ≤7d)
│   your accounts connected.                  │    bg #FFDAD6, icon warning_amber
│                                              │
│  Permissions granted                         │  ← permissions_header section labelLarge
│                                              │
│  ✓ Read account details                     │  ← permissions_list (10 rows)
│  ✓ Read balances                            │    icon check_circle_outline #266489
│  ✓ Read transactions                        │    headline bodyMedium #181C20
│  ✓ Read standing orders                     │    supporting bodySmall #41474D
│  ✓ Read direct debits                       │
│  ✓ Read scheduled payments                  │
│  ✓ Read beneficiaries                       │
│  ✓ Read statements                          │
│  ✓ Read party details                       │
│  ✓ Read products                            │
│                                              │
│         [  Revoke access  ]                 │  ← revoke_button tonal error #BA1A1A
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
top_app_bar/ (title "HSBC Connection Detail", leading back)
consent_header_card/ (card elevation 2 radius 12dp padding 16dp margin h 16dp)
│  ├── shield_icon         (icon lg #266489)
│  ├── consent_title       (titleMedium #181C20): "HSBC Open Banking Access"
│  ├── status_chip         (badge tonal primary): "Authorised"
│  ├── expiry_date         (labelMedium #41474D): "Expires 10 Oct 2026"
│  ├── created_date        (bodySmall #41474D): "Created 10 Jul 2026"
│  └── consent_id          (bodySmall Roboto Mono #41474D): "urn:ob:consent:abc123"
expiry_warning_banner/ (visible_when expiryWarningDays non-null)
│  ├── icon warning_amber #BA1A1A
│  └── body: "Expires in {expiryWarningDays} days. Reconfirm to keep accounts connected."
permissions_header/ (section_header labelLarge #41474D): "Permissions granted"
permissions_list/ (list vertical items=permissionsDetail, 10 rows)
│  └── permission_row (list_item icon check_circle_outline #266489)
│       ├── headline_text: "Read account details" … "Read products"
│       └── supporting_text: OBIE scope description
revoke_button/ (button tonal, label "Revoke access", color error #BA1A1A)
BottomNav (always)
```

---

### State: RevokeConfirm (dialog overlay)

```
┌─────────────────────────────────────────────┐
│ ← HSBC Connection Detail                    │
├─────────────────────────────────────────────┤
│ [content dim overlay]                        │
│                                              │
│ ┌─────────────────────────────────────────┐ │
│ │  Revoke access?                         │ │  ← dialog title headlineSmall #181C20
│ │                                          │ │
│ │  Revoking will disconnect your HSBC     │ │  ← dialog body bodyMedium #41474D
│ │  accounts. You can reconnect at any     │ │
│ │  time via the Connect screen.           │ │
│ │                                          │ │
│ │  [Cancel]        [Revoke]               │ │  ← text + tonal error buttons
│ └─────────────────────────────────────────┘ │
└─────────────────────────────────────────────┘
```

---

### State: Revoking

```
┌─────────────────────────────────────────────┐
│ ← HSBC Connection Detail                    │
├─────────────────────────────────────────────┤
│                   ◌                          │  ← circular spinner #266489
│   Revoking access…                          │  ← label bodyMedium #41474D
└─────────────────────────────────────────────┘
```

---

### State: Error

```
┌─────────────────────────────────────────────┐
│ ← HSBC Connection Detail                    │
├─────────────────────────────────────────────┤
│            [error_outline]                   │  ← icon 48dp #BA1A1A
│    Unable to load consent                   │  ← title headlineSmall #181C20
│  body = VM-mapped per ConsentDetailErrorCode │  ← body bodyMedium #41474D
│         [  Try again  ]                     │  ← retry_button filled (recoverable)
└─────────────────────────────────────────────┘
```

---

### Interaction Summary

| Component | Action | Target |
|---|---|---|
| back arrow | navigate_back | consent-list |
| revoke_button | confirm_revoke | → RevokeConfirm state |
| dialog Cancel | cancel_revoke | → content state |
| dialog Revoke | execute_revoke | DELETE /account-access-consents → consent-list |
| retry_button (error) | retry_load | in-place retry |

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| consent_header_card | match_parent − 32dp | ~140dp | 12dp |
| expiry_warning_banner | match_parent | ~56dp | 0 |
| permission_row | match_parent | 56dp min | 0 |
| revoke_button | match_parent − 32dp | 48dp | 12dp |
| confirm_dialog | 280dp | wrap | 16dp |
