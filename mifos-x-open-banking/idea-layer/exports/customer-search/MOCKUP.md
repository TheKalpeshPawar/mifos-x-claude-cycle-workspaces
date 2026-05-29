# MOCKUP — Find Customer

**Archetype:** search
**Shell:** Field Officer bottom navigation bar — Customers tab active (people icon). Mobile only, 390dp baseline.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│                                     │
│  Find Customer                      │  ← headline_large, #4C662B, 24dp top pad
│                                     │
│  ┌─────────────────────────────┐    │  ← search input, #F9FAEF bg, 28dp radius
│  │ 🔍 Search by name, ID...   │    │
│  └─────────────────────────────┘    │
│                                     │
│  ████████████████████████████████   │  ← Skeleton row 1 (customer card shape, #E1E4D5)
│  ████████████████████████████████   │
│  ████████████████████████████████   │  ← Skeleton row 2
│  ████████████████████████████████   │
│  ████████████████████████████████   │  ← Skeleton row 3
│  ████████████████████████████████   │
│  ████████████████████████████████   │  ← Skeleton row 4
│  ████████████████████████████████   │
│  ████████████████████████████████   │  ← Skeleton row 5
│                                     │
├─────────────────────────────────────┤
│  [home] [accounts] [customers*] [profile] │  ← Bottom nav, Customers active
└─────────────────────────────────────┘
```

**Layout notes:** Title and search input visible during loading. Five skeleton customer-card-shaped blocks shimmer at 200ms (short4). Filter chips, QR button, and onboard buttons not shown during initial load.

---

## Screen: idle

```
┌─────────────────────────────────────┐
│                                     │
│  Find Customer                      │  ← headline_large, #4C662B
│                                     │
│  ┌─────────────────────────────┐    │  ← search input, variant:search
│  │ 🔍 Search by name, ID...   │    │    #F9FAEF bg, 28dp radius, clear icon trailing
│  └─────────────────────────────┘    │
│                                     │
│  [All ✓] [Active] [Prospect] [Dormant] →  │  ← Horizontal scrollable chip row
│                                     │       All chip: #4C662B bg / #FFFFFF text
│  [📷 Scan Customer ID]              │  ← outlined, #4C662B, 12dp radius, qr_code icon
│                                     │
│  ┌─────────────────────────────┐    │  ← Onboard New Customer button
│  │ [👤+] Onboard New Customer  │    │    filled, #4C662B bg, full-width, 14dp V padding
│  └─────────────────────────────┘    │
│  ┌─────────────────────────────┐    │  ← Onboard Business Customer button
│  │ [🏢] Onboard Business...   │    │    outlined, #386663 border+text
│  └─────────────────────────────┘    │
│                                     │
├─────────────────────────────────────┤
│  [home] [accounts] [customers*] [profile] │
└─────────────────────────────────────┘
```

**Layout notes:** Default state after initial data load with no query entered. No result cards visible. Filter chips scroll horizontally if overflow. QR button is left-aligned (align_self: flex_start). Onboard buttons are full-width at bottom.

---

## Screen: searching

```
┌─────────────────────────────────────┐
│                                     │
│  Find Customer                      │
│                                     │
│  ┌─────────────────────────────┐    │
│  │ 🔍 wanjiru              [✕] │    │  ← active query, trailing clear icon (#4C662B)
│  └─────────────────────────────┘    │
│                                     │
│  [All ✓] [Active] [Prospect] [Dormant] →  │
│                                     │
│  [📷 Scan Customer ID]              │
│                                     │
│  ┌─────────────────────────────┐    │  ← Skeleton card 1 (#E1E4D5, 12dp radius, 2dp elev)
│  │ ●●  ████████████  ████████  │    │    circle avatar skeleton + 2 text skeleton rows
│  │     ████████████            │    │
│  └─────────────────────────────┘    │
│  ┌─────────────────────────────┐    │  ← Skeleton card 2
│  │ ●●  ████████████  ████████  │    │
│  │     ████████████            │    │
│  └─────────────────────────────┘    │
│  ┌─────────────────────────────┐    │  ← Skeleton card 3
│  │ ●●  ████████████  ████████  │    │
│  │     ████████████            │    │
│  └─────────────────────────────┘    │
│                                     │
├─────────────────────────────────────┤
│  [home] [accounts] [customers*] [profile] │
└─────────────────────────────────────┘
```

**Layout notes:** 3 skeleton cards replace the result area while API is in flight. Onboard buttons hidden during searching state. Filter chips and QR button remain visible for pivot/cancel.

---

## Screen: results

```
┌─────────────────────────────────────┐
│                                     │
│  Find Customer                      │
│                                     │
│  ┌─────────────────────────────┐    │
│  │ 🔍 john                 [✕] │    │
│  └─────────────────────────────┘    │
│                                     │
│  [All ✓] [Active] [Prospect] [Dormant] →  │
│                                     │
│  [📷 Scan Customer ID]              │
│                                     │
│  ┌─────────────────────────────┐    │  ← Card 1: John Mwangi
│  │ ┌──┐  John Mwangi           │    │    avatar: "JM" circle, #4C662B bg
│  │ │JM│  KYC Verified ✓        │    │    KYC: body_small, #4C662B text
│  │ └──┘  Checking Acct · KES 45,200 │    Account: body_small, #44483D
│  │        3 days ago            │    │    Timestamp: body_small, #44483D
│  └─────────────────────────────┘    │
│  ┌─────────────────────────────┐    │  ← Card 2: Sarah Odhiambo
│  │ ┌──┐  Sarah Odhiambo        │    │    avatar: "SO" circle, #E8A317 bg
│  │ │SO│  KYC Pending ⚠         │    │    KYC: body_small, #44483D (a11y fix)
│  │ └──┘  Application in Review │    │    Account: body_small, #44483D
│  │        7 days ago            │    │
│  └─────────────────────────────┘    │
│  ┌─────────────────────────────┐    │  ← Card 3: Peter Kamau
│  │ ┌──┐  Peter Kamau            │    │    avatar: "PK" circle, #386663 bg
│  │ │PK│  New Prospect           │    │    KYC: body_small, #386663 text
│  │ └──┘  No account yet        │    │    Account: body_small, #44483D
│  │        Today                 │    │    Timestamp: body_small, #4C662B (highlighted)
│  └─────────────────────────────┘    │
│                                     │
│  ┌─────────────────────────────┐    │
│  │ [👤+] Onboard New Customer  │    │  ← filled, #4C662B bg
│  └─────────────────────────────┘    │
│  ┌─────────────────────────────┐    │
│  │ [🏢] Onboard Business...   │    │  ← outlined, #386663
│  └─────────────────────────────┘    │
│                                     │
├─────────────────────────────────────┤
│  [home] [accounts] [customers*] [profile] │
└─────────────────────────────────────┘
```

**Layout notes:**
- Customer cards: #FFFFFF fill, 12dp radius, 2dp elevation, 14dp padding, 16dp H margin, 8dp bottom margin.
- Avatar circles: 44dp diameter, initials derived from legal_name (first letters of first + last name), font-weight 700.
- "JM" avatar: #4C662B bg (verified — green). "SO" avatar: #E8A317 bg (pending — amber, bg only; text uses #44483D for contrast). "PK" avatar: #386663 bg (prospect — teal).
- "KYC Pending ⚠" text: #44483D (corrected from source #E8A317 which failed WCAG AA — A11Y-002 fix).
- "Today" timestamp: #4C662B bold to highlight new addition.
- Onboard buttons appear below the result list; both full-width.

---

## Screen: no_results

```
┌─────────────────────────────────────┐
│                                     │
│  Find Customer                      │
│                                     │
│  ┌─────────────────────────────┐    │
│  │ 🔍 xyz123               [✕] │    │
│  └─────────────────────────────┘    │
│                                     │
│  [All ✓] [Active] [Prospect] [Dormant] →  │
│                                     │
│  ┌─────────────────────────────┐    │  ← Empty state box: #F9FAEF, 12dp radius
│  │                             │    │    32dp padding, 16dp H margin, 16dp top margin
│  │     [person_search icon]    │    │    person_search Material icon, centered
│  │                             │    │
│  │  No customers found for     │    │  ← body_large, #44483D, center
│  │  this search                │    │
│  │                             │    │
│  │  [ Try Different Search ]   │    │  ← outlined, #4C662B, 8dp radius
│  └─────────────────────────────┘    │
│                                     │
│  ┌─────────────────────────────┐    │
│  │ [👤+] Onboard New Customer  │    │
│  └─────────────────────────────┘    │
│  ┌─────────────────────────────┐    │
│  │ [🏢] Onboard Business...   │    │
│  └─────────────────────────────┘    │
│                                     │
├─────────────────────────────────────┤
│  [home] [accounts] [customers*] [profile] │
└─────────────────────────────────────┘
```

**Layout notes:** QR scan button is hidden in no_results state (irrelevant when there's nothing to scan for). Empty state box uses #F9FAEF (background token) for a soft contained look. "Try Different Search" clears the query and refocuses the search input.

---

## Screen: error

```
┌─────────────────────────────────────┐
│                                     │
│  Find Customer                      │
│                                     │
│  ┌─────────────────────────────┐    │
│  │ 🔍 Search by name, ID...   │    │
│  └─────────────────────────────┘    │
│                                     │
│  ┌─────────────────────────────┐    │  ← Error banner: type:banner, #FFDAD6 bg (error_container)
│  │ ⚠  Search failed.           │    │    error_outline icon, #BA1A1A text
│  │    Check your connection    │    │
│  │    and try again.           │    │
│  │                             │    │
│  │        [  Retry  ]          │    │  ← outlined button, #4C662B
│  └─────────────────────────────┘    │
│                                     │
├─────────────────────────────────────┤
│  [home] [accounts] [customers*] [profile] │
└─────────────────────────────────────┘
```

**Layout notes:** Error state shows only title, search input, and the error banner. Customer result cards, filter chips, QR button, and onboard buttons are all hidden. Banner uses `colors.light.error_container` (#FFDAD6) fill for the inline error surface per M3 error pattern.

---

## Design Checklist (Figma / Stitch)

- [ ] Screen title "Find Customer" — headline_large (Outfit 32sp/700), #4C662B, 24dp top / 16dp horizontal padding
- [ ] Search input — variant:search, #F9FAEF background, 28dp border radius, 16dp H / 12dp V padding, leading search icon, trailing clear icon (tappable, shows when non-empty)
- [ ] Filter chips row — horizontal scroll, 8dp spacing, "All" selected by default (#4C662B fill, #FFFFFF text); unselected chips use outline style
- [ ] Chip shape: 16dp border radius, 16dp H / 8dp V padding, minimum 48dp touch target
- [ ] "Scan Customer ID" — outlined button, #4C662B border+text, 12dp radius, qr_code leading icon, align-self: flex_start (not full-width)
- [ ] Customer result cards: #FFFFFF fill, 12dp radius, 2dp elevation, 14dp inner padding, 16dp horizontal margin, 8dp bottom margin, row direction, center-aligned
- [ ] Avatar circles: 44dp diameter, initials from legal_name; JM=#4C662B bg, SO=#E8A317 bg, PK=#386663 bg; all with #FFFFFF text Outfit/title_small 700
- [ ] Customer name: Outfit/title_small (14sp/500), #1A1C16
- [ ] "KYC Verified ✓" text: Outfit/body_small, #4C662B (green for verified)
- [ ] "KYC Pending ⚠" text: Outfit/body_small, #44483D — NOT #E8A317 (WCAG AA contrast fix A11Y-002: #E8A317 on white = 2.17:1 FAIL; #44483D = 7.25:1 PASS)
- [ ] "New Prospect" text: Outfit/body_small, #386663 (teal)
- [ ] Account info line: Outfit/body_small, #44483D
- [ ] "Today" timestamp: Outfit/body_small, #4C662B, font-weight 500 (highlighted)
- [ ] Other timestamps ("3 days ago", "7 days ago"): Outfit/body_small, #44483D
- [ ] Loading skeleton: 5 customer-card-shaped skeleton blocks, #E1E4D5 fill, shimmer 200ms (short4), reduced-motion fallback = static placeholder
- [ ] Searching skeleton: 3 skeleton cards, same fill/radius as result cards, circle avatar placeholder
- [ ] Empty state: #F9FAEF fill box, 12dp radius, 32dp padding, 16dp H margin, person_search icon centered, body_large #44483D message, "Try Different Search" outlined #4C662B 8dp radius
- [ ] Error banner: #FFDAD6 fill (error_container), error_outline icon, "Search failed" message, "Retry" outlined button #4C662B
- [ ] "Onboard New Customer" — filled, #4C662B bg, #FFFFFF text, full-width, 14dp V padding, person_add leading icon, Outfit/label_large, 12dp radius, 8dp top margin, 24dp bottom margin
- [ ] "Onboard Business Customer" — outlined, #386663 border+text, full-width, business leading icon, Outfit/label_large, 8dp radius
- [ ] All text: Outfit typeface. Touch targets 48dp minimum. 16dp horizontal content padding.
- [ ] Bottom navigation: Customers tab active indicator (#DCE7C8 pill), 80dp nav bar height

---

_Generated by /idea export | 2026-05-30_
