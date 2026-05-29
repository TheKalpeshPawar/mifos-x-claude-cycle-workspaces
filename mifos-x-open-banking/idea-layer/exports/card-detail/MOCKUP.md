# MOCKUP — Card Detail

**Archetype:** detail_screen
**Shell:** Top app bar ("Card Details") with arrow_back navigation and more_vert overflow. No bottom navigation bar.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: Material Design 3.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│ ←  Card Details               [⋮]   │  ← M3 TopAppBar · arrow_back + more_vert
├─────────────────────────────────────┤
│                                     │
│   ┌─────────────────────────────┐   │  ← Skeleton card (340×210dp, radius 20)
│   │ ████████████████████████████│   │     shimmer: short4/200ms, #E1E4D5 base
│   │ ████████████████████████████│   │
│   │ ████████████████████████████│   │
│   └─────────────────────────────┘   │
│                                     │
│  ████████████████████████           │  ← reveal link skeleton (label_large height)
│                                     │
│  ┌───────────────────────────────┐  │  ← Status row skeleton
│  │  ██████████████  ░░░░░░░░░░░  │  │     (label placeholder + switch placeholder)
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │  ← Limits section skeleton (4 rows)
│  │  ████████████████████████████ │  │
│  │  █████████████   ████████████ │  │
│  │  ─────────────────────────── │  │
│  │  █████████████   ████████████ │  │
│  └───────────────────────────────┘  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Skeleton card visual is full proportional size (340×210dp, radius 20). 4 skeleton field rows below. shimmer_duration: short4 (200ms); reduced_motion_fallback: static_placeholder. No action buttons during load.

---

## Screen: content (card active)

```
┌─────────────────────────────────────┐
│ ←  Card Details               [⋮]   │  ← M3 TopAppBar
├─────────────────────────────────────┤
│                                     │
│   ┌─────────────────────────────┐   │  ← #4C662B card, 340×210dp, radius 20, elev 12
│   │                             │   │
│   │  •••• •••• •••• 4521        │   │  ← title_large (22sp), #FFFFFF, monospace, spacing 4
│   │                             │   │
│   │  ALEX JOHNSON       [VISA]  │   │  ← body_large/#CDEDA3, uppercase, spacing 1
│   │  09/29                      │   │  ← body_medium/#CDEDA3, monospace
│   └─────────────────────────────┘   │
│                                     │
│         Show card details           │  ← label_large (14sp/500), #4C662B, underline, centered
│                                     │
│  ┌───────────────────────────────┐  │  ← Card status row: #FFFFFF, radius 12, elev 1
│  │  Card Active          [ ●  ] │  │  ← body_large/#1A1C16/w500 · switch checked #4C662B
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │  ← Limits section: #FFFFFF, radius 12, elev 1
│  │  Spending Limits              │  │  ← title_medium (16sp/500), #1A1C16, w600
│  │  ─────────────────────────── │  │
│  │  Daily limit     £2,500  [✎] │  │  ← body_medium/#44483D · body_large/#1A1C16/w500
│  │  ─────────────────────────── │  │     edit icon: 20dp, #4C662B
│  │  Monthly limit  £10,000  [✎] │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │  ← Freeze Card: outlined, #E8A317 border
│  │  ❄  Freeze Card              │  │     #44483D text (a11y 8.91:1), ac_unit icon, r12
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │  ← Report Lost: outlined, #BA1A1A border/text
│  │  ⚠  Report Lost/Stolen       │  │     report_problem icon, radius 12
│  └───────────────────────────────┘  │
│                                     │
│   🧾  View Transactions             │  ← text variant, #4C662B, receipt_long icon, full-width
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:**
- Card visual: 340×210dp, radius 20, elevation 12, auto horizontal margin, 8dp top margin, 24dp bottom margin.
- PAN: title_large (Outfit 22sp), #FFFFFF, monospace, letter-spacing 4. Cardholder: body_large/#CDEDA3/uppercase/letter-spacing 1. Expiry: body_medium/#CDEDA3/monospace. Visa logo: 60×22dp white tint, lower-right of card.
- Reveal link: label_large (14sp/500), #4C662B, underline, center-aligned, 4dp vertical padding.
- Card status row: #FFFFFF, radius 12dp, elevation 1dp, 16dp vertical × 20dp horizontal padding; M3 switch right-aligned.
- Limits section: #FFFFFF, radius 12dp, elevation 1dp, 20dp padding; #F9FAEF 1dp divider between daily/monthly rows. Edit icons 20dp #4C662B right-aligned.
- Freeze button: full-width, radius 12dp, 14dp vertical padding, #E8A317 border, #44483D text, ac_unit icon.
- Report Lost button: full-width, radius 12dp, 14dp vertical padding, #BA1A1A border + text, report_problem icon.
- View Transactions: text-style, full-width, receipt_long icon, #4C662B.

---

## Screen: frozen

```
┌─────────────────────────────────────┐
│ ←  Card Details               [⋮]   │
├─────────────────────────────────────┤
│                                     │
│   ┌─────────────────────────────┐   │  ← #4C662B card + #C5C8BA80 frozen overlay
│   │░░░░░░░░░░░░░░░░░░░░░░░░░░░░░│   │
│   │░░░░░  F R O Z E N  ░░░░░░░░│   │  ← "FROZEN" watermark, white, centered
│   │░░░░░░░░░░░░░░░░░░░░░░░░░░░░░│   │
│   └─────────────────────────────┘   │
│                                     │
│   (reveal link — hidden)            │
│                                     │
│  ┌───────────────────────────────┐  │  ← Status row: switch unchecked (#44483D)
│  │  Card Active          [  ○  ]│  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │  ← Limits section (daily/monthly rows hidden)
│  │  Spending Limits              │  │
│  │  ─────────────────────────── │  │
│  │  (limit rows not shown)       │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │  ← Unfreeze Card: outlined, #4C662B border/text
│  │  🔓  Unfreeze Card           │  │     lock_open icon
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  ⚠  Report Lost/Stolen       │  │
│  └───────────────────────────────┘  │
│                                     │
│   🧾  View Transactions             │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Card overlay: outline_variant (#C5C8BA) at 50% opacity (#C5C8BA80) over the full card visual. "FROZEN" watermark: white, centered. Reveal link hidden. Switch unchecked. Freeze button becomes "Unfreeze Card" with lock_open icon; #4C662B border and text (replaces #E8A317). Daily/monthly limit rows not shown in frozen state.

---

## Screen: error

```
┌─────────────────────────────────────┐
│ ←  Card Details               [⋮]   │
├─────────────────────────────────────┤
│                                     │
│                                     │
│         [credit_card_off]           │  ← Material Symbol, 48dp, #BA1A1A (error)
│                                     │
│   Unable to load card details       │  ← body_large (16sp), #1A1C16, centered
│                                     │
│   Please try again or               │
│       contact support               │  ← body_medium (14sp), #44483D, centered
│                                     │
│          [ Try Again ]              │  ← filled button, #4C662B, centered
│                                     │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Error state centered vertically. Icon 48dp. Title body_large centered. Message body_medium/#44483D centered. Retry button filled #4C662B.

---

## Screen: empty

```
┌─────────────────────────────────────┐
│ ←  Card Details               [⋮]   │
├─────────────────────────────────────┤
│                                     │
│                                     │
│         [credit_card_off]           │  ← Material Symbol, 48dp, #44483D
│                                     │
│   Card information not available    │  ← body_large (16sp), #1A1C16, centered
│                                     │
│   No card data was found.           │
│   The card may have been            │
│   cancelled or removed from         │  ← body_medium (14sp), #44483D, centered
│   your account.                     │
│                                     │
│          [ Go Back ]                │  ← outlined button, #4C662B border/text, centered
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Empty state centered vertically. Icon 48dp/#44483D. Title body_large centered. Message body_medium/#44483D centered (3 lines max). Go Back: outlined, #4C662B border + text.

---

## Design Checklist (Figma / Stitch)

- [ ] M3 TopAppBar: "Card Details" title, arrow_back nav icon, more_vert overflow — no bottom nav
- [ ] Card visual: 340×210dp, radius 20dp, elevation 12dp, #4C662B diagonal gradient fill, auto horizontal margin
- [ ] PAN: Outfit title_large (22sp/400), #FFFFFF, monospace, letter-spacing 4
- [ ] Cardholder name: Outfit body_large (16sp/400), #CDEDA3, UPPERCASE, letter-spacing 1
- [ ] Expiry: Outfit body_medium (14sp/400), #CDEDA3, monospace ("09/29" format)
- [ ] Visa network logo: 60×22dp, white tint, content_scale fit, bottom-right of card
- [ ] "Show card details" link: label_large (14sp/500), #4C662B, underline, center-aligned, 4dp vertical padding
- [ ] Card status row: #FFFFFF fill, 12dp radius, 1dp elevation, 16dp vertical / 20dp horizontal padding
- [ ] M3 Switch: checked color #4C662B, unchecked color #44483D
- [ ] Spending Limits section: #FFFFFF fill, 12dp radius, 1dp elevation, 20dp padding, #F9FAEF 1dp border
- [ ] Section title: Outfit title_medium (16sp/500), #1A1C16, weight 600
- [ ] Limit rows: body_medium/#44483D label · body_large/#1A1C16/w500 value · edit icon 20dp #4C662B right-aligned
- [ ] Divider between daily/monthly rows: #F9FAEF, 1dp thickness
- [ ] Freeze Card button: full-width, 14dp vertical padding, 12dp radius, #E8A317 border, #44483D text (8.91:1 contrast ratio — a11y PASS)
- [ ] Report Lost/Stolen: full-width, 14dp vertical padding, 12dp radius, #BA1A1A border/text, report_problem icon
- [ ] View Transactions: text-style full-width, receipt_long icon, #4C662B text
- [ ] Frozen: #C5C8BA80 overlay on card, "FROZEN" watermark white centered, switch unchecked, reveal link hidden
- [ ] Unfreeze button: #4C662B border/text, lock_open icon (replaces Freeze button in frozen state)
- [ ] Loading: skeleton card 340×210dp radius 20 + 4 field skeleton rows, shimmer 200ms, no buttons
- [ ] Error: credit_card_off 48dp #BA1A1A + centered message + "Try Again" filled #4C662B
- [ ] Empty: credit_card_off 48dp #44483D + 3-line message + "Go Back" outlined #4C662B
- [ ] All text: Outfit typeface; minimum 14sp for body content
- [ ] Touch targets: 48dp minimum (switch, edit icons, buttons)
- [ ] Horizontal content padding: 16dp throughout screen
