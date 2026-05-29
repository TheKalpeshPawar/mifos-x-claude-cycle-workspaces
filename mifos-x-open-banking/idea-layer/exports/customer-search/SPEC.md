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

Find Customer is the primary customer discovery screen for Field Officers. It provides a text search bar supporting name, ID, phone, and email queries, status filter chips (All / Active / Prospect / Dormant), a QR code scanner shortcut for instant ID lookup, and a real-time results list showing customer cards with avatar, KYC status, account info, and last interaction timestamp. It also surfaces primary entry points for Onboard New Customer and Onboard Business Customer. The screen transitions through idle → searching (skeleton cards) → results (populated cards) → no_results (empty state with try-different CTA) → error (banner + retry). Matching the Field Officer app shell, it is reachable via the Customers tab in the bottom navigation.

---

## Screens

| ID                  | Name          | Route            | Layout | Scroll   |
|---------------------|---------------|------------------|--------|----------|
| customer_search_main| Find Customer | /customer-search | Column | Vertical |

**Shell:** Field Officer bottom navigation bar (Customers tab active)

| Nav Item     | ID               | Icon         | Target               | Badge |
|--------------|------------------|--------------|----------------------|-------|
| Dashboard    | nav_dashboard    | dashboard    | fo-dashboard         | true  |
| Customers    | nav_customers    | people       | customer-search      | false |
| Applications | nav_applications | description  | account-applications | true  |
| Messages     | nav_messages     | mail         | customer-messages    | true  |
| More         | nav_more         | more_vert    | settings             | false |

---

## Components

| ID                          | Type   | Description                                                                                            |
|-----------------------------|--------|--------------------------------------------------------------------------------------------------------|
| customer_search_title       | text   | "Find Customer" — Outfit/headline_large, #4C662B, weight 700; pad T24/H16                             |
| customer_search_input       | input  | Pill search bar — radius 28, #F9FAEF bg, placeholder "Search by name, ID, phone or email…"; clear btn |
| filter_chips_row            | stack  | Horizontal scrollable row of 4 radio-chips — overflow_x scroll, pad H16/T12/B4                        |
| filter_all                  | input  | Filter chip "All" — selected: #4C662B bg, #FFFFFF text; radius 16, pad H16/V8                         |
| filter_active               | input  | Filter chip "Active" — unselected: outline, radius 16                                                  |
| filter_prospect             | input  | Filter chip "Prospect" — unselected                                                                    |
| filter_dormant              | input  | Filter chip "Dormant" — unselected                                                                     |
| scan_qr_button              | button | Outlined "Scan Customer ID", qr_code icon, #4C662B border+text, radius 12; margin H16/T8/B8           |
| customer_result_john_mwangi | box    | #FFFFFF card, radius 12, elevation 2, pad 14; row layout: JM avatar + name/status/account + last interaction |
| avatar_john                 | box    | 44×44 circle, #4C662B fill, "JM" Outfit/title_small #FFFFFF bold, margin R12                          |
| customer_john_name          | text   | "John Mwangi" — Outfit/title_small, #1A1C16, weight 600                                               |
| customer_john_kyc_status    | text   | "KYC Verified ✓" — Outfit/body_small, #4C662B, weight 500                                             |
| customer_john_account       | text   | "Checking Account · KES 45,200" — Outfit/body_small, #44483D                                          |
| customer_john_last_interaction | text| "3 days ago" — Outfit/body_small, #44483D                                                             |
| customer_result_sarah_odhiambo | box | #FFFFFF card, radius 12, elevation 2, pad 14; Sarah Odhiambo — KYC Pending, Application in Review    |
| avatar_sarah                | box    | 44×44 circle, #E8A317 fill, "SO" Outfit/title_small #FFFFFF bold                                      |
| customer_sarah_name         | text   | "Sarah Odhiambo" — Outfit/title_small, #1A1C16, weight 600                                            |
| customer_sarah_kyc_status   | text   | "KYC Pending ⚠" — Outfit/body_small, #44483D, weight 500 (a11y-corrected from amber)                 |
| customer_sarah_account      | text   | "Application in Review" — Outfit/body_small, #44483D                                                  |
| customer_sarah_last_interaction | text| "7 days ago" — Outfit/body_small, #44483D                                                            |
| customer_result_peter_kamau | box    | #FFFFFF card, radius 12, elevation 2, pad 14; Peter Kamau — New Prospect, no account                  |
| avatar_peter                | box    | 44×44 circle, #386663 fill, "PK" Outfit/title_small #FFFFFF bold                                      |
| customer_peter_name         | text   | "Peter Kamau" — Outfit/title_small, #1A1C16, weight 600                                               |
| customer_peter_kyc_status   | text   | "New Prospect" — Outfit/body_small, #386663, weight 500                                               |
| customer_peter_account      | text   | "No account yet" — Outfit/body_small, #44483D                                                         |
| customer_peter_last_interaction | text| "Today" — Outfit/body_small, #4C662B, weight 500                                                    |
| onboard_new_customer_button | button | Filled full-width "Onboard New Customer", person_add icon, #4C662B bg, #FFFFFF text; margin H16/T8/B24 |
| onboard_corporate_button    | button | Outlined "Onboard Business Customer", business icon, #386663 border+text; pad MD                      |
| empty_state_box             | box    | #F9FAEF bg, radius 12, pad 32, centered — shown when no search results                                 |
| empty_state_message         | text   | "No customers found for this search" — Outfit/body_large, #44483D, center, pad B16                    |
| try_different_search_button | button | Outlined "Try Different Search" — #4C662B border+text, radius 8                                       |

---

## States

| ID         | Trigger                              | Description                                                                                  |
|------------|--------------------------------------|----------------------------------------------------------------------------------------------|
| idle       | Screen entry (no query)              | Search input, filter chips, QR button, Onboard buttons; no results visible                   |
| searching  | Query entered (≥2 chars)             | Skeleton cards visible in place of results; filter chips remain; onboard buttons hidden       |
| results    | API response with data               | 3 customer cards rendered: John Mwangi, Sarah Odhiambo, Peter Kamau + onboard buttons        |
| no_results | API response empty list              | Empty state box + "No customers found" message + Try Different Search + onboard buttons      |
| error      | Network/API failure                  | Error banner "Search failed. Check your connection." — no results                            |
| content    | Alias for idle (pre-query state)     | Same as idle — search + filter + QR + onboard buttons; no results                            |
| empty      | Alias for no_results                 | Empty state shown with clear + onboard CTAs                                                  |

---

## State Model

**ViewModel:** `CustomerSearchViewModel`
**Screen State Type:** `CustomerSearchScreenState`

| Name          | Type              | Default               |
|---------------|-------------------|-----------------------|
| searchQuery   | String            | ""                    |
| selectedFilter| CustomerFilter    | CustomerFilter.ALL    |
| searchResults | List\<Customer\>  | emptyList()           |
| isSearching   | Boolean           | false                 |
| hasSearched   | Boolean           | false                 |
| networkError  | String?           | null                  |
| searchError   | String?           | null                  |

**Events:** `SearchQueryChangedEvent`, `FilterSelectedEvent`, `ScanQrEvent`, `CustomerSelectedEvent`, `ClearSearchEvent`, `OnboardNewCustomerEvent`

**Actions:** `search`, `filter`, `scan_qr`, `navigate`, `clear_search`

**DI Dependencies:** `CustomerRepository`, `QrScannerService`, `NavigationService`

**Errors:**
- `networkError`: "Search failed. Check your connection and try again."
- `searchError`: "Invalid search parameters."

---

## Navigation

| From            | To                  | Trigger                           | Type  |
|-----------------|---------------------|-----------------------------------|-------|
| customer-search | customer-detail     | Any customer card tap (navigate)  | push  |
| customer-search | customer-onboarding | onboard_new_customer_button tap   | push  |
| customer-search | corporate-onboarding| onboard_corporate_button tap      | push  |
| customer-search | fo-dashboard        | nav_dashboard bottom tab          | tab   |
| customer-search | account-applications| nav_applications bottom tab       | tab   |
| customer-search | customer-messages   | nav_messages bottom tab           | tab   |
| customer-search | settings            | nav_more bottom tab               | tab   |

---

## API Endpoints

| Endpoint                                                                   | Auth        | Tag      | Purpose                                      |
|----------------------------------------------------------------------------|-------------|----------|----------------------------------------------|
| GET /obp/v5.1.0/banks/{bankId}/customers                                   | DirectLogin | Customers| Search customers by name/ID/phone/email/status|
| POST /obp/v4.0.0/banks/{bankId}/search/customers/mobile-phone-number       | DirectLogin | Customer | Search customer by mobile phone number        |

---

## Design Tokens

| Token                          | Value   | Usage                                                              |
|--------------------------------|---------|--------------------------------------------------------------------|
| color.light.primary            | #4C662B | Title, chip active bg, John avatar, verified KYC text, today timestamp, onboard btn |
| color.light.secondary          | #386663 | Peter avatar, onboard corporate btn border+text                   |
| color.light.pending            | #E8A317 | Sarah Odhiambo avatar (KYC pending)                               |
| color.light.on_surface_variant | #44483D | Supporting text in cards — account, last interaction, KYC pending |
| color.light.on_surface         | #1A1C16 | Customer names                                                     |
| color.light.surface            | #FFFFFF | Customer result cards                                              |
| color.light.background         | #F9FAEF | Screen bg, search bar fill, empty state bg                        |
| typography.headline_large      | —       | "Find Customer" screen title                                       |
| typography.title_small         | —       | Customer name in card                                              |
| typography.body_small          | —       | KYC status, account info, timestamp                               |
| typography.label_large         | —       | Onboard button text                                               |
| radius.md                      | 12dp    | Customer cards, scan QR button                                    |
| radius.pill                    | 999dp   | Onboard New Customer button                                       |

---

_Generated by /idea export | 2026-05-29_
