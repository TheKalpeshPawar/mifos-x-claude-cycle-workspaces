# MOCKUP — Spending Insights

**Archetype:** dashboard
**Shell:** Top app bar ("Spending Insights", back arrow, tune icon) + Bottom nav 5 items (Insights active, #DCE7C8 pill).
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│ ←  Spending Insights          [⚙]   │  ← TopAppBar, back + tune action
├─────────────────────────────────────┤
│                                     │
│  Spending Insights                  │  ← headline_large, #4C662B
│                                     │
│  [████] [████] [████] [████]        │  ← Period chip skeletons
│  ████████████                       │  ← Period label skeleton
│                                     │
│  ┌───────────────────────────────┐  │
│  │  ████████████████████████████ │  │  ← Summary card skeleton (h 120dp)
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  ████████████████████████████ │  │  ← Budget card skeleton (h 100dp)
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  ████████████████████████████ │  │  ← Pie chart skeleton (h 220dp)
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  ████████████████████████████ │  │  ← Budget cards skeleton (h 80dp)
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  ████████████████████████████ │  │  ← Merchants card skeleton (h 200dp)
│  └───────────────────────────────┘  │
│                                     │
├─────────────────────────────────────┤
│  🏠     💳    ✦Insights  💳    ···  │  ← Bottom nav, Insights active #DCE7C8
└─────────────────────────────────────┘
```

**Layout notes:** Shimmer animation on all skeleton blocks. Period chips render (non-interactive) to show nav intent.

---

## Screen: populated

```
┌─────────────────────────────────────┐
│ ←  Spending Insights          [⚙]   │
├─────────────────────────────────────┤
│                                     │
│  Spending Insights                  │  ← headline_large, #4C662B
│                                     │
│  [●This Month] [Last Month]         │  ← Filter chips, horizontal scroll
│  [Last 3 Months] [Custom]           │  ← Selected: bg #4C662B text white
│  May 2026                           │  ← body_medium, #44483D
│                                     │
│  ┌───────────────────────────────┐  │
│  │  This Month                   │  │  ← White card, radius 20, elevation 2
│  │                               │  │
│  │  Total Spent  Received   Net  │  │  ← label_small, #44483D
│  │  £1,029.80   £3,200.00  +£2,170.20 │  ← title_large; spent #BA1A1A; net/recv #4C662B
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  Monthly Budget      68% used │  │  ← #CDEDA3 card, radius 20
│  │  £1,029.80 spent  £470.20 left│  │  ← body_medium; remaining #4C662B
│  │  ▓▓▓▓▓▓▓▓▓▓▓▓▓▓░░░░░         │  │  ← Progress bar: #E8A317 fill 68%
│  │  of £1,500.00 monthly budget  │  │  ← label_small, #44483D
│  └───────────────────────────────┘  │
│                                     │
│  Spending by Category               │  ← title_medium, #1A1C16
│                                     │
│  ┌───────────────────────────────┐  │
│  │      [  Pie Chart  ]          │  │  ← White card, h 220dp, radius 20
│  │   Bills 43.7%   Food 31.1%    │  │  ← Visual pie (accessible via a11y)
│  └───────────────────────────────┘  │
│  ● Food & Dining         £320.50    │  ← dot #BA1A1A, body_medium
│  ● Transport             £125.00    │  ← dot #386663
│  ● Shopping               £89.30    │  ← dot #CDEDA3
│  ● Bills                 £450.00    │  ← dot #4C662B
│  ● Entertainment          £45.00    │  ← dot #E8A317
│                                     │
│  Budget Progress                    │  ← title_medium, #1A1C16
│                                     │
│  ┌───────────────────────────────┐  │
│  │  Food & Dining  £320.50/£350  │  │  ← White card, radius 16
│  │  ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓░░░       │  │  ← #BA1A1A fill 92% (near limit)
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  Transport      £125.00/£200  │  │
│  │  ▓▓▓▓▓▓▓▓▓▓░░░░░░░░░░        │  │  ← #E8A317 fill 63%
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  Shopping        £89.30/£150  │  │
│  │  ▓▓▓▓▓▓▓▓▓░░░░░░░░░          │  │  ← #4C662B fill 60%
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  Bills          £450.00/£500  │  │
│  │  ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓░░        │  │  ← #BA1A1A fill 90% (near limit)
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  Entertainment   £45.00/£100  │  │
│  │  ▓▓▓▓▓▓▓░░░░░░░░░░░          │  │  ← #4C662B fill 45%
│  └───────────────────────────────┘  │
│                                     │
│          [ Manage Budgets ]         │  ← Outlined button, #4C662B
│                                     │
│  Top Merchants                      │  ← title_medium, #1A1C16
│                                     │
│  ┌───────────────────────────────┐  │
│  │  [🛒] Tesco       £142.30     │  │  ← storefront icon bg #CDEDA3
│  │       8 transactions           │  │  ← label_small, #44483D
│  ├───────────────────────────────┤  │
│  │  [▶] Netflix       £17.99     │  │  ← play_circle icon bg #CDEDA3
│  │       1 transaction            │  │
│  ├───────────────────────────────┤  │
│  │  [♪] Spotify       £11.99     │  │  ← music_note icon bg #CDEDA3
│  │       1 transaction            │  │
│  ├───────────────────────────────┤  │
│  │  [🚇] TfL          £78.50     │  │  ← directions_subway, bg #DCE7C8
│  │       23 transactions          │  │
│  └───────────────────────────────┘  │
│                                     │
│       View All Transactions         │  ← Text button, #4C662B
│                                     │
├─────────────────────────────────────┤
│  🏠     💳    ✦Insights  💳    ···  │
└─────────────────────────────────────┘
```

**Layout notes:**
- Content padding 20dp horizontal throughout.
- Cards have 20dp horizontal margin, 20dp bottom margin between cards.
- Period chip row: horizontal scroll, min_item_width 80dp, scroll indicator visible.
- Progress bars: track #E1E4D5, radius 4, h 8dp. Fill color varies by safety level (safe=green, warn=amber, danger=red).
- Merchant rows: leading icon circle 40dp with category bg, trailing amount in #BA1A1A (debit).

---

## Screen: empty

```
┌─────────────────────────────────────┐
│ ←  Spending Insights          [⚙]   │
├─────────────────────────────────────┤
│                                     │
│  Spending Insights                  │
│  [●This Month] [Last Month] …       │
│  May 2026                           │
│                                     │
│                                     │
│            🧾                       │  ← receipt_long icon, 48dp, #75796C
│                                     │
│     No transaction history yet      │  ← title_medium, center, #1A1C16
│  Spending insights will appear once │  ← body_medium, center, #44483D
│  you have transactions this period. │
│                                     │
│    ┌────────────────────────────┐   │
│    │      View Accounts         │   │  ← Outlined button, #4C662B
│    └────────────────────────────┘   │
│                                     │
├─────────────────────────────────────┤
│  🏠     💳    ✦Insights  💳    ···  │
└─────────────────────────────────────┘
```

**Layout notes:** Empty state icon + message centred vertically. CTA navigates to accounts.

---

## Screen: no_budget_set

```
┌─────────────────────────────────────┐
│ ←  Spending Insights          [⚙]   │
├─────────────────────────────────────┤
│  [Period chips + label]             │
│  [This Month summary card]          │
│  [Spending by Category section]     │
│  [Pie chart + legend]               │
│                                     │
│  ┌───────────────────────────────┐  │  ← #CDEDA3 card, amber #E8A317 border
│  │  No budget set                │  │  ← title_small, #44483D
│  │  Set a monthly budget to track│  │  ← body_small, #44483D
│  │  how much you spend…          │  │
│  │                               │  │
│  │     ┌──────────────────┐      │  │
│  │     │  Set Budget Now  │      │  │  ← Filled button, #4C662B
│  │     └──────────────────┘      │  │
│  └───────────────────────────────┘  │
│                                     │
│  [Top Merchants section]            │
│  [View All Transactions button]     │
├─────────────────────────────────────┤
│  🏠     💳    ✦Insights  💳    ···  │
└─────────────────────────────────────┘
```

**Layout notes:** Budget section replaced by prompt banner. Summary and pie chart still visible. Merchants section still at bottom.

---

## Screen: error

```
┌─────────────────────────────────────┐
│ ←  Spending Insights          [⚙]   │
├─────────────────────────────────────┤
│  Spending Insights                  │
│  [Period chips + label]             │
│                                     │
│            ⚠                        │  ← error_outline icon, 48dp, #BA1A1A
│                                     │
│  Could not load spending insights.  │  ← body_large, center, #1A1C16
│  Please try again.                  │
│                                     │
│         ┌──────────┐                │
│         │  Retry   │                │  ← Outlined button, #4C662B
│         └──────────┘                │
│                                     │
├─────────────────────────────────────┤
│  🏠     💳    ✦Insights  💳    ···  │
└─────────────────────────────────────┘
```

**Layout notes:** Error icon + message centred. Retry re-fires `RetryLoad` event.

---

## Design Checklist (Figma / Stitch)

- [ ] M3 TopAppBar with back navigation + tune filter icon action
- [ ] Filter chips: selected (#4C662B bg, white text), unselected (#CDEDA3 bg, #4C662B text), radius 20dp
- [ ] Summary card: white, radius 20, elevation 2, 3-column layout (Spent red / Received green / Net green)
- [ ] Overall budget card: #CDEDA3 fill, radius 20 — progress bar #E8A317 fill 68% of track
- [ ] Category pie chart placeholder card: white, radius 20, h 220dp, accessible aria label
- [ ] 5 category legend rows with 12dp dots in correct category colors
- [ ] Per-category budget cards: radius 16, progress fills color-coded (safe=#4C662B, warn=#E8A317, danger=#BA1A1A)
- [ ] Merchant rows: 40dp icon circles with category bg, amounts in #BA1A1A
- [ ] "Manage Budgets" outlined button centred with #4C662B border
- [ ] "Set Budget Now" filled button (#4C662B) in no_budget_set prompt banner
- [ ] Bottom nav with Insights tab active (#DCE7C8 pill)
- [ ] All text Outfit typeface; 20dp horizontal content padding throughout
- [ ] Skeleton shimmer on loading: 5 placeholder cards matching content proportions
