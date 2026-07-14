# ATM Locator — Visual Mockup

> Auto-generated from `screens/atm-locator/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Source: HSBC Open Data GET /atms (unauthenticated)
> Generated: 2026-07-14T00:00:00Z

---

## Screen: ATM Locator

Canvas: 393×852dp · Top app bar with back · Bottom nav · Material 3 light theme

---

### State: loading

```
┌─────────────────────────────────────────────┐
│ ← ATM Locator                               │  ← top_app_bar
├─────────────────────────────────────────────┤
│ ══════════════════════════════════════════  │  ← progress_indicator linear #266489
│  ┌────────────────────────────────────────┐ │
│  │ 🔍  Find an HSBC ATM near you…        │ │  ← location_search text_field (disabled
│  └────────────────────────────────────────┘ │    during loading, leading search icon)
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: content

```
┌─────────────────────────────────────────────┐
│ ← ATM Locator                               │
├─────────────────────────────────────────────┤
│                                              │
│  ┌────────────────────────────────────────┐ │
│  │ 🔍  Camden Town                    ✕  │ │  ← location_search (active, clear icon)
│  └────────────────────────────────────────┘ │
│                                              │
│  ( ⏰ 24 hours )  ( ♿ Wheelchair )  ( 💰 Cash deposit )│
│                                              │    service_filters chip_group h-scroll
│  4 ATMs found                               │  ← result_count labelMedium #41474D
│                                              │
│ ┌─────────────────────────────────────────┐ │
│ │  HSBC Camden Town                       │ │  ← atm_card card elevation 1 radius 12dp
│ │  117 Camden High Street, NW1 7JR        │ │    atm_name titleMedium #181C20
│ │  0.3 miles                              │ │    atm_address bodySmall #41474D
│ │  ( ⏰ 24 hours ) ( ♿ ) ( 💰 )         │ │    atm_distance labelSmall #50606E
│ └─────────────────────────────────────────┘ │    atm_service_chips h-scroll
│ ┌─────────────────────────────────────────┐ │
│ │  HSBC Kentish Town                      │ │
│ │  207 Kentish Town Road, NW5 2JU         │ │
│ │  0.7 miles                              │ │
│ │  ( ⏰ Mon–Sat 08:00–20:00 )            │ │
│ └─────────────────────────────────────────┘ │
│ ┌─────────────────────────────────────────┐ │
│ │  HSBC Holloway Road                     │ │
│ │  302 Holloway Road, N7 6NJ              │ │
│ │  1.2 miles                              │ │
│ │  ( ⏰ 24 hours ) ( 💰 )                │ │
│ └─────────────────────────────────────────┘ │
│ ┌─────────────────────────────────────────┐ │
│ │  HSBC Islington                         │ │
│ │  63–65 Upper Street, N1 0NY             │ │
│ │  1.6 miles                              │ │
│ │  ( ⏰ 24 hours ) ( ♿ )                 │ │
│ └─────────────────────────────────────────┘ │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
top_app_bar/ (title "ATM Locator", leading back → account-detail)
location_search/ (text_field, leading search icon, trailing clear ✕)
│  placeholder: "Find an HSBC ATM near you…"
│  on_change → search_atms (client-side Name + PostCode filter)
service_filters/ (chip_group h-scroll, state_binding=[content, empty])
│  ├── filter_24h (chip filter, toggles is24h predicate): "24 hours"
│  ├── filter_wheelchair (chip filter, toggles hasWheelchairAccess): "Wheelchair"
│  └── filter_deposit (chip filter, toggles hasCashDeposit): "Cash deposit"
result_count/ (text labelMedium #41474D): "4 ATMs found" (state_binding=[content])
atm_list/ (list vertical gap 8dp padding h 16dp, items_source=filteredAtms)
└── atm_card × N (card elevation 1 radius 12dp padding 16dp tap=open_atm_directions)
     ├── atm_name         (titleMedium #181C20): "HSBC Camden Town"
     ├── atm_address      (bodySmall #41474D): "117 Camden High Street, NW1 7JR"
     ├── atm_distance     (labelSmall #50606E): "0.3 miles"
     └── atm_service_chips/ (chip_group h-scroll, display only)
          ├── chip_hours     (chip, icon access_time, always): "24 hours"
          ├── chip_wheelchair (chip, icon accessible, visible_when HasWheelchairAccess)
          └── chip_deposit   (chip, icon savings, visible_when HasCashDeposit)
BottomNav (always)
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│ ← ATM Locator                               │
├─────────────────────────────────────────────┤
│  ┌────────────────────────────────────────┐ │
│  │ 🔍  NW7 2AA                       ✕  │ │  ← search bar still active
│  └────────────────────────────────────────┘ │
│  ( ⏰ 24 hours )  ( ♿ Wheelchair )  ( 💰 ) │  ← filter chips still shown
│                                              │
│            [location_off]                    │  ← icon 48dp #41474D
│    No ATMs found                            │  ← title headlineSmall #181C20
│  No HSBC ATMs match your search or        │  ← body bodyMedium #41474D
│  current filter.                           │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│ ← ATM Locator                               │
├─────────────────────────────────────────────┤
│            [error_outline]                   │  ← icon 48dp #BA1A1A
│    Could not load ATM data                  │  ← title headlineSmall #181C20
│  Check your connection and try again.      │  ← body bodyMedium #41474D
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
| location_search | search_atms | client-side filter (Name + PostCode) |
| filter_24h chip | toggle_filter_24h | in-place filter |
| filter_wheelchair chip | toggle_filter_wheelchair | in-place filter |
| filter_deposit chip | toggle_filter_deposit | in-place filter |
| atm_card | open_atm_directions | geo:// deep-link → maps app |
| retry_button | retry_load | in-place retry (unauthenticated endpoint) |

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| location_search | match_parent − 32dp | 56dp | 28dp |
| service_filters | match_parent, h-scroll | 40dp | 0 |
| filter chip | wrap | 32dp | 9999 |
| atm_card | match_parent − 32dp | ~120dp | 12dp |
| atm_service chip | wrap | 28dp | 9999 |
