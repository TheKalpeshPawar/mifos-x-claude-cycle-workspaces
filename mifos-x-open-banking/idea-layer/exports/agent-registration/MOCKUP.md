# MOCKUP — Agent Registration

**Archetype:** form
**Shell:** Top app bar ("Agent Registration") with back arrow. No bottom navigation bar.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: content (Primary) — idle / form ready

```
┌─────────────────────────────────────┐
│ ←  Agent Registration               │  ← TopAppBar, title_large, back arrow
├─────────────────────────────────────┤
│  Agent Registration                 │  ← headline_large/Bold, #4C662B
│  Register to become an authorised   │  ← body_medium, #44483D
│  OBP field agent with your bank     │
│                                     │
│  Legal Name                         │  ← label_medium/SemiBold, #44483D
│  ┌───────────────────────────────┐  │
│  │  e.g. Priya Chakraborty       │  │  ← Outlined input, #E1E4D5 border, 12dp radius
│  └───────────────────────────────┘  │
│                                     │
│  Mobile Phone Number                │
│  ┌────────┐  ┌────────────────────┐ │
│  │  +254  │  │  712 345 678       │ │  ← Prefix box (#F9FAEF) + phone input (outlined)
│  └────────┘  └────────────────────┘ │
│                                     │
│  Agent Number                       │
│  ┌───────────────────────────────┐  │
│  │  e.g. AGT-2026-00142          │  │
│  └───────────────────────────────┘  │
│                                     │
│  Operating Currency                 │
│  ┌──────────────────────────────▾┐  │
│  │  Select currency               │  │  ← Dropdown combobox, expand_more trailing icon
│  └───────────────────────────────┘  │
│                                     │
│  Supported Services                 │
│  ┌────────────────┐ ┌─────────────┐ │
│  │ Cash Deposit   │ │Cash Withdraw│ │  ← Chip group (wrap), unselected: #CDEDA3/#4C662B
│  └────────────────┘ └─────────────┘ │    selected: #4C662B/white
│  ┌──────────────────┐ ┌───────────┐ │
│  │ Account Opening  │ │Bill Payment││
│  └──────────────────┘ └───────────┘ │
│  ┌──────────────────┐               │
│  │  Fund Transfer   │               │
│  └──────────────────┘               │
│                                     │
│  Commission Rate (%)                │
│  ┌──────────────────────────────%┐  │
│  │  e.g. 1.5                     │  │  ← Decimal input, percent trailing icon
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │       Register as Agent       │  │  ← Filled button #4C662B/white, full-width
│  └───────────────────────────────┘  │
│  By registering, you agree to the   │  ← body_small #44483D centred
│  Mifos Agent Terms and Conditions   │
└─────────────────────────────────────┘
```

**Layout notes:**
- All inputs: outlined variant, `#E1E4D5` border, 12dp radius, 14dp H/V padding, `body_medium` text, 20dp H margin.
- Field labels: `label_medium`/SemiBold `#44483D`, 20dp H padding, 6dp bottom padding.
- Phone row: `+254` prefix box (fixed width, `#F9FAEF` bg, 12dp radius, same padding) + phone input (flex 1) in horizontal stack with 8dp gap.
- Currency select: combobox with `expand_more` trailing icon; opens bottom sheet with EUR/GBP/KES/USD options.
- Services chip group: wrap flow layout, 8dp gap, 20dp H margin. Each chip: 20dp radius, 1dp border.
- Register button: full-width, `#4C662B` fill, white `label_large` text, 14dp radius, 24dp H margin, elevation 2.
- Terms notice: `body_small` `#44483D` centred, 20dp H padding, 24dp bottom padding.
- Scroll: SingleChildScrollView — form overflows on small devices.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│ ←  Agent Registration               │
├─────────────────────────────────────┤
│  Agent Registration                 │
│                                     │
│                                     │
│              ⟳                      │  ← CircularProgressIndicator, 48dp, #4C662B
│                                     │
│      Checking registration          │  ← body_medium, #44483D, centred
│           status…                   │
│                                     │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Spinner 48dp centred horizontally with 80dp top margin. Loading label below spinner with 16dp top margin. Page title still visible. Form fields hidden.

---

## Screen: validation_error

```
┌─────────────────────────────────────┐
│ ←  Agent Registration               │
├─────────────────────────────────────┤
│  Agent Registration                 │
│  Register to become an authorised   │
│  OBP field agent with your bank     │
│                                     │
│  Legal Name                         │
│  ┌───────────────────────────────┐  │
│  │  [empty]                      │  │  ← Input with error border #BA1A1A
│  └───────────────────────────────┘  │
│  ⚠ Legal name is required           │  ← body_small #BA1A1A, alert role
│                                     │
│  Mobile Phone Number                │
│  ┌────────┐  ┌────────────────────┐ │
│  │  +254  │  │  [invalid]         │ │
│  └────────┘  └────────────────────┘ │
│  ⚠ Enter a valid 9-digit phone number│ ← body_small #BA1A1A
│                                     │
│  Agent Number                       │
│  ┌───────────────────────────────┐  │
│  │  [empty]                      │  │
│  └───────────────────────────────┘  │
│  ⚠ Agent number is required         │
│                                     │
│  [… remaining fields …]             │
│                                     │
│  ┌───────────────────────────────┐  │
│  │       Register as Agent       │  │
│  └───────────────────────────────┘  │
└─────────────────────────────────────┘
```

**Layout notes:** Each failing input gains `#BA1A1A` border. Inline error text (`body_small`, `#BA1A1A`, `alert` role) appears immediately below each field, 12dp bottom margin. Focus scrolls to first error.

---

## Screen: pending_approval

```
┌─────────────────────────────────────┐
│ ←  Agent Registration               │
├─────────────────────────────────────┤
│  Agent Registration                 │
│                                     │
│  ┌───────────────────────────────┐  │
│  │ ⧗  Pending Approval           │  │  ← Banner: #CDEDA3 bg, #E8A317 border, 14dp radius
│  │    Your agent application is  │  │    hourglass_empty icon (#44483D) + text col
│  │    under review. You will be  │  │
│  │    notified once your bank     │  │
│  │    confirms your registration. │  │
│  └───────────────────────────────┘  │
│                                     │
│  Legal Name (read-only)             │
│  ┌───────────────────────────────┐  │
│  │  Priya Chakraborty            │  │  ← Inputs disabled, greyed state
│  └───────────────────────────────┘  │
│  [… other read-only fields …]       │
│                                     │
│  (Register button hidden)           │
└─────────────────────────────────────┘
```

**Layout notes:** Pending banner full-width, 20dp H margin, 20dp bottom margin. All form inputs set to `disabled` state (greyed appearance). Register button hidden. Terms notice hidden.

---

## Screen: confirmed

```
┌─────────────────────────────────────┐
│ ←  Agent Registration               │
├─────────────────────────────────────┤
│  Agent Registration                 │
│                                     │
│  ┌───────────────────────────────┐  │
│  │ ✓  Agent Confirmed            │  │  ← Banner: #CDEDA3 bg, #CDEDA3 border, 14dp radius
│  │    You are registered as an   │  │    verified_outlined icon (#4C662B) + text col
│  │    active Mifos field agent.   │  │
│  │    You can now onboard         │  │
│  │    customers and process       │  │
│  │    transactions.               │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │       Go to Dashboard         │  │  ← Filled button #4C662B, full-width, 14dp radius
│  └───────────────────────────────┘  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Confirmed banner full-width, 20dp H margin, 20dp bottom margin. Form inputs hidden. Only banner + Go to Dashboard button visible.

---

## Screen: error

```
┌─────────────────────────────────────┐
│ ←  Agent Registration               │
├─────────────────────────────────────┤
│  Agent Registration                 │
│  Register to become an authorised   │
│  OBP field agent with your bank     │
│                                     │
│  ┌───────────────────────────────┐  │
│  │ ⚠  Registration failed.       │  │  ← Global error banner: #CDEDA3 bg, #BA1A1A border
│  │    Please check your details  │  │    error_outline icon 20dp (#BA1A1A) + message
│  │    and try again.             │  │
│  └───────────────────────────────┘  │
│                                     │
│  [Form fields re-enabled]           │
│                                     │
│  ┌───────────────────────────────┐  │
│  │       Register as Agent       │  │
│  └───────────────────────────────┘  │
└─────────────────────────────────────┘
```

**Layout notes:** Global error banner appears above all form fields. Inputs re-enabled for correction. Banner uses `#CDEDA3` background (primary_container) with `#BA1A1A` border to distinguish from field-level errors.

---

## Screen: empty

```
┌─────────────────────────────────────┐
│ ←  Agent Registration               │
├─────────────────────────────────────┤
│  Agent Registration                 │
│                                     │
│     Registration form not           │  ← body_medium, #44483D, centred
│          available                  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Title + empty message only. Shown when OBP returns no valid bank context for the current user.

---

## Design Checklist (Figma / Stitch)

- [ ] TopAppBar with back arrow; page title headline_large (32sp/Bold) in `#4C662B`
- [ ] Subtitle body_medium `#44483D` below title
- [ ] Loading state: 48dp spinner `#4C662B` centred + loading label, form hidden
- [ ] All form inputs: outlined, `#E1E4D5` border, 12dp radius, 14dp padding
- [ ] Phone row: `+254` fixed prefix box (`#F9FAEF` bg, 12dp radius) + flex phone input
- [ ] Currency select: combobox with `expand_more` trailing icon
- [ ] Services chip group: wrap layout, selected = `#4C662B` fill / white text; unselected = `#CDEDA3` bg / `#4C662B` text / `#4C662B` border
- [ ] Commission rate input: trailing `percent` icon, decimal keyboard
- [ ] Inline validation errors: `body_small` `#BA1A1A` with `alert` ARIA role, `#BA1A1A` input border
- [ ] Pending banner: `#CDEDA3` bg + `#E8A317` border; `hourglass_empty` 22dp `#44483D` icon
- [ ] Confirmed banner: `#CDEDA3` bg + `#CDEDA3` border; `verified_outlined` 22dp `#4C662B` icon
- [ ] Global error banner: `#CDEDA3` bg + `#BA1A1A` border; `error_outline` 20dp `#BA1A1A` icon
- [ ] Register + Go to Dashboard buttons: full-width, `#4C662B` fill, white `label_large`, 14dp radius
- [ ] Terms notice: `body_small` `#44483D` centred at bottom
- [ ] 48dp minimum touch targets on all inputs and buttons
