# Feature Specification — Beneficiaries
**Feature:** beneficiaries | **Flavor:** consumer | **Status:** enriched | **Quality Score:** 80

---

## Overview

The Beneficiaries screen is the counterparty management hub of the Mifos X Open Banking consumer app. It surfaces recently-used payees in a high-glance section at the top, followed by an alphabetical full beneficiary list. A search bar filters by name or IBAN, a sort control reorders the full list, and a fixed "Add Beneficiary" FAB opens the add-beneficiary bottom sheet. Each beneficiary row shows an avatar (initials or bank logo), bank name, masked IBAN, and last payment date. Tapping any row navigates to the send-money flow pre-filled with that counterparty.

---

## Screens

| Screen ID | Label | Route | Layout | Scroll |
|---|---|---|---|---|
| beneficiaries | Beneficiaries | /beneficiaries | index_list archetype, top app bar, no bottom nav | vertical |

---

## Components

| ID | Type | Description |
|---|---|---|
| beneficiary_search_bar | input | Outlined search field, placeholder "Search beneficiaries by name or IBAN...", corner_radius 28 |
| recently_used_header | text | "Recently Used" — title_medium, #111111, weight semibold |
| recent_beneficiary_john | box | John Smith card — tappable, navigates to send-money |
| recent_beneficiary_john_avatar | box | "JS" initials circle, 44px, bg #1800B1, #FFFFFF text |
| recent_john_bank | text | "Barclays UK" — body_small, #888888 |
| recent_john_last_payment | text | "£500 · 2 days ago" — body_small, #008B8B |
| recent_beneficiary_sarah | box | Sarah Williams card — tappable |
| recent_beneficiary_sarah_avatar | box | "SW" circle, 44px, bg #008B8B |
| recent_sarah_last_payment | text | "£1,200 · 5 days ago" — body_small, #008B8B |
| recent_beneficiary_michael | box | Michael Chen card — tappable |
| recent_beneficiary_michael_avatar | box | "MC" circle, 44px, bg #6750A4 |
| section_divider | divider | Horizontal rule between Recent and All sections |
| all_beneficiaries_header_row | stack | "All Beneficiaries" heading + sort icon (horizontal, space-between) |
| sort_button | icon | sort icon, 24px, #1800B1 — triggers sort action |
| beneficiary_item_anderson | box | James Anderson — NatWest, IBAN ending 8819, last: 12 May 2026 |
| natwest_logo | image | NatWest logo, 32×32, corner_radius 4 |
| anderson_iban | text | "GB29 NWBK ··· 8819" — body_small, #888888, monospace |
| beneficiary_item_patel | box | Priya Patel — Santander UK, IBAN ending 4421 |
| santander_logo | image | Santander logo, 32×32 |
| patel_iban | text | "GB72 ABBY ··· 4421" — body_small, #888888, monospace |
| add_beneficiary_fab | button | FAB, filled #1800B1, "Add Beneficiary", person_add icon, position floating |

---

## States

| ID | Trigger | Description |
|---|---|---|
| loading | ScreenOpened / RefreshTriggered | Search bar visible; skeleton list (6 items) |
| content | Beneficiaries loaded | Search bar + Recently Used section + All Beneficiaries section + FAB |
| empty | No beneficiaries exist | Search bar + FAB + empty state: person_off icon, "No beneficiaries yet", "Add a beneficiary to start sending money quickly" |
| searching | User types in search bar | Search bar + matching results shown dynamically |
| error | LOAD_FAILED | Search bar + FAB + error state: cloud_off icon, "Unable to load beneficiaries", "Check your connection and try again" + Retry button |

---

## State Model

**ViewModel:** `BeneficiariesViewModel`

| Field | Type | Default |
|---|---|---|
| beneficiaries | List\<Counterparty\> | emptyList() |
| recentBeneficiaries | List\<Counterparty\> | emptyList() |
| searchQuery | String | "" |
| filteredBeneficiaries | List\<Counterparty\> | emptyList() |
| sortOrder | SortOrder | AlphaAscending |
| uiState | BeneficiariesUiState | Loading |

**Events:** SearchQueryChanged · BeneficiarySelected · AddBeneficiaryClicked · SortChanged · RefreshTriggered

**Actions:** search · navigate · open_add_beneficiary_sheet · sort

**DI:** BeneficiaryRepository · CounterpartyRepository

---

## Navigation

| From | To | Trigger | Type |
|---|---|---|---|
| beneficiaries | send-money | Tap any beneficiary row | push (pre-fills counterparty) |
| beneficiaries | (add sheet) | Tap add_beneficiary_fab | bottom sheet |
| beneficiaries | (parent screen) | Top app bar back | pop |

---

## API Endpoints

| Endpoint | Auth | Purpose |
|---|---|---|
| GET /obp/v4.0.0/banks/{bankId}/accounts/{accountId}/{viewId}/counterparties | Not specified in YAML (assumes DirectLogin) | Fetch all counterparties (beneficiaries) for a given account view |

---

## Design Tokens

| Token | Value | Usage |
|---|---|---|
| color.primary | #1800B1 | John Smith avatar, sort icon, FAB background, search input tint |
| color.search_bg | #F5F5FF | Search bar background (cool white tint) |
| color.surface | #FFFFFF | Beneficiary card backgrounds |
| color.surface_border | #F0F0F0 | Card border (1px) |
| color.savings_accent | #008B8B | Sarah avatar, last payment tint |
| color.secondary_purple | #6750A4 | Michael avatar |
| color.secondary_text | #888888 | Bank name, IBAN, last payment date |
| color.last_payment | #008B8B | Recent payment amount + date text (teal) |
| color.on_primary | #FFFFFF | Avatar initials text |
| typography.title_medium | — | "Recently Used" and "All Beneficiaries" section headers |
| typography.body_small / monospace | — | Masked IBAN display |
| typography.body_small | — | Bank name, last payment metadata |
| elevation.card | 1 | Beneficiary card shadow |

---

_Generated by /idea export | 2026-05-25_
