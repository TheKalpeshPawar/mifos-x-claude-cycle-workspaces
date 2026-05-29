# MOCKUP — Agent Registration

**Archetype:** form
**Shell:** Top app bar — title "Agent Registration", `arrow_back` navigation icon. No bottom navigation bar.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│ ←  Agent Registration               │  ← TopAppBar: title_large, arrow_back, #F9FAEF bg
├─────────────────────────────────────┤
│                                     │
│  Agent Registration                 │  ← headline_large/Bold (32sp), #4C662B
│                                     │
│                                     │
│                                     │
│                ⟳                    │  ← CircularProgressIndicator 48dp, #4C662B
│                                     │     centred, 80dp top margin
│   Checking registration status…     │  ← body_medium (14sp), #44483D, centred
│                                     │     16dp below spinner
│                                     │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Title visible; subtitle hidden. Spinner centred horizontally with 80dp top margin. Loading label centred below spinner. Full form region hidden while `isLoading=true`.

---

## Screen: idle / content (Primary) — empty form ready

```
┌─────────────────────────────────────┐
│ ←  Agent Registration               │  ← TopAppBar
├─────────────────────────────────────┤
│                                     │
│  Agent Registration                 │  ← headline_large/Bold (32sp), #4C662B, 20dp H pad
│  Register to become an authorised   │  ← body_medium (14sp), #44483D
│  OBP field agent with your bank     │
│                                     │
│  Legal Name                         │  ← label_medium/SemiBold (12sp), #44483D
│  ┌───────────────────────────────┐  │
│  │  e.g. Priya Chakraborty       │  │  ← Outlined input, #E1E4D5 border, 12dp radius
│  └───────────────────────────────┘  │    14dp H/V padding, body_medium
│                                     │
│  Mobile Phone Number                │  ← label_medium/SemiBold, #44483D
│  ┌────────┐  ┌────────────────────┐ │
│  │  +254  │  │  712 345 678       │ │  ← Prefix box (#F9FAEF, 12dp r) + phone input (flex 1)
│  └────────┘  └────────────────────┘ │    8dp gap between elements, 20dp H margin row
│                                     │
│  Agent Number                       │  ← label_medium/SemiBold, #44483D
│  ┌───────────────────────────────┐  │
│  │  e.g. AGT-2026-00142          │  │  ← Outlined input, 12dp radius
│  └───────────────────────────────┘  │
│                                     │
│  Operating Currency                 │  ← label_medium/SemiBold, #44483D
│  ┌──────────────────────────────▾┐  │
│  │  Select currency               │  │  ← Combobox, expand_more trailing icon
│  └───────────────────────────────┘  │    options: EUR / GBP / KES / USD
│                                     │
│  Supported Services                 │  ← label_medium/SemiBold, #44483D (role: heading)
│  ┌───────────────┐ ┌─────────────┐  │  ← Chips: #CDEDA3 bg / #4C662B text+border (unselected)
│  │ Cash Deposit  │ │Cash Withdraw│  │    #4C662B bg / white text (selected)
│  └───────────────┘ └─────────────┘  │    20dp radius, 1dp border, 8dp gap, wrap flow
│  ┌─────────────────┐ ┌───────────┐  │
│  │ Account Opening │ │Bill Payment│  │
│  └─────────────────┘ └───────────┘  │
│  ┌─────────────────┐                │
│  │  Fund Transfer  │                │
│  └─────────────────┘                │
│                                     │
│  Commission Rate (%)                │  ← label_medium/SemiBold, #44483D
│  ┌──────────────────────────────%┐  │
│  │  e.g. 1.5                     │  │  ← Decimal outlined input, % trailing icon
│  └───────────────────────────────┘  │    keyboard: decimal, range 0.5–5.0
│                                     │
│  ┌───────────────────────────────┐  │
│  │       Register as Agent       │  │  ← Filled button: #4C662B / white, full-width
│  └───────────────────────────────┘  │    label_large (14sp/500), 14dp radius, 2dp elevation
│  By registering, you agree to the   │  ← body_small (12sp), #44483D, centred
│  Mifos Agent Terms and Conditions   │    20dp H / 24dp bottom padding
└─────────────────────────────────────┘
```

**Layout notes:**
- All inputs: outlined variant, `#E1E4D5` border, 12dp radius, 14dp H/V padding, body_medium text, 20dp H margin.
- Field labels: label_medium/SemiBold `#44483D`, 20dp H / 6dp bottom padding.
- Phone row: `+254` prefix box (fixed, `#F9FAEF` bg, 12dp radius, 14dp H/V pad, body_medium/SemiBold `#1A1C16`) + phone input (flex 1), horizontal stack 8dp gap, 20dp H margin.
- Currency select: combobox with `expand_more` trailing icon; bottom sheet opens EUR / GBP / KES / USD.
- Services chip group: wrap flow, 8dp gap, 20dp H margin; unselected = `#CDEDA3`/`#4C662B`/`#4C662B` border; selected = `#4C662B`/white; 20dp radius.
- Commission input: trailing `percent` icon; decimal keyboard; 28dp bottom margin before button.
- Register button: full-width, 24dp H margin, `#4C662B`, white label_large, 14dp radius, elevation 2.
- Scroll: SingleChildScrollView — form content overflows on small viewport.

---

## Screen: validation_error

```
┌─────────────────────────────────────┐
│ ←  Agent Registration               │
├─────────────────────────────────────┤
│                                     │
│  Agent Registration                 │
│  Register to become an authorised   │
│  OBP field agent with your bank     │
│                                     │
│  Legal Name                         │
│  ┌───────────────────────────────┐  │
│  │  [empty field — error border] │  │  ← Border changes to #BA1A1A
│  └───────────────────────────────┘  │
│  ⚠ Legal name is required           │  ← body_small, #BA1A1A, role: alert
│                                     │
│  Mobile Phone Number                │
│  ┌────────┐  ┌────────────────────┐ │
│  │  +254  │  │  [invalid input]   │ │  ← Phone input error border #BA1A1A
│  └────────┘  └────────────────────┘ │
│  ⚠ Enter a valid 9-digit phone number│  ← body_small, #BA1A1A, role: alert
│                                     │
│  Agent Number                       │
│  ┌───────────────────────────────┐  │
│  │  [empty field — error border] │  │
│  └───────────────────────────────┘  │
│  ⚠ Agent number is required         │  ← body_small, #BA1A1A
│                                     │
│  Operating Currency                 │
│  ┌──────────────────────────────▾┐  │
│  │  Select currency               │  │
│  └───────────────────────────────┘  │
│  ⚠ Select an operating currency     │  ← body_small, #BA1A1A
│                                     │
│  [Services chips + Commission rate] │
│                                     │
│  ┌───────────────────────────────┐  │
│  │       Register as Agent       │  │  ← Button re-enabled after validation
│  └───────────────────────────────┘  │
└─────────────────────────────────────┘
```

**Layout notes:** Each field with an error displays its error text immediately below with 12dp bottom margin. Input border colour changes to `#BA1A1A`. Scroll focuses to first error field. All inputs remain enabled (`inputs_enabled=true`). Accessibility: each error text has `role: alert` and `live: assertive` — read aloud by screen readers immediately.

---

## Screen: submitting

```
┌─────────────────────────────────────┐
│ ←  Agent Registration               │
├─────────────────────────────────────┤
│                                     │
│  Agent Registration                 │
│  Register to become an authorised   │
│  OBP field agent with your bank     │
│                                     │
│  Legal Name                         │
│  ┌───────────────────────────────┐  │
│  │  Priya Chakraborty            │  │  ← Input disabled (greyed), value preserved
│  └───────────────────────────────┘  │
│                                     │
│  [All other fields: disabled, values preserved]
│                                     │
│  ┌───────────────────────────────┐  │
│  │  ⟳  Register as Agent        │  │  ← Button shows inline loading indicator
│  └───────────────────────────────┘  │    still #4C662B fill; `isSubmitting=true`
│  By registering, you agree to…      │
└─────────────────────────────────────┘
```

**Layout notes:** All form inputs disabled — greyed appearance, no interaction. Register button shows a small circular progress indicator alongside label; remains full-width `#4C662B` fill. OBP POST call in flight.

---

## Screen: pending_approval

```
┌─────────────────────────────────────┐
│ ←  Agent Registration               │
├─────────────────────────────────────┤
│                                     │
│  Agent Registration                 │  ← headline_large, #4C662B; subtitle hidden
│                                     │
│  ┌───────────────────────────────┐  │  ← Banner: #CDEDA3 bg, #E8A317 border (1dp), 14dp r
│  │ ⧗  Pending Approval           │  │    hourglass_empty 22dp #44483D + text column
│  │    Your agent application is  │  │    body_medium/SemiBold "Pending Approval" #44483D
│  │    under review. You will be  │  │    body_small message #44483D
│  │    notified once your bank    │  │    20dp H margin / 20dp bottom margin
│  │    confirms your registration.│  │
│  └───────────────────────────────┘  │
│                                     │
│  Legal Name (read-only)             │
│  ┌───────────────────────────────┐  │
│  │  Priya Chakraborty            │  │  ← Disabled input, value read-only
│  └───────────────────────────────┘  │
│                                     │
│  Mobile Phone Number (read-only)    │
│  ┌────────┐  ┌────────────────────┐ │
│  │  +254  │  │  712 345 678       │ │  ← Both disabled
│  └────────┘  └────────────────────┘ │
│                                     │
│  [Agent Number / Currency / Services / Commission — all read-only]
│                                     │
│  (Register button hidden)           │
│  (Terms notice hidden)              │
└─────────────────────────────────────┘
```

**Layout notes:** `status_banner_pending` full-width, 20dp H / 20dp bottom margin. `hourglass_empty` 22dp icon uses `#44483D` (accessibility-corrected — original `#E8A317` had insufficient contrast on `#CDEDA3` bg). All form inputs `disabled=true` — greyed visual state. Register button and terms notice not rendered.

---

## Screen: confirmed

```
┌─────────────────────────────────────┐
│ ←  Agent Registration               │
├─────────────────────────────────────┤
│                                     │
│  Agent Registration                 │  ← headline_large, #4C662B
│                                     │
│  ┌───────────────────────────────┐  │  ← Banner: #CDEDA3 bg, #CDEDA3 border (1dp), 14dp r
│  │ ✓  Agent Confirmed            │  │    verified_outlined 22dp #4C662B + text column
│  │    You are registered as an   │  │    body_medium/SemiBold "Agent Confirmed" #4C662B
│  │    active Mifos field agent.  │  │    body_small message #4C662B
│  │    You can now onboard        │  │    20dp H margin / 20dp bottom margin
│  │    customers and process      │  │
│  │    transactions.              │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │       Go to Dashboard         │  │  ← Filled button: #4C662B / white, full-width
│  └───────────────────────────────┘  │    label_large, 14dp radius, 2dp elevation
│                                     │    → navigates to fo-dashboard
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** All form fields hidden. Only `agent_reg_title`, `status_banner_confirmed`, and `go_to_dashboard_button` rendered. Banner border matches bg (`#CDEDA3`) to appear solid. Button 20dp H margin / 32dp bottom margin.

---

## Screen: error

```
┌─────────────────────────────────────┐
│ ←  Agent Registration               │
├─────────────────────────────────────┤
│                                     │
│  Agent Registration                 │
│  Register to become an authorised   │
│  OBP field agent with your bank     │
│                                     │
│  ┌───────────────────────────────┐  │  ← Global error banner:
│  │ ⚠  Registration failed.       │  │    #CDEDA3 bg, #BA1A1A border (1dp), 12dp radius
│  │    Please check your details  │  │    error_outline 20dp #BA1A1A (decorative)
│  │    and try again.             │  │    global_error_message body_small #BA1A1A
│  └───────────────────────────────┘  │    20dp H / 16dp bottom margin
│                                     │
│  [All form fields re-enabled]       │
│                                     │
│  Legal Name                         │
│  ┌───────────────────────────────┐  │
│  │  Priya Chakraborty            │  │  ← Inputs enabled for correction
│  └───────────────────────────────┘  │
│                                     │
│  [… remaining fields …]             │
│                                     │
│  ┌───────────────────────────────┐  │
│  │       Register as Agent       │  │  ← Button re-enabled
│  └───────────────────────────────┘  │
│  By registering, you agree to…      │
└─────────────────────────────────────┘
```

**Layout notes:** Global error banner (#CDEDA3 bg with #BA1A1A border) distinguishes from field-level errors. Banner appears above all form fields. Inputs re-enabled (`inputs_enabled=true`). No snackbar (`show_error_snackbar=false`).

---

## Screen: empty

```
┌─────────────────────────────────────┐
│ ←  Agent Registration               │
├─────────────────────────────────────┤
│                                     │
│  Agent Registration                 │  ← headline_large, #4C662B
│                                     │
│     Registration form not           │  ← body_medium, #44483D, centred
│          available                  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Only page title rendered. Empty message centred. Shown when OBP returns no valid bank context for the current user session. No form fields rendered.

---

## Design Checklist (Figma / Stitch)

- [ ] TopAppBar: title "Agent Registration" (title_large), `arrow_back` navigation icon; background `#F9FAEF`
- [ ] Page heading: headline_large (32sp/Bold), `#4C662B`; 20dp H padding, 16dp top / 4dp bottom
- [ ] Subtitle: body_medium (14sp), `#44483D`; 20dp H / 24dp bottom padding
- [ ] Loading state: 48dp spinner `#4C662B` centred with 80dp top margin; loading label body_medium `#44483D` centred below; form hidden
- [ ] All form inputs: outlined variant, `#E1E4D5` border (1dp), 12dp radius, 14dp H/V padding, body_medium text, 20dp H margin
- [ ] Field labels: label_medium (12sp/500) `#44483D` SemiBold, 20dp H / 6dp bottom padding
- [ ] Phone row: `+254` prefix box (`#F9FAEF` bg, `#E1E4D5` border, 12dp radius, body_medium/SemiBold `#1A1C16`) + phone input (flex 1); horizontal stack 8dp gap, 20dp H margin
- [ ] Currency select: combobox with `expand_more` trailing icon; bottom sheet: EUR / GBP / KES / USD
- [ ] Services chip group: wrap flow, 8dp gap, 20dp H margin; unselected = `#CDEDA3` bg / `#4C662B` text / `#4C662B` border 1dp; selected = `#4C662B` bg / white text; chip 20dp radius
- [ ] Commission rate: decimal outlined input, trailing `percent` icon; 28dp bottom margin
- [ ] Inline validation errors: body_small (12sp) `#BA1A1A` below each field; `#BA1A1A` input border in error state; role: alert / live: assertive
- [ ] Pending banner: `#CDEDA3` bg, `#E8A317` border (1dp), 14dp radius; `hourglass_empty` 22dp `#44483D` + "Pending Approval" body_medium/SemiBold `#44483D` + message body_small `#44483D`
- [ ] Confirmed banner: `#CDEDA3` bg, `#CDEDA3` border (1dp), 14dp radius; `verified_outlined` 22dp `#4C662B` + "Agent Confirmed" body_medium/SemiBold `#4C662B` + message body_small `#4C662B`
- [ ] Global error banner: `#CDEDA3` bg, `#BA1A1A` border (1dp), 12dp radius; `error_outline` 20dp `#BA1A1A` + message body_small `#BA1A1A`
- [ ] Register + Go to Dashboard buttons: full-width, `#4C662B` fill, `#FFFFFF` label_large (14sp/500), 14dp radius, 2dp elevation, 24dp H margin
- [ ] Terms notice: body_small (12sp) `#44483D` centred; 20dp H / 24dp bottom padding
- [ ] Submitting state: all inputs disabled (greyed); button shows inline circular progress `#FFFFFF` alongside label
- [ ] Pending state: all form inputs disabled; Register button and terms notice hidden; subtitle hidden
- [ ] Confirmed state: form fields hidden; only banner + Go to Dashboard button shown
- [ ] All interactive elements meet 48dp minimum touch target (M3 standard)
- [ ] Scroll: SingleChildScrollView — content scrolls when form overflows viewport
- [ ] Typeface: Outfit throughout; no fallback fonts in Figma/Stitch

---

_Generated by /idea export | 2026-05-30_
