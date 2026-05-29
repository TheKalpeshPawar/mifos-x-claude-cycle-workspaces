# MOCKUP — Customer Messages

**Archetype:** index_list
**Shell:** Field Officer bottom navigation bar — Messages tab active (mail icon, badge visible). Top app bar hidden on this screen.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: content (Primary)

```
┌─────────────────────────────────────┐
│                                     │  ← Background #F9FAEF
│  Messages            [5 unread]     │  ← headline_large #4C662B + red badge #BA1A1A
│                                     │
│  ┌──────────────────────────────┐   │
│  │ 🔍 Search messages...        │   │  ← Pill search bar #F9FAEF bg, radius 28
│  └──────────────────────────────┘   │
│                                     │
│  ┌──────────────────────────────┐   │  ← Unread thread — #CDEDA3 bg, border #C5C8BA
│  │ [JM]  John Mwangi     2 min  │   │    44×44 circle avatar #4C662B
│  │       Please send me the acc…│   │    title_small bold + body_medium
│  │                           ●  │   │    10dp green dot (#4C662B) unread indicator
│  └──────────────────────────────┘   │
│                                     │
│  ┌──────────────────────────────┐   │  ← Read thread — #FFFFFF bg, border #E1E4D5
│  │ [SO]  Sarah Odhiambo  1 hr   │   │    44×44 circle avatar #386663
│  │       Thank you for approving│   │    title_small w600 + body_medium #44483D
│  └──────────────────────────────┘   │
│                                     │
│  ┌──────────────────────────────┐   │  ← Read thread — #FFFFFF bg
│  │ [PK]  Peter Kamau  Yesterday │   │    44×44 circle avatar #44483D
│  │       When can I expect my…  │   │
│  └──────────────────────────────┘   │
│                                     │
│                                     │
│              [✏ New Message]        │  ← Extended FAB, #4C662B, bottom-right
│                                     │
├─────────────────────────────────────┤
│  [⊞]   [👥]   [📋]   [✉]   [⋮]   │  ← Bottom nav: Dashboard / Customers / Applications / Messages★ / More
└─────────────────────────────────────┘
```

**Layout notes:**
- Header row: "Messages" headline_large + red badge side-by-side, pad H16 T20 B8.
- Search bar: margin H16, radius 28, 8dp bottom margin.
- Thread cards: margin H16, margin B8 between cards, pad 14. Horizontal layout: avatar (flex-shrink 0) + content column (flex 1) + dot/time.
- Unread card: #CDEDA3 background + bold name + green (#4C662B) timestamp + unread dot.
- Read card: #FFFFFF background + regular weight name + #44483D timestamp, no dot.
- FAB: position bottom-right, margin B24 R16, elevation 6.
- Bottom nav height 80dp, border-top #C5C8BA.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│  Messages            [████]         │  ← Title + badge skeleton
│                                     │
│  ┌──────────────────────────────┐   │
│  │ ████████████████████████████ │   │  ← Search bar skeleton
│  └──────────────────────────────┘   │
│                                     │
│  ┌──────────────────────────────┐   │
│  │ [██] ████████████  ████      │   │  ← Thread card skeleton ×3
│  │      ████████████████████    │   │    shimmer animation on #F0F1E6
│  └──────────────────────────────┘   │
│  ┌──────────────────────────────┐   │
│  │ [██] ████████████  ████      │   │
│  │      ████████████████████    │   │
│  └──────────────────────────────┘   │
│  ┌──────────────────────────────┐   │
│  │ [██] ████████████  ████      │   │
│  │      ████████████████████    │   │
│  └──────────────────────────────┘   │
├─────────────────────────────────────┤
│  [⊞]   [👥]   [📋]   [✉]   [⋮]   │
└─────────────────────────────────────┘
```

**Layout notes:** Shimmer animation applied to all skeleton blocks on #F0F1E6 base. Avatar circle placeholder 44dp. No interactive elements during loading.

---

## Screen: empty

```
┌─────────────────────────────────────┐
│  Messages                           │
│                                     │
│  ┌──────────────────────────────┐   │
│  │ 🔍 Search messages...        │   │
│  └──────────────────────────────┘   │
│                                     │
│                                     │
│           ✉                         │  ← forum icon 48dp, #44483D
│                                     │
│         No Messages                 │  ← title_medium #1A1C16, centered
│  Start a conversation by            │  ← body_medium #44483D, centered
│  composing a new message            │
│  to a customer                      │
│                                     │
│              [✏ New Message]        │  ← FAB still visible
│                                     │
├─────────────────────────────────────┤
│  [⊞]   [👥]   [📋]   [✉]   [⋮]   │
└─────────────────────────────────────┘
```

**Layout notes:** Icon + text block centered in remaining vertical space. FAB remains accessible to compose first message.

---

## Screen: error

```
┌─────────────────────────────────────┐
│  Messages                           │
│                                     │
│  ┌──────────────────────────────┐   │
│  │ ⚠ Could not load messages.   │   │  ← Error banner, #FFDAD6 bg, #BA1A1A icon
│  │        [Try Again]            │   │  ← Outlined retry button
│  └──────────────────────────────┘   │
│                                     │
├─────────────────────────────────────┤
│  [⊞]   [👥]   [📋]   [✉]   [⋮]   │
└─────────────────────────────────────┘
```

**Layout notes:** Error banner full-width, M3 error container color. Retry button text-style, #BA1A1A.

---

## Design Checklist (Figma / Stitch)

- [ ] Field Officer bottom nav: 5 items, Messages tab has active indicator (#DCE7C8 pill), mail icon with badge
- [ ] Unread thread: #CDEDA3 background, bold name, #4C662B timestamp, 10dp green dot trailing
- [ ] Read thread: #FFFFFF background, regular weight name, #44483D timestamp, no dot
- [ ] Avatar circles 44×44, border-radius 22dp, initials Outfit/label_large white bold
- [ ] Extended FAB: #4C662B fill, white text + edit icon, bottom-right, elevation 6
- [ ] Compose dialog: radius 20, white bg, customer autocomplete + subject + textarea min 4 lines
- [ ] Skeleton shimmer 3 cards; animation on #F0F1E6 base
- [ ] Search pill radius 28, #F9FAEF fill, search icon leading
- [ ] Empty state: forum icon 48dp + title + subtitle centered
- [ ] All text Outfit typeface; 16dp horizontal content padding throughout
