# ATM Locator — Visual Mockup

> Auto-generated from `screens/atm-locator/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-16T00:00:00Z

---

## Screen: ATM Locator

Canvas: 393×852dp (Pixel 5) · Top app bar visible (back) · Bottom nav visible · No FAB · Roboto font · Material 3 light theme · bg #F7F9FF

Shell (from `app-shell.yaml`):
- Bottom navigation: Home (home) | Accounts (account_balance) | Transactions (receipt_long) | More (more_horiz). None selected — ATM Locator is a secondary screen not part of the nav rail.
- Top app bar: variant small, title "Find HSBC ATM" (resolved from `strings.atm_locator_title`), leading back arrow (← icon 24dp #266489, 48dp touch target, invokes `NavController.popBackStack()`).
- FAB: disabled per `ui.yaml#shell.fab_visible: false`.

---

### State: loading

```
┌─────────────────────────────────────────────┐
│ ←  Find HSBC ATM                           │  ← top_app_bar: h 64dp, bg #F7F9FF
│                                              │    title "Find HSBC ATM" titleLarge 22sp #181C20
│                                              │    back ← icon 24dp #266489, touch 48dp
├─────────────────────────────────────────────┤
│                                              │    content area: 708dp (852 − 64 − 80)
│  ┌──────────────────────────────────────┐   │
│  │ 🔍  Search by postcode or area       │   │  ← location_search: filled text_field
│  └──────────────────────────────────────┘   │    h 56dp, radius 28dp, bg #DDE3EA
│                                              │    placeholder bodyMedium 14sp #41474D
│                                              │    padding h 16dp, top 8dp, bottom 4dp
│  ▓▓▓▓▓▓▓▓▓▓▓▓▓▓░░░░░░░░░░░░░░░░░░░░░░░░░  │  ← progress_indicator linear h 4dp
│                                              │    indicator #266489 (primary)
│                                              │    track #C9E6FF (primaryContainer)
│                                              │    indeterminate animation, padding top 16dp
│                                              │
│   [service_filters: hidden — state=loading] │  ← chip_group state_binding=[content,empty]
│   [result_count: hidden — state=loading]    │  ← text state_binding=[content]
│   [atm_list: hidden — state=loading]        │  ← list state_binding=[content]
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│  ← bottom_nav h 80dp bg #F7F9FF
│                                              │    no tab selected; tint #41474D all tabs
└─────────────────────────────────────────────┘
```

### Component Hierarchy — loading

```
Screen: ATM Locator (AtmLocatorUiState.Loading)
│
top_app_bar/ (variant small, h 64dp, bg #F7F9FF, elevation 0)
│   title: "Find HSBC ATM" (titleLarge 22sp Roboto 400 #181C20)
│   leading: ← back icon 24dp color #266489, touch target 48dp
│
location_search/ (filled text_field, h 56dp, radius 28dp)
│   bg: #DDE3EA (surfaceVariant)
│   label: "Search by postcode or area" (bodySmall 12sp #41474D)
│   placeholder: "e.g. NW1 0LT or Camden" (bodyMedium 14sp #41474D)
│   leading icon: search 24dp #41474D
│   trailing icon: clear ✕ 24dp #41474D (visible when text ≠ empty)
│   padding h 16dp, top 8dp (spacing.sm), bottom 4dp (spacing.xs)
│   on_change → search_atms: effect=transform_state (client-side filter)
│
progress_indicator/ (linear, state_binding=[loading])
│   h 4dp, width match_parent
│   track: #C9E6FF (primaryContainer)
│   indicator: #266489 (primary)
│   animation: indeterminate (cubic-bezier(0.2,0,0,1.0), duration 300ms)
│   accessibility_label: "Searching for nearby ATMs" (role: progressBar)
│   padding top 16dp (spacing.md)
│
BottomNav/ (persistent, h 80dp bg #F7F9FF)
├── tab Home          (icon home,           label "Home",         tint #41474D unselected)
├── tab Accounts      (icon account_balance, label "Accounts",    tint #41474D unselected)
├── tab Transactions  (icon receipt_long,   label "Transactions", tint #41474D unselected)
└── tab More          (icon more_horiz,     label "More",         tint #41474D unselected)
```

---

### State: content

```
┌─────────────────────────────────────────────┐
│ ←  Find HSBC ATM                           │  ← top_app_bar h 64dp bg #F7F9FF
│                                              │    title titleLarge 22sp #181C20
├─────────────────────────────────────────────┤
│                                              │
│  ┌──────────────────────────────────────┐   │  ← location_search: active with clear icon
│  │ 🔍  NW1 0LT                     ✕  │   │    text "NW1 0LT" (demo search query)
│  └──────────────────────────────────────┘   │    radius 28dp bg #DDE3EA
│                                              │    focused bottom-stroke 2dp #266489
│  [ 24h ] [ Wheelchair ] [ Cash deposit ]    │  ← service_filters chip_group h-scroll
│                                              │    chip h 32dp radius 9999dp border 1dp #72787E
│                                              │    unselected: fill transparent text #41474D
│                                              │    selected: fill #C9E6FF border #266489 text #004B6F
│  4 ATMs found                               │  ← result_count labelMedium 12sp W500 #41474D
│                                              │    padding h 16dp, bottom 4dp
│ ┌─────────────────────────────────────────┐ │
│ │  HSBC Camden Town                       │ │  ← atm_card[0] outlined card
│ │  218 Camden High Street, London NW1 8QR │ │    radius 12dp, padding 16dp, elevation 1dp
│ │  0.3 miles                              │ │    border 1dp #72787E (outline), bg #F7F9FF
│ │  [⏰ 24 hours] [♿ Wheelchair] [💰]    │ │    name: titleMedium 16sp W500 #181C20
│ └─────────────────────────────────────────┘ │    addr: bodySmall 12sp W400 #41474D
│                                              │    dist: labelSmall 11sp W500 #50606E
│ ┌─────────────────────────────────────────┐ │    tap → open_atm_directions (share_external)
│ │  HSBC Kentish Town                      │ │  ← atm_card[1] HasCashDeposit: false
│ │  152 Kentish Town Road, London NW1 9QB  │ │    chip_deposit HIDDEN (visible_when false)
│ │  0.7 miles                              │ │
│ │  [⏰ 24 hours] [♿ Wheelchair]          │ │
│ └─────────────────────────────────────────┘ │
│                                              │
│ ┌─────────────────────────────────────────┐ │  ← atm_card[2] OpeningHours ≠ 24h
│ │  HSBC Euston Road                       │ │
│ │  376 Euston Road, London NW1 3BL        │ │
│ │  1.1 miles                              │ │
│ │  [⏰ Mon–Sat 08:00–20:00] [♿] [💰]    │ │
│ └─────────────────────────────────────────┘ │
│                                              │
│ ┌─────────────────────────────────────────┐ │  ← atm_card[3] all three chips visible
│ │  HSBC Oxford Street                     │ │    (HasWheelchairAccess: true,
│ │  92 Oxford Street, London W1D 1LR       │ │     HasCashDeposit: true)
│ │  2.0 miles                              │ │
│ │  [⏰ 24 hours] [♿ Wheelchair] [💰]    │ │
│ └─────────────────────────────────────────┘ │
│   ↕ scrollable list · gap 8dp · bottom 24dp │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│  ← bottom_nav h 80dp bg #F7F9FF
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
Screen: ATM Locator (AtmLocatorUiState.Content)
│
top_app_bar/ (variant small, bg #F7F9FF h 64dp)
│   title: "Find HSBC ATM" titleLarge 22sp #181C20
│   leading: ← icon 24dp #266489 touch 48dp
│
location_search/ (filled text_field, active, h 56dp radius 28dp)
│   value: "NW1 0LT" (drives search_atms client-side filter)
│   bg: #DDE3EA, focused bottom-stroke 2dp #266489
│   trailing_icon: clear ✕ 24dp #41474D (visible, searchQuery ≠ empty)
│   on_change → search_atms: transform_state (substring match Name + PostCode)
│
service_filters/ (chip_group h-scroll, state_binding=[content,empty])
│   padding h 16dp (spacing.md), v 4dp (spacing.xs), gap 4dp (spacing.xs)
│   ├── filter_24h      (chip variant=filter, h 32dp radius 9999dp)
│   │     label: "24h" (strings.atm_locator_filter_24h, labelLarge 14sp)
│   │     on_click → toggle_filter_24h: transform_state (toggles is24h)
│   ├── filter_wheelchair (chip variant=filter, h 32dp radius 9999dp)
│   │     label: "Wheelchair" (strings.atm_locator_filter_wheelchair)
│   │     on_click → toggle_filter_wheelchair: transform_state
│   └── filter_deposit  (chip variant=filter, h 32dp radius 9999dp)
│         label: "Cash deposit" (strings.atm_locator_filter_deposit)
│         on_click → toggle_filter_deposit: transform_state
│
result_count/ (text labelMedium 12sp W500 #41474D)
│   value: "4 ATMs found" (filteredAtms.size=4 → strings.atm_locator_results_count)
│   padding h 16dp, bottom 4dp
│
atm_list/ (list vertical scroll, items_source=filteredAtms, gap 8dp, padding h 16dp bottom 24dp)
│
├── atm_card[0] (card outlined, elevation 1, radius 12dp, padding 16dp, bg #F7F9FF)
│   │   border 1dp #72787E, ripple #266489 12%, tap → open_atm_directions
│   ├── atm_name     "HSBC Camden Town"                 (titleMedium 16sp W500 #181C20)
│   ├── atm_address  "218 Camden High Street, London    (bodySmall 12sp W400 #41474D)
│   │                 NW1 8QR"                           accessibility: "ATM address"
│   ├── atm_distance "0.3 miles"                        (labelSmall 11sp W500 #50606E)
│   │                                                    accessibility: "Distance to ATM"
│   └── atm_service_chips/ (chip_group h-scroll, display only, h 28dp chips)
│       ├── chip_hours     (icon access_time 16dp, "24 hours",    always shown)
│       ├── chip_wheelchair (icon accessible 16dp,  "Wheelchair", visible HasWheelchairAccess=true)
│       └── chip_deposit   (icon savings 16dp,      "Cash deposit", visible HasCashDeposit=true)
│
├── atm_card[1] (outlined card, tap → open_atm_directions)
│   ├── atm_name     "HSBC Kentish Town"
│   ├── atm_address  "152 Kentish Town Road, London NW1 9QB"
│   ├── atm_distance "0.7 miles"
│   └── atm_service_chips/
│       ├── chip_hours    "24 hours"
│       └── chip_wheelchair "Wheelchair"   (HasCashDeposit=false → chip_deposit NOT rendered)
│
├── atm_card[2] (outlined card, tap → open_atm_directions)
│   ├── atm_name     "HSBC Euston Road"
│   ├── atm_address  "376 Euston Road, London NW1 3BL"
│   ├── atm_distance "1.1 miles"
│   └── atm_service_chips/
│       ├── chip_hours    "Mon–Sat 08:00–20:00"
│       ├── chip_wheelchair "Wheelchair"
│       └── chip_deposit  "Cash deposit"
│
└── atm_card[3] (outlined card, tap → open_atm_directions)
    ├── atm_name     "HSBC Oxford Street"
    ├── atm_address  "92 Oxford Street, London W1D 1LR"
    ├── atm_distance "2.0 miles"
    └── atm_service_chips/
        ├── chip_hours    "24 hours"
        ├── chip_wheelchair "Wheelchair"
        └── chip_deposit  "Cash deposit"

BottomNav/ (persistent, h 80dp bg #F7F9FF)
├── tab Home          (icon home,           tint #41474D unselected)
├── tab Accounts      (icon account_balance, tint #41474D unselected)
├── tab Transactions  (icon receipt_long,   tint #41474D unselected)
└── tab More          (icon more_horiz,     tint #41474D unselected)
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│ ←  Find HSBC ATM                           │  ← top_app_bar h 64dp bg #F7F9FF
├─────────────────────────────────────────────┤
│                                              │
│  ┌──────────────────────────────────────┐   │  ← location_search: active, no results
│  │ 🔍  TR1 9ZZ                     ✕  │   │    value: "TR1 9ZZ" (demo empty search query)
│  └──────────────────────────────────────┘   │    bg #DDE3EA radius 28dp
│                                              │
│  [ 24h ] [ Wheelchair ] [ Cash deposit ]    │  ← service_filters visible (state_binding=[content,empty])
│                                              │    chips remain active for predicate adjustment
│                                              │
│                                              │
│               [location_off]                 │  ← icon 48dp #41474D (onSurfaceVariant)
│                                              │    centred, padding top 48dp from chip row
│         No ATMs found nearby                │  ← empty_atms title
│                                              │    headlineSmall 24sp W400 #181C20, centred
│  No HSBC ATMs match your search. Try a      │  ← empty_atms body
│  different postcode or area name.            │    bodyMedium 14sp W400 #41474D, centred
│                                              │    padding h 32dp, top 8dp
│                                              │    [no retry button — data loaded, adjust filters]
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│  ← bottom_nav h 80dp bg #F7F9FF
└─────────────────────────────────────────────┘
```

### Component Hierarchy — empty

```
Screen: ATM Locator (AtmLocatorUiState.Empty)
│
top_app_bar/ (variant small, bg #F7F9FF h 64dp)
│   title: "Find HSBC ATM" titleLarge 22sp #181C20
│   leading: ← icon 24dp #266489
│
location_search/ (filled text_field, active, h 56dp radius 28dp)
│   value: "TR1 9ZZ" (postcode with zero HSBC ATM matches)
│   on_change → search_atms: filteredAtms=[] → UiState.Empty
│   trailing_icon: clear ✕ 24dp #41474D
│
service_filters/ (chip_group h-scroll, state_binding=[content,empty])
│   [same chip structure as content state — all unselected by default]
│   ├── filter_24h      label "24h"
│   ├── filter_wheelchair label "Wheelchair"
│   └── filter_deposit  label "Cash deposit"
│
empty_atms/ (empty_state, state_binding=[empty])
│   icon: location_off 48dp color #41474D — centred, padding top 48dp
│   title: "No ATMs found nearby"
│          (headlineSmall 24sp Roboto W400 #181C20) — centred, padding h 32dp
│   body: "No HSBC ATMs match your search. Try a different postcode or area name."
│          (bodyMedium 14sp Roboto W400 #41474D) — centred, padding h 32dp, top 8dp
│   accessibility_label: "No ATMs found near your search location"
│   note: no action button — ATM data loaded successfully; user adjusts query/filters
│
BottomNav/ (persistent, h 80dp bg #F7F9FF, all tabs unselected #41474D)
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│ ←  Find HSBC ATM                           │  ← top_app_bar h 64dp bg #F7F9FF
├─────────────────────────────────────────────┤
│                                              │
│  ┌──────────────────────────────────────┐   │  ← location_search: resting (empty after retry reset)
│  │ 🔍  Search by postcode or area       │   │    placeholder text (filterState.default + searchQuery="")
│  └──────────────────────────────────────┘   │    bg #DDE3EA radius 28dp
│                                              │
│  [service_filters: hidden — state=error]    │  ← chip_group NOT shown (state_binding=[content,empty])
│                                              │
│             [error_outline]                  │  ← icon 48dp #BA1A1A (error color)
│                                              │    centred, padding top 48dp from search field
│           Could not load ATMs               │  ← error_state title
│                                              │    headlineSmall 24sp W400 #181C20, centred
│  Could not reach HSBC Open Data.            │  ← error_state body (error.message)
│  Check your connection.                      │    bodyMedium 14sp W400 #41474D, centred
│                                              │    padding h 32dp, top 8dp
│          [       Retry       ]               │  ← retry_button filled_button
│                                              │    bg #266489, text #FFFFFF labelLarge 14sp W500
│                                              │    h 40dp (min touch 48dp), radius 9999dp
│                                              │    padding h 24dp; centred; margin top 24dp
│                                              │    on_click → retry_load: call_api GET /atms
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│  ← bottom_nav h 80dp bg #F7F9FF
└─────────────────────────────────────────────┘
```

### Component Hierarchy — error

```
Screen: ATM Locator (AtmLocatorUiState.Error)
│
top_app_bar/ (variant small, bg #F7F9FF h 64dp)
│   title: "Find HSBC ATM" titleLarge 22sp #181C20
│   leading: ← icon 24dp #266489
│
location_search/ (filled text_field, state_binding=[loading,content,empty,error])
│   value: "" (reset — retryLoad clears searchQuery + filterState.default)
│   placeholder: "e.g. NW1 0LT or Camden" bodyMedium 14sp #41474D
│   bg: #DDE3EA radius 28dp; no trailing icon (empty)
│
error_state/ (empty_state variant=error, state_binding=[error])
│   icon: error_outline 48dp color #BA1A1A (error) — centred, padding top 48dp
│   title: "Could not load ATMs"
│          (strings.atm_locator_error_title — headlineSmall 24sp W400 #181C20) — centred
│   body: "Could not reach HSBC Open Data. Check your connection."
│          (error.message from NETWORK_ERROR — bodyMedium 14sp W400 #41474D) — centred
│          [HTTP_5XX variant: "HSBC Open Data service unavailable. Please try again."]
│   accessibility_label: "Error loading ATM list"
│   │
│   └── retry_button/ (filled_button, child of error_state)
│         label: "Retry" (strings.atm_locator_retry)
│         style: labelLarge 14sp W500 color #FFFFFF
│         bg: #266489 (primary)
│         radius: 9999dp (full pill)
│         h: 40dp, padding h 24dp, min touch target 48dp
│         accessibility_label: "Retry loading ATM list"
│         on_click → retry_load: effect=call_api
│                    (resets filterState.default, delegates to atmsLoad,
│                     GET /atms HSBC Open Data unauthenticated 15s timeout)
│
BottomNav/ (persistent, h 80dp bg #F7F9FF, all tabs unselected #41474D)
```

---

### Interaction Summary

| Component | Action | Target |
|---|---|---|
| back button (top_app_bar_leading) | navigate_back | NavController.popBackStack() — returns to previous screen |
| location_search (text_field) | search_atms | filteredAtms re-derived: substring match on ATM Name + PostCode; no API call |
| filter_24h chip | toggle_filter_24h | filterState.is24h toggled → filteredAtms re-derived; no API call |
| filter_wheelchair chip | toggle_filter_wheelchair | filterState.hasWheelchairAccess toggled → filteredAtms re-derived; no API call |
| filter_deposit chip | toggle_filter_deposit | filterState.hasCashDeposit toggled → filteredAtms re-derived; no API call |
| atm_card (any row) | open_atm_directions | geo: URI (Android) / maps:// URL (iOS) via gps-expect-actual → exits to native Maps app |
| retry_button | retry_load | Resets filterState.default + re-issues GET /atms to HSBC Open Data (unauthenticated, 15s timeout) |

---

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| top_app_bar | match_parent (393dp) | 64dp | 0 |
| location_search | match_parent − 32dp (361dp) | 56dp | 28dp (filled pill variant) |
| progress_indicator linear | match_parent (393dp) | 4dp | 0 |
| service_filters chip_group | match_parent, h-scroll | 40dp | 0 (container) |
| filter chip (24h / Wheelchair / Cash deposit) | wrap_content min 48dp | 32dp | 9999dp (full pill) |
| result_count text | match_parent − 32dp | 20dp | 0 |
| atm_list container | match_parent − 32dp | fill + scroll | 0 |
| atm_card | match_parent − 32dp (361dp) | ~112–128dp (content-driven) | 12dp (radius.medium) |
| atm_service_chips chip_group | match_parent, h-scroll | 28dp | 0 (container) |
| chip_hours / chip_wheelchair / chip_deposit | wrap_content | 28dp | 9999dp (full pill) |
| empty_state icon (location_off / error_outline) | 48dp | 48dp | 0 |
| retry_button | ~160dp (centred) | 40dp (touch target 48dp) | 9999dp (full pill) |
| bottom_nav | match_parent (393dp) | 80dp | 0 |
