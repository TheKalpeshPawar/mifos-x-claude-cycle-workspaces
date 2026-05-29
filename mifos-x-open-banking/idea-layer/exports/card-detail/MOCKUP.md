# MOCKUP — Card Detail

**Archetype:** detail_screen
**Shell:** Top app bar ("Card Details") with back arrow and more_vert overflow. No bottom navigation bar.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│ ←  Card Details               [⋮]   │  ← TopAppBar, back + more_vert
├─────────────────────────────────────┤
│                                     │
│  ┌───────────────────────────────┐  │
│  │                               │  │  ← Card visual skeleton (340×210dp)
│  │  ████████████████████████████ │  │     shimmer over #4C662B
│  │                               │  │
│  └───────────────────────────────┘  │
│                                     │
│  ████████████████████████           │  ← "Show card details" link skeleton
│                                     │
│  ┌───────────────────────────────┐  │
│  │  ████████████████  ░░░░░░░░░  │  │  ← Status row skeleton (label + switch)
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  ████████████████████████████ │  │  ← Limits skeleton
│  │  ████████████  ████████████   │  │
│  │  ████████████  ████████████   │  │
│  └───────────────────────────────┘  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Card visual skeleton is full proportional size (340×210dp, radius 20). 4 skeleton field rows below. No buttons visible during load.

---

## Screen: content (card active)

```
┌─────────────────────────────────────┐
│ ←  Card Details               [⋮]   │
├─────────────────────────────────────┤
│                                     │
│   ┌─────────────────────────────┐   │
│   │                             │   │  ← #4C662B card, radius 20, elevation 12
│   │  •••• •••• •••• 4521        │   │  ← title_large, #FFFFFF, monospace, spacing 4
│   │                             │   │
│   │  ALEX JOHNSON        [VISA] │   │  ← body_large/#CDEDA3 uppercase · Visa logo white
│   │  09/29                      │   │  ← body_medium/#CDEDA3 monospace
│   └─────────────────────────────┘   │
│                                     │
│       Show card details             │  ← label_large, #4C662B, underline, centered
│   (tap to reveal via biometrics)    │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  Card Active            [●]  │  │  ← body_large/#1A1C16 · switch checked #4C662B
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  Spending Limits              │  │  ← title_medium, #1A1C16, weight 600
│  │  ─────────────────────────── │  │
│  │  Daily limit     £2,500  [✎] │  │  ← body_medium/#44483D · body_large/#1A1C16 · edit #4C662B
│  │  ─────────────────────────── │  │
│  │  Monthly limit  £10,000  [✎] │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │ ❄  Freeze Card               │  │  ← outlined, #E8A317 border, #44483D text, ac_unit icon
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │ ⚠  Report Lost/Stolen        │  │  ← outlined, #BA1A1A border/text, report_problem icon
│  └───────────────────────────────┘  │
│                                     │
│    🧾  View Transactions            │  ← text #4C662B, receipt_long icon, label_large
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:**
- Card visual: 340dp wide, 210dp tall, radius 20, elevation 12. Auto-centered with 8dp top margin and 24dp bottom margin.
- Card text: PAN title_large/white/monospace/spacing 4. Cardholder body_large/#CDEDA3/uppercase. Expiry body_medium/#CDEDA3. Visa logo 60×22dp white tinted right-bottom.
- "Show card details" link: text-centered, label_large, #4C662B, underline, 4dp vertical padding.
- Card status row: white fill, 12dp radius, 1dp elevation, 16dp horizontal/vertical padding; toggle switch right-aligned.
- Limits section: white fill, 12dp radius, 1dp elevation, 20dp padding; dividers between rows using #F9FAEF 1px.
- Edit icons: 20dp, #4C662B, right-aligned per row.
- Freeze button: full-width, radius 12, 14dp vertical padding, #E8A317 border, #44483D text (accessible).
- Report button: full-width, radius 12, 14dp vertical padding, #BA1A1A border/text.
- View Transactions: text-only button, full-width, receipt_long icon leading, #4C662B.

---

## Screen: frozen

```
┌─────────────────────────────────────┐
│ ←  Card Details               [⋮]   │
├─────────────────────────────────────┤
│                                     │
│   ┌─────────────────────────────┐   │
│   │░░░░░░░░░░░░░░░░░░░░░░░░░░░░░│   │  ← #4C662B card with #C5C8BA80 grey overlay
│   │░░░░░  F R O Z E N  ░░░░░░░░│   │  ← "FROZEN" watermark, centered, white/50%
│   │░░░░░░░░░░░░░░░░░░░░░░░░░░░░░│   │
│   └─────────────────────────────┘   │
│                                     │
│   (reveal_card_details_link hidden) │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  Card Active            [○]  │  │  ← switch unchecked (greyed)
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  Spending Limits              │  │
│  │  ─────────────────────────── │  │
│  │  (limits hidden in frozen)    │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │ 🔓  Unfreeze Card            │  │  ← outlined, #4C662B border/text, lock_open icon
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │ ⚠  Report Lost/Stolen        │  │
│  └───────────────────────────────┘  │
│                                     │
│    🧾  View Transactions            │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Card overlay: #C5C8BA at 50% opacity covers the card visual. "FROZEN" watermark in white center. Reveal link hidden. Freeze button relabeled "Unfreeze Card" with lock_open icon and #4C662B border/text.

---

## Screen: error

```
┌─────────────────────────────────────┐
│ ←  Card Details               [⋮]   │
├─────────────────────────────────────┤
│                                     │
│         credit_card_off             │  ← 48dp icon, #BA1A1A
│                                     │
│   Unable to load card details       │  ← body_large, #1A1C16, centered
│   Please try again or               │
│       contact support               │  ← body_medium, #44483D, centered
│                                     │
│          [ Try Again ]              │  ← filled #4C662B, centered
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Error icon + messages + retry centered vertically in viewport.

---

## Screen: empty

```
┌─────────────────────────────────────┐
│ ←  Card Details               [⋮]   │
├─────────────────────────────────────┤
│                                     │
│         credit_card_off             │  ← 48dp icon, #44483D
│                                     │
│   Card information not available    │  ← body_large, #1A1C16, centered
│                                     │
│   No card data was found.           │
│   The card may have been            │
│   cancelled or removed.             │  ← body_medium, #44483D, centered
│                                     │
│          [ Go Back ]                │  ← outlined #4C662B, centered
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Empty state centered. Go Back uses outlined button style with #4C662B border/text.

---

## Design Checklist (Figma / Stitch)

- [ ] M3 TopAppBar with back arrow and more_vert overflow action
- [ ] Card visual: 340×210dp, radius 20, elevation 12, #4C662B fill
- [ ] PAN text: title_large, #FFFFFF, monospace, letter-spacing 4
- [ ] Cardholder: body_large, #CDEDA3, uppercase, letter-spacing 1
- [ ] Expiry: body_medium, #CDEDA3, monospace
- [ ] Visa logo: 60×22dp, white tinted, right-aligned bottom of card
- [ ] "Show card details" link centered, label_large, #4C662B, underline
- [ ] Card status row: white fill, 12dp radius, M3 Switch with #4C662B on-state
- [ ] Spending Limits section: white fill, 12dp radius, title_medium header
- [ ] Limit rows: body_medium label/#44483D · body_large value/#1A1C16 · edit icon #4C662B 20dp
- [ ] Divider between Daily and Monthly rows: #F9FAEF 1px
- [ ] Freeze Card: outlined, #E8A317 border, #44483D text (accessible contrast), ac_unit icon
- [ ] Report Lost/Stolen: outlined, #BA1A1A border/text, report_problem icon
- [ ] View Transactions: text-only, #4C662B, receipt_long icon
- [ ] Frozen state: grey overlay #C5C8BA at 50%, "FROZEN" watermark, lock_open icon for Unfreeze
- [ ] Reveal link hidden in frozen state
- [ ] Skeleton card visual proportional to content card size
- [ ] All text Outfit typeface; minimum 14sp body content
- [ ] 16dp horizontal content padding throughout
