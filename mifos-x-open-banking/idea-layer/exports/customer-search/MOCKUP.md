# MOCKUP — Find Customer

**Archetype:** search
**Shell:** Field Officer bottom navigation bar — Customers tab active (people icon). Top app bar hidden on this screen.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: idle (Pre-search)

```
┌─────────────────────────────────────┐
│                                     │  ← Background #F9FAEF
│  Find Customer                      │  ← headline_large #4C662B bold, pad T24/H16
│                                     │
│  ┌──────────────────────────────┐   │
│  │ 🔍 Search by name, ID…       │   │  ← Pill search bar radius 28, #F9FAEF bg
│  └──────────────────────────────┘   │
│                                     │
│  [All ✓] [Active] [Prospect] [Dormant]│  ← Chip row, horizontal scroll
│          "All" chip active #4C662B  │
│                                     │
│  [ ▢ Scan Customer ID         ]     │  ← Outlined #4C662B, qr_code icon, radius 12
│                                     │
│                                     │
│  [ + Onboard New Customer     ]     │  ← Filled #4C662B full-width pill
│  [ 🏢 Onboard Business Customer ]   │  ← Outlined #386663
│                                     │
├─────────────────────────────────────┤
│  [⊞]   [👥★]  [📋]   [✉]   [⋮]   │  ← Customers tab active
└─────────────────────────────────────┘
```

**Layout notes:**
- Title: pad T24, H16, headline_large weight 700.
- Search bar: margin H16/T12, radius 28, #F9FAEF fill, search icon leading, clear icon trailing (when text).
- Filter chips: margin H16/T12/B4, gap 8, horizontal scroll. Active chip: #4C662B bg #FFFFFF text; inactive: outline.
- Scan QR: margin H16/T8/B8, align flex-start (not full-width).
- Onboard buttons: margin H16/T8/B24.

---

## Screen: searching (Loading results)

```
┌─────────────────────────────────────┐
│  Find Customer                      │
│                                     │
│  ┌──────────────────────────────┐   │
│  │ 🔍 John M|                   │   │  ← Query typed, clear button shown
│  └──────────────────────────────┘   │
│  [All ✓] [Active] [Prospect] [Dormant]
│                                     │
│  [ ▢ Scan Customer ID         ]     │
│                                     │
│  ┌──────────────────────────────┐   │
│  │ [██] ████████████  ████      │   │  ← Skeleton card ×3 (shimmer)
│  │      ████████████████████    │   │
│  └──────────────────────────────┘   │
│  ┌──────────────────────────────┐   │
│  │ [██] ████████████  ████      │   │
│  │      ████████████████████    │   │
│  └──────────────────────────────┘   │
│  ┌──────────────────────────────┐   │
│  │ [██] ████████████  ████      │   │
│  └──────────────────────────────┘   │
│                                     │
├─────────────────────────────────────┤
│  [⊞]   [👥★]  [📋]   [✉]   [⋮]   │
└─────────────────────────────────────┘
```

**Layout notes:** Onboard buttons hidden during active search. Skeleton cards replace results area, 3 placeholders.

---

## Screen: results

```
┌─────────────────────────────────────┐
│  Find Customer                      │
│  ┌──────────────────────────────┐   │
│  │ 🔍 John M               ✕   │   │
│  └──────────────────────────────┘   │
│  [All ✓] [Active] [Prospect] [Dormant]
│  [ ▢ Scan Customer ID         ]     │
│                                     │
│  ┌──────────────────────────────┐   │  ← #FFFFFF card, radius 12, elevation 2
│  │ [JM]  John Mwangi            │   │    44×44 #4C662B circle, bold name
│  │       KYC Verified ✓  3d ago │   │    #4C662B KYC text; timestamp right
│  │       Checking · KES 45,200  │   │    #44483D account
│  └──────────────────────────────┘   │
│                                     │
│  ┌──────────────────────────────┐   │
│  │ [SO]  Sarah Odhiambo         │   │    44×44 #E8A317 circle (KYC pending)
│  │       KYC Pending ⚠   7d ago │   │    #44483D KYC text (a11y corrected)
│  │       Application in Review  │   │
│  └──────────────────────────────┘   │
│                                     │
│  ┌──────────────────────────────┐   │
│  │ [PK]  Peter Kamau            │   │    44×44 #386663 circle (prospect)
│  │       New Prospect    Today  │   │    #386663 status; Today in #4C662B
│  │       No account yet         │   │
│  └──────────────────────────────┘   │
│                                     │
│  [ + Onboard New Customer     ]     │
│  [ 🏢 Onboard Business Customer ]   │
├─────────────────────────────────────┤
│  [⊞]   [👥★]  [📋]   [✉]   [⋮]   │
└─────────────────────────────────────┘
```

**Layout notes:** Cards margin H16/B8, pad 14, direction row. Avatar 44×44 flex-shrink 0, margin R12. Right side column: name (title_small bold), status row (body_small), account row (body_small), last interaction (body_small aligned flex-start).

---

## Screen: no_results

```
┌─────────────────────────────────────┐
│  Find Customer                      │
│  ┌──────────────────────────────┐   │
│  │ 🔍 Xyz_                 ✕   │   │
│  └──────────────────────────────┘   │
│  [All ✓] [Active] [Prospect] [Dormant]
│                                     │
│  ┌──────────────────────────────┐   │  ← #F9FAEF empty state box, radius 12
│  │                              │   │    centered content
│  │     👤                       │   │    person_search icon 48dp
│  │  No customers found          │   │    body_large #44483D center
│  │  for this search             │   │
│  │  [ Try Different Search ]    │   │    Outlined #4C662B
│  └──────────────────────────────┘   │
│                                     │
│  [ + Onboard New Customer     ]     │
│  [ 🏢 Onboard Business Customer ]   │
├─────────────────────────────────────┤
│  [⊞]   [👥★]  [📋]   [✉]   [⋮]   │
└─────────────────────────────────────┘
```

---

## Screen: error

```
┌─────────────────────────────────────┐
│  Find Customer                      │
│  ┌──────────────────────────────┐   │
│  │ 🔍 Search by name, ID…       │   │
│  └──────────────────────────────┘   │
│                                     │
│  ┌──────────────────────────────┐   │
│  │ ⚠ Search failed.             │   │  ← Error banner #FFDAD6
│  │   Check your connection.     │   │
│  │       [ Try Again ]          │   │
│  └──────────────────────────────┘   │
│                                     │
├─────────────────────────────────────┤
│  [⊞]   [👥★]  [📋]   [✉]   [⋮]   │
└─────────────────────────────────────┘
```

---

## Design Checklist (Figma / Stitch)

- [ ] Search bar: pill radius 28, #F9FAEF fill, search icon, clear ✕ when text present
- [ ] Filter chips: 4 radio chips, horizontal scroll overflow, gap 8; active=#4C662B bg, inactive=outline
- [ ] Scan QR: outlined #4C662B button, qr_code leading icon, align-start (not full-width), radius 12
- [ ] Result cards: #FFFFFF, radius 12, elevation 2, pad 14; row with 44dp avatar circle + text column
- [ ] Avatar colors: John=#4C662B, Sarah=#E8A317 (amber for pending), Peter=#386663 (teal for prospect)
- [ ] KYC Verified: body_small #4C662B; KYC Pending: body_small #44483D (contrast-corrected); New Prospect: #386663
- [ ] "Today" timestamp: #4C662B weight 500 (stands out); other timestamps: #44483D
- [ ] Empty state: radius 12, pad 32, person_search icon 48dp, body_large centered, outlined Try Different Search
- [ ] Onboard New Customer: filled full-width pill #4C662B, person_add icon; below both results and empty state
- [ ] Onboard Business Customer: outlined #386663, business icon
- [ ] Skeleton cards: 3×, avatar placeholder circle + 2 text row skeletons, shimmer animation
- [ ] Field Officer bottom nav: Customers tab active, people icon
