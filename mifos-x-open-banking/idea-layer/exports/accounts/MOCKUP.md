# MOCKUP — My Accounts

**Archetype:** index_list
**Shell:** Consumer bottom navigation bar (Accounts tab active). No top app bar (screen-level headline).
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: content (Primary)

```
┌─────────────────────────────────────┐
│  My Accounts                   [?]  │  ← headline_large #1A1C16 + help_outline #44483D
├─────────────────────────────────────┤
│  [ALL] [CHECKING] [SAVINGS]         │  ← Filter tabs; ALL = filled #4C662B/white
│  [BUSINESS]                         │    others = outlined #E1E4D5/#44483D
├─────────────────────────────────────┤
│  ┌── 4dp ─────────────────────────┐ │
│  ║  Primary Checking  [CHECKING]  │ │  ← Left border #4C662B; type badge #CDEDA3/#4C662B
│  ║  £4,250.00                     │ │  ← display_small/SemiBold, color #4C662B
│  ║  🏦 DE89 3704 0044 0532 0130 00│ │  ← account_box icon 16dp + body_small monospace
│  └────────────────────────────────┘ │
│  ┌── 4dp ─────────────────────────┐ │
│  ║  Holiday Savings   [SAVINGS]   │ │  ← Left border #386663; badge text #386663
│  ║  £6,180.50                     │ │  ← display_small/SemiBold, color #386663
│  ║  🏦 DE89 3704 0044 0532 0131 00│ │
│  └────────────────────────────────┘ │
│  ┌── 4dp ─────────────────────────┐ │
│  ║  Business Current  [BUSINESS]  │ │  ← Left border #E8A317; badge text #44483D (a11y)
│  ║  £2,050.00                     │ │  ← display_small/SemiBold, color #44483D (a11y)
│  ║  🏦 DE89 3704 0044 0532 0132 00│ │
│  └────────────────────────────────┘ │
│  ─────────────────────────────────  │  ← footer_divider #E1E4D5
│  Total across 3 accounts  £12,480.50│  ← body_medium #44483D | title_large/Bold #4C662B
│                                 [+] │  ← FAB add icon, #4C662B, 56×56dp, fixed bottom-right
├─────────────────────────────────────┤
│  Home | [Accounts] | Pay | Cards    │  ← Consumer BottomNav; Accounts active (#DCE7C8)
│  | More                             │
└─────────────────────────────────────┘
```

**Layout notes:**
- Header row: "My Accounts" headline_large (32sp) left + `help_outline` icon button right, 20dp H padding, 24dp top padding, 8dp bottom padding.
- Filter tab row: horizontal scroll, 8dp gap between tabs, 20dp H padding, 16dp V padding. ALL chip: filled `#4C662B` bg + white text + 20dp radius. Other tabs: outlined `#E1E4D5` border + `#44483D` text.
- Account cards: white `#FFFFFF`, 16dp radius, 24dp padding, 20dp H margin, 16dp bottom gap, elevation 2. Left border: 4dp wide, color per account type.
- Card header row: account name (title_medium/SemiBold, flex 1) + type badge (right-aligned, `#CDEDA3` bg, 6dp radius, 8dp H / 4dp V padding, label_small).
- Balance: display_small (32sp/SemiBold) color matches left border accent.
- IBAN row: `account_box` icon 16dp (color `#44483D`) + body_small monospace text (color `#44483D`), 8dp gap.
- Footer: `#F9FAEF` bg, 12dp radius, 16dp padding, 20dp H margin. Row: label (flex 1) + total (right-aligned).
- FAB: fixed position, 20dp from right, 80dp bottom (clears bottom nav), 56×56dp, `#4C662B` fill, 16dp radius, elevation 6.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│  My Accounts                   [?]  │
├─────────────────────────────────────┤
│  [ALL] [CHECKING] [SAVINGS]         │
│  [BUSINESS]                         │
├─────────────────────────────────────┤
│  ┌────────────────────────────────┐ │
│  │  ░░░░░░░░░░░░   ░░░░░░░░░░░░  │ │  ← Card skeleton (120dp height, #E1E4D5)
│  │  ░░░░░░░░░░░░                  │ │
│  │  ░░░░░░░░░░░░░░░░░░░░░░░░░░   │ │
│  └────────────────────────────────┘ │
│  ┌────────────────────────────────┐ │
│  │  ░░░░░░░░░░░░   ░░░░░░░░░░░░  │ │
│  │  ░░░░░░░░░░░░                  │ │
│  │  ░░░░░░░░░░░░░░░░░░░░░░░░░░   │ │
│  └────────────────────────────────┘ │
│  ┌────────────────────────────────┐ │
│  │  ░░░░░░░░░░░░   ░░░░░░░░░░░░  │ │
│  │  ░░░░░░░░░░░░                  │ │
│  │  ░░░░░░░░░░░░░░░░░░░░░░░░░░   │ │
│  └────────────────────────────────┘ │
├─────────────────────────────────────┤
│  Home | [Accounts] | Pay | Cards    │
└─────────────────────────────────────┘
```

**Layout notes:** Shimmer on 3 skeleton cards (120dp height each, `#E1E4D5` with 16dp radius). Header and filter tabs visible. Footer and FAB hidden during load.

---

## Screen: empty

```
┌─────────────────────────────────────┐
│  My Accounts                   [?]  │
├─────────────────────────────────────┤
│  [ALL] [CHECKING] [SAVINGS]         │
│  [BUSINESS]                         │
├─────────────────────────────────────┤
│                                     │
│          account_balance            │  ← account_balance icon, 48dp, #44483D
│                                     │
│       No accounts found             │  ← title_medium, #1A1C16, centred
│  You don't have any accounts        │  ← body_medium, #44483D, centred
│  matching this filter. Try a        │
│  different category or request a    │
│  new account.                       │
│                                     │
│  ┌──────────────────────────────┐   │
│  │      Request Account         │   │  ← Filled button #4C662B
│  └──────────────────────────────┘   │
│                                 [+] │  ← FAB still visible
├─────────────────────────────────────┤
│  Home | [Accounts] | Pay | Cards    │
└─────────────────────────────────────┘
```

**Layout notes:** Empty state centred in content area. Filter tabs remain active for category switching. FAB visible for new account requests.

---

## Screen: error

```
┌─────────────────────────────────────┐
│  My Accounts                   [?]  │
├─────────────────────────────────────┤
│  [ALL] [CHECKING] [SAVINGS]         │
├─────────────────────────────────────┤
│              ⚠                      │  ← error_outline, 48dp, #BA1A1A, centred
│                                     │
│     Could not load accounts         │  ← title_medium, #1A1C16, centred
│  We were unable to fetch your       │  ← body_medium, #44483D, centred
│  account list. Please check your    │
│  connection and try again.          │
│                                     │
│  ┌──────────────────────────────┐   │
│  │           Retry              │   │  ← Filled button #4C662B
│  └──────────────────────────────┘   │
├─────────────────────────────────────┤
│  Home | [Accounts] | Pay | Cards    │
└─────────────────────────────────────┘
```

**Layout notes:** Error icon + message + Retry button centred vertically. Bottom nav visible.

---

## Design Checklist (Figma / Stitch)

- [ ] "My Accounts" headline_large (32sp, `#1A1C16`) left + `help_outline` icon right
- [ ] Scrollable filter tab row: filled `#4C662B` for ALL, outlined `#E1E4D5` border for unselected
- [ ] Three account cards: white `#FFFFFF`, 16dp radius, elevation 2, 4dp left border accent
- [ ] Left border colors: Checking = `#4C662B`, Savings = `#386663`, Business = `#E8A317`
- [ ] Account type badges: `#CDEDA3` bg; Checking text `#4C662B`, Savings `#386663`, Business `#44483D` (a11y-corrected)
- [ ] Balance in display_small (32sp/SemiBold) matching accent color per account type
- [ ] Business balance uses `#44483D` not `#E8A317` (a11y contrast correction)
- [ ] IBAN row: `account_box` icon 16dp + body_small monospace, both `#44483D`
- [ ] Footer: `#F9FAEF` bg, 12dp radius, "Total across 3 accounts" + "£12,480.50" in title_large/Bold `#4C662B`
- [ ] FAB: `#4C662B` fill, `add` icon, 56×56dp, fixed bottom-right clearing 80dp bottom nav
- [ ] Skeleton cards: 3 cards × 120dp height, `#E1E4D5` shimmer
- [ ] Consumer bottom navigation (5 tabs), Accounts active with `#DCE7C8` pill indicator
