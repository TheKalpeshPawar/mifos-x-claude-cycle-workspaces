# Beneficiaries — Visual Mockup

> Auto-generated from `screens/beneficiaries/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-14T00:00:00Z

---

## Screen: Beneficiaries

Canvas: 393×852dp · Top app bar with back · Bottom nav · Material 3 light theme

---

### State: loading

```
┌─────────────────────────────────────────────┐
│ ← Beneficiaries                             │  ← top_app_bar
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
│ ← Beneficiaries                             │
├─────────────────────────────────────────────┤
│                                              │
│  ┌────────────────────────────────────────┐ │
│  │ 🔍  Search beneficiaries               │ │  ← beneficiary_search search_bar
│  └────────────────────────────────────────┘ │    placeholder "Search by name or reference"
│                                              │
│ ┌─────────────────────────────────────────┐ │
│ │  [JL]  J Leach                          │ │  ← beneficiary_card card elevation 1
│ │        Sort Code                        │ │    avatar initials circle #C9E6FF #004B6F
│ │        40-05-15 98765432                │ │    scheme_label labelSmall #50606E
│ │        Ref: Family transfer             │ │    identification Roboto Mono bodySmall
│ └─────────────────────────────────────────┘ │    reference bodySmall #41474D
│ ┌─────────────────────────────────────────┐ │
│ │  [AK]  A Kumar                          │ │
│ │        Sort Code                        │ │
│ │        60-40-20 11223344                │ │
│ │        Ref: Freelance invoice           │ │
│ └─────────────────────────────────────────┘ │
│ ┌─────────────────────────────────────────┐ │
│ │  [SP]  S Patel                          │ │
│ │        IBAN                             │ │
│ │        GB29NWBK60161331926819           │ │
│ └─────────────────────────────────────────┘ │
│ ┌─────────────────────────────────────────┐ │
│ │  [BT]  BT Phone                         │ │
│ │        Sort Code                        │ │
│ │        30-91-56 00004715                │ │
│ └─────────────────────────────────────────┘ │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
top_app_bar/ (title "Beneficiaries", leading back → account-detail)
back_button/ (icon_button arrow_back always visible)
beneficiary_search/ (search_bar, state_binding=[content])
│  placeholder: "Search by name or reference"
│  on_change → filter_beneficiaries (client-side, no API)
beneficiaries_list/ (list vertical gap 8dp padding h 16dp)
└── beneficiary_card × N (card elevation 1 radius 12dp padding 16dp)
     ├── avatar_initials (circle 40dp bg #C9E6FF text #004B6F, 2-char initials)
     ├── creditor_name   (titleMedium #181C20): "J Leach"
     ├── scheme_label    (labelSmall #50606E): "Sort Code" / "IBAN" / "Paym"
     ├── identification  (bodySmall Roboto Mono #41474D): "40-05-15 98765432"
     └── reference       (bodySmall #41474D, optional): "Ref: Family transfer"
BottomNav (always)
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│ ← Beneficiaries                             │
├─────────────────────────────────────────────┤
│            [people]                          │  ← icon 48dp #41474D
│    No beneficiaries                         │  ← title headlineSmall #181C20
│  No payees have been set up for this       │  ← body bodyMedium #41474D
│  account.                                  │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│ ← Beneficiaries                             │
├─────────────────────────────────────────────┤
│            [error_outline]                   │  ← icon 48dp #BA1A1A
│    Unable to load beneficiaries            │  ← title headlineSmall #181C20
│  body from typed error (401=retry / 403=View Consents)│
│         [  Try again  ]                     │  ← retry (not shown 403)
│         [  View consents  ]                 │  ← → consent-list (403 only)
└─────────────────────────────────────────────┘
```

---

### Interaction Summary

| Component | Action | Target |
|---|---|---|
| back_button | navigate_back | account-detail |
| beneficiary_search | filter_beneficiaries | in-place filter (Name/Reference) |
| beneficiary_card | (display only, AIS read) | — |
| retry_button (error, 401/network) | retry_load | in-place retry |
| view_consents_button (error, 403) | navigate_consent_list | consent-list |

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| search_bar | match_parent − 32dp | 48dp | 28dp |
| beneficiary_card | match_parent − 32dp | ~80dp | 12dp |
| avatar_initials | 40dp | 40dp | circle |
