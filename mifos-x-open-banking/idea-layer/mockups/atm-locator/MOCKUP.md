# Visual Specification — ATM & Branch Locator

| Field | Value |
|---|---|
| Feature | atm-locator |
| Flavor | consumer |
| Archetype | index_list |

---

## Screen Layout

Top-to-bottom hierarchy on a scrollable column (background #FCF8FF):

1. **Page title** — "ATM & Branches" headline_large, #1800B1, padding top 24, horizontal 16
2. **Location search input** — Pill-shaped search field (radius 28, background #F5F5F5), leading search icon, placeholder "Enter city, postcode or address...", margin horizontal 16, top 12
3. **Location permission banner** *(location_denied state only)* — Blue-bordered box (#1800B1 border, #E8F4FD background), "Use my location for nearby ATMs" text with "Enable" text button
4. **Map area** — 240dp tall rounded map (radius 12) displaying ATM/branch pins, margin horizontal 16, top 12
5. **Filter chips row** — Horizontal scrollable row of radio chips: "All" (selected, filled #1800B1), "ATMs", "Branches", "24/7", padding horizontal 16, vertical 12
6. **Results header** — "3 ATMs found within 500m" title_medium, #212121
7. **Result cards** — Three elevated cards (elevation 2, radius 12, padding 16, margin horizontal 16, bottom 8):
   - Mifos ATM Oxford Street (0.2km, Open 24/7, £300 max withdrawal)
   - Mifos ATM Bond Street Station (0.5km, Open 24/7)
   - Mifos Branch Mayfair (0.8km, Mon–Fri 9am–5pm, Services: Cashier · FX · Safe Deposit)
8. **Divider** — #E0E0E0, margin horizontal 16

---

## Components

### Location Search Input
- **Position:** Directly below page title
- **Style:** Radius 28, background #F5F5F5, leading "search" icon, padding horizontal 16 vertical 12
- **Interaction:** Tap opens text entry; triggers location search on text change

### Filter Chips Row
- **Position:** Below map area, horizontal scrollable
- **Style:** Chips with radius 16, padding horizontal 16 vertical 8; selected chip fills #1800B1 with white text; unselected chips use border-only style
- **Default selected:** "All" chip

### ATM Result Card — Oxford Street
- **Background:** #FFFFFF, radius 12, elevation 2, padding 16
- **Name:** "Mifos ATM — Oxford Street" title_small, weight 600, #212121
- **Distance:** "0.2km away" body_small, #757575
- **Hours:** "Open 24/7" body_small, #4CAF50 (green), weight 500
- **Limit:** "£300 max withdrawal" body_small, #616161
- **Directions link:** "Get Directions" label_medium, #1800B1, trailing directions icon

### ATM Result Card — Bond Street Station
- **Background:** #FFFFFF, radius 12, elevation 2, padding 16
- **Name:** "Mifos ATM — Bond Street Station" title_small, weight 600, #212121
- **Distance:** "0.5km away" body_small, #757575
- **Hours:** "Open 24/7" body_small, #4CAF50 (green)
- **Directions link:** "Get Directions" label_medium, #1800B1

### Branch Result Card — Mayfair
- **Background:** #FFFFFF, radius 12, elevation 2, padding 16
- **Name:** "Mifos Branch — Mayfair" title_small, weight 600, #212121
- **Distance:** "0.8km away" body_small, #757575
- **Hours:** "Mon–Fri 9am–5pm" body_small, #FF8F00 (amber), weight 500
- **Services:** "Services: Cashier · FX · Safe Deposit" body_small, #616161
- **Directions link:** "Get Directions" label_medium, #1800B1

---

## Interaction Patterns

| Target | Gesture | Result |
|---|---|---|
| location_search_input | Tap | Keyboard opens, user types city/postcode; live search triggers |
| enable_location_button | Tap | OS location permission dialog appears |
| filter_all / filter_atms / filter_branches / filter_24_7 | Tap | Filter applied; result count header and visible cards update |
| atm_result_oxford_street / bond_street / mayfair_branch | Tap | ATM detail view pushed (view_atm_detail action) |
| atm_oxford_directions / bond_directions / branch_directions | Tap | Native maps app opens with destination pre-filled |

---

## Content Data

| Element | Sample Value |
|---|---|
| Result count header | 3 ATMs found within 500m |
| ATM 1 name | Mifos ATM — Oxford Street |
| ATM 1 distance | 0.2km away |
| ATM 1 hours | Open 24/7 |
| ATM 1 limit | £300 max withdrawal |
| ATM 2 name | Mifos ATM — Bond Street Station |
| ATM 2 distance | 0.5km away |
| ATM 2 hours | Open 24/7 |
| Branch 1 name | Mifos Branch — Mayfair |
| Branch 1 distance | 0.8km away |
| Branch 1 hours | Mon–Fri 9am–5pm |
| Branch 1 services | Cashier · FX · Safe Deposit |

---

## Design Notes

**Color Usage:**
- Primary #1800B1 used for title, selected filter chip, "Enable" banner button, and all "Get Directions" links
- Green #4CAF50 signals 24/7 availability — instantly communicates "always open"
- Amber #FF8F00 for limited-hours branches distinguishes them from always-open ATMs without using error red

**Typography:**
- Page title: headline_large — consistent with app's screen identity pattern
- Result card names: title_small weight 600 — prominent but contained within the card hierarchy
- Distance and hours: body_small — secondary metadata that doesn't compete with the name

**Map Area:**
- 240dp fixed height prevents the map from dominating the screen; scrollable result list gives access to more results below
- Radius 12 matches the result card radius, creating a cohesive visual family

**Accessibility:**
- Result cards are full-width tappable targets with aria listitem role
- "Get Directions" links have explicit role="link" and describe the full destination in the a11y label
- Location permission banner reads out the full request context for screen readers
- Filter chips use role="radio" with clear group label "Filter ATMs and branches by type"

*Generated by /idea export | 2026-05-25*
