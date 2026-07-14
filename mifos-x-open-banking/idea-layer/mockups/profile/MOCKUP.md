# Profile — Visual Mockup

> Auto-generated from `screens/profile/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Source: hsbc-obie-ais-v4.0:party + cached consent record
> Generated: 2026-07-14T00:00:00Z

---

## Screen: Profile

Canvas: 393×852dp · Top app bar with back · Bottom nav · Material 3 light theme

---

### State: loading

```
┌─────────────────────────────────────────────┐
│ ← Profile                                   │  ← top_app_bar
├─────────────────────────────────────────────┤
│                   ◌                          │  ← circular progress #266489 centred
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: content

```
┌─────────────────────────────────────────────┐
│ ← Profile                                   │
├─────────────────────────────────────────────┤
│                                              │
│ ┌─────────────────────────────────────────┐ │
│ │          [PS]                           │ │  ← user_avatar circle 72dp #C9E6FF #004B6F
│ │    Priya Sharma                         │ │  ← user_full_name headlineMedium #181C20
│ │    Personal account                     │ │  ← party_type labelMedium #50606E
│ └─────────────────────────────────────────┘ │    identity_header_card elevation 2
│                                              │
│  IDENTITY                                   │  ← identity_section_header
│                                              │
│  ✉  Email                                  │  ← email_row list_item icon email
│     priya.sharma@example.com               │
│  📱  Mobile                                 │  ← mobile_row list_item icon phone
│     +447700900123                          │
│  🏠  Address                                │  ← address_row list_item icon home
│     14 Oak Lane, London SW1A 1AA           │
│                                              │
│  OPEN BANKING CONNECTION                    │  ← connection_section_header
│                                              │
│ ┌─────────────────────────────────────────┐ │
│ │  🏛  HSBC Open Banking                  │ │  ← consent_summary_card elevation 1
│ │  Status      Authorised                 │ │    consent_status_row icon verified
│ │  Expires     14 Sep 2026                │ │    consent_expiry_row icon schedule
│ │                                          │ │
│ │  Permissions                            │ │  ← permissions sub-section
│ │  ✓  Account information                 │ │    perm_accounts_detail check_circle
│ │  ✓  Account balances                    │ │    perm_balances
│ │  ✓  Transaction history                 │ │    perm_transactions
│ │  ✓  Account holder identity             │ │    perm_party
│ │                                          │ │
│ │  [  Manage consent  ]                   │ │  ← manage_consent_button tonal #266489
│ └─────────────────────────────────────────┘ │    → consent-detail
│                                              │
│         [  Sign out  ]                      │  ← sign_out_button outlined #BA1A1A
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
top_app_bar/ (title "Profile", leading back)
identity_header_card/ (card elevation 2 radius 12dp padding 16dp margin h 16dp)
│  ├── user_avatar        (circle 72dp bg #C9E6FF text #004B6F): "PS"
│  ├── user_full_name     (headlineMedium #181C20): "Priya Sharma"
│  └── party_type         (labelMedium #50606E): "Personal account"
identity_section_header/ "IDENTITY"
identity_list/
│  ├── email_row   (list_item icon email): "priya.sharma@example.com"
│  ├── mobile_row  (list_item icon phone): "+447700900123"
│  └── address_row (list_item icon home): "14 Oak Lane, London SW1A 1AA"
connection_section_header/ "OPEN BANKING CONNECTION"
consent_summary_card/ (card elevation 1 radius 12dp padding 16dp)
│  ├── bank_label           (titleMedium icon account_balance): "HSBC Open Banking"
│  ├── consent_status_row   (list_item icon verified): status=Authorised
│  ├── consent_expiry_row   (list_item icon schedule): "14 Sep 2026"
│  ├── permissions_section_header/ "Permissions"
│  ├── permissions_list/
│  │    ├── perm_accounts_detail (list_item icon check_circle #266489)
│  │    ├── perm_balances        (list_item icon check_circle #266489)
│  │    ├── perm_transactions    (list_item icon check_circle #266489)
│  │    └── perm_party           (list_item icon check_circle #266489)
│  └── manage_consent_button  (button tonal → consent-detail)
sign_out_button/ (button outlined color=#BA1A1A → confirm_sign_out)
BottomNav (always)
```

---

### State: content_expiring

```
┌─────────────────────────────────────────────┐
│ ← Profile                                   │
├─────────────────────────────────────────────┤
│  [identity_header_card — same as content]   │
│  [identity_list — same as content]          │
│                                              │
│ ┌─────────────────────────────────────────┐ │
│ │ ⚠  Your consent expires in 5 days      │ │  ← expiry_warning_banner elevation 0
│ │    [  Renew now  ]                      │ │    bg #FFDAD6 text warning color
│ └─────────────────────────────────────────┘ │    renew_consent_button tonal error
│                                              │
│  [connection section + consent card]        │
│         [  Sign out  ]                      │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: confirm_sign_out

```
┌─────────────────────────────────────────────┐
│ ← Profile                                   │
├─────────────────────────────────────────────┤
│  [content screen — dimmed behind dialog]    │
│                                              │
│  ┌───────────────────────────────────────┐  │
│  │  Sign out?                            │  │  ← sign_out_dialog M3 AlertDialog
│  │  This will clear your secure session  │  │
│  │  and consent tokens. You'll need to   │  │
│  │  re-authorise with HSBC to reconnect. │  │
│  │                                        │  │
│  │  [Cancel]            [Sign out]        │  │  ← cancel=dismiss / sign_out=error filled
│  └───────────────────────────────────────┘  │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│ ← Profile                                   │
├─────────────────────────────────────────────┤
│            [error_outline]                   │  ← icon 48dp #BA1A1A
│    Unable to load profile                  │
│  body from error.message (401/403/404/net) │
│         [  Try again  ]                     │  ← retry_button filled #266489
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│ ← Profile                                   │
├─────────────────────────────────────────────┤
│            [account_circle_off]              │  ← icon 48dp #41474D
│    Profile data unavailable                │
│  No identity record found. ReadParty may  │  ← body bodyMedium #41474D
│  not be in your current consent scope.    │
│         [  Sign in again  ]                 │  ← profile_empty_reauth_button → login
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### Interaction Summary

| Component | Action | Target |
|---|---|---|
| back_button | navigate_back | prior screen |
| manage_consent_button | navigate_consent_detail | consent-detail |
| renew_consent_button (content_expiring) | navigate_consent_renew | consent-detail |
| sign_out_button (content / content_expiring) | confirm_sign_out | confirm_sign_out state |
| cancel_sign_out_button (dialog) | dismiss_sign_out_dialog | content / content_expiring |
| confirm_sign_out_button (dialog) | execute_sign_out | login (clears tokens) |
| retry_button (error) | retry_load | in-place retry |
| profile_empty_reauth_button (empty) | navigate_reauth | login |

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| identity_header_card | match_parent − 32dp | ~112dp | 12dp |
| user_avatar | 72dp | 72dp | circle |
| expiry_warning_banner | match_parent − 32dp | ~80dp | 12dp |
| consent_summary_card | match_parent − 32dp | ~220dp | 12dp |
| sign_out_button | match_parent − 64dp | 48dp | 12dp |
| sign_out_dialog | match_parent − 48dp | ~200dp | 28dp |
