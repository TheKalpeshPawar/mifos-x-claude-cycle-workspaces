# MOCKUP — Beneficiaries

**Archetype:** index_list
**Shell:** Top app bar ("Beneficiaries") with back arrow and filter_list action. No bottom navigation bar.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│ ←  Beneficiaries              [≡]   │  ← TopAppBar, arrow_back + filter_list action
├─────────────────────────────────────┤
│                                     │
│  ┌─────────────────────────────────┐│
│  │ 🔍  Search beneficiaries...    ││  ← search input, pill radius, #F9FAEF
│  └─────────────────────────────────┘│
│                                     │
│  ████████████████                   │  ← "Recently Used" header skeleton
│                                     │
│  ┌─────────────────────────────────┐│
│  │  (●)  ████████████████████████  ││  ← avatar skeleton + name skeleton
│  │       ████████   ██████████     ││  ← bank + payment skeletons
│  └─────────────────────────────────┘│
│  ┌─────────────────────────────────┐│
│  │  (●)  ████████████████████████  ││
│  └─────────────────────────────────┘│
│  ┌─────────────────────────────────┐│
│  │  (●)  ████████████████████████  ││
│  └─────────────────────────────────┘│
│  ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ │  ← divider skeleton
│  ████████████████                   │  ← "All Beneficiaries" header skeleton
│  ┌─────────────────────────────────┐│
│  │  [●]  ████████████████████████  ││  ← bank logo skeleton + name
│  └─────────────────────────────────┘│
│  ┌─────────────────────────────────┐│
│  │  [●]  ████████████████████████  ││
│  └─────────────────────────────────┘│
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** 6-item skeleton list. Avatar circles are 44dp. Bank logo placeholders are 32×32dp. No FAB during loading.

---

## Screen: content

```
┌─────────────────────────────────────┐
│ ←  Beneficiaries              [≡]   │  ← filter_list icon action
├─────────────────────────────────────┤
│                                     │
│  ┌─────────────────────────────────┐│
│  │ 🔍  Search beneficiaries...    ││  ← search, pill radius 28, leading search icon
│  └─────────────────────────────────┘│
│                                     │
│  Recently Used                      │  ← title_medium, #1A1C16, semibold
│                                     │
│  ┌─────────────────────────────────┐│
│  │  (JS)  John Smith               ││  ← 44dp circle, #4C662B bg, #FFFFFF "JS"
│  │        Barclays UK              ││  ← body_small, #44483D
│  │        £500 · 2 days ago        ││  ← body_small, #386663
│  └─────────────────────────────────┘│
│                                     │
│  ┌─────────────────────────────────┐│
│  │  (SW)  Sarah Williams           ││  ← 44dp circle, #386663 bg, #FFFFFF "SW"
│  │        HSBC UK                  ││
│  │        £1,200 · 5 days ago      ││  ← body_small, #386663
│  └─────────────────────────────────┘│
│                                     │
│  ┌─────────────────────────────────┐│
│  │  (MC)  Michael Chen             ││  ← 44dp circle, #4C662B bg, #FFFFFF "MC"
│  │        Lloyds Bank              ││
│  └─────────────────────────────────┘│
│                                     │
│  ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ │  ← divider #E1E4D5, 1px
│                                     │
│  All Beneficiaries          [sort↕] │  ← title_medium + sort icon #4C662B
│                                     │
│  ┌─────────────────────────────────┐│
│  │  [NW]  James Anderson           ││  ← NatWest logo 32×32, radius 4
│  │        GB29 NWBK ··· 8819       ││  ← body_small/#44483D, monospace
│  │        Last: 12 May 2026        ││  ← body_small, #44483D
│  └─────────────────────────────────┘│
│                                     │
│  ┌─────────────────────────────────┐│
│  │  [S]   Priya Patel              ││  ← Santander logo 32×32
│  │        GB72 ABBY ··· 4421       ││  ← monospace, #44483D
│  └─────────────────────────────────┘│
│                                     │
│                                     │
│                          [+ Add Beneficiary]│ ← FAB: #4C662B fill, person_add icon,
│                                     │        elevation 6, bottom-right floating
└─────────────────────────────────────┘
```

**Layout notes:**
- Search bar: 28dp radius (pill), 16dp horizontal margin, #F9FAEF background, leading search icon + trailing clear icon.
- Avatar circles: 44dp diameter, initials in title_medium/bold/white.
- Beneficiary cards: white fill, 12dp radius, 1dp elevation, 14dp vertical padding, 16dp horizontal padding.
- Section divider: #E1E4D5, 1px, 8dp vertical padding.
- "All Beneficiaries" row: space-between layout with sort icon 24dp in #4C662B.
- Bank logos: 32×32dp, 4dp radius, content_scale fit.
- IBAN text: body_small, #44483D, monospace font family.
- FAB: 56dp, #4C662B fill, 16dp radius, elevation 6, person_add icon, "Add Beneficiary" label, floating bottom-right with 16dp margin.

---

## Screen: searching

```
┌─────────────────────────────────────┐
│ ←  Beneficiaries              [≡]   │
├─────────────────────────────────────┤
│                                     │
│  ┌─────────────────────────────────┐│
│  │ 🔍  john                 [✕]   ││  ← search active, trailing clear button
│  └─────────────────────────────────┘│
│                                     │
│  ┌─────────────────────────────────┐│
│  │  (JS)  John Smith               ││  ← filtered result
│  │        Barclays UK              ││
│  │        £500 · 2 days ago        ││
│  └─────────────────────────────────┘│
│                                     │
│                          [+ Add Beneficiary]│
└─────────────────────────────────────┘
```

**Layout notes:** Filtered results shown without section headers. Clear icon (✕) appears in trailing position while text is entered.

---

## Screen: empty

```
┌─────────────────────────────────────┐
│ ←  Beneficiaries              [≡]   │
├─────────────────────────────────────┤
│                                     │
│  ┌─────────────────────────────────┐│
│  │ 🔍  Search beneficiaries...    ││
│  └─────────────────────────────────┘│
│                                     │
│                                     │
│       person_off (48dp, #44483D)    │  ← centered empty icon
│                                     │
│       No beneficiaries yet          │  ← body_large, #1A1C16, centered
│                                     │
│  Add a beneficiary to start         │
│     sending money quickly           │  ← body_medium, #44483D, centered
│                                     │
│                                     │
│                          [+ Add Beneficiary]│
└─────────────────────────────────────┘
```

**Layout notes:** Empty state icon + title + message centred vertically. FAB remains visible for primary action.

---

## Screen: error

```
┌─────────────────────────────────────┐
│ ←  Beneficiaries              [≡]   │
├─────────────────────────────────────┤
│                                     │
│  ┌─────────────────────────────────┐│
│  │ 🔍  Search beneficiaries...    ││
│  └─────────────────────────────────┘│
│                                     │
│         cloud_off (48dp, #44483D)   │  ← error icon
│                                     │
│    Unable to load beneficiaries     │  ← body_large, #1A1C16, centered
│    Check your connection            │
│         and try again               │  ← body_medium, #44483D, centered
│                                     │
│          [ Try Again ]              │  ← filled #4C662B, centered
│                                     │
│                          [+ Add Beneficiary]│
└─────────────────────────────────────┘
```

**Layout notes:** Error icon + message + retry button centred. FAB remains visible.

---

## Design Checklist (Figma / Stitch)

- [ ] M3 TopAppBar with back arrow and filter_list action icon
- [ ] Search input pill radius (28dp), leading search icon, trailing clear, #F9FAEF background
- [ ] "Recently Used" section title_medium/#1A1C16 with 24dp top padding
- [ ] Avatar circles 44dp: John+Michael #4C662B bg, Sarah #386663 bg, white initials title_medium bold
- [ ] Beneficiary cards: white fill, 12dp radius, 1dp elevation, 14dp vertical padding
- [ ] Last payment tint uses secondary color #386663
- [ ] Section divider #E1E4D5, 1px
- [ ] "All Beneficiaries" row: space-between with sort icon #4C662B 24dp
- [ ] Bank logos 32×32dp, 4dp radius, content_scale fit
- [ ] IBAN in monospace body_small, #44483D
- [ ] FAB: #4C662B fill, 16dp radius, person_add icon, elevation 6, floating bottom-right
- [ ] Empty state: person_off 48dp icon centered, descriptive copy
- [ ] Error state: cloud_off 48dp icon + retry button centered
- [ ] Skeleton 6 items matching card layout proportions
- [ ] All text Outfit typeface; minimum 14sp body content
- [ ] 16dp horizontal content padding throughout
