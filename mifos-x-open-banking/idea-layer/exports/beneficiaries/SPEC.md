# SPEC — Beneficiaries

| Field         | Value                    |
|---------------|--------------------------|
| Feature       | beneficiaries            |
| Flavor        | consumer                 |
| Status        | designed                 |
| Quality Score | 93                       |
| ViewModel     | BeneficiariesViewModel   |

---

## Overview

The Beneficiaries screen is the counterparty management hub of the Mifos X Open Banking consumer app. Recently-used payees appear in a high-glance section at the top for fast re-payment access, followed by an alphabetical full beneficiary list with masked account numbers and last payment dates. A search bar filters by name or account number across both sections; a sort control reorders the full list; and a fixed "Add Beneficiary" FAB opens the add-beneficiary bottom sheet. Each beneficiary row shows an avatar (initials circle or bank logo), bank name, and last payment metadata. Tapping any row navigates to send-money pre-filled with that counterparty. The screen sources live counterparty data from the OBP Counterparties API endpoint and supports loading, content, empty, searching, and error states. Demo data reflects a Kenyan consumer persona with beneficiaries at Equity Bank, Co-op Bank, NCBA, KCB, and utility biller Kenya Power & Lighting.

---

## Screens

| ID            | Name          | Route          | Layout     | Scroll   |
|---------------|---------------|----------------|------------|----------|
| beneficiaries | Beneficiaries | /beneficiaries | index_list | Vertical |

**Shell:** Top app bar ("Beneficiaries") with back arrow + filter_list action. No bottom navigation bar.

| Element          | Detail                                      |
|------------------|---------------------------------------------|
| top_bar.title    | "Beneficiaries"                             |
| navigation_icon  | arrow_back                                  |
| action           | filter_list icon → sort_beneficiaries       |
| bottom_nav       | false                                       |

---

## Components

| ID                               | Type    | Description                                                                                                |
|----------------------------------|---------|------------------------------------------------------------------------------------------------------------|
| beneficiary_search_bar           | input   | Outlined search field (radius 28, #F9FAEF bg) — placeholder "Search beneficiaries by name or IBAN...", leading search icon, trailing clear icon |
| recently_used_header             | text    | "Recently Used" — Outfit/title_medium, #1A1C16, weight semibold, role heading                              |
| recent_beneficiary_john          | box     | White card (radius 12, elevation 1, 14dp vertical padding) for John Smith; taps → send-money               |
| recent_beneficiary_john_avatar   | box     | "JS" circle avatar (44dp diameter, #4C662B bg, #FFFFFF text, Outfit/title_medium, bold)                    |
| recent_john_bank                 | text    | "Barclays UK" — Outfit/body_small, #44483D                                                                 |
| recent_john_last_payment         | text    | "£500 · 2 days ago" — Outfit/body_small, #386663                                                           |
| recent_beneficiary_sarah         | box     | White card (radius 12, elevation 1) for Sarah Williams; taps → send-money                                  |
| recent_beneficiary_sarah_avatar  | box     | "SW" circle avatar (44dp, #386663 bg, #FFFFFF text, Outfit/title_medium, bold)                             |
| recent_sarah_bank                | text    | "HSBC UK" — Outfit/body_small, #44483D                                                                     |
| recent_sarah_last_payment        | text    | "£1,200 · 5 days ago" — Outfit/body_small, #386663                                                         |
| recent_beneficiary_michael       | box     | White card (radius 12, elevation 1) for Michael Chen; taps → send-money                                    |
| recent_beneficiary_michael_avatar| box     | "MC" circle avatar (44dp, #4C662B bg, #FFFFFF text, Outfit/title_medium, bold)                             |
| recent_michael_bank              | text    | "Lloyds Bank" — Outfit/body_small, #44483D                                                                 |
| section_divider                  | divider | Horizontal rule, #E1E4D5, 1px thickness, 8dp vertical padding                                             |
| all_beneficiaries_header_row     | stack   | Horizontal row (space-between, align center): "All Beneficiaries" heading + sort icon button               |
| all_beneficiaries_header         | text    | "All Beneficiaries" — Outfit/title_medium, #1A1C16, weight semibold, role heading                          |
| sort_button                      | icon    | sort icon, 24dp, #4C662B; triggers sort action                                                             |
| beneficiary_item_anderson        | box     | White card (radius 12, elevation 1) for James Anderson — NatWest, IBAN ending 8819                         |
| natwest_logo                     | image   | NatWest logo, 32×32dp, radius 4, content_scale fit                                                         |
| anderson_iban                    | text    | "GB29 NWBK ··· 8819" — Outfit/body_small, #44483D, monospace                                              |
| anderson_last_payment            | text    | "Last: 12 May 2026" — Outfit/body_small, #44483D                                                           |
| beneficiary_item_patel           | box     | White card (radius 12, elevation 1) for Priya Patel — Santander UK, IBAN ending 4421                       |
| santander_logo                   | image   | Santander logo, 32×32dp, radius 4, content_scale fit                                                       |
| patel_iban                       | text    | "GB72 ABBY ··· 4421" — Outfit/body_small, #44483D, monospace                                              |
| add_beneficiary_fab              | button  | FAB: filled #4C662B, "Add Beneficiary", person_add icon, elevation 6, position floating_action_button      |

---

## States

| ID        | Trigger                              | Description                                                                                                                       |
|-----------|--------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| loading   | ScreenOpened / RefreshTriggered      | Search bar visible; shimmer skeleton list (6 items, 200ms shimmer duration); FAB hidden; Recently Used + All sections skeletonised |
| content   | Beneficiaries loaded successfully    | Search bar + Recently Used section (3 cards: JS, SW, MC) + divider + All Beneficiaries section (Anderson, Patel) + FAB visible   |
| empty     | No beneficiaries exist               | Search bar + FAB + empty state: person_off icon (48dp), "No beneficiaries yet", "Add a beneficiary to start sending money quickly" |
| searching | User types in search bar             | Search bar (with trailing clear icon active) + dynamically filtered beneficiary results; section headers hidden                   |
| error     | LOAD_FAILED from API                 | Search bar + FAB + cloud_off icon (48dp), "Unable to load beneficiaries", "Check your connection and try again", Retry button     |

---

## State Model

**ViewModel:** `BeneficiariesViewModel`
**Screen State Type:** `BeneficiariesUiState`

| Name                  | Type                    | Default          |
|-----------------------|-------------------------|------------------|
| beneficiaries         | List\<Counterparty\>    | emptyList()      |
| recentBeneficiaries   | List\<Counterparty\>    | emptyList()      |
| searchQuery           | String                  | ""               |
| filteredBeneficiaries | List\<Counterparty\>    | emptyList()      |
| sortOrder             | SortOrder               | AlphaAscending   |
| uiState               | BeneficiariesUiState    | Loading          |

**Events:** `SearchQueryChanged`, `BeneficiarySelected`, `AddBeneficiaryClicked`, `SortChanged`, `RefreshTriggered`

**Actions:** `search()`, `navigate()`, `open_add_beneficiary_sheet()`, `sort()`

**DI Dependencies:** `BeneficiaryRepository`, `CounterpartyRepository`

**Errors:**
- `LOAD_FAILED`: "Unable to load beneficiaries. Please try again."

---

## Navigation

| From          | To                | Trigger                         | Type                        |
|---------------|-------------------|---------------------------------|-----------------------------|
| beneficiaries | send-money        | Tap any beneficiary row         | push (pre-fills counterparty) |
| beneficiaries | (add-beneficiary) | add_beneficiary_fab tap         | bottom sheet                |
| beneficiaries | (parent screen)   | Top app bar back arrow          | pop                         |

---

## API Endpoints

| Endpoint                                                                         | Auth        | Tag            | Purpose                                                   |
|----------------------------------------------------------------------------------|-------------|----------------|-----------------------------------------------------------|
| GET /obp/v4.0.0/banks/{bankId}/accounts/{accountId}/{viewId}/counterparties      | DirectLogin | Counterparties | Fetch all counterparties (beneficiaries) for the account  |

---

## Design Tokens

| Token                           | Value     | Usage                                                                       |
|---------------------------------|-----------|-----------------------------------------------------------------------------|
| colors.light.primary            | #4C662B   | John Smith avatar, Michael Chen avatar, sort icon, FAB background, search leading icon |
| colors.light.secondary          | #386663   | Sarah Williams avatar bg, last payment amount+date text color               |
| colors.light.on_primary         | #FFFFFF   | Avatar initials text (JS, SW, MC), FAB label + icon                        |
| colors.light.surface            | #FFFFFF   | Beneficiary card backgrounds                                                |
| colors.light.background         | #F9FAEF   | Screen background, search bar background                                    |
| colors.light.on_surface         | #1A1C16   | "Recently Used" and "All Beneficiaries" section headers                     |
| colors.light.on_surface_variant | #44483D   | Bank names, account routing text, last payment dates                        |
| colors.light.surface_variant    | #E1E4D5   | Section divider, card border color                                          |
| colors.light.outline_variant    | #C5C8BA   | Card borders (1px)                                                          |
| typography.title_medium         | 16sp/500  | "Recently Used" and "All Beneficiaries" headers                             |
| typography.body_small           | 12sp/400  | Bank name, account routing text, last payment metadata                      |
| elevation.level1                | 1dp       | Beneficiary card elevation                                                  |
| elevation.level3                | 6dp       | FAB elevation                                                               |
| radius.md                       | 12dp      | Beneficiary card corners                                                    |
| radius.lg                       | 16dp      | FAB corner radius                                                           |
| motion.duration.short4          | 200ms     | Skeleton shimmer animation duration                                         |

---

_Generated by /idea export | 2026-05-30_
