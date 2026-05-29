# MOCKUP — Account Applications

**Archetype:** index_list
**Shell:** Field Officer bottom navigation bar (Applications tab active). Top app bar visible.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: content (Primary)

```
┌─────────────────────────────────────┐
│  Account Applications               │  ← TopAppBar, headline_large, #4C662B
├─────────────────────────────────────┤
│  [All (8)] [Pending (3)] [Approved] │  ← Scrollable filter chips; All = #4C662B filled
│            [Rejected (2)]           │
├─────────────────────────────────────┤
│  ┌───────────────────────────────┐  │
│  │  John Mwangi    [Pending Rev] │  │  ← title_medium/Bold + status chip (#CDEDA3/#E8A317)
│  │  KCB Savings Account          │  │  ← body_medium #4C662B
│  │  Submitted: 20 May 2026 [Review]│  ← body_small #44483D + filled btn #4C662B
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  Sarah Odhiambo  [Approved ✓] │  │  ← status chip (#CDEDA3/#4C662B border+text)
│  │  M-Shwari Checking Account    │  │
│  │  Submitted: 18 May 2026       │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  Peter Kamau    [Rejected ✗]  │  │  ← status chip (#CDEDA3/#BA1A1A border+text)
│  │  Business Current Account     │  │
│  │  Submitted: 12 May 2026 [View]│  │  ← "View Reason" #BA1A1A underline link
│  └───────────────────────────────┘  │
│                                 [+] │  ← Extended FAB "New Application" #4C662B, bottom-right
├─────────────────────────────────────┤
│  Dashboard | Customers |[Apps]|Msgs |  ← Field Officer BottomNav; Applications active
│             | More                  │
└─────────────────────────────────────┘
```

**Layout notes:**
- Filter chip bar: horizontal scroll, `spacing.sm` (8dp) gap between chips, `spacing.md` (16dp) horizontal padding. Active chip: solid `#4C662B` fill + white text. Unselected: `#F9FAEF` bg + `#44483D` text.
- Application cards: white `#FFFFFF`, 12dp radius, 14dp padding, 16dp horizontal margin, 10dp bottom gap, elevation 2.
- Card header row: applicant name (flex 1, title_medium/Bold) + status chip (right-aligned, 12dp radius, 10dp H padding, 3dp V padding).
- Card footer row: date text (flex 1, body_small) + action (Review button or View Reason link).
- FAB: fixed bottom-right, 16dp right + bottom margin; extended FAB with `add` icon + "New Application" label.
- Bottom nav: `#F9FAEF` bg, `#C5C8BA` border-top, 80dp height. Applications tab has `#DCE7C8` active pill.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│  Account Applications               │
├─────────────────────────────────────┤
│  [All (8)] [Pending (3)] [Approved] │
│            [Rejected (2)]           │
├─────────────────────────────────────┤
│  ┌───────────────────────────────┐  │
│  │  ░░░░░░░░░░░░  ░░░░░░░░░░░░  │  │  ← Card skeleton row 1 (name + chip)
│  │  ░░░░░░░░░░░░░░░░░░░░░░░░░░  │  │  ← Card skeleton row 2 (product)
│  │  ░░░░░░░░░░░░  ░░░░░░░░░░░   │  │  ← Card skeleton row 3 (date + button)
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  ░░░░░░░░░░░░  ░░░░░░░░░░░░  │  │
│  │  ░░░░░░░░░░░░░░░░░░░░░░░░░░  │  │
│  │  ░░░░░░░░░░░░               │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  ░░░░░░░░░░░░  ░░░░░░░░░░░░  │  │
│  │  ░░░░░░░░░░░░░░░░░░░░░░░░░░  │  │
│  │  ░░░░░░░░░░░░               │  │
│  └───────────────────────────────┘  │
├─────────────────────────────────────┤
│  Dashboard | Customers |[Apps]|Msgs |
└─────────────────────────────────────┘
```

**Layout notes:** Shimmer (`#E1E4D5` → `#F0F1E6`) on all card skeleton blocks. Filter tabs remain rendered. FAB hidden during load. Bottom nav visible.

---

## Screen: empty

```
┌─────────────────────────────────────┐
│  Account Applications               │
├─────────────────────────────────────┤
│  [All (8)] [Pending (3)] [Approved] │
├─────────────────────────────────────┤
│                                     │
│             📋                      │  ← assignment icon, 48dp, #44483D, centred
│                                     │
│        No Applications Found        │  ← title_medium, centred, #1A1C16
│  No account applications match the  │  ← body_medium, centred, #44483D
│      selected filter                │
│                                     │
│                                 [+] │  ← FAB still visible
├─────────────────────────────────────┤
│  Dashboard | Customers |[Apps]|Msgs |
└─────────────────────────────────────┘
```

**Layout notes:** Empty state centred in content area. Filter chips remain active so user can switch filters. FAB always visible to enable new application creation.

---

## Screen: error

```
┌─────────────────────────────────────┐
│  Account Applications               │
├─────────────────────────────────────┤
│  [All (8)] [Pending (3)] [Approved] │
├─────────────────────────────────────┤
│  ┌───────────────────────────────┐  │
│  │  ⚠  Could not load           │  │  ← Error banner, #FFDAD6 bg, #BA1A1A text
│  │     account applications.     │  │
│  │     [Retry]                   │  │  ← Text button #4C662B
│  └───────────────────────────────┘  │
│                                     │
├─────────────────────────────────────┤
│  Dashboard | Customers |[Apps]|Msgs |
└─────────────────────────────────────┘
```

**Layout notes:** Error banner full-width with 16dp horizontal margin. Error icon + message + retry button in column. Filter chips remain visible for potential retry with different state.

---

## Design Checklist (Figma / Stitch)

- [ ] Page title headline_large (32sp) in `#4C662B`
- [ ] Scrollable filter chip row: filled chip for active state (green/amber/red per filter), outlined for inactive
- [ ] Application cards: white `#FFFFFF`, 12dp radius, 2dp elevation, 16dp horizontal margin
- [ ] Card header: applicant name (title_medium/Bold) + status chip (right-aligned, 12dp radius)
- [ ] Status chip colors: Pending = `#CDEDA3` bg + `#E8A317` border; Approved = `#CDEDA3` + `#4C662B`; Rejected = `#CDEDA3` + `#BA1A1A`
- [ ] Status chip text contrast: `#44483D` for Pending (a11y-corrected), `#4C662B` for Approved, `#BA1A1A` for Rejected
- [ ] Pending card: "Review" filled button bottom-right
- [ ] Rejected card: "View Reason" underlined link in `#BA1A1A`
- [ ] Extended FAB "New Application" `#4C662B`, fixed bottom-right, elevation 6
- [ ] Shimmer skeleton matching 3-row card layout proportions
- [ ] Empty state: `assignment` icon + message centred
- [ ] Field Officer bottom navigation bar (5 items), Applications tab active with `#DCE7C8` pill
- [ ] 48dp touch targets on all interactive elements
