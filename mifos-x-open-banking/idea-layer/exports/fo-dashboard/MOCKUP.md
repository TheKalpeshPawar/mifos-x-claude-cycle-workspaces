# MOCKUP — Field Officer Dashboard

**Archetype:** dashboard
**Shell:** fieldOfficer bottom navigation bar (Dashboard/Customers/Applications/Messages/More). Top app bar with profile + settings icons (absolute positioned).
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│                          ⚙  👤      │  ← Settings + Profile icons, absolute top-right
├─────────────────────────────────────┤
│  Good morning, Priya 👋             │  ← headline_medium, #4C662B (visible during loading)
│  Mon, 25 May 2026 · Mifos Nairobi   │  ← body_medium, #44483D
│                                     │
│  ┌──────────────┐ ┌──────────────┐  │
│  │  ████████    │ │  ████████    │  │  ← Skeleton KPI cards (2-column grid)
│  │  ████████    │ │  ████████    │  │
│  └──────────────┘ └──────────────┘  │
│  ┌──────────────┐ ┌──────────────┐  │
│  │  ████████    │ │  ████████    │  │
│  │  ████████    │ │  ████████    │  │
│  └──────────────┘ └──────────────┘  │
│                                     │
│  Action Needed                      │  ← Skeleton section
│  ┌───────────────────────────────┐  │
│  │ ████████████████  [████████]  │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │ ████████████████  [████████]  │  │
│  └───────────────────────────────┘  │
│                                     │
│  Today's Schedule                   │
│  ┌───────────────────────────────┐  │
│  │ ████████  ████████████████    │  │
│  └───────────────────────────────┘  │
│                                     │
├─────────────────────────────────────┤
│  [dashboard] [people] [desc] [mail] [more] │  ← Bottom nav, Dashboard active
└─────────────────────────────────────┘
```

**Layout notes:** Greeting + date visible during loading; everything else skeletons.

---

## Screen: content

```
┌─────────────────────────────────────┐
│                          ⚙  👤      │
├─────────────────────────────────────┤
│  Good morning, Priya 👋             │
│  Mon, 25 May 2026 · Mifos Nairobi   │
│                                     │
│  ┌──────────────┐ ┌──────────────┐  │
│  │ 124          │ │  5           │  │  ← display_small values
│  │ Active       │ │  Pending     │  │  ← body_medium labels
│  │ Customers    │ │  Applications│  │
│  └──────────────┘ └──────────────┘  │
│  ┌──────────────┐ ┌──────────────┐  │
│  │  3           │ │  2           │  │
│  │  KYC Pending │ │  Meetings    │  │
│  │              │ │  Today       │  │
│  └──────────────┘ └──────────────┘  │
│                                     │
│  Action Needed                      │  ← title_large, 700 weight
│                                     │
│  ┌───────────────────────────────┐  │  ← KYC expiry alert, amber left border
│  │ ⚠ John Mwangi — KYC in 3 days│  │
│  │                  [Review KYC] │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │  ← Overdue app, red left border
│  │ ⚠ Sarah Odhiambo — 7 days    │  │
│  │             [View Application]│  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │  ← New lead, green left border
│  │ ✦ New lead: Peter Kamau       │  │
│  │            [Start Onboarding] │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │  ← Corporate inquiry
│  │ Acme Trading Ltd — Biz inquiry│  │
│  │       [Start Corporate Onb.]  │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │  ← Agent registration
│  │ Complete Agent Registration   │  │
│  │                    [Register] │  │
│  └───────────────────────────────┘  │
│                                     │
│  Today's Schedule                   │  ← title_medium, 600 weight
│                                     │
│  ┌───────────────────────────────┐  │  ← Meeting row 1, white card
│  │ 10:00 AM  Mary Wanjiku        │  │
│  │           Loan Review         │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │  ← Meeting row 2
│  │  2:30 PM  James Otieno        │  │
│  │           New Account         │  │
│  └───────────────────────────────┘  │
│                                     │
├─────────────────────────────────────┤
│  [dashboard*] [people] [desc!] [mail!] [more] │  ← Active = Dashboard
└─────────────────────────────────────┘
```

**Layout notes:**
- KPI grid: 2 columns, 12dp gap, all cards #CDEDA3 fill except Meetings (#DCE7C8).
- Left border accents: Active Customers = #4C662B · Pending Apps = #E8A317 · KYC = #BA1A1A · Meetings = #386663.
- KPI values: display_small (32sp/600). Labels: body_medium (14sp/500).
- Alert rows: #CDEDA3 fill, 12dp radius, 4dp coloured left border, row layout.
- Alert action buttons: outlined, small, contrast-safe text (#44483D for amber border, #BA1A1A for red, #4C662B for green).
- Meeting time column: 72dp fixed width, label_large #4C662B 600 weight.
- Meeting card: #FFFFFF fill, 10dp radius, 1dp elevation.

---

## Screen: error

```
┌─────────────────────────────────────┐
│                          ⚙  👤      │
├─────────────────────────────────────┤
│  Good morning, Priya 👋             │
│  Mon, 25 May 2026 · Mifos Nairobi   │
│                                     │
│                                     │
│  Unable to load dashboard data.     │  ← body_large, center
│  Check your connection and          │
│  try again.                         │
│                                     │
│         ┌─────────────┐             │
│         │    Retry    │             │  ← outlined, #4C662B
│         └─────────────┘             │
│                                     │
├─────────────────────────────────────┤
│  [dashboard] [people] [desc] [mail] [more] │
└─────────────────────────────────────┘
```

---

## Screen: empty

```
┌─────────────────────────────────────┐
│                          ⚙  👤      │
├─────────────────────────────────────┤
│  Good morning, Priya 👋             │
│  Mon, 25 May 2026 · Mifos Nairobi   │
│                                     │
│     [dashboard_customize icon]      │  ← 48dp, #44483D
│                                     │
│  No dashboard data available yet.   │  ← title_medium, center
│  Start by onboarding a customer.    │  ← body_medium, #44483D, center
│                                     │
│     ┌───────────────────────────┐   │
│     │   Onboard a Customer      │   │  ← filled, #4C662B
│     └───────────────────────────┘   │
│                                     │
├─────────────────────────────────────┤
│  [dashboard] [people] [desc] [mail] [more] │
└─────────────────────────────────────┘
```

---

## Design Checklist (Figma / Stitch)

- [ ] Greeting in headline_medium (Outfit 28sp), earth-green #4C662B
- [ ] Profile icon (32dp) and settings icon (24dp) absolute top-right
- [ ] 2-column KPI grid: 12dp gap, 16dp horizontal padding
- [ ] KPI cards: #CDEDA3 fill except Meetings (#DCE7C8), 12dp radius, 4dp coloured left border
- [ ] KPI values: display_small (32sp/700) — colour matches left border accent
- [ ] Pending Applications value #44483D (contrast-safe override for amber background)
- [ ] Alert rows: #CDEDA3 fill, 12dp radius, left border matches urgency colour
- [ ] Alert buttons: outlined, small (label_small), contrast-safe text on #CDEDA3
- [ ] Meeting rows: #FFFFFF fill, 10dp radius, 1dp elevation
- [ ] Meeting time: label_large (14sp/600) #4C662B, 72dp fixed width column
- [ ] "Action Needed" header: title_large (22sp/700), #1A1C16
- [ ] "Today's Schedule" header: title_medium (16sp/600), #1A1C16
- [ ] fieldOfficer bottom nav: Dashboard/Customers/Applications/Messages/More — Application + Messages badges active
- [ ] Shimmer skeleton during loading state on all data-driven sections
- [ ] All text: Outfit typeface. Touch targets 48dp minimum.
- [ ] 16dp horizontal content padding throughout
