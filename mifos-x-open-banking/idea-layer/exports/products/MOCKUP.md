# MOCKUP — Products

**Archetype:** index_list
**Shell:** Top app bar ("Products", back arrow, search icon) + Bottom nav 5 items (Products active, #DCE7C8 pill).
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│ ←  Products                   [🔍]  │  ← TopAppBar with search action
├─────────────────────────────────────┤
│                                     │
│  Products                           │  ← headline_large, #4C662B
│  Explore accounts, savings…         │  ← body_medium, #44483D
│                                     │
│  [All] [Savings] [Loans] [Cards] …  │  ← Filter tabs row (chips)
│                                     │
│  ┌───────────────────────────────┐  │
│  │  ████████████████  [Savings]  │  │  ← Product card skeleton × 4
│  │  ████████████████████         │  │
│  │  ████████████                 │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  ████████████████  [Savings]  │  │
│  │  ████████████████████         │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  ████████████████  [Loans  ]  │  │
│  │  ████████████████████         │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  ████████████████  [Cards  ]  │  │
│  │  ████████████████████         │  │
│  └───────────────────────────────┘  │
│                                     │
├─────────────────────────────────────┤
│  🏠     💳  ●Products  💸    ···    │  ← Bottom nav, Products active
└─────────────────────────────────────┘
```

**Layout notes:** Shimmer on 4 product card placeholders. Filter tabs are present but non-interactive.

---

## Screen: populated

```
┌─────────────────────────────────────┐
│ ←  Products                   [🔍]  │
├─────────────────────────────────────┤
│                                     │
│  Products                           │  ← headline_large, #4C662B
│  Explore accounts, savings, loans   │  ← body_medium, #44483D
│  and cards tailored for you.        │
│                                     │
│  [●All] [Savings] [Loans] [Cards]   │  ← Active tab: bg #4C662B text white
│  [Mortgages]                        │  ← Inactive: outlined #E1E4D5 text #44483D
│                                     │
│  ┌───────────────────────────────┐  │
│  │  Instant Access Savings [Savings]│ ← White card, radius 16, elevation 2
│  │                               │  │  ← Badge: bg #CDEDA3, text #4C662B
│  │  4.5% AER                     │  │  ← display_small, #4C662B, bold
│  │  Earn 4.5% AER on every pound │  │  ← body_medium, #44483D
│  │  you save. Withdraw anytime…  │  │
│  │  [4.5% AER] [Instant access]  │  │  ← Feature chips: #CDEDA3, #DCE7C8
│  │  [No minimum deposit]         │  │
│  │                [Details][Apply Now]│ ← Outlined + Filled #4C662B, radius 8
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  Fixed Rate Bond 1yr [Savings]│  │
│  │  5.1% AER                     │  │  ← display_small, #4C662B, bold
│  │  Lock in a market-leading     │  │
│  │  5.1% AER for 12 months…      │  │
│  │  [5.1% AER][12-month term]    │  │
│  │  [FSCS protected]             │  │
│  │                [Details][Apply Now]│
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  Personal Loan          [Loans]│  │
│  │  From 6.9% APR                │  │  ← display_small, #4C662B, bold
│  │  Borrow from £1,000 to        │  │
│  │  £25,000 at 6.9% APR…         │  │
│  │  [From 6.9% APR][Up to £25k]  │  │
│  │  [1–7 year terms]             │  │  ← DCE7C8 chip, text #386663
│  │                [Details][Apply Now]│
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  Platinum Credit Card  [Cards]│  │  ← Cards badge: bg #DCE7C8, text #386663
│  │  0% for 20 months             │  │  ← display_small, #4C662B, bold
│  │  0% interest on purchases     │  │
│  │  for 20 months. No annual fee │  │
│  │  [0% for 20 months][No fee]   │  │
│  │  [Contactless & Pay]          │  │
│  │                [Details][Apply Now]│
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  Refer a friend — earn £50    │  │  ← #4C662B filled banner, radius 12
│  │  When your friend opens any   │  │  ← title_small white; body_small #CDEDA3
│  │  account before 30 June 2026  │  │
│  └───────────────────────────────┘  │
│                                     │
├─────────────────────────────────────┤
│  🏠     💳  ●Products  💸    ···    │
└─────────────────────────────────────┘
```

**Layout notes:**
- Content padding 16dp horizontal.
- Each product card: 20dp horizontal margin, 12dp bottom margin, radius 16, elevation 2.
- Category badge: top-right of card header row, radius 6, label_small text.
- Headline rate: display_small (32sp, SemiBold) in #4C662B — primary visual hierarchy.
- Feature chips: horizontal scroll row, radius 8, label_small.
- Action row: right-aligned, "Details" outlined + "Apply Now" filled, both radius 8.
- Promotions banner: #4C662B fill, radius 12, 20dp horizontal margin, 16dp bottom margin.

---

## Screen: empty

```
┌─────────────────────────────────────┐
│ ←  Products                   [🔍]  │
├─────────────────────────────────────┤
│  Products                           │
│  Explore accounts, savings…         │
│  [All][Savings][Loans][Cards][Mortgages]│
│                                     │
│              🏪                     │  ← store icon, 48dp, #75796C, centred
│                                     │
│     No products available           │  ← title_medium, centre, #1A1C16
│  No products match the selected     │  ← body_medium, centre, #44483D
│  category. Try a different filter   │
│  or check back later.               │
│                                     │
├─────────────────────────────────────┤
│  🏠     💳  ●Products  💸    ···    │
└─────────────────────────────────────┘
```

**Layout notes:** Empty state centred below filter row. No product cards shown.

---

## Screen: error

```
┌─────────────────────────────────────┐
│ ←  Products                   [🔍]  │
├─────────────────────────────────────┤
│  Products                           │
│  Explore accounts, savings…         │
│  [All][Savings][Loans][Cards][Mortgages]│
│                                     │
│              ☁                      │  ← cloud_off icon, 48dp, #BA1A1A
│                                     │
│      Unable to load products        │  ← title_medium, centre, #1A1C16
│  Check your connection and retry.   │  ← body_medium, centre, #44483D
│  Your saved favourites are offline. │
│                                     │
│         ┌──────────┐                │
│         │  Retry   │                │  ← Outlined button, #4C662B
│         └──────────┘                │
│                                     │
├─────────────────────────────────────┤
│  🏠     💳  ●Products  💸    ···    │
└─────────────────────────────────────┘
```

**Layout notes:** Error icon + message centred. Retry fires `RetryLoad`.

---

## Design Checklist (Figma / Stitch)

- [ ] M3 TopAppBar with back nav + search icon action
- [ ] Filter tab chips: active (#4C662B bg + white text), inactive (outlined #E1E4D5 border + #44483D text), radius 20dp
- [ ] Product cards: white (#FFFFFF), radius 16, elevation 2, 16dp padding
- [ ] Category badges: appropriate bg + text colors per category (Savings=#CDEDA3/#4C662B, Cards=#DCE7C8/#386663)
- [ ] Headline rates in display_small (32sp, SemiBold), #4C662B — prominent visual anchor
- [ ] Feature chips in horizontal scroll row; correct bg/text color pairs
- [ ] "Details" outlined + "Apply Now" filled — both radius 8, same row right-aligned
- [ ] Promotions banner: #4C662B fill, white title, #CDEDA3 subtitle, radius 12
- [ ] Loading: 4 skeleton product cards shimmer
- [ ] Empty state: store_outlined icon + message below filter row
- [ ] Error state: cloud_off icon + message + Retry button
- [ ] Bottom nav: Products tab active (#DCE7C8 pill)
- [ ] All text Outfit typeface; 16dp horizontal content padding
