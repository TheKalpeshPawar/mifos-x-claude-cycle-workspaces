# MOCKUP — Application Detail

**Archetype:** detail_screen
**Shell:** Top app bar ("Application Detail") with back arrow. No bottom navigation bar (fieldOfficer flow).
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│ ←  Application Detail               │  ← TopAppBar, back arrow
├─────────────────────────────────────┤
│  ██████████████████████████████████ │  ← Header skeleton (#4C662B shimmer)
│  ████████████  ██████████           │  ← Ref number + status chip skeleton
├─────────────────────────────────────┤
│                                     │
│  ┌───────────────────────────────┐  │
│  │  ██████████████████████████  │  │  ← Customer info card skeleton
│  │  ██████████████████████████  │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  ██████████████████████████  │  │  ← Application details card skeleton
│  │  ██████████  ████████████    │  │
│  │  ██████████  ████████████    │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  ████████████████████████████│  │  ← KYC row skeleton
│  └───────────────────────────────┘  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Full-width shimmer blocks animate left-to-right at 300ms. Header block reflects #4C662B tonal shimmer. No action buttons visible during load.

---

## Screen: reviewing (content)

```
┌─────────────────────────────────────┐
│ ←  Application Detail               │  ← TopAppBar, back arrow, #F9FAEF bg
├─────────────────────────────────────┤
│  ┌─────────────────────────────────┐│
│  │ Application #OBP-2026-00234     ││  ← #4C662B header, title_large/700, #FFFFFF
│  │ [Pending Review]  20 May 2026   ││  ← Chip: #CDEDA3/#44483D · date: body_small/#CDEDA3
│  └─────────────────────────────────┘│
│                                     │
│  ┌───────────────────────────────┐  │
│  │  CUSTOMER                     │  │  ← label_medium/#44483D, uppercase
│  │  John Kamau Mwangi   View Profile│ ← title_medium/#1A1C16 · link: #4C662B underline
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  APPLICATION DETAILS          │  │  ← label_medium/#44483D, uppercase
│  │  Account Type   KCB Savings   │  │  ← body_medium label/#44483D · value/#1A1C16 600
│  │  Requested Limit  KES 500,000 │  │  ← value monospace, weight 600
│  │  Purpose                      │  │
│  │  Personal savings and         │  │
│  │  salary credit                │  │  ← body_medium, #1A1C16
│  └───────────────────────────────┘  │
│                                     │
│  ┌─────────────────────────────────┐│
│  │ ✓  KYC Status: Verified ✓      ││  ← #CDEDA3 bg, #4C662B border+text, icon 20dp
│  └─────────────────────────────────┘│
│                                     │
│  Supporting Documents               │  ← title_medium/#1A1C16
│                                     │
│  ┌───────────────────────────────┐  │
│  │ [ID img] National ID          │  │  ← 56×40dp thumb, #4C662B border
│  │          Verified ✓    [View] │  │  ← body_small/#4C662B · label_medium link
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │ [ home ] Proof of Address     │  │  ← icon placeholder, #E8A317 border
│  │          Pending Upload [Upload]│ ← #44483D · outlined button #4C662B
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  Review Notes                 │  │  ← outlined textarea, 3 min lines
│  │  Add internal notes about...  │  │  ← placeholder body_medium/#44483D
│  │                               │  │
│  └───────────────────────────────┘  │
│                                     │
│  [    Approve Application    ]      │  ← filled #4C662B, full-width, label_large/White
│  [    Reject Application     ]      │  ← outlined #BA1A1A, full-width
│       Request Information           │  ← text button #4C662B
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:**
- Header box: full-width, 16dp horizontal padding, 16dp vertical padding; chip is 12dp radius, 8dp hpad, 4dp vpad.
- Customer and application detail cards: 16dp horizontal margin, 12dp radius, 2dp elevation.
- KYC row: #CDEDA3 fill, 1px #4C662B border, 12dp radius, 14dp padding. verified_user icon 20dp left of text.
- Document cards: 10dp radius, 1dp #E1E4D5 border, 14dp padding. National ID thumbnail 56×40dp with 6dp radius and #4C662B border.
- Review notes input: 16dp horizontal margin, min 3 / max 6 lines, outlined variant.
- Approve / Reject buttons: full-width with 16dp horizontal margin, 16dp padding. 8dp gap between buttons. Request Information is text-only with 24dp bottom margin.

---

## Screen: approved

```
┌─────────────────────────────────────┐
│ ←  Application Detail               │
├─────────────────────────────────────┤
│  ┌─────────────────────────────────┐│
│  │  ✓  Application approved        ││  ← Success banner: #CDEDA3 bg, body_medium/#4C662B
│  │     successfully               ││
│  └─────────────────────────────────┘│
│                                     │
│  [full reviewing layout below...]   │
│                                     │
│  [   Approve Application (✓)  ]     │  ← disabled / confirmed state
│  [    Reject Application      ]     │  ← disabled
└─────────────────────────────────────┘
```

**Layout notes:** Banner is a full-width box with #CDEDA3 background and #4C662B text, inserted above the application header. Action buttons disabled after decision.

---

## Screen: rejected

```
┌─────────────────────────────────────┐
│ ←  Application Detail               │
├─────────────────────────────────────┤
│  ┌─────────────────────────────────┐│
│  │  ✗  Application rejected        ││  ← Error banner: #FFDAD6 bg, body_medium/#BA1A1A
│  └─────────────────────────────────┘│
│                                     │
│  [full reviewing layout below...]   │
│                                     │
│  [    Approve Application     ]     │  ← disabled
│  [   Reject Application (✓)  ]      │  ← disabled / confirmed state
└─────────────────────────────────────┘
```

**Layout notes:** Rejection banner uses error_container (#FFDAD6) background, on_error_container (#410002) text.

---

## Screen: empty

```
┌─────────────────────────────────────┐
│ ←  Application Detail               │
├─────────────────────────────────────┤
│                                     │
│                                     │
│         [description_off icon]      │  ← 48dp icon, #44483D
│                                     │
│    Application details not          │
│         available                   │  ← body_large, #1A1C16, centered
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Centered vertically in viewport. Icon 48dp using description_off. No action buttons visible.

---

## Screen: error

```
┌─────────────────────────────────────┐
│ ←  Application Detail               │
├─────────────────────────────────────┤
│                                     │
│              ⚠                      │  ← error icon, 48dp, #BA1A1A
│                                     │
│   Unable to load application        │
│   Check your connection and         │
│         try again.                  │  ← body_medium, #44483D, centered
│                                     │
│        [ Try Again ]                │  ← filled #4C662B, centered
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Error icon + messages + retry button centred vertically.

---

## Design Checklist (Figma / Stitch)

- [ ] M3 TopAppBar with back navigation icon, #F9FAEF background
- [ ] Full-width #4C662B header box with application reference number and status chip
- [ ] Status chip uses #CDEDA3 background and #44483D text (WCAG AA compliant)
- [ ] White cards with 12dp radius and 2dp elevation for customer and application sections
- [ ] KYC verified row: #CDEDA3 fill, 1px #4C662B border, verified_user icon 20dp
- [ ] National ID thumbnail 56×40dp with #4C662B border-radius 6dp
- [ ] Proof of Address placeholder with home icon and #E8A317 border (pending state)
- [ ] Outlined textarea with 3–6 line range for review notes
- [ ] Approve button: filled #4C662B, full-width pill (999dp radius), Label Large
- [ ] Reject button: outlined #BA1A1A border/text, full-width pill
- [ ] Request Information: text-only #4C662B button
- [ ] Success banner: #CDEDA3 background, #4C662B text
- [ ] Rejection banner: error_container #FFDAD6 background
- [ ] All text uses Outfit typeface; min 14sp body text
- [ ] 16dp horizontal content padding throughout
- [ ] Skeleton shimmer on loading state matches content layout proportions
