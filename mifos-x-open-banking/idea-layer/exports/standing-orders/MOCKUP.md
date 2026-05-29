# MOCKUP — Standing Orders

**Archetype:** index_list
**Shell:** Top app bar ("Standing Orders", back arrow, filter action). No bottom navigation bar.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│ ←  Standing Orders        [filter]  │  ← TopAppBar, arrow_back + filter_list
├─────────────────────────────────────┤
│                                     │
│  Standing Orders                    │  ← headline_large, #4C662B
│                                     │
│  ┌───────────────────────────────┐  │
│  │  ████████████████████████████ │  │  ← Skeleton card 1 (68dp)
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  ████████████████████████████ │  │  ← Skeleton card 2 (68dp)
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  ████████████████████████████ │  │  ← Skeleton card 3 (68dp)
│  └───────────────────────────────┘  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Shimmer animation on 3 skeleton cards (radius 16dp, height ~100dp each). No FAB during load.

---

## Screen: content

```
┌─────────────────────────────────────┐
│ ←  Standing Orders        [filter]  │
├─────────────────────────────────────┤
│                                     │
│  Standing Orders  [3 active]        │  ← title row: headline_large #4C662B +
│                                     │    chip #CDEDA3 bg / #4C662B text
│  ┌───────────────────────────────┐  │
│  │  Rent Payment      [Active]   │  │  ← white card, elevation 2, radius 16
│  │  To: Landlord Holdings Ltd    │  │  ← body_medium #44483D
│  │  £1,200 / month  Next: 1 Jun  │  │  ← body_large #4C662B | body_small #44483D
│  │                      [✎] [🗑] │  │  ← edit #4C662B | delete #BA1A1A
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  Netflix Subscription [Active]│  │  ← white card
│  │  £15.99 / month  Next: 7 Jun  │  │
│  │                      [✎] [🗑] │  │
│  └───────────────────────────────┘  │
│  ┌ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─┐  │
│  │  Gym Membership    [Paused]   │  │  ← outlined card #F9FAEF, border #E1E4D5
│  │  £45.00 / month  Next: 15 Jun │  │  ← muted color #44483D throughout
│   ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ │  │
│                                     │
│                 [+ Create Standing Order]│  ← Extended FAB, #4C662B, radius 16
└─────────────────────────────────────┘
```

**Layout notes:**
- Title row: "Standing Orders" headline_large left-aligned + "3 active" chip (#CDEDA3, radius 12, 10dp H-pad).
- Active cards: white `#FFFFFF`, radius 16dp, elevation 2, 16dp padding. Status badge "Active" in `#CDEDA3`/`#4C662B`.
- Paused card: `#F9FAEF` background, `#E1E4D5` 1dp border, all text muted `#44483D`. Badge "Paused" in `#F9FAEF`/`#44483D`.
- Edit icon (edit_outlined, 22dp, `#4C662B`) and delete icon (delete_outlined, 22dp, `#BA1A1A`) at flex_end per card.
- Extended FAB: `#4C662B` fill, white text "Create Standing Order", + icon, radius 16dp, elevation 6. Anchored bottom-right over scrollable content.
- Cards separated by 16dp margin_bottom.

---

## Screen: empty

```
┌─────────────────────────────────────┐
│ ←  Standing Orders        [filter]  │
├─────────────────────────────────────┤
│                                     │
│  Standing Orders                    │
│                                     │
│         ┌────────────────┐          │
│         │  [repeat_off]  │          │  ← icon 48dp, #44483D
│         └────────────────┘          │
│         No standing orders          │  ← titleMedium, #1A1C16, center
│   Set up recurring payments to      │  ← bodyMedium, #44483D, center
│   automate your regular bills       │
│                                     │
│                 [+ Create Standing Order]│  ← Extended FAB
└─────────────────────────────────────┘
```

**Layout notes:** Empty state centred vertically below title. Icon 48dp in `#44483D`. Title titleMedium `#1A1C16`, body bodyMedium `#44483D`. FAB still visible to drive first creation.

---

## Screen: error

```
┌─────────────────────────────────────┐
│ ←  Standing Orders        [filter]  │
├─────────────────────────────────────┤
│                                     │
│  Standing Orders                    │
│                                     │
│         ┌────────────────┐          │
│         │  [cloud_off]   │          │  ← icon 48dp, #BA1A1A
│         └────────────────┘          │
│    Unable to load standing orders   │  ← titleMedium, #1A1C16, center
│  Check your connection and try again│  ← bodyMedium, #44483D, center
│                                     │
│         ┌──────────────┐            │
│         │    Retry     │            │  ← OutlinedButton, #4C662B border+text
│         └──────────────┘            │
│                 [+ Create Standing Order]│  ← FAB persists
└─────────────────────────────────────┘
```

**Layout notes:** Error icon 48dp in `#BA1A1A`. Retry is OutlinedButton (pill radius, `#4C662B` text + border). FAB persists — user can still attempt new order creation while viewing error.

---

## Design Checklist (Figma / Stitch)

- [ ] M3 TopAppBar with back arrow + filter_list icon action
- [ ] Active order cards: white `#FFFFFF`, radius 16dp, elevation 2
- [ ] Paused order card: `#F9FAEF` background, `#E1E4D5` 1dp outline border
- [ ] "Active" badge: `#CDEDA3` fill, `#4C662B` text, radius 10dp
- [ ] "Paused" badge: `#F9FAEF` fill, `#44483D` text, radius 10dp
- [ ] Count chip ("3 active"): `#CDEDA3` fill, `#4C662B` text, radius 12dp
- [ ] Edit icon `edit_outlined` 22dp in `#4C662B` per card
- [ ] Delete icon `delete_outlined` 22dp in `#BA1A1A` per card
- [ ] Extended FAB: `#4C662B` fill, white text, + icon, radius 16dp, elevation 6
- [ ] Empty state: repeat_off 48dp icon, centred body copy
- [ ] Error state: cloud_off 48dp icon, OutlinedButton retry
- [ ] 3 skeleton shimmer cards (loading state, radius 16dp)
- [ ] All text uses Outfit typeface
- [ ] 16dp horizontal content padding throughout
- [ ] 16dp vertical gap between order cards
