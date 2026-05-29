# MOCKUP — Consumer Home

**Archetype:** dashboard
**Shell:** No top app bar. Bottom navigation bar (Home active). Notification icon in header band.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: content (Primary)

```
┌─────────────────────────────────────┐
│ ████████████ Green Header ████████  │  ← bg #4C662B, top safe-area inset
│                                     │
│  Good morning, Alex        🔔(3)   │  ← headline_medium, white; bell icon badge=3
│                                     │
│  ┌───────────────────────────────┐  │
│  │  Total Balance                │  │  ← balance card, white, 20dp radius, elevation 4
│  │                               │     card uses margin-top: -24dp (overlaps header)
│  │  £4,250.00                    │  │  ← display_small (32sp), bold, #4C662B
│  │  [Primary Checking]           │  │  ← chip, #CDEDA3 bg, #4C662B text, 12dp radius
│  │  ─────────────────────────── │  │  ← divider #E8E8E8
│  │  Income this month  │ Spent   │  │  ← label_small #757575
│  │  + £3,200.00       │-£1,840  │  │  ← body_large, green #2E7D32 / red #C62828
│  └───────────────────────────────┘  │
│                                     │
│  [ Send ]  [Accounts] [Standing] [Cards] │  ← 4 quick-action tiles, space_evenly
│                                     │     each: icon 28dp + label_small, min 48dp touch
│                                     │
│  Recent Transactions        See all │  ← title_medium #1A1C16 + label_medium #4C662B
│                                     │
│  ┌───────────────────────────────┐  │
│  │  ☕ Coffee Shop       -£3.50  │  │  ← white card, 12dp radius, elevation 1
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  💰 Salary         +£3,200   │  │  ← credit amount green #2E7D32
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  🛒 Supermarket      -£42.80  │  │  ← debit amount red #C62828
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │   View All Transactions       │  │  ← OutlinedButton, border #4C662B, text #4C662B
│  └───────────────────────────────┘  │
│                                     │
├─────────────────────────────────────┤
│ [Home] [Accounts] [Pay] [Cards][More]│  ← BottomNav 80dp, Home active #DCE7C8 pill
└─────────────────────────────────────┘
```

**Layout notes:**
- Header band: 100% width, `#4C662B` bg, 32dp top padding, 24dp bottom padding. Notification bell trailing.
- Balance card floats 24dp into header (negative margin-top creates layered effect).
- Balance card: white, 20dp radius, `elevation 4`. 24dp horizontal padding. Income/expense in 50/50 split row.
- Quick-actions row: `#F9FAEF` bg, 24dp vertical padding, 4 tiles evenly spaced.
- Transaction cards: 16dp horizontal/vertical padding, white bg, 12dp radius, 4dp bottom margin.
- "View All Transactions": full-width outlined button, 24dp radius, 48dp height, 8dp top margin.
- Bottom nav: `#F9FAEF` bg, `#C5C8BA` 1dp border-top. Home active: `#DCE7C8` pill indicator.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│ ████████████ Green Header ████████  │  ← #4C662B
│                                     │
│  Good morning, Alex        🔔      │  ← greeting visible in loading
│                                     │
│  ████████████████████████████████   │  ← skeleton balance card ~200dp, #E1E4D5
│                                     │
│  ████████████████████████████████   │  ← skeleton quick-actions row ~72dp
│                                     │
│  ████████████████████████████████   │  ← skeleton txn row 1, 64dp
│                                     │
│  ████████████████████████████████   │  ← skeleton txn row 2, 64dp
│                                     │
├─────────────────────────────────────┤
│ [Home] [Accounts] [Pay] [Cards][More]│
└─────────────────────────────────────┘
```

**Layout notes:** Green header band and greeting always visible. Four shimmer skeleton blocks with 16dp horizontal margin and 8dp vertical spacing. Shimmer: `trust_horizon` gradient `#F0F1E6 → #E1E4D5` left-to-right animation 1200ms looping.

---

## Screen: error

```
┌─────────────────────────────────────┐
│ ████████████ Green Header ████████  │
│                                     │
│  Good morning, Alex        🔔      │
│                                     │
│                                     │
│              ⚠                      │  ← error_outline icon 48dp, #D32F2F
│                                     │
│   Could not load your account.      │  ← body_medium, #757575, centered
│   Check your connection and try     │
│   again.                            │
│                                     │
│  ┌───────────────────────────────┐  │
│  │          Retry                │  │  ← FilledButton, #4C662B, 24dp radius, 48dp height
│  └───────────────────────────────┘  │
│                                     │
├─────────────────────────────────────┤
│ [Home] [Accounts] [Pay] [Cards][More]│
└─────────────────────────────────────┘
```

**Layout notes:** Error icon + message + button centred in content area (below header). Error icon 48dp, 32dp padding on text, button 32dp horizontal margin.

---

## Screen: empty

```
┌─────────────────────────────────────┐
│ ████████████ Green Header ████████  │
│                                     │
│  Good morning, Alex        🔔      │
│                                     │
│                                     │
│           👝                        │  ← account_balance_wallet 64dp, tint #CDEDA3
│                                     │
│  No accounts found.                 │  ← body_medium, #757575, centered
│  Contact your bank to set up        │
│  your account.                      │
│                                     │
├─────────────────────────────────────┤
│ [Home] [Accounts] [Pay] [Cards][More]│
└─────────────────────────────────────┘
```

**Layout notes:** Wallet icon 64dp tinted `#CDEDA3` (primary container). Body text centered, 32dp horizontal padding. No retry button (no network error — empty is a data state).

---

## Design Checklist (Figma / Stitch)

- [ ] Green header band `#4C662B`, full-width, no top app bar chrome
- [ ] Greeting text `headline_medium` white; notification bell white with badge
- [ ] Balance card overlaps header via negative margin-top: -24dp; 20dp radius; elevation 4
- [ ] `display_small` (32sp SemiBold) balance amount in `#4C662B`
- [ ] Account name chip: `#CDEDA3` bg, `#4C662B` text, 12dp radius, `label_small`
- [ ] Income/expense sub-row: income `#2E7D32`, expense `#C62828`, `body_large` Medium
- [ ] 4 quick-action tiles: icon 28dp + `label_small` beneath, 48dp min touch target
- [ ] "Recent Transactions" header row: title_medium + "See all" label_medium `#4C662B`
- [ ] 3 transaction cards: white, 12dp radius, elevation 1, 4dp margin-bottom each
- [ ] "View All Transactions" OutlinedButton: full-width, 24dp radius, `#4C662B`
- [ ] M3 BottomNavigationBar 80dp; Home tab shows `#DCE7C8` active indicator pill
- [ ] Loading: 4 shimmer skeleton blocks, `#E1E4D5` base, looping animation
- [ ] Error state: `error_outline` 48dp `#D32F2F` + body_medium text + Retry FilledButton
- [ ] Empty state: `account_balance_wallet` 64dp `#CDEDA3` + body_medium text
- [ ] All text: Outfit typeface; minimum 12sp label_small on chips
- [ ] Responsive: 2-column layout on ≥600dp width; 3-column on ≥840dp

---

_Generated by /idea export | 2026-05-30_
