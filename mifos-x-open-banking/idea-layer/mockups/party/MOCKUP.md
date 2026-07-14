# Account Holder (Party) — Visual Mockup

> Auto-generated from `screens/party/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Source: OBReadParty2 — GET /accounts/{id}/party + /parties (parallel)
> Generated: 2026-07-14T00:00:00Z

---

## Screen: Account Holder

Canvas: 393×852dp · Top app bar with back · Bottom nav · Material 3 light theme

---

### State: loading

```
┌─────────────────────────────────────────────┐
│ ← Account Holder                            │  ← top_app_bar
├─────────────────────────────────────────────┤
│                   ◌                          │  ← circular progress #266489 centred
│                                              │    (parallel /party + /parties in flight)
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: content

```
┌─────────────────────────────────────────────┐
│ ← Account Holder                            │
├─────────────────────────────────────────────┤
│                                              │
│ ┌─────────────────────────────────────────┐ │
│ │  Sole                                   │ │  ← party_type_label labelMedium #50606E
│ │  Priya Sharma                           │ │  ← party_name headlineMedium #181C20
│ │  PRIYA ANJALI SHARMA                    │ │  ← party_full_legal_name bodyMedium #41474D
│ └─────────────────────────────────────────┘ │    elevation 2 radius 12dp
│                                              │
│  CONTACT                                    │  ← contact_header section_header #41474D
│                                              │
│  ✉  Email                                  │  ← email_row list_item leading_icon email
│     priya.sharma@example.com               │    trailing bodyMedium #181C20
│  📱  Mobile                                 │  ← mobile_row leading_icon phone_android
│     +447700900123                          │    trailing bodyMedium #181C20
│  📞  Phone                                  │  ← phone_row (visible_when non-empty)
│     (not on record)                        │
│                                              │
│  ADDRESS                                    │  ← address_header section_header #41474D
│                                              │
│ ┌─────────────────────────────────────────┐ │
│ │  RESIDENTIAL                            │ │  ← address_type labelSmall #50606E
│ │  14 Oak Lane                            │ │  ← address_line_1 bodyMedium
│ │  London, SW1A 1AA                       │ │  ← address_town_postcode bodyMedium
│ │  GB                                     │ │  ← address_country bodySmall #41474D
│ └─────────────────────────────────────────┘ │    card elevation 1 radius 12dp
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
top_app_bar/ (title "Account Holder", leading back)
party_header_card/ (card elevation 2 radius 12dp padding 16dp margin h 16dp)
│  ├── party_type_label   (labelMedium #50606E): "Sole"  [OBParty2.PartyType]
│  ├── party_name         (headlineMedium #181C20): "Priya Sharma"
│  └── party_full_legal_name (bodyMedium #41474D): "PRIYA ANJALI SHARMA"
contact_header/ (section_header): "CONTACT"
email_row/ (list_item leading_icon email): "priya.sharma@example.com"
mobile_row/ (list_item leading_icon phone_android): "+447700900123"
phone_row/ (list_item leading_icon phone, visible_when non-empty)
address_header/ (section_header): "ADDRESS"
address_list/ (list vertical gap 8dp, items_source=party.Address)
└── address_card × N (card elevation 1 radius 12dp padding 16dp)
     ├── address_type       (labelSmall #50606E): "RESIDENTIAL"
     ├── address_line_1     (bodyMedium): "14 Oak Lane"
     ├── address_line_2     (bodyMedium, optional AddressLine[0])
     ├── address_town_postcode (bodyMedium): "London, SW1A 1AA"
     └── address_country    (bodySmall #41474D): "GB"
BottomNav (always)
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│ ← Account Holder                            │
├─────────────────────────────────────────────┤
│            [person_off]                      │  ← icon 48dp #41474D
│    No account holder data                  │  ← title headlineSmall #181C20
│  No party record found for this account.  │  ← body bodyMedium #41474D
│  This may be a joint or business account. │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: consent_required

```
┌─────────────────────────────────────────────┐
│ ← Account Holder                            │
├─────────────────────────────────────────────┤
│            [lock_person]                     │  ← icon 48dp #50606E
│  ReadParty permission not granted          │  ← title headlineSmall #181C20
│  Your consent does not include permission  │  ← body bodyMedium #41474D
│  to read account holder data. Reauthorise  │
│  to grant ReadParty.                       │
│         [  Manage consents  ]               │  ← reauthorise_button filled #266489
│                                              │    → consent-list
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│ ← Account Holder                            │
├─────────────────────────────────────────────┤
│            [error_outline]                   │  ← icon 48dp #BA1A1A
│    Unable to load account holder           │  ← title headlineSmall #181C20
│  body from error.message (401/network)     │
│         [  Try again  ]                     │  ← retry_button filled #266489
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### Interaction Summary

| Component | Action | Target |
|---|---|---|
| back_button | navigate_back | account-detail |
| reauthorise_button (consent_required) | navigate_consent_list | consent-list |
| retry_button (error) | retry_load | in-place retry |

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| party_header_card | match_parent − 32dp | ~96dp | 12dp |
| address_card | match_parent − 32dp | ~112dp | 12dp |
| list_item row | match_parent | 56dp min | 0 |
