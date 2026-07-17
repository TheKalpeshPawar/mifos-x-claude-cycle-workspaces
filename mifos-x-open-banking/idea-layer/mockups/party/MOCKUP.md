# Account Holder (Party) — Visual Mockup

> Auto-generated from `screens/party/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Source: OBReadParty2/3 — parallel GET /accounts/{AccountId}/party + /parties (ReadParty gated)
> Generated: 2026-07-16T00:00:00Z

---

## Screen: Account Holder

Canvas: 393×852dp (Pixel 5) · Top app bar (small, back leading, title "Account Holder") · Bottom nav visible · No FAB · Roboto font · Material 3 light theme · bg #F7F9FF

Shell (from `app-shell.yaml` + `screens/party/ui.yaml#shell`):
- Top app bar — small variant, title "Account Holder", leading back arrow (returns to account-detail).
- Bottom navigation — Home | Accounts | Transactions | More; active tab: **Accounts** (#266489); others #41474D.
- FAB disabled: `ui.yaml#shell.fab_visible: false`.

---

### State: loading

```
┌─────────────────────────────────────────────┐
│ ← Account Holder                            │  ← top_app_bar small, bg #F7F9FF elev 0
├─────────────────────────────────────────────┤    back_button icon 24dp #41474D
│                                              │    title titleLarge 22sp #181C20
│                                              │
│                                              │
│                       ◌                     │  ← loading_indicator circular 48dp
│                                              │    color #266489 (primary), centred
│                                              │    padding 24dp all sides
│                                              │    a11y: "Loading account holder details"
│                                              │    (parallel /party + /parties in flight)
│                                              │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│  ← bottom_nav h 80dp bg #F7F9FF
│          ─────────                           │    Accounts selected tint #266489
└─────────────────────────────────────────────┘
```

### Component Hierarchy — loading

```
Screen: Account Holder (PartyUiState.Loading)
│
top_app_bar/ (small variant, bg #F7F9FF, elevation 0, h 56dp)
│  ├── back_button  (icon navigate_before 24dp #41474D, touch 48dp×48dp)
│  │   on_click → system back → account-detail
│  └── title        (titleLarge 22sp/28sp w400 #181C20): "Account Holder"
│
loading_indicator/ (circular progress, 48dp diameter, strokeWidth 4dp)
│   color: #266489 (primary)
│   layout: centred vertically + horizontally, padding 24dp all sides
│   accessibility_label: "Loading account holder details"
│   purpose: both parallel GET /party + GET /parties are in flight
│
BottomNav/ (persistent, h 80dp, bg #F7F9FF)
├── tab Home         (icon:home 24dp,          label:"Home",         default, tint #41474D)
├── tab Accounts     (icon:account_balance 24dp,label:"Accounts",    selected, tint #266489)
├── tab Transactions (icon:receipt_long 24dp,  label:"Transactions", default, tint #41474D)
└── tab More         (icon:more_horiz 24dp,    label:"More",         default, tint #41474D)
```

---

### State: content

```
┌─────────────────────────────────────────────┐
│ ← Account Holder                            │  ← top_app_bar small bg #F7F9FF
├─────────────────────────────────────────────┤
│ ↕ scrollable column spacing 16dp pad h 16dp │
│ ┌─────────────────────────────────────────┐ │  ← party_header_card
│ │  Sole                                   │ │    bg #F7F9FF, elev 2, radius 12dp
│ │                                          │ │    padding 16dp
│ │  Priya Sharma                           │ │  ← party_name headlineMedium 28sp #181C20
│ │                                          │ │
│ │  Priya Anjali Sharma                    │ │  ← party_full_legal_name bodyMedium 14sp
│ └─────────────────────────────────────────┘ │    #41474D (onSurfaceVariant)
│                                              │
│  Contact                                    │  ← contact_header labelLarge 14sp #41474D
│  ─────────────────────────────────────────  │    with horizontal divider
│                                              │
│  ✉  Email              priya.sharma@         │  ← email_row list_item h 56dp
│                         example.co.uk        │    icon 24dp #50606E | label #41474D
│                                              │    trailing bodyMedium 14sp #181C20
│  📱  Mobile           +44 7700 900482       │  ← mobile_row list_item h 56dp
│                                              │    icon phone_android 24dp #50606E
│  📞  Phone          +44 20 7946 0301        │  ← phone_row list_item h 56dp
│                                              │    icon phone 24dp #50606E
│                                              │
│  Address                                    │  ← address_header labelLarge 14sp #41474D
│  ─────────────────────────────────────────  │
│                                              │
│ ┌─────────────────────────────────────────┐ │  ← address_card[0] Residential
│ │  RESIDENTIAL                            │ │    elev 1, radius 12dp, padding 16dp
│ │  48 Camden High Street                  │ │  ← address_line_1 bodyMedium 14sp #181C20
│ │  Flat 12                                │ │  ← address_line_2 (AddressLine[0])
│ │  London, NW1 0LT                        │ │  ← address_town_postcode bodyMedium #181C20
│ │  GB                                     │ │  ← address_country bodySmall 12sp #41474D
│ └─────────────────────────────────────────┘ │
│                                              │    gap 8dp between address cards
│ ┌─────────────────────────────────────────┐ │  ← address_card[1] Business
│ │  BUSINESS                               │ │    elev 1, radius 12dp, padding 16dp
│ │  1 Canada Square                        │ │  ← address_line_1 bodyMedium 14sp #181C20
│ │  Suite 400                              │ │  ← address_line_2 (AddressLine[0])
│ │  London, E14 5AB                        │ │  ← address_town_postcode bodyMedium #181C20
│ │  GB                                     │ │  ← address_country bodySmall 12sp #41474D
│ └─────────────────────────────────────────┘ │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
Screen: Account Holder (PartyUiState.Content — merged /party + /parties, accountId: 40051512345678)
│
top_app_bar/ (small, bg #F7F9FF, elevation 0, h 56dp)
│  ├── back_button  (icon navigate_before 24dp #41474D, touch 48dp×48dp)
│  │   on_click → system back → account-detail
│  └── title        (titleLarge 22sp/28sp w400 #181C20): "Account Holder"
│
scrollable_column/ (vertical scroll, spacing 16dp, padding horizontal 16dp, top 16dp, bottom 16dp)
│
├── party_header_card/ (card bg #F7F9FF, elevation 2 → tonal shadow, radius 12dp, padding 16dp)
│   stack vertical gap 4dp:
│   ├── party_type_label  (labelMedium 12sp/16sp w500 #50606E): "Sole"
│   │                      [OBParty2.PartyType — Sole / JointSole / JointMortgagor]
│   ├── party_name        (headlineMedium 28sp/36sp w400 #181C20): "Priya Sharma"
│   │                      [OBParty2.Name]
│   └── party_full_legal_name (bodyMedium 14sp/20sp w400 #41474D): "Priya Anjali Sharma"
│                              [OBParty2.FullLegalName]
│                              a11y: "Legal name: Priya Anjali Sharma"
│
├── contact_header/ (section_header: labelLarge 14sp w500 #41474D + divider outlineVariant #C1C7CE)
│   label: "Contact"
│
├── email_row/ (list_item, min-height 56dp, padding vertical 12dp horizontal 16dp)
│   ├── leading_icon  (email 24dp #50606E, decorative:true)
│   ├── supporting    (labelSmall 11sp/16sp w500 #41474D): "Email"
│   └── trailing      (bodyMedium 14sp/20sp w400 #181C20 align:end): "priya.sharma@example.co.uk"
│       visible_when: party.EmailAddress non-empty
│       a11y: "Email address: priya.sharma@example.co.uk"
│
├── mobile_row/ (list_item, min-height 56dp, padding vertical 12dp horizontal 16dp)
│   ├── leading_icon  (phone_android 24dp #50606E, decorative:true)
│   ├── supporting    (labelSmall 11sp/16sp w500 #41474D): "Mobile"
│   └── trailing      (bodyMedium 14sp/20sp w400 #181C20 align:end): "+44 7700 900482"
│       visible_when: party.Mobile non-empty
│       a11y: "Mobile number: +44 7700 900482"
│
├── phone_row/ (list_item, min-height 56dp, padding vertical 12dp horizontal 16dp)
│   ├── leading_icon  (phone 24dp #50606E, decorative:true)
│   ├── supporting    (labelSmall 11sp/16sp w500 #41474D): "Phone"
│   └── trailing      (bodyMedium 14sp/20sp w400 #181C20 align:end): "+44 20 7946 0301"
│       visible_when: party.Phone non-empty
│       a11y: "Phone number: +44 20 7946 0301"
│
├── address_header/ (section_header: labelLarge 14sp w500 #41474D + divider #C1C7CE)
│   label: "Address"
│
└── address_list/ (list, vertical gap 8dp, items_source: party.Address — 2 entries)
    │
    ├── address_card[0]/ (card bg #F7F9FF, elevation 1, radius 12dp, padding 16dp)
    │   [OBPostalAddress8 — AddressType: Residential]
    │   stack vertical gap 4dp:
    │   ├── address_type       (labelSmall 11sp/16sp w500 #50606E): "RESIDENTIAL"
    │   │                       [item.AddressType uppercased in display]
    │   ├── address_line_1     (bodyMedium 14sp/20sp w400 #181C20): "48 Camden High Street"
    │   │                       [item.BuildingNumber + " " + item.StreetName]
    │   ├── address_line_2     (bodyMedium 14sp/20sp w400 #181C20): "Flat 12"
    │   │                       [item.AddressLine[0] — visible when non-empty]
    │   ├── address_town_postcode (bodyMedium 14sp/20sp w400 #181C20): "London, NW1 0LT"
    │   │                          [item.TownName + ", " + item.PostCode]
    │   └── address_country    (bodySmall 12sp/16sp w400 #41474D): "GB"
    │       [item.Country — ISO 3166]
    │       a11y (screen_reader_only): "Address: 48 Camden High Street, Flat 12, London, NW1 0LT, GB"
    │
    └── address_card[1]/ (card bg #F7F9FF, elevation 1, radius 12dp, padding 16dp)
        [OBPostalAddress8 — AddressType: Business]
        stack vertical gap 4dp:
        ├── address_type       (labelSmall 11sp/16sp w500 #50606E): "BUSINESS"
        ├── address_line_1     (bodyMedium 14sp/20sp w400 #181C20): "1 Canada Square"
        ├── address_line_2     (bodyMedium 14sp/20sp w400 #181C20): "Suite 400"
        ├── address_town_postcode (bodyMedium 14sp/20sp w400 #181C20): "London, E14 5AB"
        └── address_country    (bodySmall 12sp/16sp w400 #41474D): "GB"
            a11y (screen_reader_only): "Address: 1 Canada Square, Suite 400, London, E14 5AB, GB"

BottomNav/ (persistent, h 80dp)
├── tab Home         (icon:home,           label:"Home",         default, tint #41474D)
├── tab Accounts     (icon:account_balance, label:"Accounts",    selected, tint #266489)
├── tab Transactions (icon:receipt_long,   label:"Transactions", default, tint #41474D)
└── tab More         (icon:more_horiz,     label:"More",         default, tint #41474D)
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│ ← Account Holder                            │  ← top_app_bar small bg #F7F9FF
├─────────────────────────────────────────────┤
│                                              │
│                                              │
│                                              │
│              [error_outline]                 │  ← icon 48dp color #BA1A1A (error) centred
│                                              │
│       Unable to load account holder        │  ← title headlineSmall 24sp #181C20 centred
│                                              │
│   Request timed out. Please check your      │  ← body bodyMedium 14sp #41474D centred
│   connection and try again.                 │    (error.message — demo-data.yaml NETWORK_ERROR)
│                                              │
│                                              │
│        [        Try again        ]           │  ← retry_button filled, bg #266489
│                                              │    label-color #FFFFFF, radius 9999
│                                              │    min-height 56dp, padding h 24dp
│                                              │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│
└─────────────────────────────────────────────┘
```

### Component Hierarchy — error

```
Screen: Account Holder (PartyUiState.Error — code: NETWORK_ERROR, accountId: 40051512345678)
│
top_app_bar/ (small, bg #F7F9FF, elevation 0)
│  ├── back_button  (icon navigate_before 24dp #41474D)
│  └── title        (titleLarge 22sp/28sp #181C20): "Account Holder"
│
error_state/ (empty_state variant:error, vertically centred, padding horizontal 24dp)
│   accessibility_label: "Unable to load account holder details"
│
├── icon   (error_outline 48dp #BA1A1A, decorative:false,
│           contentDescription: "Error loading account holder data")
├── title  (headlineSmall 24sp/32sp w400 #181C20 center):
│           "Unable to load account holder"
│           [strings.party.error_title]
├── body   (bodyMedium 14sp/20sp w400 #41474D center):
│           "Request timed out. Please check your connection and try again."
│           [error.message from demo-data.yaml — NETWORK_ERROR fixture]
│           Note: 401 would render "Session expired. Please re-authenticate."
└── retry_button (button variant:filled, min-height 56dp, bg #266489 label-color #FFFFFF,
                  radius 9999, padding horizontal 24dp, touch target 56dp)
    label: "Try again"
    accessibility_label: "Retry loading account holder details"
    on_click → retry_load → partyLoad(accountId)
    action_contract: effect=call_api, library_refs=[ktorfit, hsbc-obie-ais-v4.0:party]
    Transitions: error → Loading → Content | Empty | ConsentRequired

BottomNav/ (persistent)
├── tab Home         (default, tint #41474D)
├── tab Accounts     (selected, tint #266489)
├── tab Transactions (default, tint #41474D)
└── tab More         (default, tint #41474D)
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│ ← Account Holder                            │  ← top_app_bar small bg #F7F9FF
├─────────────────────────────────────────────┤
│                                              │
│                                              │
│                                              │
│              [person_off]                    │  ← icon 48dp #41474D centred
│                                              │    (info variant — secondary tone)
│      No account holder details              │  ← title headlineSmall 24sp #181C20 centred
│                                              │    [strings.party.empty_title]
│   No party record found for this account.  │  ← body bodyMedium 14sp #41474D centred
│   This is typical for business accounts    │    [strings.party.empty_body]
│   where PSU identity is not exposed.       │    accountId: 40051999000001 (empty fixture)
│                                              │
│                                              │
│                                              │    No CTA — non-recoverable info state
│                                              │    (200 OK, empty Data.Party[])
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│
└─────────────────────────────────────────────┘
```

### Component Hierarchy — empty

```
Screen: Account Holder (PartyUiState.Empty — accountId: 40051999000001)
│   Triggered by: 200 OK with OBReadParty3.Data.Party[] empty AND OBReadParty2.Data.Party absent
│
top_app_bar/ (small, bg #F7F9FF, elevation 0)
│  ├── back_button  (icon navigate_before 24dp #41474D)
│  └── title        (titleLarge 22sp/28sp #181C20): "Account Holder"
│
empty_state_view/ (empty_state variant:info, vertically centred, padding horizontal 24dp)
│   accessibility_label: "No account holder details available"
│
├── icon   (person_off 48dp #41474D onSurfaceVariant, decorative:false,
│           contentDescription: "No account holder data for this account")
├── title  (headlineSmall 24sp/32sp w400 #181C20 center):
│           "No account holder details"
│           [strings.party.empty_title]
└── body   (bodyMedium 14sp/20sp w400 #41474D center):
           "No party record found for this account. This is typical for business accounts where PSU identity is not exposed."
           [strings.party.empty_body]
           No CTA button — state is informational; user can press back to account-detail.

BottomNav/ (persistent)
├── tab Home         (default, tint #41474D)
├── tab Accounts     (selected, tint #266489)
├── tab Transactions (default, tint #41474D)
└── tab More         (default, tint #41474D)
```

---

### State: consent_required

```
┌─────────────────────────────────────────────┐
│ ← Account Holder                            │  ← top_app_bar small bg #F7F9FF
├─────────────────────────────────────────────┤
│                                              │
│                                              │
│                                              │
│              [lock_person]                   │  ← icon 48dp #50606E (secondary) centred
│                                              │    warning variant — consent/permission tone
│     Permission not granted                  │  ← title headlineSmall 24sp #181C20 centred
│                                              │    [strings.party.consent_title]
│   Your consent does not include access to  │  ← body bodyMedium 14sp #41474D centred
│   account holder details. Please re-       │    [strings.party.consent_body]
│   authorise to grant ReadParty permission. │
│                                              │
│        [    Manage consents    ]             │  ← reauthorise_button filled
│                                              │    bg #266489 label-color #FFFFFF
│                                              │    min-height 56dp, radius 9999
│                                              │    → navigates to consent-list screen
│                                              │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│
└─────────────────────────────────────────────┘
```

### Component Hierarchy — consent_required

```
Screen: Account Holder (PartyUiState.ConsentRequired — HTTP 403 PermissionNotGranted: ReadParty missing)
│
top_app_bar/ (small, bg #F7F9FF, elevation 0)
│  ├── back_button  (icon navigate_before 24dp #41474D)
│  └── title        (titleLarge 22sp/28sp #181C20): "Account Holder"
│
consent_required_view/ (empty_state variant:warning, vertically centred, padding horizontal 24dp)
│   accessibility_label: "ReadParty permission not granted for this account"
│
├── icon   (lock_person 48dp #50606E secondary, decorative:false,
│           contentDescription: "Permission required to view account holder data")
├── title  (headlineSmall 24sp/32sp w400 #181C20 center):
│           "Permission not granted"
│           [strings.party.consent_title]
├── body   (bodyMedium 14sp/20sp w400 #41474D center):
│           "Your consent does not include access to account holder details. Please re-authorise to grant ReadParty permission."
│           [strings.party.consent_body]
└── reauthorise_button (button variant:filled, min-height 56dp, bg #266489 label-color #FFFFFF,
                        radius 9999, padding horizontal 24dp)
    label: "Manage consents"
    accessibility_label: "Manage your Open Banking consent permissions"
    on_click → navigate → consent-list
    action_contract: effect=navigate, target=consent-list
    Routes user to consent-list (Manage consents) screen to re-grant ReadParty permission.
    consent-list screen exists: idea-layer/screens/consent-list/ ✓

BottomNav/ (persistent)
├── tab Home         (default, tint #41474D)
├── tab Accounts     (selected, tint #266489)
├── tab Transactions (default, tint #41474D)
└── tab More         (default, tint #41474D)
```

---

### Interaction Summary

| Component | Action | Effect | Target / Behaviour |
|---|---|---|---|
| back_button (all states) | navigate_back | navigate | Returns to account-detail screen via system back navigation |
| retry_button (error state) | retry_load | call_api | Re-triggers parallel GET /accounts/{id}/party + /parties via ktorfit; screen → Loading → Content \| Empty \| ConsentRequired |
| reauthorise_button (consent_required state) | navigate_to_consent | navigate | consent-list (Manage consents) screen — user re-grants ReadParty permission in active consent scope |

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| party_header_card | match_parent − 32dp (≈ 361dp) | ≈ 112dp (wrap: 16+16+4+20+4+36+16) | 12dp |
| address_card (3-line body) | match_parent − 32dp (≈ 361dp) | ≈ 128dp (wrap: 16+16+4+20+4+20+4+20+4+16) | 12dp |
| email_row / mobile_row / phone_row | match_parent (393dp) | 56dp min | 0dp |
| contact_header / address_header | match_parent (393dp) | 40dp | 0dp |
| loading_indicator (circular) | 48dp | 48dp | n/a |
| error_outline / person_off / lock_person icon | 48dp | 48dp | n/a |
| retry_button / reauthorise_button | match_parent − 48dp (≈ 345dp) | 56dp | 9999dp (full pill) |
| leading_icon (email / phone / phone_android) | 24dp | 24dp | n/a |
| top_app_bar | match_parent (393dp) | 56dp | 0dp |
| bottom_nav | match_parent (393dp) | 80dp | 0dp |
