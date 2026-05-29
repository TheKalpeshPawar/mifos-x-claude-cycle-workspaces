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

The ATM & Branch Locator screen enables Consumer persona users to find nearby Mifos ATMs and branches using GPS or manual address search. A 240dp map area renders pin locations when location permission is granted; below it a horizontally-scrollable filter chip row narrows results to ATMs only, Branches only, or 24/7 locations. A dynamic results header reports the current count ("3 ATMs found within 500m") and scrollable result cards each display name, distance, opening hours, withdrawal limit, and a "Get Directions" link that opens the native maps app. A location permission banner prompts users who have not yet granted location access.

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

| ID                         | Type  | Description                                                                                                    |
|----------------------------|-------|----------------------------------------------------------------------------------------------------------------|
| atm_locator_title          | text  | "ATM & Branches" — headline_large, #4C662B, 24dp padding top, role heading h1                                  |
| location_search_input      | input | Search field (pill radius 28, #F9FAEF bg) — placeholder "Enter city, postcode or address...", leading search icon |
| location_permission_banner | box   | #DCE7C8 bg, 1px #4C662B border, radius 8 — shown only when location_not_granted                               |
| enable_location_button     | button| "Enable" — text variant, #4C662B; triggers request_location_permission                                        |
| atm_map_area               | image | 240dp tall map area (#E1E4D5 bg placeholder), radius 12; renders ATM pins in content state                     |
| filter_chips_row           | stack | Horizontal scrollable chip row (h-scroll, 8dp spacing, 16dp horizontal padding)                               |
| filter_all                 | input | "All" chip — selected by default (#4C662B fill, #FFFFFF text), radius 16                                       |
| filter_atms                | input | "ATMs" chip — radio chip, radius 16; filters to ATM type only                                                  |
| filter_branches            | input | "Branches" chip — radio chip, radius 16; filters to branch type only                                           |
| filter_24_7                | input | "24/7" chip — radio chip, radius 16; filters to 24/7 locations only                                           |
| nearby_results_header      | text  | "3 ATMs found within 500m" — title_medium, #1A1C16, role heading h2; count updates on filter change           |
| atm_result_oxford_street   | box   | White card (radius 12, elevation 2, 16dp padding) for Mifos ATM Oxford Street                                  |
| atm_oxford_name            | text  | "Mifos ATM — Oxford Street" — title_small, #1A1C16, weight 600                                                |
| atm_oxford_distance        | text  | "0.2km away" — body_small, #44483D                                                                            |
| atm_oxford_hours           | text  | "Open 24/7" — body_small, #4C662B, weight 500                                                                 |
| atm_oxford_limit           | text  | "£300 max withdrawal" — body_small, #44483D                                                                   |
| atm_oxford_directions      | link  | "Get Directions" — label_medium, #4C662B, trailing directions icon; opens native maps                          |
| atm_result_bond_street     | box   | White card (radius 12, elevation 2) for Mifos ATM Bond Street Station                                          |
| atm_bond_name              | text  | "Mifos ATM — Bond Street Station" — title_small, #1A1C16, weight 600                                          |
| atm_bond_distance          | text  | "0.5km away" — body_small, #44483D                                                                            |
| atm_bond_hours             | text  | "Open 24/7" — body_small, #4C662B, weight 500                                                                 |
| atm_bond_directions        | link  | "Get Directions" — label_medium, #4C662B; opens native maps                                                   |
| atm_result_mayfair_branch  | box   | White card (radius 12, elevation 2) for Mifos Branch Mayfair                                                   |
| branch_mayfair_name        | text  | "Mifos Branch — Mayfair" — title_small, #1A1C16, weight 600                                                   |
| branch_mayfair_distance    | text  | "0.8km away" — body_small, #44483D                                                                            |
| branch_mayfair_hours       | text  | "Mon–Fri 9am–5pm" — body_small, #44483D, weight 500                                                           |
| branch_mayfair_services    | text  | "Services: Cashier · FX · Safe Deposit" — body_small, #44483D                                                 |
| branch_mayfair_directions  | link  | "Get Directions" — label_medium, #4C662B; opens native maps                                                   |
| results_divider            | divider| Horizontal rule, #E1E4D5, 16dp horizontal margin                                                             |

---

## States

| ID              | Trigger                                       | Description                                                                                        |
|-----------------|-----------------------------------------------|----------------------------------------------------------------------------------------------------|
| loading         | Screen entry / API calls in flight            | Title, search, filter chips visible; map area and all result cards shown as skeleton shimmer blocks |
| content         | Location + API data available                 | Map renders, result count header active, all 3 result cards visible with full details               |
| error           | Network or API failure                        | Title and search input only; map and result cards hidden; error message shown with retry             |
| empty           | Search returns no results for current filter  | Title, search, filter chips; empty message "No ATMs or branches found in this area"                |
| location_denied | Location permission not granted               | Permission banner + Enable button shown; map area hidden; manual search still active                |

---

## State Model

**ViewModel:** `AtmLocatorViewModel`
**Screen State Type:** `AtmLocatorUiState`

| Name                      | Type              | Default          |
|---------------------------|-------------------|------------------|
| atmList                   | List\<AtmLocation\> | emptyList()    |
| searchQuery               | String            | ""               |
| selectedFilter            | AtmFilter         | AtmFilter.ALL    |
| userLocation              | LatLng?           | null             |
| locationPermissionGranted | Boolean           | false            |
| isLoading                 | Boolean           | true             |
| resultCount               | Int               | 0                |
| networkError              | String?           | null             |
| locationError             | String?           | null             |

**Events:** `SearchLocationEvent`, `FilterChangedEvent`, `RequestLocationPermissionEvent`, `AtmSelectedEvent`, `DirectionsRequestedEvent`

**Actions:** `search_location()`, `filter_type()`, `request_location_permission()`, `view_atm_detail()`, `open_directions()`

**DI Dependencies:** `AtmRepository`, `LocationService`, `NavigationService`

**Errors:**
- `networkError`: "Unable to load ATMs. Check your connection and try again."
- `locationError`: "Location unavailable. Use the search box to find ATMs manually."

---

## Navigation

| From             | To               | Trigger                          | Type             |
|------------------|------------------|----------------------------------|------------------|
| atm-locator      | (native maps)    | Any Get Directions link tap      | external intent  |
| bottom nav       | home             | nav_home tab tap                 | tab              |
| bottom nav       | accounts         | nav_accounts tab tap             | tab              |
| bottom nav       | send-money       | nav_pay tab tap                  | tab              |
| bottom nav       | cards            | nav_cards tab tap                | tab              |
| bottom nav       | settings         | nav_more tab tap                 | tab              |

---

## API Endpoints

| Endpoint                                     | Auth        | Tag    | Purpose                                                    |
|----------------------------------------------|-------------|--------|------------------------------------------------------------|
| GET /obp/v5.1.0/banks/{bankId}/atms          | DirectLogin | ATM    | Fetch nearby ATMs by latitude/longitude; limit 10          |
| GET /obp/v5.1.0/banks/{bankId}/branches      | DirectLogin | Branch | Fetch nearby branches by latitude/longitude                |

---

## Design Tokens

| Token                           | Value     | Usage                                                           |
|---------------------------------|-----------|-----------------------------------------------------------------|
| colors.light.primary            | #4C662B   | Title color, selected chip fill, "Open 24/7" text, direction links, Enable button |
| colors.light.on_primary         | #FFFFFF   | Selected chip label text                                        |
| colors.light.nav_active_indicator | #DCE7C8 | Location permission banner background                          |
| colors.light.surface            | #FFFFFF   | ATM and branch result cards                                     |
| colors.light.surface_variant    | #E1E4D5   | Map placeholder background, divider, unselected chip border     |
| colors.light.on_surface         | #1A1C16   | ATM and branch name text                                        |
| colors.light.on_surface_variant | #44483D   | Distance, non-24/7 hours, services text                        |
| colors.light.background         | #F9FAEF   | Screen background, search input background                      |
| colors.light.outline_variant    | #C5C8BA   | Result card borders                                             |
| typography.headline_large       | 32sp/400  | Screen title "ATM & Branches"                                   |
| typography.title_medium         | 16sp/500  | Results count header                                            |
| typography.title_small          | 14sp/500  | ATM and branch name in result cards                             |
| typography.body_small           | 12sp/400  | Distance, hours, limit, services text                           |
| typography.label_medium         | 12sp/500  | "Get Directions" link, "Enable" button                          |
| radius.pill                     | 999dp     | Filter chip radius (radius 16dp in YAML — pill-style)           |
| radius.md                       | 12dp      | Result card corners, map area corners                           |
| elevation.level2                | 3dp       | Result card elevation                                           |

---

_Generated by /idea export | 2026-05-29_
