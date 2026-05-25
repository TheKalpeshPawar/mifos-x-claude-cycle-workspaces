# Visual Specification — Beneficiaries
**Feature:** beneficiaries | **Flavor:** consumer

---

## Screen Layout

Vertical scroll with top app bar ("Beneficiaries" + back + filter_list sort action); no bottom navigation:

```
┌────────────────────────────────────┐
│ ← Beneficiaries              [≡]  │  ← top app bar
├────────────────────────────────────┤
│ 🔍 Search beneficiaries by name... │  ← beneficiary_search_bar
├────────────────────────────────────┤
│  Recently Used                     │  ← recently_used_header
│ ┌──────────────────────────────┐   │
│ │ [JS] John Smith              │   │  ← recent_beneficiary_john
│ │       Barclays UK            │   │
│ │       £500 · 2 days ago      │   │
│ └──────────────────────────────┘   │
│ ┌──────────────────────────────┐   │
│ │ [SW] Sarah Williams          │   │  ← recent_beneficiary_sarah
│ │       HSBC UK                │   │
│ │       £1,200 · 5 days ago    │   │
│ └──────────────────────────────┘   │
│ ┌──────────────────────────────┐   │
│ │ [MC] Michael Chen            │   │  ← recent_beneficiary_michael
│ │       Lloyds Bank            │   │
│ │       £250 · 1 week ago      │   │
│ └──────────────────────────────┘   │
├────────────────────────────────────┤
│  All Beneficiaries            [↕]  │  ← all_beneficiaries_header_row
│ ┌──────────────────────────────┐   │
│ │ [NatWest] James Anderson     │   │  ← beneficiary_item_anderson
│ │            GB29 NWBK ··· 8819│   │
│ │            Last: 12 May 2026  │   │
│ └──────────────────────────────┘   │
│ ┌──────────────────────────────┐   │
│ │ [Santander] Priya Patel      │   │  ← beneficiary_item_patel
│ │            GB72 ABBY ··· 4421│   │
│ └──────────────────────────────┘   │
│                                    │
│                     [+ Add Beneficiary]  ← FAB (floating bottom-right)
└────────────────────────────────────┘
```

---

## Components

### beneficiary_search_bar
- **Style:** variant=outlined, input_type=search, corner_radius 28, background #F5F5FF (cool off-white)
- **Padding:** horizontal 16
- **Leading icon:** search (24px)
- **Trailing icon:** clear (24px) — appears when field is non-empty
- **Placeholder:** "Search beneficiaries by name or IBAN..." — a11y role: search_field

### recently_used_header
- **Content:** "Recently Used"
- **Style:** title_medium, color #111111, font_weight semibold, padding_top 16, padding_bottom 8

### Recent Beneficiary Cards (john / sarah / michael)

Each card follows the same composition:

| Property | Value |
|---|---|
| Background | #FFFFFF |
| Corner radius | 12 |
| Elevation | 1 |
| Padding | horizontal 16, vertical 14 |
| Border | 1px #F0F0F0 |
| On tap | Navigate → send-money (pre-fill counterparty) |

**Internal layout (horizontal row):**
- **Avatar circle (44px diameter):**
  - John: bg #1800B1, initials "JS", white title_medium bold
  - Sarah: bg #008B8B (teal), initials "SW"
  - Michael: bg #6750A4 (secondary purple), initials "MC"
- **Info column (vertical, flex 1):**
  - Name: title_medium or body_medium weight 500, #111111
  - Bank name: body_small, #888888
  - Last payment: body_small, #008B8B (teal) — e.g. "£500 · 2 days ago"

### section_divider
- **Color:** #E0E0E0, thickness 1px, padding_vertical 8

### all_beneficiaries_header_row
- **Layout:** horizontal, space-between, align center, padding_vertical 4
- **Left:** "All Beneficiaries" — title_medium, #111111, weight semibold
- **Right:** sort icon (sort, 24px, #1800B1) — tappable, triggers sort bottom sheet

### beneficiary_item_anderson — James Anderson (NatWest)
- **Same card style as recent beneficiary cards**
- **Left element:** NatWest logo image (32×32, corner_radius 4, content_scale=fit)
- **Info column:**
  - "James Anderson" — body_medium, weight 500
  - "GB29 NWBK ··· 8819" — body_small, #888888, monospace
  - "Last: 12 May 2026" — body_small, #888888

### beneficiary_item_patel — Priya Patel (Santander)
- **Left element:** Santander logo image (32×32)
- **IBAN:** "GB72 ABBY ··· 4421" — body_small, #888888, monospace

### add_beneficiary_fab
- **Style:** filled, background #1800B1, text #FFFFFF, corner_radius 16, elevation 6
- **Position:** floating_action_button (fixed bottom-right)
- **Label:** "Add Beneficiary"
- **Leading icon:** person_add

---

## Interaction Patterns

| Target | Gesture | Outcome |
|---|---|---|
| beneficiary_search_bar | Type | SearchQueryChanged event; filteredBeneficiaries updated live; state=searching |
| beneficiary_search_bar trailing clear | Tap | Clear search; reset to content state |
| recent_beneficiary_john | Tap | Navigate → send-money pre-filled with John Smith / Barclays UK |
| recent_beneficiary_sarah | Tap | Navigate → send-money pre-filled with Sarah Williams / HSBC UK |
| recent_beneficiary_michael | Tap | Navigate → send-money pre-filled with Michael Chen / Lloyds Bank |
| beneficiary_item_anderson | Tap | Navigate → send-money pre-filled with James Anderson / NatWest |
| beneficiary_item_patel | Tap | Navigate → send-money pre-filled with Priya Patel / Santander |
| sort_button | Tap | SortChanged event; sort bottom sheet opens (Alpha A-Z / Alpha Z-A / Recent) |
| Top app bar filter_list | Tap | sort_beneficiaries action (same as sort_button) |
| add_beneficiary_fab | Tap | AddBeneficiaryClicked event → open_add_beneficiary_sheet bottom sheet |

---

## Content Data

| Beneficiary | Bank | IBAN / Routing | Last Payment |
|---|---|---|---|
| John Smith | Barclays UK | (full IBAN in API) | £500 · 2 days ago |
| Sarah Williams | HSBC UK | (full IBAN in API) | £1,200 · 5 days ago |
| Michael Chen | Lloyds Bank | (full IBAN in API) | £250 · 1 week ago |
| James Anderson | NatWest | GB29 NWBK ··· 8819 | 12 May 2026 |
| Priya Patel | Santander UK | GB72 ABBY ··· 4421 | (from API) |

---

## Design Notes

- **Avatar color diversity:** Three distinct colors for recent beneficiary avatars (#1800B1, #008B8B, #6750A4) prevent visual monotony and help users identify frequent payees at a glance without reading names.
- **Last payment teal (#008B8B):** The teal accent on recent payment metadata creates a warm "active relationship" signal distinct from the static bank/IBAN info in grey — draws the eye to recency cues.
- **Masked IBANs:** Only the last 4 digits shown (GB29 NWBK ··· 8819) for privacy. Monospace font makes partial IBANs easy to verify at a glance.
- **Two-section layout:** "Recently Used" (frequency-based, max 3) above "All Beneficiaries" (alphabetical, sortable) mirrors UX patterns from WhatsApp contacts and Apple Pay recents, reducing friction for repeat payments.
- **No bottom nav:** Beneficiaries is accessed from within the payment flow or More menu; removing bottom nav keeps the user focused on counterparty selection.
- **Search corner_radius 28:** Pill-shaped search field (vs the 12px cards) visually differentiates the input from list items, a common Material You pattern.
- **Empty state:** Uses person_off illustration icon with action-oriented message "Add a beneficiary to start sending money quickly" — FAB remains visible so the user has an immediate path forward.
- **FAB label visible:** "Add Beneficiary" extended FAB (not icon-only) is shown because users may not know the person_add icon, especially new users in the empty state.

---

_Generated by /idea export | 2026-05-25_
