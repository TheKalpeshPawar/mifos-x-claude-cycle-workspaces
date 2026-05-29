# MOCKUP — Meetings

**Archetype:** index_list
**Shell:** Top app bar ("Meetings") with back arrow. Field Officer bottom navigation bar (5 tabs).
**Accent:** #4C662B (Earth-green primary). Typography: Outfit. Design system: M3.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│ ←  Meetings                          │  ← M3 TopAppBar
├─────────────────────────────────────┤
│  ████████████████████  (skeleton)   │  ← Title shimmer
│                                     │
│  ┌──┐┌──┐┌──┐┌──┐┌──┐┌──┐┌──┐     │  ← 7 day-pill skeletons
│  └──┘└──┘└──┘└──┘└──┘└──┘└──┘     │
│                                     │
│  ██████████████  (skeleton)         │  ← Section header shimmer
│                                     │
│  ┌───────────────────────────────┐  │
│  │  ███████████  ███  ████████   │  │  ← Meeting card skeleton
│  │  ████████████████████████████ │  │
│  │  ████████████████             │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  ███████████  ███  ████████   │  │
│  │  ████████████████████████████ │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  ███████████  ███  ████████   │  │
│  │  ████████████████████████████ │  │
│  └───────────────────────────────┘  │
├─────────────────────────────────────┤
│  ⊞     👥     📄     ✉     ⋮      │  ← Field Officer bottom nav
└─────────────────────────────────────┘
```

---

## Screen: content (Primary)

```
┌─────────────────────────────────────┐
│ ←  Meetings                          │  ← M3 TopAppBar
├─────────────────────────────────────┤
│                                     │
│  Meetings · May 2026                │  ← headline_large #4C662B weight 700
│                                     │
│  ┌─────────────────────────────┐    │
│  │Mon Tue[Wed]Thu Fri Sat Sun  │    │  ← 7-day strip
│  │ 19  20 [21] 22  23  24  25 │    │    Wed: #4C662B bg, white text
│  └─────────────────────────────┘    │    Others: #F9FAEF bg, #1A1C16/#44483D text
│  Today                              │  ← text button #4C662B
│                                     │
│  3 meetings this week               │  ← title_medium #1A1C16
│                                     │
│  ┌───────────────────────────────┐  │
│  ║10:00 AM          [Online]     ║  │  ← Left accent 4dp #4C662B
│  │ Account Opening Meeting       │  │    Time: label_large #4C662B bold
│  │ John Mwangi · 1 hr · Google Meet│    Title: title_small #1A1C16 bold
│  │ [Join ▶] [Notes 📝]           │  │    Customer: body_medium #44483D
│  └───────────────────────────────┘  │    Online chip: #CDEDA3 bg, #4C662B text
│                                     │    Join: filled #4C662B; Notes: outlined #4C662B
│  ┌───────────────────────────────┐  │
│  ║2:00 PM          [In-Person]   ║  │  ← Left accent 4dp #386663
│  │ KYC Review                    │  │    Time: label_large #386663 bold
│  │ Sarah Odhiambo · 30 min       │  │    In-Person chip: #DCE7C8 bg, #386663 text
│  │ Nairobi Branch, Kimathi St    │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  ║Tomorrow · 11:00 AM    [Phone] ║  │  ← Left accent 4dp #E8A317
│  │ New Prospect — Introductory   │  │    Time: label_large #44483D bold
│  │ Call                          │  │    Phone chip: #CDEDA3 bg, #44483D text
│  │ Peter Kamau · Referral from   │  │
│  │ Equity Bank                   │  │
│  └───────────────────────────────┘  │
│                                     │
│                         [+Schedule] │  ← Extended FAB bottom-right
│                                     │    #4C662B bg, calendar_add icon + "Schedule Meeting"
├─────────────────────────────────────┤
│  ⊞     👥     📄     ✉     ⋮      │  ← Field Officer bottom nav
└─────────────────────────────────────┘
```

**Layout notes:**
- Title: 20dp horizontal padding, 20dp top, 12dp bottom.
- Day strip: 12dp horizontal padding, 4dp gap between pills. Each pill 8dp vertical + 10dp horizontal.
- "Today" button: 16dp horizontal padding, 4dp bottom margin.
- Section header: 16dp horizontal padding, 8dp top, 10dp bottom.
- Meeting cards: 16dp horizontal margin, 10dp bottom margin, 16dp internal padding, 12dp radius, elevation 2.
- Each card: 4dp left accent border (colored per type).
- Extended FAB: fixed bottom-right, 24dp bottom margin, 16dp right margin, elevation 6.

---

## Screen: content (Schedule Dialog open)

```
┌─────────────────────────────────────┐
│  [... content layout dimmed ...]    │  ← Scrim 50% opacity over content
│                                     │
│  ╔═════════════════════════════════╗ │
│  ║  Schedule Meeting               ║ │  ← Dialog, 20dp radius, white, 20dp padding
│  ║                                 ║ │    title_medium #1A1C16 bold
│  ║  ┌─────────────────────────┐   ║ │
│  ║  │ Customer       ▼        │   ║ │  ← Autocomplete, outlined
│  ║  │ Search customers…       │   ║ │
│  ║  └─────────────────────────┘   ║ │
│  ║  ┌─────────────────────────┐   ║ │
│  ║  │ Date & Time      📅     │   ║ │  ← Outlined text + calendar suffix icon
│  ║  │ 22 May 2026 · 10:00 AM  │   ║ │
│  ║  └─────────────────────────┘   ║ │
│  ║  ┌─────────────────────────┐   ║ │
│  ║  │ Duration         ▼      │   ║ │  ← Select dropdown
│  ║  └─────────────────────────┘   ║ │
│  ║  ┌─────────────────────────┐   ║ │
│  ║  │ Meeting Type     ▼      │   ║ │  ← Select dropdown
│  ║  └─────────────────────────┘   ║ │
│  ║  ┌─────────────────────────┐   ║ │
│  ║  │ Notes                   │   ║ │  ← Outlined textarea, 3–6 lines
│  ║  │ Agenda, location…       │   ║ │
│  ║  └─────────────────────────┘   ║ │
│  ║  ┌─────────────────────────┐   ║ │
│  ║  │     Confirm Meeting     │   ║ │  ← Filled #4C662B, full-width
│  ║  └─────────────────────────┘   ║ │
│  ╚═════════════════════════════════╝ │
└─────────────────────────────────────┘
```

---

## Screen: empty

```
┌─────────────────────────────────────┐
│ ←  Meetings                          │
├─────────────────────────────────────┤
│  Meetings · May 2026                │
│                                     │
│  ┌──┐┌──┐┌──┐┌──┐┌──┐┌──┐┌──┐     │  ← Calendar strip unchanged
│  └──┘└──┘└──┘└──┘└──┘└──┘└──┘     │
│  Today                              │
│                                     │
│              📅                     │  ← event_available 48dp #75796C centered
│                                     │
│       No Meetings Scheduled         │  ← headline_small #1A1C16 centered
│  Tap the button below to schedule   │
│  your first meeting for this week   │  ← body_medium #44483D centered
│                                     │
│                         [+Schedule] │  ← FAB still visible
│                                     │
├─────────────────────────────────────┤
│  ⊞     👥     📄     ✉     ⋮      │
└─────────────────────────────────────┘
```

---

## Screen: error

```
┌─────────────────────────────────────┐
│ ←  Meetings                          │
├─────────────────────────────────────┤
│                                     │
│              ⚠                      │  ← Error icon 48dp #BA1A1A centered
│                                     │
│   Could not load meetings           │  ← body_large #1A1C16 centered
│   Check your connection and         │
│   try again.                        │  ← body_medium #44483D centered
│                                     │
│  ┌───────────────────────────────┐  │
│  │            Retry              │  │  ← Filled #4C662B
│  └───────────────────────────────┘  │
│                                     │
├─────────────────────────────────────┤
│  ⊞     👥     📄     ✉     ⋮      │
└─────────────────────────────────────┘
```

---

## Design Checklist (Figma / Stitch)

- [ ] M3 TopAppBar with back arrow; Field Officer bottom nav (5 tabs)
- [ ] "Meetings · May 2026" headline_large `#4C662B` weight 700
- [ ] 7-day horizontal strip: selected pill `#4C662B` bg + white text; others `#F9FAEF`; weekend dates muted `#44483D`
- [ ] "Today" text button in `#4C662B`
- [ ] 3 meeting cards: white surface, 12dp radius, elevation 2, 4dp left accent border (green/teal/amber)
- [ ] Online chip: `#CDEDA3` bg, `#4C662B` text, 12dp radius
- [ ] In-Person chip: `#DCE7C8` bg, `#386663` text, 12dp radius
- [ ] Phone chip: `#CDEDA3` bg, `#44483D` text, 12dp radius
- [ ] Meeting 1 inline actions: "Join" filled `#4C662B` + "Notes" outlined `#4C662B`, 8dp gap
- [ ] Extended FAB: `#4C662B` bg, calendar_add icon, "Schedule Meeting", bottom-right, elevation 6
- [ ] Schedule dialog: 20dp radius, all 5 inputs, Confirm button full-width filled `#4C662B`
- [ ] All text Outfit typeface; 16dp standard horizontal padding
