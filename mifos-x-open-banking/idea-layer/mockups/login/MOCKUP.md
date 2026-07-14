# Login — Visual Mockup

> Auto-generated from `screens/login/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-14T00:00:00Z

---

## Screen: Connect with HSBC

Canvas: 393×852dp · Top app bar with back arrow · No bottom nav · Material 3 light theme

---

### State: content

```
┌─────────────────────────────────────────────┐
│ ← Connect with HSBC                         │  ← top_app_bar bg #F7F9FF, titleMedium
├─────────────────────────────────────────────┤
│                                              │
│ ┌─────────────────────────────────────────┐ │
│ │  [HSBC brand mark]                      │ │  ← hsbc_logo image ic_hsbc_logo 48dp h
│ │                                          │ │
│ │  ✓ Regulated UK Open Banking connection │ │  ← ob_regulated_badge labelSmall #266489
│ │    verified_user icon #266489           │ │    icon_leading verified_user
│ │                                          │ │
│ │  Connect with HSBC                      │ │  ← explainer_headline titleMedium #181C20
│ │  You'll be redirected to HSBC to        │ │  ← explainer_body bodySmall #41474D
│ │  approve permissions and select         │ │
│ │  accounts. Your credentials are never   │ │
│ │  shared with this app.                  │ │
│ │                                          │ │
│ │  ──────────────────────────────────     │ │  ← divider (card_divider)
│ │                                          │ │
│ │  🔒 Secured with FAPI 1.0 Advanced,    │ │  ← security_notice labelSmall #41474D
│ │     mTLS, and PS256-signed tokens.      │ │    icon_leading lock_outline #41474D
│ └─────────────────────────────────────────┘ │
│                                              │
│  Permissions requested                       │  ← permissions_header section labelLarge
│                                              │
│  ✓ Read account details                     │  ← permission_row list_item
│    View account name, number, sort code     │    icon check_circle_outline primary #266489
│  ✓ Read balances                            │
│    See available and booked balances        │
│  ✓ Read transactions                        │
│    Access transaction history               │
│  ✓ Read standing orders                     │
│  ✓ Read direct debits                       │
│  ✓ Read scheduled payments                  │
│  ✓ Read beneficiaries                       │
│  ✓ Read statements                          │
│  ✓ Read party details                       │
│  ✓ Read offers                              │
│  ✓ Read products                            │
│                                              │
│  Your consent is valid for 90 days and      │  ← consent_validity_note bodySmall #41474D
│  covers transactions from 12 months ago.    │
│  Expires 10 Oct 2026                        │  ← consent_expiry_display labelMedium #266489
│                                              │
│      [  Continue to HSBC  ↗  ]             │  ← continue_hsbc_button filled 48dp #266489
│      [  Cancel              ]               │  ← cancel_button text variant
│                                              │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
top_app_bar/ (bg #F7F9FF, title "Connect with HSBC", leading back arrow)
hsbc_explainer_card/ (card elevation 1, padding 16dp, radius 12dp)
│  ├── hsbc_logo          (image ic_hsbc_logo, 48dp h, centred)
│  ├── ob_regulated_badge (text labelSmall #266489, icon verified_user)
│  ├── explainer_headline (titleMedium #181C20): "Connect with HSBC"
│  ├── explainer_body     (bodySmall #41474D): redirect & credential-protection copy
│  ├── card_divider       (divider)
│  └── security_notice    (labelSmall #41474D, icon lock_outline): "FAPI 1.0 Advanced…"
permissions_header/ (section_header labelLarge): "Permissions requested"
permissions_list/ (list vertical, items=requested_permissions, 11 rows)
│  └── permission_row × 11 (list_item, icon check_circle_outline #266489)
│       ├── headline_text:  "Read account details" … "Read products"
│       └── supporting_text: human-readable description per OBIE scope
consent_validity_note  (text bodySmall #41474D): "Valid for 90 days…"
consent_expiry_display (text labelMedium #266489): "Expires 10 Oct 2026"
continue_hsbc_button   (button filled 140×48dp radius 12dp #266489, icon open_in_new)
cancel_button          (button text, → user-onboarding)
```

---

### State: loading

```
┌─────────────────────────────────────────────┐
│ ← Connect with HSBC                         │
├─────────────────────────────────────────────┤
│                                              │
│         ────────────────────────            │  ← loading_indicator linear progress bar
│                                              │    primary #266489, full width
│                                              │
│    Preparing your secure connection…        │  ← loading_label bodyMedium #41474D centred
│                                              │
└─────────────────────────────────────────────┘
```

---

### State: authorising

```
┌─────────────────────────────────────────────┐
│ ← Connect with HSBC                         │
├─────────────────────────────────────────────┤
│                                              │
│                  ◌                           │  ← authorising_spinner circular #266489
│              (spinning)                      │
│                                              │
│    Waiting for HSBC authorisation…          │  ← authorising_label bodyMedium #41474D
│                                              │
│    Complete sign-in in the HSBC app or      │  ← authorising_hint bodySmall #41474D
│    website, then return here.               │
│                                              │
└─────────────────────────────────────────────┘
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│ ← Connect with HSBC                         │
├─────────────────────────────────────────────┤
│                                              │
│              [error_outline]                 │  ← icon 48dp #BA1A1A centred
│                                              │
│       Unable to connect to HSBC             │  ← title headlineSmall #181C20
│  The consent request could not be           │  ← body bodyMedium #41474D
│  submitted. Please try again.               │
│                                              │
│         [  Try again  ]                     │  ← retry_button filled #266489
│                                              │
└─────────────────────────────────────────────┘
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│ ← Connect with HSBC                         │
├─────────────────────────────────────────────┤
│                                              │
│              [manage_search]                 │  ← icon 48dp #41474D centred
│                                              │
│     No permissions configured               │  ← title headlineSmall #181C20
│  No Open Banking read scopes are            │  ← body bodyMedium #41474D
│  available to request.                      │
│                                              │
│         [  Go back  ]                       │  ← login_empty_back_button → user-onboarding
│                                              │
└─────────────────────────────────────────────┘
```

---

### Interaction Summary

| Component | Action | Target |
|---|---|---|
| back arrow (top bar) | navigate_back | user-onboarding |
| continue_hsbc_button | start_oauth | (HSBC FAPI redirect) |
| cancel_button | navigate_back | user-onboarding |
| retry_button (error) | start_oauth | retry consent-create POST |
| login_empty_back_button | navigate_back | user-onboarding |

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| hsbc_explainer_card | match_parent − 32dp | wrap | 12dp |
| hsbc_logo | centred | 48dp | n/a |
| permission_row | match_parent | 56dp min | 0 |
| continue_hsbc_button | match_parent − 32dp | 48dp | 12dp |
| loading_indicator (linear) | match_parent | 4dp | 0 |
| authorising_spinner | 48dp | 48dp | circle |
