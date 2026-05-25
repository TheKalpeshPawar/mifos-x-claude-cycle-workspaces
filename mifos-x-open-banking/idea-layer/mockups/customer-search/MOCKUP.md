# Mockup Specification: Find Customer

| Field | Value |
|---|---|
| Feature | customer-search |
| Flavor | fieldOfficer |
| Archetype | search |

---

## Screen Layout

```
[ Status Bar ]
[ "Find Customer" ]                         ← headline_large #1800B1 bold, pt:24 ph:16
[ Search Input ]                            ← pill shape br:28, bg:#F5F5F5, leading 🔍, clearable X
                                              placeholder: "Search by name, ID, phone or email..."
[ Filter Chips Row — horizontal scroll ]
  [All ✓] [Active] [Prospect] [Dormant]    ← radio chips, selected fills #1800B1 text white
[ [qr_code] Scan Customer ID ]             ← outlined button br:12, #1800B1
──────────────────────────────────────────────────
  === RESULTS STATE ===
[ Customer Card: John Mwangi ]
  [JM] bg:#1800B1 circle 44px  |  "John Mwangi" title_small bold
                                  "KYC Verified ✓" body_small #4CAF50
                                  "Checking Account · KES 45,200" #616161
                               |  "3 days ago" body_small #9E9E9E (top-right)
[ Customer Card: Sarah Odhiambo ]
  [SO] bg:#FF8F00 circle 44px  |  "Sarah Odhiambo" title_small bold
                                  "KYC Pending ⚠" body_small #FF8F00
                                  "Application in Review" #616161
                               |  "7 days ago" #9E9E9E
[ Customer Card: Peter Kamau ]
  [PK] bg:#008B8B circle 44px  |  "Peter Kamau" title_small bold
                                  "New Prospect" body_small #008B8B
                                  "No account yet" #9E9E9E
                               |  "Today" body_small #1800B1 bold
──────────────────────────────────────────────────
  === NO RESULTS STATE ===
[ Empty State Box ]                         ← br:12, bg:#FAFAFA, centered, p:32
  "No customers found for this search"
  [ Try Different Search ] outlined #1800B1
──────────────────────────────────────────────────
[ [person_add] Onboard New Customer ]       ← filled #1800B1 full-width, label_large
[ [business] Onboard Business Customer ]   ← outlined teal full-width
[ Bottom Nav Bar ]
```

---

## Components

### Search Input
- **Style:** Pill-shaped (border_radius:28), background #F5F5F5, 16px horizontal padding, leading search icon, trailing clear-X when text present
- **Behavior:** Triggers API search on each keystroke after ≥2 characters with 300ms debounce; placeholder fades on focus

### Filter Chips
- **Style:** Horizontal row with 8px spacing, overflow scrolls horizontally; each chip is border_radius:16, padding 16px/8px
- **Selected state:** Background fills to #1800B1, text white; unselected is outlined or bare with body text color
- **Default:** "All" chip pre-selected

### Customer Result Cards
- **Style:** bg:#FFFFFF, border_radius:12, elevation:2, padding:14, margin_horizontal:16, margin_bottom:8
- **Layout:** Row — circular avatar (44px, initials) + vertical content stack + timestamp top-right
- **Avatar colors:** John = #1800B1 (verified customer), Sarah = #FF8F00 (pending), Peter = #008B8B (prospect)
- **KYC badge color:** Verified = #4CAF50, Pending = #FF8F00, Prospect = #008B8B

### Onboard Buttons
- **Onboard New Customer:** Filled #1800B1, white text, full-width, 14px vertical padding, border_radius:12, person_add icon
- **Onboard Business Customer:** Outlined #008B8B, teal text, full-width, business icon

---

## Interaction Patterns

| Element | Gesture | Result |
|---|---|---|
| Search input | Tap + type | Triggers search; result cards appear or searching skeleton shows |
| Filter chip | Tap | Switches active filter; re-queries results |
| Scan Customer ID | Tap | Opens device camera in QR scan mode |
| Customer result card | Tap anywhere on card | Push navigate to /customer-detail/{customerId} |
| Onboard New Customer | Tap | Push navigate to /customer-onboarding |
| Onboard Business Customer | Tap | Push navigate to /corporate-onboarding |
| Try Different Search | Tap | Clears search input; returns to idle state |

**Searching state:** All three result card slots show shimmer skeleton (rounded rect placeholders for avatar, name line, subtitle line, timestamp).

---

## Content Data

| Customer | Avatar | KYC Status | Account Info | Last Seen |
|---|---|---|---|---|
| John Mwangi | JM (#1800B1) | KYC Verified ✓ (green) | Checking Account · KES 45,200 | 3 days ago |
| Sarah Odhiambo | SO (#FF8F00) | KYC Pending ⚠ (amber) | Application in Review | 7 days ago |
| Peter Kamau | PK (#008B8B) | New Prospect (teal) | No account yet | Today (#1800B1 bold) |

---

## Design Notes

**Color semantics:** Avatar background color mirrors KYC status — verified customers get brand purple, pending get amber, prospects get teal. This provides immediate visual cues without reading the label.

**Typography:** Title is headline_large (32sp) for strong page identity. Search input uses body_medium. Customer names use title_small (14sp, 600 weight). KYC status uses body_small (12sp) with semantic colors.

**Spacing rhythm:** 16px horizontal margins on all cards and buttons. 12px top gap from title to search input. 8px spacing between filter chips. 8px bottom margin between result cards.

**Accessibility:** Search field has role: searchbox with hint "Enter at least 2 characters to start searching." Filter chips use radio role for group semantics. Each customer card has a full-sentence a11y label including KYC status and last interaction.

**Empty state:** Centered content in a #FAFAFA rounded box with generous 32px padding. Message in body_large #757575 followed by an outlined Try Different Search button.

---
_Generated by /idea export | 2026-05-25_
