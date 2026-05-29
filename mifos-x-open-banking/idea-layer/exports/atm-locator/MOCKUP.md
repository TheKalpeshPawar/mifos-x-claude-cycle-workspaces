# MOCKUP — ATM & Branch Locator

**Archetype:** index_list
**Shell:** Bottom navigation bar (Home/Accounts/Pay/Cards/More). No top app bar back arrow — this is a direct nav destination.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│                                     │  ← No TopAppBar; screen-level title below
│  ATM & Branches                     │  ← headline_large, #4C662B, shimmer on rest
│                                     │
│  ┌─────────────────────────────────┐│
│  │ 🔍  Enter city, postcode...     ││  ← Search input, pill radius, #F9FAEF
│  └─────────────────────────────────┘│
│                                     │
│  [All] [ATMs] [Branches] [24/7]     │  ← filter chips row, All selected (#4C662B)
│                                     │
│  ┌─────────────────────────────────┐│
│  │  ████████████████████████████  ││  ← Map area skeleton (240dp, #E1E4D5 shimmer)
│  │  ████████████████████████████  ││
│  │  ████████████████████████████  ││
│  └─────────────────────────────────┘│
│                                     │
│  ████████████████████               │  ← Results header skeleton
│                                     │
│  ┌─────────────────────────────────┐│
│  │  ██████████████████████████████││  ← Card skeleton 1
│  │  ████████████  ████████         ││
│  └─────────────────────────────────┘│
│  ┌─────────────────────────────────┐│
│  │  ██████████████████████████████││  ← Card skeleton 2
│  └─────────────────────────────────┘│
├─────────────────────────────────────┤
│ 🏠    💳    ↗    💳    ···          │  ← Bottom nav, Cards tab active indicator
└─────────────────────────────────────┘
```

**Layout notes:** Shimmer applied to map area, results header, and result cards. Search input and filter chips remain interactive during load.

---

## Screen: location_denied

```
┌─────────────────────────────────────┐
│                                     │
│  ATM & Branches                     │  ← headline_large, #4C662B
│                                     │
│  ┌─────────────────────────────────┐│
│  │ 🔍  Enter city, postcode...     ││  ← Search input
│  └─────────────────────────────────┘│
│                                     │
│  ┌─────────────────────────────────┐│
│  │ Use my location for nearby ATMs ││  ← Permission banner: #DCE7C8 bg, #4C662B border
│  │                    [Enable]     ││  ← text button #4C662B
│  └─────────────────────────────────┘│
│                                     │
│  [All] [ATMs] [Branches] [24/7]     │  ← filter chips
│                                     │
│  (no map — awaiting permission)     │
│                                     │
├─────────────────────────────────────┤
│ 🏠    💳    ↗    💳    ···          │
└─────────────────────────────────────┘
```

**Layout notes:** Permission banner is 8dp radius, 1px #4C662B border, 12dp padding, 16dp horizontal margin. "Enable" is a text-variant button right-aligned. Map area hidden until permission granted.

---

## Screen: content

```
┌─────────────────────────────────────┐
│                                     │
│  ATM & Branches                     │  ← headline_large, #4C662B, 24dp top padding
│                                     │
│  ┌─────────────────────────────────┐│
│  │ 🔍  Enter city, postcode...     ││  ← search, pill radius 28, #F9FAEF bg
│  └─────────────────────────────────┘│
│                                     │
│  ┌─────────────────────────────────┐│
│  │  [MAP — ATM pins: 3 markers]    ││  ← 240dp, radius 12, real map tile
│  │                                 ││     ATM pins in #4C662B
│  │         [Oxford St ●]           ││
│  │  [Bond St ●]         [Mayfair ●]││
│  └─────────────────────────────────┘│
│                                     │
│  ← [All] [ATMs] [Branches] [24/7] → │  ← horizontal scroll chips
│     ████  (All selected #4C662B)    │
│                                     │
│  3 ATMs found within 500m           │  ← title_medium, #1A1C16
│                                     │
│  ┌─────────────────────────────────┐│
│  │ Mifos ATM — Oxford Street        ││  ← title_small, #1A1C16, weight 600
│  │ 0.2km away                      ││  ← body_small, #44483D
│  │ Open 24/7             [Get Directions →]│ ← #4C662B · body_small/#4C662B
│  │ £300 max withdrawal              ││  ← body_small, #44483D
│  └─────────────────────────────────┘│
│                                     │
│  ┌─────────────────────────────────┐│
│  │ Mifos ATM — Bond Street Station  ││  ← title_small, #1A1C16, weight 600
│  │ 0.5km away                      ││
│  │ Open 24/7             [Get Directions →]│
│  └─────────────────────────────────┘│
│                                     │
│  ┌─────────────────────────────────┐│
│  │ Mifos Branch — Mayfair           ││
│  │ 0.8km away                      ││
│  │ Mon–Fri 9am–5pm       [Get Directions →]│ ← hours: #44483D
│  │ Services: Cashier · FX · Safe Deposit │
│  └─────────────────────────────────┘│
│  ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ │  ← divider #E1E4D5
│                                     │
├─────────────────────────────────────┤
│ 🏠    🏦    ↗    💳    ···          │  ← bottom nav, More tab navigates to Settings
└─────────────────────────────────────┘
```

**Layout notes:**
- Map area: 240dp height, 12dp radius, 16dp horizontal margin. Map renders with ATM/branch pin markers when location available.
- Filter chips row: horizontal scroll, 8dp gap, 16dp left padding. Selected chip: #4C662B fill + #FFFFFF text. Unselected: #F9FAEF fill + #1A1C16 text + 1px #C5C8BA border.
- Result cards: 12dp radius, 2dp elevation, 16dp padding, 16dp horizontal margin, 8dp gap between cards.
- "Get Directions" links: right-aligned, label_medium #4C662B, trailing directions icon 20dp.
- "Open 24/7" text: #4C662B. Non-24/7 hours: #44483D.

---

## Screen: empty

```
┌─────────────────────────────────────┐
│                                     │
│  ATM & Branches                     │
│                                     │
│  ┌─────────────────────────────────┐│
│  │ 🔍  No results for "Birmingham" ││
│  └─────────────────────────────────┘│
│                                     │
│  [All] [ATMs] [Branches] [24/7]     │
│                                     │
│                                     │
│    location_off icon (48dp, #44483D)│  ← centered
│                                     │
│   No ATMs or branches found         │
│        in this area                 │  ← body_large, #1A1C16, centered
│                                     │
├─────────────────────────────────────┤
│ 🏠    🏦    ↗    💳    ···          │
└─────────────────────────────────────┘
```

**Layout notes:** Empty state icon + message centred. Search bar and filter chips remain active for new searches.

---

## Screen: error

```
┌─────────────────────────────────────┐
│                                     │
│  ATM & Branches                     │
│                                     │
│  ┌─────────────────────────────────┐│
│  │ 🔍  Enter city, postcode...     ││
│  └─────────────────────────────────┘│
│                                     │
│              ⚠                      │  ← error icon 48dp, #BA1A1A
│                                     │
│   Unable to load ATMs.              │
│   Check your connection             │
│       and try again.                │  ← body_medium, #44483D, centered
│                                     │
│          [ Try Again ]              │  ← filled #4C662B, centered
│                                     │
├─────────────────────────────────────┤
│ 🏠    🏦    ↗    💳    ···          │
└─────────────────────────────────────┘
```

**Layout notes:** Map area, filter chips, and result list hidden on error. Error icon + message + retry centred below search input.

---

## Design Checklist (Figma / Stitch)

- [ ] Screen title "ATM & Branches" headline_large in #4C662B with 24dp top padding
- [ ] Search input with pill radius (28dp), leading search icon, #F9FAEF background
- [ ] Location permission banner: #DCE7C8 bg, 1px #4C662B border, 8dp radius, "Enable" text button
- [ ] Map area: 240dp height, 12dp radius, 16dp horizontal margin, #E1E4D5 placeholder until loaded
- [ ] Filter chip row horizontally scrollable: selected chip #4C662B fill, unselected transparent + border
- [ ] Results count header: title_medium, #1A1C16, h2 role
- [ ] Result cards: white fill, 12dp radius, 2dp elevation, 16dp padding, 8dp vertical gap
- [ ] "Open 24/7" label in #4C662B; non-24/7 hours in #44483D
- [ ] "Get Directions" links: label_medium, #4C662B, trailing directions icon, right-aligned
- [ ] Skeleton shimmer covers map area and all result cards on loading state
- [ ] Empty state: location_off icon 48dp + message centered
- [ ] Error state: warning icon 48dp + message + retry button centered
- [ ] Bottom nav visible with correct 5 tabs; active tab indicator #DCE7C8
- [ ] All text Outfit typeface; minimum 14sp for body content
- [ ] 16dp horizontal content padding throughout
