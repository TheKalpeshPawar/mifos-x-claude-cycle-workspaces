# SPEC — Find Customer

| Field         | Value                       |
|---------------|-----------------------------|
| Feature       | customer-search             |
| Flavor        | fieldOfficer                |
| Status        | approved                    |
| Quality Score | 97                          |
| ViewModel     | CustomerSearchViewModel     |

---

## Overview

Find Customer is the primary customer discovery screen for Field Officers. It provides a text search bar supporting name, ID, phone, and email queries, status filter chips (All / Active / Prospect / Dormant), a QR code scanner shortcut for instant ID lookup, and a real-time results list showing customer cards with avatar initials, KYC status badge, account summary, and last interaction timestamp. It also surfaces entry points for Onboard New Customer (individual) and Onboard Business Customer (corporate). The screen transitions through six states: loading (skeleton list) → idle (search prompt, no results) → searching (skeleton overlay) → results (populated cards) → no_results (empty state with try-different CTA) → error (banner + retry). Customer rows use the OBP v5.1.0 customers endpoint; phone-number lookup uses the OBP v4.0.0 mobile phone search endpoint. Demo data includes Kenyan customers with full KYC fields. The screen belongs to the field-officer flow and feeds into customer-detail, customer-onboarding, and corporate-onboarding.

---

## Screens

| ID                    | Name          | Route             | Layout | Scroll   |
|-----------------------|---------------|-------------------|--------|----------|
| customer_search_main  | Find Customer | /customer-search  | Column | Vertical |

**Shell:** Field Officer bottom navigation bar (Customers tab active). Mobile only, baseline width 390dp.

---

## Components

| ID                              | Type   | Description                                                                                              |
|---------------------------------|--------|----------------------------------------------------------------------------------------------------------|
| customer_search_title           | text   | "Find Customer" — Outfit/headline_large, #4C662B, 24dp top / 16dp horizontal padding, font-weight 700, a11y heading level 1 |
| customer_search_input           | input  | Search searchbox — variant:search, placeholder "Search by name, ID, phone or email...", #F9FAEF bg, 28dp radius, leading search icon, trailing clear icon, 16dp H / 12dp V padding, 12dp top margin, 16dp H margin, a11y hint "Enter at least 2 characters to start searching" |
| filter_chips_row                | stack  | Horizontal scrollable chip row — 8dp spacing, 16dp H padding, 12dp top, 4dp bottom, a11y group "Filter customers by status" |
| filter_all                      | input  | "All" — radio chip, default selected (#4C662B bg / #FFFFFF text), 16dp radius, 16dp H / 8dp V padding   |
| filter_active                   | input  | "Active" — radio chip, unselected, 16dp radius, 16dp H / 8dp V padding                                  |
| filter_prospect                 | input  | "Prospect" — radio chip, unselected, 16dp radius, 16dp H / 8dp V padding                                |
| filter_dormant                  | input  | "Dormant" — radio chip, unselected, 16dp radius, 16dp H / 8dp V padding                                 |
| scan_qr_button                  | button | "Scan Customer ID" — outlined, #4C662B border+text, 12dp radius, qr_code leading icon, align_self flex_start, 16dp H / 10dp V padding, 16dp H margin, 8dp V margin |
| customer_result_john_mwangi     | box    | Customer card — #FFFFFF bg, 12dp radius, 2dp elevation, 14dp padding, 16dp H margin, 8dp bottom margin, row + center-aligned, taps → customer-detail; loading:skeleton×3, error:banner with retry, empty:box with person_search icon |
| avatar_john                     | box    | "JM" initials circle — 44dp, #4C662B bg, #FFFFFF text, Outfit/title_small 700, 12dp right margin        |
| customer_john_name              | text   | "John Mwangi" — Outfit/title_small, #1A1C16, font-weight 600                                            |
| customer_john_kyc_status        | text   | "KYC Verified ✓" — Outfit/body_small, #4C662B, font-weight 500                                         |
| customer_john_account           | text   | "Checking Account · KES 45,200" — Outfit/body_small, #44483D                                            |
| customer_john_last_interaction  | text   | "3 days ago" — Outfit/body_small, #44483D, align_self flex_start                                        |
| customer_result_sarah_odhiambo  | box    | Customer card — same shell as john card; taps → customer-detail; same component_states                  |
| avatar_sarah                    | box    | "SO" initials circle — 44dp, #E8A317 bg, #FFFFFF text, Outfit/title_small 700, 12dp right margin        |
| customer_sarah_name             | text   | "Sarah Odhiambo" — Outfit/title_small, #1A1C16, font-weight 600                                         |
| customer_sarah_kyc_status       | text   | "KYC Pending ⚠" — Outfit/body_small, #44483D, font-weight 500 (a11y fix: was #E8A317 ≤2.17:1; #44483D ≥7.25:1) |
| customer_sarah_account          | text   | "Application in Review" — Outfit/body_small, #44483D                                                    |
| customer_sarah_last_interaction | text   | "7 days ago" — Outfit/body_small, #44483D, align_self flex_start                                        |
| customer_result_peter_kamau     | box    | Customer card — same shell as john card; taps → customer-detail; same component_states                   |
| avatar_peter                    | box    | "PK" initials circle — 44dp, #386663 bg, #FFFFFF text, Outfit/title_small 700, 12dp right margin        |
| customer_peter_name             | text   | "Peter Kamau" — Outfit/title_small, #1A1C16, font-weight 600                                            |
| customer_peter_kyc_status       | text   | "New Prospect" — Outfit/body_small, #386663, font-weight 500                                            |
| customer_peter_account          | text   | "No account yet" — Outfit/body_small, #44483D                                                           |
| customer_peter_last_interaction | text   | "Today" — Outfit/body_small, #4C662B, font-weight 500 (highlighted)                                     |
| onboard_new_customer_button     | button | "Onboard New Customer" — filled, #4C662B bg / #FFFFFF text, 12dp radius, full-width, person_add leading icon, Outfit/label_large, 14dp V padding, 16dp H margin, 8dp top margin, 24dp bottom margin; taps → customer-onboarding |
| onboard_corporate_button        | button | "Onboard Business Customer" — outlined, #386663 border+text, 8dp radius, full-width, business leading icon, Outfit/label_large; taps → corporate-onboarding |
| empty_state_box                 | box    | #F9FAEF bg, 12dp radius, 32dp padding, 16dp H margin, 16dp top margin, center-aligned; visible when no_results |
| empty_state_message             | text   | "No customers found for this search" — Outfit/body_large, #44483D, center, 16dp bottom padding          |
| try_different_search_button     | button | "Try Different Search" — outlined, #4C662B border+text, 8dp radius, 16dp H / 10dp V padding; taps → clear_search on customer_search_main |

---

## States

| ID          | Trigger                              | Description                                                                                                         |
|-------------|--------------------------------------|---------------------------------------------------------------------------------------------------------------------|
| loading     | Screen entry (initial API fetch)     | Title + search input visible; skeleton list of 5 customer-card-shaped rows (#E1E4D5, shimmer duration 200ms short4) |
| idle        | Initial load complete, no query      | Title + search + filter chips + QR button + onboard buttons; no result cards; no empty state                        |
| searching   | User typed ≥2 chars, API in flight   | Title + search + filter chips + QR button visible; 3 skeleton result cards in place; onboard buttons hidden         |
| results     | API returns ≥1 customer matches      | Full list of customer cards (John Mwangi, Sarah Odhiambo, Peter Kamau examples) + onboard buttons below             |
| no_results  | API returns 0 matches                | Empty-state box + message + "Try Different Search" button + onboard buttons; result cards and QR button hidden       |
| error       | Network/auth failure during search   | Title + search input; error message "Search failed. Check your connection and try again."; result cards hidden       |
| content     | Alias for idle (post-load default)   | Same layout as idle; onboard buttons always visible; no result cards                                                |
| empty       | Alias for no_results               | Empty-state layout identical to no_results                                                                          |

---

## State Model

**ViewModel:** `CustomerSearchViewModel`
**Screen State Type:** `CustomerSearchScreenState`

| Name           | Type              | Default                |
|----------------|-------------------|------------------------|
| searchQuery    | String            | `""`                   |
| selectedFilter | CustomerFilter    | `CustomerFilter.ALL`   |
| searchResults  | List\<Customer\>  | `emptyList()`          |
| isSearching    | Boolean           | `false`                |
| hasSearched    | Boolean           | `false`                |
| networkError   | String?           | `null`                 |
| searchError    | String?           | `null`                 |

**Events:** `SearchQueryChangedEvent`, `FilterSelectedEvent`, `ScanQrEvent`, `CustomerSelectedEvent`, `ClearSearchEvent`, `OnboardNewCustomerEvent`

**Actions:** `search`, `filter`, `scan_qr`, `navigate`, `clear_search`

**DI Dependencies:** `CustomerRepository`, `QrScannerService`, `NavigationService`

**Errors:**
- `networkError`: "Could not connect to banking services. Please try again."
- `searchError`: "Search failed. Check your connection and try again."

---

## Navigation

| From            | To                   | Trigger                             | Type |
|-----------------|----------------------|-------------------------------------|------|
| customer-search | customer-detail      | Customer card row tap               | push |
| customer-search | customer-onboarding  | onboard_new_customer_button tap     | push |
| customer-search | corporate-onboarding | onboard_corporate_button tap        | push |

---

## API Endpoints

| Endpoint                                                                          | Auth        | Tag      | Purpose                                            |
|-----------------------------------------------------------------------------------|-------------|----------|----------------------------------------------------|
| GET /obp/v5.1.0/banks/{bankId}/customers                                         | DirectLogin | Customers | Search customers by name, ID, status               |
| POST /obp/v4.0.0/banks/{bankId}/search/customers/mobile-phone-number             | DirectLogin | Customer  | Search customer by mobile phone number             |

---

## Design Tokens

| Token                             | Value    | Usage                                                                          |
|-----------------------------------|----------|--------------------------------------------------------------------------------|
| colors.light.primary              | #4C662B  | Screen title, KYC Verified badge text, "Today" timestamp, selected chip bg, QR + onboard button border+text, search icon |
| colors.light.on_primary           | #FFFFFF  | Selected chip text, avatar initials, onboard_new_customer_button text          |
| colors.light.secondary            | #386663  | avatar_peter bg, onboard_corporate_button border+text, prospect status text    |
| colors.light.background           | #F9FAEF  | Screen base, search input background, empty-state box background               |
| colors.light.surface              | #FFFFFF  | Customer result card background                                                |
| colors.light.on_surface           | #1A1C16  | Customer name text (title_small)                                               |
| colors.light.on_surface_variant   | #44483D  | Account info text, last interaction text, KYC Pending text (a11y-corrected from #E8A317) |
| colors.light.pending              | #E8A317  | avatar_sarah background (amber, avatar only — not used for text per a11y fix)  |
| typography.headline_large         | Outfit 32sp/700 | Screen title "Find Customer"                                             |
| typography.title_small            | Outfit 14sp/500 | Customer names, avatar initials                                          |
| typography.body_small             | Outfit 12sp/400 | KYC status, account info, last interaction, chip labels                  |
| typography.label_large            | Outfit 14sp/500 | Onboard button labels                                                    |
| radius.pill (28dp)                | 28dp     | Search input border radius                                                     |
| radius.lg (16dp)                  | 16dp     | Filter chip border radius                                                      |
| radius.md (12dp)                  | 12dp     | Customer result cards, QR button, onboard_new_customer_button                  |
| radius.sm (8dp)                   | 8dp      | onboard_corporate_button, try_different_search_button, empty_state_box         |
| elevation.level2                  | 3dp      | Customer result cards (specified 2dp in source)                                |
| motion.duration.short4            | 200ms    | Skeleton shimmer duration for loading state                                    |
| touchTargets.min_touch_target     | 48dp     | All interactive elements (chips, buttons, card rows)                           |
| spacing.md (16dp)                 | 16dp     | Horizontal content padding                                                     |
| spacing.lg (24dp)                 | 24dp     | Screen title top padding, bottom margin on onboard button                      |

---

_Generated by /idea export | 2026-05-30_
