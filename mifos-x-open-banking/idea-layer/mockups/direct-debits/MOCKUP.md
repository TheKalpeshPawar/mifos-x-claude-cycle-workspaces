# Direct Debits — Visual Mockup

> Auto-generated from `screens/direct-debits/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-14T00:00:00Z

---

## Screen: Direct Debits

Canvas: 393×852dp · Top app bar with back · Bottom nav · Material 3 light theme

---

### State: loading

```
┌─────────────────────────────────────────────┐
│ ← Direct Debits                             │  ← top_app_bar
├─────────────────────────────────────────────┤
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │  ← skeleton list_card × 4
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │    each ~80dp radius 12dp
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
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
│ ← Direct Debits                             │
├─────────────────────────────────────────────┤
│                                              │
│  ( 5 Active )  ( 1 Inactive )               │  ← mandate_summary_chips (non-interactive)
│                                              │    Active chip primary tonal
│ ┌─────────────────────────────────────────┐ │    Inactive chip secondary tonal
│ │  📋  EDF Energy                         │ │  ← direct_debit_card elevation 1 radius 12dp
│ │      [Active]                           │ │    status badge tonal primary
│ │      Last: £68.50 on 05 Jul 2026        │ │    bodyMedium #181C20
│ │      Mandate: DDM-001                   │ │    bodySmall Roboto Mono #41474D
│ └─────────────────────────────────────────┘ │
│ ┌─────────────────────────────────────────┐ │
│ │  📋  Sky Broadband                      │ │
│ │      [Active]                           │ │
│ │      Last: £42.00 on 02 Jul 2026        │ │
│ │      Mandate: DDM-002                   │ │
│ └─────────────────────────────────────────┘ │
│ ┌─────────────────────────────────────────┐ │
│ │  📋  Thames Water                       │ │
│ │      [Active]                           │ │
│ │      Last: £35.20 on 01 Jul 2026        │ │
│ └─────────────────────────────────────────┘ │
│ ┌─────────────────────────────────────────┐ │
│ │  📋  Council Tax — LB Hackney           │ │
│ │      [Active]                           │ │
│ │      Last: £142.00 on 01 Jul 2026       │ │
│ └─────────────────────────────────────────┘ │
│ ┌─────────────────────────────────────────┐ │
│ │  📋  Old gym membership                 │ │
│ │      [Inactive]                         │ │  ← Inactive badge secondary outline
│ │      Last: £24.99 on 01 Mar 2026        │ │
│ └─────────────────────────────────────────┘ │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
top_app_bar/ (title "Direct Debits", leading back → account-detail)
back_button/ (icon_button arrow_back, always visible)
mandate_summary_chips/ (chip_group informational non-interactive, padding h 16dp)
│  ├── active_count_chip   "5 Active" (tonal primary)
│  └── inactive_count_chip "1 Inactive" (tonal secondary)
direct_debits_list/ (list vertical gap 8dp padding h 16dp, Active-first sort)
└── direct_debit_card × N (card elevation 1 radius 12dp padding 16dp)
     ├── dd_icon          (icon subscriptions md #50606E)
     ├── creditor_name    (titleMedium #181C20): "EDF Energy"
     ├── status_badge     (chip tonal, Active=primary, Inactive=secondary)
     ├── prev_payment     (bodyMedium #181C20): "Last: £68.50 on 05 Jul 2026"
     └── mandate_id       (bodySmall Roboto Mono #41474D): "Mandate: DDM-001"
BottomNav (always)
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│ ← Direct Debits                             │
├─────────────────────────────────────────────┤
│            [subscriptions]                   │  ← icon 48dp #41474D
│    No direct debits                         │  ← title headlineSmall #181C20
│  No direct debits are set up for this      │  ← body bodyMedium #41474D
│  account.                                  │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│ ← Direct Debits                             │
├─────────────────────────────────────────────┤
│            [error_outline]                   │  ← icon 48dp #BA1A1A
│    Unable to load direct debits            │
│  body from VM typed error (401/403/429/network)│
│         [  Try again  ]                     │  ← retry (suppressed for 403)
│         [  View consents ]                  │  ← → consent-list (if 403)
└─────────────────────────────────────────────┘
```

---

### Interaction Summary

| Component | Action | Target |
|---|---|---|
| back_button | navigate_back | account-detail |
| direct_debit_card | (display only, AIS) | — |
| retry_button (error) | retry_load | in-place (not shown for 403) |
| view_consents_button (error 403) | navigate_consent_list | consent-list |

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| direct_debit_card | match_parent − 32dp | ~96dp | 12dp |
| status_badge | wrap | 24dp | 9999 |
| summary chip | wrap | 28dp | 9999 |
