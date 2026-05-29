# MOCKUP — Exchange Rates

**Archetype:** dashboard
**Shell:** No top app bar. No bottom navigation bar (accessed via Home services tile).
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│                                     │
│  Exchange Rates                     │  ← headline_large, #4C662B (visible during load)
│  ████████████████████               │  ← skeleton: timestamp line
│                                     │
│  ┌───────────────────────────────┐  │
│  │ ████████████████████████████  │  │  ← skeleton: converter card
│  │ ████  [GBP 🇬🇧 ▼]           │  │
│  │       ⇅                       │  │
│  │       [EUR 🇪🇺 ▼]           │  │
│  │ = ████████████████████        │  │  ← skeleton: result
│  │ ████████████                  │  │
│  │ ┌─────────────────────────┐   │  │
│  │ │  ████ Send this amount  │   │  │  ← skeleton: CTA
│  │ └─────────────────────────┘   │  │
│  └───────────────────────────────┘  │
│                                     │
│  ── Popular Pairs ─────────────── ──│
│  ┌───────────────────────────────┐  │
│  │ ████████  ███████  ████       │  │  ← skeleton rate rows (×6)
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │ ████████  ███████  ████       │  │
│  └───────────────────────────────┘  │
│  …                                  │
└─────────────────────────────────────┘
```

**Layout notes:** Title visible. Everything else skeleton. Converter card shimmer fills full height.

---

## Screen: content

```
┌─────────────────────────────────────┐
│                                     │
│  Exchange Rates                     │  ← headline_large, #4C662B
│  Rates updated: 14 May 2026, 15:42  │  ← body_small, #44483D
│                                     │
│  ┌───────────────────────────────┐  │  ← Converter card: white, 16dp radius, 4dp elev
│  │  I want to send               │  │  ← label text
│  │  ┌─────────────────────────┐  │  │
│  │  │  1,000                  │  │  │  ← Number input, title_large 700 #4C662B, #F9FAEF
│  │  └─────────────────────────┘  │  │
│  │                               │  │
│  │  From                         │  │
│  │  ┌─────────────────────────┐  │  │
│  │  │  GBP 🇬🇧            ▼  │  │  │  ← Currency select, #F9FAEF
│  │  └─────────────────────────┘  │  │
│  │                               │  │
│  │           ⇅                   │  │  ← swap_vert, 32dp, #4C662B, #CDEDA3 circle
│  │                               │  │
│  │  To                           │  │
│  │  ┌─────────────────────────┐  │  │
│  │  │  EUR 🇪🇺            ▼  │  │  │
│  │  └─────────────────────────┘  │  │
│  │                               │  │
│  │      = 1,167.20 EUR           │  │  ← display_medium, 700, #4C662B, centered
│  │   Rate: 1 GBP = 1.1672 EUR    │  │  ← body_small, #44483D, centered
│  │                               │  │
│  │  ┌─────────────────────────┐  │  │
│  │  │    Send this amount  →  │  │  │  ← filled, #4C662B, label_large, full-width
│  │  └─────────────────────────┘  │  │
│  └───────────────────────────────┘  │
│                                     │
│  ─────────────────────────────────  │  ← divider, #E1E4D5
│                                     │
│  Popular Pairs                      │  ← title_medium, #1A1C16, 600w
│                                     │
│  ┌───────────────────────────────┐  │
│  │  GBP / EUR     1.1672   +0.2%↑│  │  ← pair + rate + green change
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  GBP / USD     1.2834  −0.1%↓ │  │  ← red change
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  GBP / JPY    193.45   +0.4%↑ │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  EUR / USD     1.0993  −0.3%↓ │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  USD / INR     83.22    0.0% — │  │  ← neutral, #44483D, remove icon
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  EUR / GBP     0.8568  −0.2%↓ │  │
│  └───────────────────────────────┘  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:**
- Converter card: 16dp margin horizontal, 16dp padding, 16dp radius, 4dp elevation.
- Amount input: title_large (22sp) 700 weight, #4C662B, #F9FAEF fill.
- Swap icon: circular #CDEDA3 container (16dp radius), swap_vert 32dp #4C662B inside.
- Result: display_medium (45sp) 700 weight, #4C662B, centered.
- Rate rows: #FFFFFF fill, 8dp radius, horizontal layout, space-between. 16dp margin.
- Change colour: positive = #4C662B + arrow_upward; negative = #BA1A1A + arrow_downward; zero = #44483D + remove.
- Tapping any rate row populates the converter with that currency pair.

---

## Screen: error

```
┌─────────────────────────────────────┐
│                                     │
│  Exchange Rates                     │
│                                     │
│                                     │
│  Unable to load exchange rates.     │  ← body_large, center
│  Check your connection and retry.   │  ← body_medium, #44483D
│                                     │
│         ┌─────────────┐             │
│         │    Retry    │             │  ← outlined, #4C662B
│         └─────────────┘             │
│                                     │
└─────────────────────────────────────┘
```

---

## Screen: empty

```
┌─────────────────────────────────────┐
│                                     │
│  Exchange Rates                     │
│                                     │
│     [currency_exchange icon]        │  ← 48dp, #44483D
│                                     │
│  No rates available for the         │  ← title_medium, center
│  selected currencies.               │
│                                     │
│     ┌───────────────────────────┐   │
│     │    Reset to GBP / EUR     │   │  ← text button, #4C662B
│     └───────────────────────────┘   │
│                                     │
└─────────────────────────────────────┘
```

---

## Design Checklist (Figma / Stitch)

- [ ] Screen title "Exchange Rates" — headline_large (Outfit 32sp), #4C662B, 24dp top padding
- [ ] Timestamp — body_small (Outfit 12sp), #44483D, API-driven from effective_date
- [ ] Converter card: #FFFFFF fill, 16dp radius, 4dp elevation, 20dp padding
- [ ] Amount input: title_large (22sp/700) #4C662B, #F9FAEF fill, 8dp radius
- [ ] Currency dropdowns: select input, #F9FAEF fill, arrow_drop_down trailing icon
- [ ] Swap button: swap_vert 32dp icon, #4C662B on #CDEDA3 circular container (16dp radius), 48dp tap target
- [ ] Result display: display_medium (45sp/700) #4C662B, centered
- [ ] Rate info text: body_small #44483D, centered
- [ ] "Send this amount" CTA: filled #4C662B, white label_large text, 12dp radius, full content width
- [ ] Section divider: #E1E4D5, 8dp vertical margin
- [ ] "Popular Pairs" header: title_medium (16sp/600), #1A1C16
- [ ] Rate rows: #FFFFFF fill, 8dp radius, horizontal layout, space-between, 16dp margin
- [ ] Change indicator: #4C662B + arrow_upward (positive) / #BA1A1A + arrow_downward (negative) / #44483D + remove (zero)
- [ ] All rate rows tappable — populates converter with that pair
- [ ] Skeleton shimmer during loading for converter card and all rate rows
- [ ] All text: Outfit typeface. 16dp horizontal content padding throughout.
