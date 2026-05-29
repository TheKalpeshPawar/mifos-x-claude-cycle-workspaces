# MOCKUP — Account Applications

**Archetype:** index_list
**Shell:** Field Officer bottom navigation bar — 5 tabs (Dashboard / Customers / **Applications** / Messages / More). Applications tab active with `#DCE7C8` indicator pill.
**Accent:** `#4C662B` (Earth-green primary). Typography: Outfit. Design system: Material Design 3.

---

## Screen: content

```
┌─────────────────────────────────────────┐
│  Account Applications                   │  ← headline_large (32sp), #4C662B, 20dp top / 4dp bottom pad
│                                         │
│  ┌──────────────────────────────────────┤  ← Horizontal scrollable filter chip row
│  │ [■ All (8)] [Pending (3)] [Approved (3)] [Rejected (2)] →
│  └──────────────────────────────────────┤     "All" selected: #4C662B fill / white; rest: #F9FAEF / #44483D
│                                         │
│  ┌─────────────────────────────────────┐│
│  │  John Mwangi        [Pending Review]││  ← title_medium/700 #1A1C16 + chip: #CDEDA3 bg, #E8A317 border
│  │  KCB Savings Account                ││  ← body_medium #4C662B                [status text: #44483D 7.25:1]
│  │  Submitted: 20 May 2026   [Review ▶]││  ← body_small #44483D  +  filled btn #4C662B / white, 8dp radius
│  └─────────────────────────────────────┘│  ← card: #FFFFFF, 12dp radius, 14dp pad, 16dp H margin, elev 2
│  ┌─────────────────────────────────────┐│
│  │  Sarah Odhiambo       [Approved ✓] ││  ← chip: #CDEDA3 bg, #4C662B border + text
│  │  M-Shwari Checking Account          ││  ← body_medium #4C662B
│  │  Submitted: 18 May 2026             ││  ← body_small #44483D (no action — approved, read-only)
│  └─────────────────────────────────────┘│
│  ┌─────────────────────────────────────┐│
│  │  Peter Kamau          [Rejected ✗]  ││  ← chip: #CDEDA3 bg, #BA1A1A border + text
│  │  Business Current Account           ││
│  │  Submitted: 12 May 2026  [View Reason]│  ← label_medium #BA1A1A underlined link
│  └─────────────────────────────────────┘│
│                                         │
│                               [+ New Application]│  ← Extended FAB: #4C662B, white, add icon, bottom-right
│                                         │     elevation 6; 24dp bottom, 16dp right margin
├─────────────────────────────────────────┤
│  [Dashboard] [Customers] [■Apps] [Msgs] │  ← Field Officer bottom nav; 80dp height; #F9FAEF bg
│                           [More]        │     Applications: #DCE7C8 active indicator pill
└─────────────────────────────────────────┘
```

**Layout notes:**
- Screen background: `#F9FAEF` (colors.light.background).
- Filter chip bar: 10dp V padding, 16dp H padding, 8dp gap (spacing.sm) between chips. Pill shape: 20dp radius. Min touch target 48dp.
- Card structure: 3-row internal layout — (1) header row: name + status chip, space-between, flex-start; (2) product text (body_medium, `#4C662B`, xs bottom margin); (3) footer row: date + action, space-between, center.
- Pending card footer: "Review" filled button (`#4C662B` bg, white text, 8dp radius, 16dp H pad, 8dp V pad).
- Rejected card footer: "View Reason" link (label_medium, `#BA1A1A`, underlined). No button on Approved card.
- Status chip: 12dp radius, 10dp H pad, 3dp V pad, 1dp border. All chips share `#CDEDA3` bg; only border/text color varies.
- A11Y fix applied to Pending chip text: `#44483D` (7.25:1 vs. `#CDEDA3`) replaces former `#E8A317` (1.68:1 FAIL).

---

## Screen: loading

```
┌─────────────────────────────────────────┐
│  Account Applications                   │  ← Title always visible during load
│                                         │
│  [■ All (8)] [Pending (3)] [Approved]   │  ← Filter row rendered (static, not interactive during load)
│              [Rejected (2)]             │
│                                         │
│  ┌─────────────────────────────────────┐│
│  │  ░░░░░░░░░░░░░░   ░░░░░░░░░░░░░   ││  ← Shimmer: name placeholder + chip placeholder
│  │  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   ││  ← Shimmer: product placeholder (full width)
│  │  ░░░░░░░░░░░░░░   ░░░░░░░░░░░░    ││  ← Shimmer: date + action placeholder
│  └─────────────────────────────────────┘│
│  ┌─────────────────────────────────────┐│
│  │  ░░░░░░░░░░░░░░   ░░░░░░░░░░░░░   ││
│  │  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   ││
│  │  ░░░░░░░░░░░░░░                   ││
│  └─────────────────────────────────────┘│
│  ┌─────────────────────────────────────┐│
│  │  ░░░░░░░░░░░░░░   ░░░░░░░░░░░░░   ││
│  │  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   ││
│  │  ░░░░░░░░░░░░░░                   ││
│  └─────────────────────────────────────┘│
│                                         │  ← FAB hidden during loading
├─────────────────────────────────────────┤
│  [Dashboard] [Customers] [■Apps] [Msgs] │
│                           [More]        │
└─────────────────────────────────────────┘
```

**Layout notes:**
- Shimmer blocks: `#E1E4D5` base → `#F0F1E6` highlight (trust_horizon gradient reversed), duration `short4` = 200ms, standard easing.
- Reduced-motion fallback: static `#E1E4D5` placeholder blocks with no animation.
- Each skeleton card mirrors the real card's 3-row height proportions. Card shape preserved: `#FFFFFF` bg, 12dp radius, 14dp padding.
- FAB not rendered during `loading` state.

---

## Screen: empty

```
┌─────────────────────────────────────────┐
│  Account Applications                   │
│                                         │
│  [■ All (8)] [Pending (3)] [Approved]   │  ← Filter chips remain active (switch filters)
│              [Rejected (2)]             │
│                                         │
│                                         │
│                   📋                    │  ← assignment icon, 48dp (icon-2xl), #44483D, centred
│                                         │
│          No Applications Found          │  ← title_medium (16sp/500), #1A1C16, centred
│                                         │
│   No account applications match the    │  ← body_medium (14sp/400), #44483D, centred
│          selected filter                │
│                                         │
│                                         │
│                               [+ New Application]│  ← FAB always visible
├─────────────────────────────────────────┤
│  [Dashboard] [Customers] [■Apps] [Msgs] │
│                           [More]        │
└─────────────────────────────────────────┘
```

**Layout notes:**
- Empty state content centred in available space between filter row and FAB. `spacing.xl` (32dp) padding around the empty zone.
- Icon: Material Symbols `assignment`, 48dp (`icon-2xl`), `#44483D` (on_surface_variant — sufficient contrast on `#F9FAEF`).
- FAB always visible in empty state to allow starting a new application.
- Filter chips remain interactive — Field Officer can switch filters to check if other statuses have applications.

---

## Screen: error

```
┌─────────────────────────────────────────┐
│  Account Applications                   │
│                                         │
│  [■ All (8)] [Pending (3)] [Approved]   │  ← Filter row visible (may retry with different filter)
│              [Rejected (2)]             │
│                                         │
│  ┌─────────────────────────────────────┐│
│  │  ⚠  Could not load account          ││  ← error_outline icon, #BA1A1A; body_medium #BA1A1A
│  │     applications.                   ││  ← error banner: #FFDAD6 bg, 12dp radius, 16dp H margin
│  │                                     ││
│  │     Check your connection and       ││  ← body_small #44483D
│  │     try again.                      ││
│  │                                     ││
│  │              [Retry]                ││  ← text button, label_medium #4C662B
│  └─────────────────────────────────────┘│
│                                         │
│                               [+ New Application]│
├─────────────────────────────────────────┤
│  [Dashboard] [Customers] [■Apps] [Msgs] │
│                           [More]        │
└─────────────────────────────────────────┘
```

**Layout notes:**
- Error banner: `#FFDAD6` bg (error_container), 12dp radius, 16dp H margin, 16dp padding. Layout: icon row → message row → Retry row.
- Error icon: `error_outline`, 20dp (`icon-sm`), `#BA1A1A`.
- Retry: text button (no fill), label_medium, `#4C662B`, centred. Dispatches `RetryLoad` event → re-calls `loadApplications()`.
- FAB remains visible in error state — Field Officer can still initiate a new application.

---

## Design Checklist (Figma / Stitch)

- [ ] Page title: Outfit headline_large (32sp/Regular), `#4C662B`, 20dp top / 4dp bottom / 16dp H padding
- [ ] Screen background: `#F9FAEF` (colors.light.background)
- [ ] Filter chip row: horizontal scroll, 8dp gap, 16dp H pad, 10dp V pad; pill chips 20dp radius
- [ ] Active filter chip ("All"): `#4C662B` solid fill, white text, Outfit/label_medium
- [ ] Pending filter selected: `#E8A317` solid fill, white text
- [ ] Rejected filter selected: `#BA1A1A` solid fill, white text
- [ ] Unselected chip: `#F9FAEF` bg, `#44483D` text
- [ ] Application cards: `#FFFFFF`, 12dp radius, 14dp padding, 16dp H margin, 10dp bottom gap, elevation 2
- [ ] Card name: Outfit/title_medium weight 700, `#1A1C16`
- [ ] Status chip shared bg: `#CDEDA3`, 12dp radius, 10dp H pad, 3dp V pad, 1dp border
- [ ] Pending chip: `#E8A317` border; text **`#44483D`** Outfit/label_small (a11y-corrected — NOT `#E8A317` on chip bg)
- [ ] Approved chip: `#4C662B` border + text
- [ ] Rejected chip: `#BA1A1A` border + text
- [ ] Card product name: Outfit/body_medium, `#4C662B`
- [ ] Card date: Outfit/body_small, `#44483D`
- [ ] Pending card: "Review" filled btn — `#4C662B` bg, white, Outfit/label_medium, 8dp radius, 16dp H / 8dp V pad
- [ ] Rejected card: "View Reason" link — Outfit/label_medium, `#BA1A1A`, underlined
- [ ] Extended FAB: `#4C662B` bg, white text + `add` icon (24dp), fixed bottom-right, 24dp bottom / 16dp right margin, elevation 6
- [ ] Loading: shimmer `#E1E4D5→#F0F1E6`, 200ms `short4`, 3 skeleton cards, FAB hidden
- [ ] Empty: `assignment` 48dp `#44483D` + centred title_medium + body_medium; FAB visible
- [ ] Error: `#FFDAD6` banner, `error_outline` 20dp `#BA1A1A`, Retry text btn `#4C662B`; FAB visible
- [ ] Field Officer bottom nav: 80dp height, `#F9FAEF` bg, `#C5C8BA` border-top, Applications tab has `#DCE7C8` active indicator pill
- [ ] All interactive elements: 48dp minimum touch target
- [ ] All text: Outfit typeface exclusively

---

_Generated by /idea export | 2026-05-30_
