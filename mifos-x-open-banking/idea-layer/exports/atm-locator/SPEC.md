# SPEC — ATM & Branch Locator

| Field         | Value                  |
|---------------|------------------------|
| Feature       | atm-locator            |
| Flavor        | consumer               |
| Status        | approved               |
| Quality Score | 93                     |
| ViewModel     | AtmLocatorViewModel    |

---

## Overview

The ATM & Branch Locator is a consumer utility screen that lets Mifos X Open Banking users find nearby ATMs and branches. At the top, the headline "ATM & Branches" (headline_large, #4C662B) anchors the screen with 24dp top padding. A pill-shaped search input (#F9FAEF background, 28dp radius, leading search icon) accepts a city, postcode, or address, triggering the `search_location` action. When location permission has not been granted, a teal-bordered banner (#DCE7C8 fill, #4C662B 1dp border) appears below the search bar with an inline "Enable" text button that requests the system permission. A 240dp map tile (12dp radius, #E1E4D5 placeholder) renders geographic context in content state. Below the map, a horizontally-scrollable chip row provides four filter modes: "All" (selected by default — #4C662B fill/#FFFFFF text), "ATMs", "Branches", and "24/7". A reactive results header ("3 ATMs found within 500m") precedes up to three result cards (white, 12dp radius, 2dp elevation), each showing location name (title_small, #1A1C16, weight 600), distance (body_small, #44483D), hours/status, optional withdrawal limit or service list, and a "Get Directions" link (#4C662B, trailing directions icon) that opens the native maps app. API data comes from OBP v5.1.0 ATM and Branch endpoints keyed by the user's latitude/longitude; demo data covers 4 ATMs and 3 branches across Nairobi, Kenya (KCB Westlands, Equity CBD, Co-op Karen, NCBA Mombasa Road). An a11y colour fix is applied to branch hours: was #E8A317 (2.17:1 contrast ratio, WCAG fail) — corrected to #44483D (8.91:1, WCAG AA pass).

---

## Screens

| ID               | Name                   | Route        | Layout | Scroll   |
|------------------|------------------------|--------------|--------|----------|
| atm_locator_main | ATM & Branch Locator   | /atm-locator | Column | Vertical |

**Shell:** Bottom navigation bar visible (consumer app-shell, Home/Accounts/Pay/Cards/More).

| Nav Item | ID           | Icon              | Target     |
|----------|--------------|-------------------|------------|
| Home     | nav_home     | home              | home       |
| Accounts | nav_accounts | account_balance   | accounts   |
| Pay      | nav_pay      | send              | send-money |
| Cards    | nav_cards    | credit_card       | cards      |
| More     | nav_more     | more_horiz        | settings   |

---

## Components

| ID                         | Type    | Description                                                                                                              |
|----------------------------|---------|--------------------------------------------------------------------------------------------------------------------------|
| atm_locator_title          | text    | "ATM & Branches" — headline_large (32sp/400), #4C662B, 24dp top padding, 16dp h-padding; a11y heading h1               |
| location_search_input      | input   | Search variant, 28dp radius pill, #F9FAEF bg, leading search icon; placeholder "Enter city, postcode or address…"; triggers `search_location` |
| location_permission_banner | box     | #DCE7C8 fill, 1dp #4C662B border, 8dp radius, 12dp padding, row layout; conditional on `location_not_granted`          |
| enable_location_button     | button  | "Enable" — text variant, #4C662B, label_medium, 8dp h-padding; triggers `request_location_permission`                  |
| atm_map_area               | image   | 240dp height, #E1E4D5 placeholder bg, 12dp radius, cover fit; skeleton during loading; a11y img "ATM map showing nearby locations" |
| filter_chips_row           | stack   | Horizontal scroll, 8dp item spacing, 16dp h-padding, 12dp v-padding; wraps 4 filter chips                              |
| filter_all                 | input   | Radio chip "All"; default selected — #4C662B fill/#FFFFFF text; 16dp radius, 16dp h-pad, 8dp v-pad                     |
| filter_atms                | input   | Radio chip "ATMs"; unselected style; triggers `filter_type` action with value `atm`                                     |
| filter_branches            | input   | Radio chip "Branches"; triggers `filter_type` with value `branch`                                                       |
| filter_24_7                | input   | Radio chip "24/7"; triggers `filter_type` with value `24_7`                                                             |
| nearby_results_header      | text    | "3 ATMs found within 500m" — title_medium (16sp/500), #1A1C16, 16dp h-pad, 8dp top pad; updates reactively on filter; h2 |
| atm_result_oxford_street   | box     | Result card: #FFFFFF fill, 12dp radius, 2dp elevation, 16dp padding, 16dp h-margin, 8dp bottom margin; tappable → `view_atm_detail` |
| atm_oxford_name            | text    | "Mifos ATM — Oxford Street" — title_small (14sp/500), #1A1C16, weight 600                                              |
| atm_oxford_distance        | text    | "0.2km away" — body_small (12sp/400), #44483D                                                                           |
| atm_oxford_hours           | text    | "Open 24/7" — body_small, #4C662B, weight 500                                                                           |
| atm_oxford_limit           | text    | "£300 max withdrawal" — body_small, #44483D                                                                              |
| atm_oxford_directions      | link    | "Get Directions" — label_medium, #4C662B, trailing directions icon; triggers `open_directions`                           |
| atm_result_bond_street     | box     | Result card: same style; a11y label "Mifos ATM Bond Street Station, 0.5km, Open 24/7"                                  |
| atm_bond_name              | text    | "Mifos ATM — Bond Street Station" — title_small, #1A1C16, weight 600                                                   |
| atm_bond_distance          | text    | "0.5km away" — body_small, #44483D                                                                                      |
| atm_bond_hours             | text    | "Open 24/7" — body_small, #4C662B, weight 500                                                                           |
| atm_bond_directions        | link    | "Get Directions" — label_medium, #4C662B, trailing directions icon; triggers `open_directions`                           |
| atm_result_mayfair_branch  | box     | Result card: same style; a11y label "Mifos Branch Mayfair, 0.8km, Mon–Fri 9am–5pm"                                    |
| branch_mayfair_name        | text    | "Mifos Branch — Mayfair" — title_small, #1A1C16, weight 600                                                            |
| branch_mayfair_distance    | text    | "0.8km away" — body_small, #44483D                                                                                      |
| branch_mayfair_hours       | text    | "Mon–Fri 9am–5pm" — body_small, **#44483D**, weight 500 (**a11y fix A11Y-002**: was #E8A317 at 2.17:1 contrast, WCAG fail → #44483D at 8.91:1, WCAG AA pass) |
| branch_mayfair_services    | text    | "Services: Cashier · FX · Safe Deposit" — body_small, #44483D                                                          |
| branch_mayfair_directions  | link    | "Get Directions" — label_medium, #4C662B, trailing directions icon; triggers `open_directions`                           |
| results_divider            | divider | Horizontal separator, #E1E4D5, 16dp h-margin                                                                            |

---

## States

| ID              | Trigger                                           | Description                                                                                                  |
|-----------------|---------------------------------------------------|--------------------------------------------------------------------------------------------------------------|
| loading         | Screen entry / API calls in flight                | Title + search input + filter chips visible; map area and all 3 result cards shown as skeleton shimmer (short4 = 200ms, reduced-motion: static placeholder); permission banner hidden |
| content         | Location + OBP API data available                 | Full layout: map tile renders, results count header active, 3 result cards with name/distance/hours/limit/directions; permission banner hidden |
| error           | Network failure or OBP 401/500 response           | Title + search visible; map, results header, result cards all hidden; inline error "Unable to load ATMs. Check your connection and try again." |
| empty           | Search/filter returns zero results                | Title + search + filter chips visible; map, results header, result cards hidden; "No ATMs or branches found in this area" |
| location_denied | Location permission not granted by OS             | Title + search + permission banner + Enable button + filter chips shown; map tile hidden; manual search active |

---

## State Model

**ViewModel:** `AtmLocatorViewModel`
**Screen State Type:** `AtmLocatorUiState`

| Name                      | Type                 | Default          |
|---------------------------|----------------------|------------------|
| atmList                   | List\<AtmLocation\>  | emptyList()      |
| searchQuery               | String               | ""               |
| selectedFilter            | AtmFilter            | AtmFilter.ALL    |
| userLocation              | LatLng?              | null             |
| locationPermissionGranted | Boolean              | false            |
| isLoading                 | Boolean              | true             |
| resultCount               | Int                  | 0                |
| networkError              | String?              | null             |
| locationError             | String?              | null             |

**Events:** `SearchLocationEvent`, `FilterChangedEvent`, `RequestLocationPermissionEvent`, `AtmSelectedEvent`, `DirectionsRequestedEvent`

**Actions:** `search_location()`, `filter_type(value: AtmFilter)`, `request_location_permission()`, `view_atm_detail(id: String)`, `open_directions(lat: Double, lng: Double, label: String)`

**DI Dependencies:** `AtmRepository`, `LocationService`, `NavigationService`

**Errors:**
- `networkError`: "Unable to load ATMs. Check your connection and try again."
- `locationError`: "Location unavailable. Use the search box to find ATMs manually."

---

## Navigation

| From             | To             | Trigger                     | Type            |
|------------------|----------------|-----------------------------|-----------------|
| atm-locator      | (native maps)  | Any "Get Directions" link   | external intent |
| bottom nav       | home           | nav_home tab tap            | tab             |
| bottom nav       | accounts       | nav_accounts tab tap        | tab             |
| bottom nav       | send-money     | nav_pay tab tap             | tab             |
| bottom nav       | cards          | nav_cards tab tap           | tab             |
| bottom nav       | settings       | nav_more tab tap            | tab             |

---

## API Endpoints

| Endpoint                                | Auth        | Tag    | Purpose                                         |
|-----------------------------------------|-------------|--------|-------------------------------------------------|
| GET /obp/v5.1.0/banks/{bankId}/atms     | DirectLogin | ATM    | Fetch nearby ATMs by latitude/longitude; limit 10 |
| GET /obp/v5.1.0/banks/{bankId}/branches | DirectLogin | Branch | Fetch nearby branches by latitude/longitude     |

---

## Design Tokens

| Token                             | Value      | Usage                                                                              |
|-----------------------------------|------------|------------------------------------------------------------------------------------|
| colors.light.primary              | #4C662B    | Screen title, selected filter chip fill, "Open 24/7" hours text, direction links, "Enable" button |
| colors.light.on_primary           | #FFFFFF    | Selected filter chip label text                                                    |
| colors.light.nav_active_indicator | #DCE7C8    | Location permission banner background fill                                         |
| colors.light.surface              | #FFFFFF    | ATM and branch result card fill                                                    |
| colors.light.surface_variant      | #E1E4D5    | Map placeholder background, divider, unselected chip border                        |
| colors.light.on_surface           | #1A1C16    | ATM/branch name text, results count header                                         |
| colors.light.on_surface_variant   | #44483D    | Distance text, branch hours (a11y-corrected), services text                        |
| colors.light.background           | #F9FAEF    | Screen background, search input background                                         |
| colors.light.outline              | #4C662B    | Permission banner border                                                            |
| typography.headline_large         | Outfit 32sp/400  | Screen title "ATM & Branches"                                               |
| typography.title_medium           | Outfit 16sp/500  | Results count header                                                         |
| typography.title_small            | Outfit 14sp/500  | ATM/branch name per result card                                              |
| typography.body_small             | Outfit 12sp/400  | Distance, hours, withdrawal limit, services                                  |
| typography.label_medium           | Outfit 12sp/500  | "Get Directions" links, "Enable" button                                      |
| radius.md                         | 12dp       | Result card corners, map area corners                                              |
| radius.pill                       | 999dp      | Search input (28dp in source ≈ pill), filter chips (16dp in source)                |
| elevation.level2                  | 3dp        | Result card elevation (2dp specified in source — nearest M3 level is level2)       |
| motion.duration.short4            | 200ms      | Loading skeleton shimmer duration                                                  |
| touchTargets.min_touch_target     | 48dp       | Filter chips, direction links, Enable button                                       |

---

_Generated by /idea export | 2026-05-30_
