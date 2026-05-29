# MOCKUP — Connected Apps

**Archetype:** index_list
**Shell:** Top app bar ("Connected Apps") with back arrow and info action. No bottom navigation bar.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: populated (Primary — 3 apps)

```
┌─────────────────────────────────────┐
│ ←  Connected Apps              [ℹ] │  ← TopAppBar, info icon → PSD2 info sheet
├─────────────────────────────────────┤
│                                     │
│  Connected Apps                     │  ← headline_large, #4C662B, bold
│  Manage third-party apps that       │  ← body_medium, #44483D
│  have access to your account data   │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  [MM] MoneyManager Pro  ACTIVE│  │  ← 40dp logo, DCE7C8 bg; ACTIVE chip #CDEDA3
│  │       Granted 1 Mar 2026      │  │  ← body_small #44483D
│  │       Expires 1 Mar 2027      │  │
│  │  [Read Accounts] [View Txns]  │  │  ← scope chips, #CDEDA3 bg, #4C662B text
│  │  [Check Balances]             │  │
│  │                   [Revoke ×]  │  │  ← outlined button, border #BA1A1A, text #BA1A1A
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │  [TH] TaxHelper         ACTIVE│  │  ← 40dp logo, #CDEDA3 bg
│  │       Granted 15 Jan 2026     │  │
│  │       Expires 15 Jan 2027     │  │
│  │  [View Transactions]          │  │  ← scope chips
│  │  [Read Accounts]              │  │
│  │                   [Revoke ×]  │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─┐  │  ← expired card, #F9FAEF bg, #E1E4D5 border
│  │  [BW] BudgetWise     EXPIRED  │  │  ← EXPIRED chip #CDEDA3 bg, #44483D text (muted)
│  │       Granted 10 Oct 2025     │  │     name text also #44483D (muted)
│  │       Expired 10 Apr 2026     │  │
│  │  [Check Balances]             │  │  ← scope chip #F9FAEF bg, #44483D text
│  │                     [Remove]  │  │  ← text button, #44483D
│  └ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─┘  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:**
- Screen background `#F9FAEF`. 20dp horizontal margin for consent cards.
- Active cards: white `#FFFFFF` background, 16dp radius, 2dp elevation, 12dp margin-bottom.
- Expired card: `#F9FAEF` background, 16dp radius, 1dp `#E1E4D5` border — visually demoted.
- Scope chip row scrolls horizontally if > 3 chips. Each chip: 8px horizontal padding, 4px vertical, 8dp radius.
- "Revoke Access" button floated to card's trailing edge (`align_self: flex_end`), 10dp radius.
- 40×40dp app logo with 10dp radius in leading position.

---

## Screen: revoke_confirm (Confirmation dialog overlay)

```
┌─────────────────────────────────────┐
│ ←  Connected Apps              [ℹ] │
├─────────────────────────────────────┤
│                                     │
│  [dimmed populated list behind]     │  ← scrim applied over list
│                                     │
│  ┌───────────────────────────────┐  │
│  │  Revoke access?               │  │  ← title_large #1A1C16 bold
│  │                               │  │  ← dialog: white, 24dp radius, elevation 8
│  │  This will immediately remove  │  │  ← body_medium #44483D
│  │  this app's access to your    │  │
│  │  account data. You can        │  │
│  │  reconnect it at any time.    │  │
│  │                               │  │
│  │            [Cancel]  [Revoke] │  │  ← Cancel: text #4C662B
│  └───────────────────────────────┘  │     Revoke: filled #BA1A1A, white text
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:**
- Dialog centered with 32dp horizontal margin. 24dp internal padding.
- Buttons in `Row` with `Arrangement.End` — Cancel text button left, Revoke filled button right.
- Revoke button: `#BA1A1A` background, white text, 10dp radius, 16dp horizontal padding.

---

## Screen: empty (No connected apps)

```
┌─────────────────────────────────────┐
│ ←  Connected Apps              [ℹ] │
├─────────────────────────────────────┤
│                                     │
│  Connected Apps                     │
│  Manage third-party apps that       │
│  have access to your account data   │
│                                     │
│                                     │
│             🔗̸                       │  ← ic_link_off, 80dp, tint #E1E4D5
│                                     │
│        No apps connected            │  ← title_medium, #44483D, bold, centered
│                                     │
│  Third-party apps you authorise     │  ← body_medium, #44483D, centered
│  will appear here. Visit your       │
│  bank's app marketplace to          │
│  connect apps.                      │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Empty state centred vertically in content area below subtitle. Icon 80dp, 24dp below subtitle, title 8dp below icon, body 8dp below title. 32dp horizontal padding on body text.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│ ←  Connected Apps              [ℹ] │
├─────────────────────────────────────┤
│                                     │
│  Connected Apps                     │
│  Manage third-party apps that       │
│  have access to your account data   │
│                                     │
│  ████████████████████████████████   │  ← skeleton card 1 (~130dp), shimmer
│                                     │
│  ████████████████████████████████   │  ← skeleton card 2
│                                     │
│  ████████████████████████████████   │  ← skeleton card 3
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Three skeleton cards 130dp height each. `trust_horizon` gradient `#F0F1E6 → #E1E4D5` shimmer animation. 20dp horizontal margin matching real cards.

---

## Screen: error

```
┌─────────────────────────────────────┐
│ ←  Connected Apps              [ℹ] │
├─────────────────────────────────────┤
│                                     │
│  Connected Apps                     │
│  Manage third-party apps that       │
│  have access to your account data   │
│                                     │
│              ☁                      │  ← cloud_off icon 48dp, #44483D
│                                     │
│   Unable to load connected apps     │  ← body_large, #1A1C16, centered
│   Check your connection and         │  ← body_medium, #44483D, centered
│   try again                         │
│                                     │
│  ┌───────────────────────────────┐  │
│  │          Retry                │  │  ← FilledButton, #4C662B
│  └───────────────────────────────┘  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Error icon + messages centred. Retry button full-width with 20dp horizontal margin.

---

## Design Checklist (Figma / Stitch)

- [ ] M3 TopAppBar with back arrow + info icon action
- [ ] Active consent cards: white bg, 16dp radius, elevation 2, `#F9FAEF` border
- [ ] Expired consent card: `#F9FAEF` bg, 1dp `#E1E4D5` border — visually demoted
- [ ] 40×40dp app logos with 10dp radius (placeholder uses brand initials)
- [ ] ACTIVE status chip: `#CDEDA3` bg, `#4C662B` text, 10dp radius
- [ ] EXPIRED status chip: `#CDEDA3` bg, `#44483D` text, 10dp radius (muted)
- [ ] Scope chips: 8dp radius, horizontally scrollable row
- [ ] "Revoke Access" button: outlined, border + text `#BA1A1A`, `align_self: flex_end`
- [ ] "Remove" button: text variant, `#44483D` (for expired)
- [ ] Revoke confirmation dialog: white, 24dp radius, elevation 8, 32dp horizontal margin
- [ ] Dialog "Revoke" button: `#BA1A1A` filled, white text
- [ ] Empty state: `ic_link_off` 80dp tinted `#E1E4D5`
- [ ] Loading: 3× skeleton cards 130dp height with shimmer
- [ ] Error state: cloud_off icon + retry button
- [ ] All text: Outfit typeface
- [ ] 16dp content padding, 20dp card horizontal margins
