# MOCKUP — My Cards

**Archetype:** index_list
**Shell:** Bottom navigation bar (Home/Accounts/Pay/Cards/More). Top app bar ("My Cards") with notifications_outlined action.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│  My Cards                  [🔔]     │  ← TopAppBar, notifications_outlined, #F9FAEF
├─────────────────────────────────────┤
│                                     │
│  My Cards                           │  ← headline_large, #4C662B (visible during load)
│                                     │
│  ┌──────────────────────────────┐   │
│  │  ████████████████████████   │   │  ← Card carousel skeleton (320×200dp shimmer)
│  │  ████████████████████████   │   │
│  │  ████████████████████████   │   │
│  └──────────────────────────────┘   │
│                                     │
│  [████] [████] [████] [████]        │  ← Quick action buttons skeleton (4 pills)
│                                     │
│  ████████████████████████           │  ← "Card Transactions" header skeleton
│                                     │
│  ┌─────────────────────────────────┐│
│  │  ████████████████  ████████████ ││  ← Transaction row skeleton 1
│  └─────────────────────────────────┘│
│  ┌─────────────────────────────────┐│
│  │  ████████████████  ████████████ ││  ← Transaction row skeleton 2
│  └─────────────────────────────────┘│
│  ┌─────────────────────────────────┐│
│  │  ████████████████  ████████████ ││  ← Transaction row skeleton 3
│  └─────────────────────────────────┘│
│                                     │
├─────────────────────────────────────┤
│ 🏠    🏦    ↗    💳    ···          │  ← Bottom nav, Cards tab active (#DCE7C8 indicator)
└─────────────────────────────────────┘
```

**Layout notes:** Carousel skeleton is 320×200dp matching card visual dimensions. Quick-action skeleton shows 4 evenly-spaced pill placeholders. 3 transaction row skeletons.

---

## Screen: content

```
┌─────────────────────────────────────┐
│  My Cards                  [🔔]     │  ← TopAppBar
├─────────────────────────────────────┤
│                                     │
│  My Cards                           │  ← headline_large, #4C662B, 4dp bottom
│                                     │
│  ← ┌────────────────────────────┐ → │  ← horizontal scroll carousel
│    │                            │   │
│    │  •••• •••• •••• 4521       │   │  ← title_large/#FFFFFF/monospace/spacing 4
│    │                            │   │  ← #4C662B gradient card, 320×200dp, radius 20
│    │  Alex Johnson        [VISA]│   │  ← body_large/#CDEDA3 upper · Visa logo 56×20
│    │  [Active]                  │   │  ← badge: #4C662B bg/#FFFFFF text, radius 12
│    └────────────────────────────┘   │
│       ┌──────────────────────────┐  │
│       │  •••• •••• •••• 7834    │  │  ← 2nd card (partially visible in carousel)
│       │  #386663 gradient       │  │
│       │  [Frozen]               │  │  ← badge: #C5C8BA bg/#FFFFFF text
│       └──────────────────────────┘  │
│                                     │
│   [❄ Freeze] [⚙ Limit] [# PIN] [⚠ Report]│ ← quick actions, evenly spaced
│    #4C662B ×3             #BA1A1A   │  ← label_small, icon above label
│                                     │
│  Card Transactions                  │  ← title_large, #1A1C16, weight 600
│                                     │
│  ┌─────────────────────────────────┐│
│  │  Netflix            -£15.99     ││  ← merchant body_large/#1A1C16 · amount #BA1A1A
│  │  20 May 2026                    ││  ← body_small/#44483D
│  └─────────────────────────────────┘│
│  ┌─────────────────────────────────┐│
│  │  Tesco Express      -£34.56     ││
│  │  19 May 2026                    ││
│  └─────────────────────────────────┘│
│  ┌─────────────────────────────────┐│
│  │  Uber               -£12.40     ││
│  │  18 May 2026                    ││
│  └─────────────────────────────────┘│
│  ┌─────────────────────────────────┐│
│  │  Amazon.co.uk       -£67.99     ││
│  │  17 May 2026                    ││
│  └─────────────────────────────────┘│
│  ┌─────────────────────────────────┐│
│  │  Starbucks           -£5.85     ││
│  │  17 May 2026                    ││
│  └─────────────────────────────────┘│
│                                     │
│  ┌─────────────────────────────────┐│
│  │ [+] Order New Card              ││  ← outlined #4C662B, full-width, add_card icon
│  └─────────────────────────────────┘│
│                                     │
├─────────────────────────────────────┤
│ 🏠    🏦    ↗    💳    ···          │  ← Cards tab active, #DCE7C8 indicator
└─────────────────────────────────────┘
```

**Layout notes:**
- Carousel: horizontal scroll with 16dp gap between cards, 4dp horizontal padding, 8dp vertical. Cards snap to start alignment. Second card partially visible to communicate scrollability.
- Debit Visa card: 320×200dp, radius 20, elevation 8, #4C662B fill. PAN title_large/white/monospace/spacing 4. Name body_large/#CDEDA3/uppercase. Active chip: #4C662B bg, label_small/white.
- Business Mastercard: same dimensions, #386663 fill. Frozen chip: #C5C8BA bg, label_small/white.
- Quick-action row: 4 buttons evenly spaced, each vertical-orientation (icon 20dp above label_small). Freeze/Limit/PIN use #4C662B. Report uses #BA1A1A.
- Transaction cards: white fill, 12dp radius, 1dp elevation, 16dp horizontal/14dp vertical padding, 8dp vertical gap. Amount body_large/#BA1A1A. Date body_small/#44483D.
- Order New Card: outlined, full-width, radius 12, 14dp vertical padding, add_card icon leading, label_large.

---

## Screen: empty

```
┌─────────────────────────────────────┐
│  My Cards                  [🔔]     │
├─────────────────────────────────────┤
│                                     │
│  My Cards                           │
│                                     │
│         credit_card_off             │  ← 48dp icon, #44483D, centered
│                                     │
│         No cards yet                │  ← body_large, #1A1C16, centered
│                                     │
│  Order your first Mifos card        │
│   to start making payments          │  ← body_medium, #44483D, centered
│                                     │
│  ┌─────────────────────────────────┐│
│  │ [+] Order New Card              ││  ← outlined #4C662B, full-width
│  └─────────────────────────────────┘│
│                                     │
├─────────────────────────────────────┤
│ 🏠    🏦    ↗    💳    ···          │
└─────────────────────────────────────┘
```

**Layout notes:** Empty state icon + title + description centered. Order New Card button full-width with 16dp horizontal margin.

---

## Screen: error

```
┌─────────────────────────────────────┐
│  My Cards                  [🔔]     │
├─────────────────────────────────────┤
│                                     │
│  My Cards                           │
│                                     │
│           cloud_off                 │  ← 48dp icon, #44483D, centered
│                                     │
│      Unable to load cards           │  ← body_large, #1A1C16, centered
│   Check your connection             │
│       and try again                 │  ← body_medium, #44483D, centered
│                                     │
│          [ Try Again ]              │  ← filled #4C662B, centered
│                                     │
├─────────────────────────────────────┤
│ 🏠    🏦    ↗    💳    ···          │
└─────────────────────────────────────┘
```

**Layout notes:** Error icon + message + retry centered vertically below title.

---

## Design Checklist (Figma / Stitch)

- [ ] M3 TopAppBar with "My Cards" title and notifications_outlined action
- [ ] Screen title headline_large in #4C662B with 4dp bottom padding
- [ ] Card carousel: horizontal scroll, 16dp gap, snap to start, cards 320×200dp
- [ ] Debit Visa card: #4C662B fill, radius 20, elevation 8 — PAN white monospace, name #CDEDA3 uppercase
- [ ] Active chip: #4C662B fill, #FFFFFF text, radius 12, label_small
- [ ] Business Mastercard: #386663 fill — same layout; Frozen chip #C5C8BA fill
- [ ] Mastercard logo 48×30dp, Visa logo 56×20dp, both white tinted
- [ ] Quick-action row: 4 evenly-spaced vertical text buttons; Report Lost uses #BA1A1A
- [ ] "Card Transactions" header title_large/#1A1C16/weight 600
- [ ] Transaction rows: white fill, 12dp radius, 1dp elevation; all amounts in #BA1A1A body_large
- [ ] Transaction dates body_small/#44483D
- [ ] "Order New Card" outlined full-width button, #4C662B, add_card icon leading
- [ ] Skeleton carousel proportional to card dimensions; 3 transaction row skeletons
- [ ] Empty state: credit_card_off 48dp icon, descriptive copy, order button
- [ ] Error state: cloud_off 48dp icon, copy, retry button
- [ ] Bottom nav visible, Cards tab active indicator #DCE7C8
- [ ] All text Outfit typeface; minimum 14sp body content
- [ ] 16dp horizontal content padding throughout
