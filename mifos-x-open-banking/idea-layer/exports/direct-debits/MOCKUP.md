# MOCKUP — Direct Debits

**Archetype:** index_list
**Shell:** Top app bar ("Direct Debits") + back arrow + overflow (more_vert). No bottom navigation bar.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│ ←  Direct Debits          ⋮         │  ← M3 TopAppBar, back arrow, overflow
├─────────────────────────────────────┤
│                                     │
│  Direct Debits   [████████]         │  ← Title + skeleton active-count chip
│                                     │
│  ┌───────────────────────────────┐  │
│  │ ████████████████   [██████]   │  │  ← Skeleton mandate card 1 (110dp)
│  │ ████████████████              │  │
│  │ ████████  ████████████████    │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │ ████████████████   [██████]   │  │  ← Skeleton mandate card 2 (110dp)
│  │ ████████████████              │  │
│  │ ████████  ████████████████    │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │ ████████████████   [██████]   │  │  ← Skeleton mandate card 3 (110dp)
│  │ ████████████████              │  │
│  │ ████████  ████████████████    │  │
│  └───────────────────────────────┘  │
│                                     │
│                       [+ Set Up DD] │  ← FAB, earth-green, bottom-right
└─────────────────────────────────────┘
```

**Layout notes:** Shimmer animation on 3 skeleton cards, each 110dp height. FAB always visible.

---

## Screen: populated

```
┌─────────────────────────────────────┐
│ ←  Direct Debits          ⋮         │
├─────────────────────────────────────┤
│                                     │
│  Direct Debits   [3 active]         │  ← Title (headline_large, #4C662B) + chip (#CDEDA3)
│                                     │
│  ┌───────────────────────────────┐  │
│  │  Netflix              [Active]│  │  ← title_medium + green badge
│  │  £15.99 / month  Next: 3 Jun  │  │  ← body_large green + body_small grey
│  │  Ref: DD-NF-20240301          │  │  ← label_small grey
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  Spotify              [Active]│  │
│  │  £10.99 / month  Next: 12 Jun │  │
│  │  Ref: DD-SP-20231115          │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┐  │
│  │  PureGym          [Cancelled] │  │  ← Muted card (#F9FAEF fill, grey text)
│  │  £29.99 / month               │  │
│  │  Ref: DD-GYM-20220601         │  │
│  └ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┘  │
│                                     │
│                       [+ Set Up DD] │
└─────────────────────────────────────┘
```

**Layout notes:**
- Active cards: white fill (#FFFFFF), 16dp radius, 2dp elevation, 20dp horizontal margin.
- Cancelled card: #F9FAEF fill, #E1E4D5 border, 0dp elevation — visually recedes.
- Badge: Active = #CDEDA3 + #4C662B; Cancelled = #F9FAEF + #44483D.
- Amount: Active = #4C662B semibold; Cancelled = #44483D normal weight.

---

## Screen: empty

```
┌─────────────────────────────────────┐
│ ←  Direct Debits          ⋮         │
├─────────────────────────────────────┤
│                                     │
│  Direct Debits                      │
│                                     │
│                                     │
│         [account_balance_wallet]    │  ← icon 48dp, #44483D
│                                     │
│       No direct debits set up       │  ← title_medium, #1A1C16, center
│                                     │
│  Authorise merchants like Netflix   │  ← body_medium, #44483D, center
│  or utility providers to collect    │
│  payments automatically.            │
│                                     │
│                       [+ Set Up DD] │
└─────────────────────────────────────┘
```

**Layout notes:** Empty state centred vertically in content area. FAB remains accessible.

---

## Screen: cancel_confirm

```
┌─────────────────────────────────────┐
│ ←  Direct Debits          ⋮         │
├─────────────────────────────────────┤
│░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░│  ← 50% alpha scrim over mandate list
│░  Netflix              [Active]   ░│
│░  £15.99 / month  Next: 3 Jun     ░│
│░  ...                             ░│
│░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░│
│                                     │
│  ┌───────────────────────────────┐  │  ← Dialog: white, 20dp radius, 8dp elevation
│  │  Cancel Direct Debit?         │  │  ← headline_small, #1A1C16, bold
│  │                               │  │
│  │  Netflix (DD-NF-20240301)     │  │  ← body_medium, #44483D
│  │  will stop collecting         │  │
│  │  payments. Cannot be undone.  │  │
│  │                               │  │
│  │  ┌─────────────────────────┐  │  │  ← Filled button, #BA1A1A
│  │  │   Yes, Cancel Mandate   │  │  │
│  │  └─────────────────────────┘  │  │
│  │  ┌─────────────────────────┐  │  │  ← Outlined button, #4C662B
│  │  │      Keep Mandate       │  │  │
│  │  └─────────────────────────┘  │  │
│  └───────────────────────────────┘  │
└─────────────────────────────────────┘
```

**Layout notes:** Dialog is centred with 24dp padding. Destructive action (red) above safe action (green). Esc / outside tap → dismiss.

---

## Screen: error

```
┌─────────────────────────────────────┐
│ ←  Direct Debits          ⋮         │
├─────────────────────────────────────┤
│                                     │
│  Direct Debits                      │
│                                     │
│                                     │
│              [cloud_off]            │  ← icon 48dp, #44483D
│                                     │
│    Unable to load direct debits     │  ← title_medium, center
│  Check your connection and retry.   │  ← body_medium, #44483D, center
│                                     │
│         ┌─────────────┐             │
│         │    Retry    │             │  ← outlined button, #4C662B
│         └─────────────┘             │
│                                     │
│                       [+ Set Up DD] │
└─────────────────────────────────────┘
```

**Layout notes:** Error state centred. FAB remains visible for setup.

---

## Design Checklist (Figma / Stitch)

- [ ] M3 TopAppBar with back navigation + overflow (more_vert) icon
- [ ] Screen title in headline_large (Outfit 32sp), earth-green #4C662B
- [ ] Active count chip: #CDEDA3 fill, #4C662B text, 12dp radius, label_medium semibold
- [ ] Active mandate cards: #FFFFFF fill, 16dp radius, 2dp elevation; 20dp horizontal margin
- [ ] Cancelled mandate card: #F9FAEF fill, #E1E4D5 border, 0dp elevation — muted visual
- [ ] Status badge: Active = #CDEDA3 + #4C662B; Cancelled = #F9FAEF + #44483D
- [ ] Amount text: Active = #4C662B semibold; Cancelled = #44483D normal
- [ ] FAB: #4C662B fill, add icon, 16dp radius, always floating bottom-right
- [ ] Cancel dialog: 20dp radius, 8dp elevation, 24dp padding, 50% scrim behind
- [ ] Destructive CTA: #BA1A1A fill (Yes, Cancel Mandate)
- [ ] Safe CTA: outlined #4C662B (Keep Mandate)
- [ ] Skeleton cards: 3 shimmer blocks, 110dp height each
- [ ] Empty state: account_balance_wallet icon + title + instruction copy
- [ ] Error state: cloud_off icon + message + Retry button
- [ ] All text: Outfit typeface. Touch targets: 48dp minimum.
- [ ] 20dp horizontal content padding throughout
