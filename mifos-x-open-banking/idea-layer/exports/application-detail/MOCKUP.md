# MOCKUP — Application Detail

**Archetype:** detail_screen
**Shell:** M3 TopAppBar ("Application Detail") with back arrow, #F9FAEF background. No bottom navigation bar (fieldOfficer detail flow).
**Accent:** #4C662B (Earth-green). Primary container: #CDEDA3. Typography: Outfit. Design system: M3.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│ ←  Application Detail               │  ← M3 TopAppBar, back arrow, #F9FAEF bg
├─────────────────────────────────────┤
│  ██████████████████████████████████ │  ← Header skeleton: #4C662B tonal shimmer
│  ████████████  ██████████           │  ← Ref number + status chip skeleton
├─────────────────────────────────────┤
│                                     │
│  ┌───────────────────────────────┐  │
│  │  ████████  ██████████████████│  │  ← Customer card skeleton (#E1E4D5, radius 12dp)
│  │  ████████  ████████  ████████│  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  ████████████  ██████████████│  │  ← Application details card skeleton
│  │  ████████       ██████████   │  │
│  │  ████████       ██████████   │  │
│  │  ██████   ██████████████████ │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  ██████████████████████████  │  │  ← KYC row skeleton
│  └───────────────────────────────┘  │
│                                     │
│  ████████████████                   │  ← Supporting Documents heading skeleton
│                                     │
│  ┌───────────────────────────────┐  │
│  │  ████  ████████████  ████████│  │  ← Document card skeleton 1
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │  ████  ████████████  ████████│  │  ← Document card skeleton 2
│  └───────────────────────────────┘  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Full-width shimmer blocks animate left-to-right at 200ms (motion.duration.short4). Header block uses #4C662B tonal shimmer (#354E16 at reduced opacity). No action buttons or review notes input visible during load. Reduced-motion fallback: static_placeholder (static grey blocks, no animation).

---

## Screen: reviewing (content)

```
┌─────────────────────────────────────┐
│ ←  Application Detail               │  ← TopAppBar, #F9FAEF bg, title_large
├─────────────────────────────────────┤
│  ┌─────────────────────────────────┐│
│  │ Application #OBP-2026-00234     ││  ← #4C662B fill, title_large/700, #FFFFFF
│  │ [Pending Review]  20 May 2026   ││  ← Chip: #CDEDA3 bg / #44483D text (label_small/600)
│  └─────────────────────────────────┘│  ← Submitted: body_small / #CDEDA3 text
│                                     │  ← #F9FAEF screen bg
│  ┌───────────────────────────────┐  │  ← White card, radius 12dp, elevation 2
│  │  CUSTOMER                     │  │  ← label_medium/12sp, #44483D, uppercase, ls 0.8
│  │  John Kamau Mwangi  View Profile│ ← title_medium/700/#1A1C16 · link: label_medium/#4C662B underline
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │  ← White card, radius 12dp, elevation 2
│  │  APPLICATION DETAILS          │  │  ← label_medium/#44483D, uppercase, ls 0.8
│  │  Account Type  KCB Savings Acct│ ← body_medium/#44483D label + body_medium/600/#1A1C16 value
│  │  Requested Limit  KES 500,000 │  │  ← value: monospace, weight 600, #1A1C16
│  │  Purpose                      │  │  ← label body_medium/#44483D
│  │  Personal savings and         │  │
│  │  salary credit                │  │  ← body_medium, #1A1C16
│  └───────────────────────────────┘  │
│                                     │
│  ┌─────────────────────────────────┐│  ← #CDEDA3 fill, 1px #4C662B border, radius 12dp
│  │ [✓] KYC Status: Verified ✓     ││  ← verified_user icon 20dp #4C662B · body_medium/600/#4C662B
│  └─────────────────────────────────┘│
│                                     │
│  Supporting Documents               │  ← title_medium/16sp, #1A1C16, heading level 2
│                                     │
│  ┌───────────────────────────────┐  │  ← White card, radius 10dp, elevation 1, #E1E4D5 border
│  │ [ID img│] National ID         │  │  ← 56×40dp thumbnail, 6dp radius, 1px #4C662B border
│  │         Verified ✓    [View]  │  │  ← body_small/#4C662B · label_medium/#4C662B link
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │  ← White card, radius 10dp, elevation 1, #E1E4D5 border
│  │ [home  ] Proof of Address     │  │  ← 56×40dp box, #F9FAEF fill, 1px #E8A317 border
│  │ [icon  ] Pending Upload [Upload]│  ← icon: home 20dp #44483D (a11y) · status: body_small/#44483D
│  └───────────────────────────────┘  │  ← Upload: outlined button, #4C662B border+text, label_small
│                                     │
│  ┌───────────────────────────────┐  │  ← Outlined textarea, 3 min / 6 max lines
│  │  Review Notes                 │  │  ← label: body_medium, #1A1C16
│  │  Add internal notes about     │  │
│  │  this application — e.g.      │  │  ← placeholder: body_medium, #44483D
│  │  income verified via payslip… │  │
│  └───────────────────────────────┘  │
│                                     │
│  [    Approve Application    ]      │  ← filled #4C662B, full-width pill (999dp), label_large/White
│  [    Reject Application     ]      │  ← outlined #BA1A1A border+text, full-width pill
│       Request Information           │  ← text button, #4C662B, 24dp bottom margin
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:**
- Header box: full-width, 16dp vertical + horizontal padding. Status chip: radius 12dp, 8dp hpad, 4dp vpad. 10dp gap between chip and date.
- Customer info card: 16dp horizontal margin, 16dp top margin, 8dp bottom margin. Info row: space-between.
- Application details card: 16dp horizontal margin, 8dp bottom margin. Account type + limit rows are horizontal space-between. Purpose is vertical stack 4dp gap.
- KYC row: 16dp horizontal margin, 8dp bottom margin, 14dp inner padding. verified_user icon 20dp, 8dp gap.
- Document cards: 16dp horizontal margin, 8dp bottom margin, 14dp inner padding. 12dp gap between thumbnail and info text.
- National ID thumbnail: 56×40dp, 6dp radius, cover fit, 1px #4C662B border.
- Proof of Address placeholder: 56×40dp, 6dp radius, #F9FAEF fill, 1px #E8A317 border, centered home icon 20dp #44483D.
- Review notes input: 16dp horizontal margin, 16dp bottom margin, min 3 / max 6 lines.
- Approve / Reject buttons: full-width, 16dp horizontal margin, 8dp bottom margin. Request Information: 16dp horizontal, 24dp bottom margin.

---

## Screen: approved

```
┌─────────────────────────────────────┐
│ ←  Application Detail               │  ← TopAppBar
├─────────────────────────────────────┤
│  ┌─────────────────────────────────┐│
│  │  ✓  Application approved        ││  ← Success banner: #CDEDA3 bg, body_medium/#4C662B
│  │     successfully               ││
│  └─────────────────────────────────┘│
│                                     │
│  ┌─────────────────────────────────┐│
│  │ Application #OBP-2026-00234     ││  ← Same header; status chip now "Approved"
│  │ [Approved]  20 May 2026         ││  ← Chip: #CDEDA3/#44483D updated
│  └─────────────────────────────────┘│
│                                     │
│  [full reviewing layout…]           │
│                                     │
│  [  ✓ Approve Application (done) ]  │  ← disabled state, #4C662B lowered opacity
│  [    Reject Application         ]  │  ← disabled
│       Request Information           │  ← disabled
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Success banner is a full-width box with #CDEDA3 background, #4C662B text (body_medium), 16dp padding. Inserted above the application header. All action buttons disabled after successful APPROVED decision. Screen auto-navigates to customer-detail after brief delay.

---

## Screen: rejected

```
┌─────────────────────────────────────┐
│ ←  Application Detail               │
├─────────────────────────────────────┤
│  ┌─────────────────────────────────┐│
│  │  ✗  Application rejected        ││  ← Rejection banner: #FFDAD6 bg, body_medium/#BA1A1A
│  └─────────────────────────────────┘│
│                                     │
│  ┌─────────────────────────────────┐│
│  │ Application #OBP-2026-00234     ││
│  │ [Rejected]  20 May 2026         ││  ← Status chip updated to "Rejected"
│  └─────────────────────────────────┘│
│                                     │
│  [full reviewing layout…]           │
│                                     │
│  [    Approve Application         ] │  ← disabled
│  [  ✓ Reject Application (done)  ]  │  ← disabled / confirmed state, #BA1A1A lowered opacity
│       Request Information           │  ← disabled
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Rejection banner uses error_container (#FFDAD6) background, error (#BA1A1A) text (body_medium), 16dp padding. All action buttons disabled after REJECTED decision.

---

## Screen: empty

```
┌─────────────────────────────────────┐
│ ←  Application Detail               │  ← TopAppBar
├─────────────────────────────────────┤
│                                     │
│                                     │
│                                     │
│         [description_off icon]      │  ← 48dp icon (icon-2xl), #44483D
│                                     │
│    Application details not          │
│         available                   │  ← body_large, #1A1C16, center-aligned
│                                     │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Vertically centered in viewport. No action buttons. 16dp horizontal padding. `description_off` icon at 48dp (icon-2xl scale token).

---

## Screen: error

```
┌─────────────────────────────────────┐
│ ←  Application Detail               │  ← TopAppBar
├─────────────────────────────────────┤
│                                     │
│                                     │
│              ⚠                      │  ← error_outline icon, 48dp (icon-2xl), #BA1A1A
│                                     │
│    Unable to load application        │
│    details. Check your connection   │  ← body_medium, #44483D, center-aligned
│         and try again.              │
│                                     │
│        [    Try Again    ]          │  ← filled button, #4C662B, centered, pill radius
│                                     │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Error icon (48dp), message (body_medium/#44483D), and "Try Again" button (filled #4C662B, pill) vertically centered. "Try Again" triggers `RetryLoad` action → re-fetches GET endpoint. 16dp horizontal padding.

---

## Design Checklist (Figma / Stitch)

- [ ] M3 TopAppBar with back navigation arrow, "Application Detail" title, #F9FAEF background, 56dp height
- [ ] Full-width #4C662B header box, 16dp vertical + horizontal padding, no corner radius (flush top below app bar)
- [ ] Application reference number: Outfit title_large (22sp), #FFFFFF, weight 700
- [ ] Status chip: #CDEDA3 fill, 12dp radius, 8dp hpad + 4dp vpad, label_small (11sp/600), #44483D text (WCAG AA 7.25:1)
- [ ] Submitted date: body_small (12sp), #CDEDA3 text; 10dp gap from status chip
- [ ] Customer card: #FFFFFF fill, 12dp radius, elevation 2, 16dp padding, 16dp horizontal margin
- [ ] "CUSTOMER" heading: label_medium (12sp/500), #44483D, uppercase, letter-spacing 0.8
- [ ] Customer name: title_medium (16sp/500), #1A1C16, weight 700
- [ ] "View Profile" link: label_medium, #4C662B, underline — navigates to customer-detail
- [ ] Application details card: #FFFFFF, 12dp radius, elevation 2, 16dp padding, 16dp horizontal margin
- [ ] "APPLICATION DETAILS" heading: label_medium, #44483D, uppercase
- [ ] Account type + limit rows: horizontal space-between; limit value in monospace weight 600
- [ ] KYC verified row: #CDEDA3 fill, 1px #4C662B border, 12dp radius, 14dp padding, verified_user icon 20dp #4C662B
- [ ] "KYC Status: Verified ✓" text: body_medium (14sp), #4C662B, weight 600
- [ ] "Supporting Documents" heading: title_medium (16sp), #1A1C16, heading level 2
- [ ] National ID document card: 10dp radius, 1dp #E1E4D5 border, 14dp padding, 56×40dp thumbnail with 6dp radius + 1px #4C662B border
- [ ] "Verified ✓" status: body_small, #4C662B
- [ ] "View" link: label_medium, #4C662B, underline
- [ ] Proof of Address card: 10dp radius, 1dp #E1E4D5 border, 14dp padding
- [ ] Address placeholder box: 56×40dp, 6dp radius, #F9FAEF fill, 1px #E8A317 border, home icon 20dp #44483D (NOT #E8A317 — a11y contrast fix: ≥7.25:1)
- [ ] "Pending Upload" status: body_small, #44483D (NOT #E8A317 — a11y contrast fix applied)
- [ ] "Upload" button: outlined, #4C662B border + text, label_small, 8dp hpad + 4dp vpad
- [ ] Review notes textarea: outlined variant, 3 min / 6 max lines, 16dp horizontal margin
- [ ] "Approve Application" button: filled #4C662B, #FFFFFF text, full-width, pill radius (999dp), label_large
- [ ] "Reject Application" button: outlined #BA1A1A border + text, full-width, pill radius
- [ ] "Request Information" button: text-only, #4C662B, 24dp bottom margin
- [ ] Success banner (approved state): #CDEDA3 background, #4C662B text, body_medium, 16dp padding
- [ ] Rejection banner (rejected state): #FFDAD6 (error_container) background, #BA1A1A text, body_medium
- [ ] Loading shimmer: 200ms duration (motion.duration.short4), left-to-right; no action buttons shown
- [ ] All text: Outfit typeface only. Minimum body text 14sp. Touch targets 48dp minimum. 16dp horizontal content padding throughout.

---

_Generated by /idea export | 2026-05-30_
