# MOCKUP — Send Money

**Archetype:** form
**Shell:** Top app bar ("Send Money", back arrow, no actions). No bottom navigation bar.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│ ←  Send Money                       │  ← TopAppBar, back arrow
│  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━  │  ← Linear progress indicator
├─────────────────────────────────────┤
│                                     │
│  Send Money                         │  ← headline_large, #4C662B
│                                     │
│  ████████████████████████████████   │  ← Account selector skeleton
│  ████████████████████████████████   │  ← Amount input skeleton
│  ████████████████████████████████   │  ← Beneficiary search skeleton
│                                     │
│  ████████████ ██████████ ██████████ │  ← Recent beneficiary chips skeleton
│                                     │
│  ████████████████████████████████   │  ← Reference input skeleton
│  ████████████████████████████████   │  ← Fee banner skeleton
│                                     │
│  ┌─────────────────────────────┐    │
│  │         Continue            │    │  ← Filled button, #4C662B, disabled
│  └─────────────────────────────┘    │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Shimmer on account selector, amount, beneficiary search, recent chips, reference, fee banner. Continue disabled.

---

## Screen: draft

```
┌─────────────────────────────────────┐
│ ←  Send Money                       │
├─────────────────────────────────────┤
│                                     │
│  Send Money                         │  ← headline_large, #4C662B
│                                     │
│  From Account                       │
│  ┌─────────────────────────────┐    │
│  │ 🏦 Primary Checking — £4,250.00 ▾│ ← Outlined input, account_balance icon
│  └─────────────────────────────┘    │  ← bg #F9FAEF, radius 12
│                                     │
│  Amount                             │
│  ┌─────────────────────────────┐    │
│  │ £  [         0.00         ] │    │  ← Prefix "£", decimal keyboard, radius 12
│  └─────────────────────────────┘    │
│  [GBP ▾]                            │  ← Currency chip, radius 8, min 44dp
│                                     │
│  To                                 │
│  ┌─────────────────────────────┐    │
│  │ 🔍 Search beneficiary…      │    │  ← Search icon, placeholder, radius 12
│  └─────────────────────────────┘    │
│                                     │
│  ┌──────────────┐ ┌────────────────┐│  ← Recent beneficiary chips
│  │  John Smith  │ │ Sarah Williams ││  ← #CDEDA3 bg, radius 12
│  │  Barclays UK │ │   HSBC UK      ││
│  └──────────────┘ └────────────────┘│
│                                     │
│  Reference                          │
│  ┌─────────────────────────────┐    │
│  │ Payment for invoice #1234   │    │  ← Placeholder, max 35 chars, radius 12
│  └─────────────────────────────┘    │
│  Max 35 characters                  │  ← helper text, body_small, #44483D
│                                     │
│  Payment Type                       │
│  [●SEPA]  [Domestic]  [International]│ ← Chips: selected bg #4C662B text white; radius 20
│                                     │
│  ┌─────────────────────────────┐    │
│  │ ℹ  Estimated fee: Free (SEPA)│   │  ← #CDEDA3 bg, #4C662B border, info icon
│  └─────────────────────────────┘    │
│                                     │
│  ┌─────────────────────────────┐    │
│  │         Continue            │    │  ← Filled #4C662B, disabled (form incomplete)
│  └─────────────────────────────┘    │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:**
- 16dp horizontal content padding.
- All inputs use bg #F9FAEF, border outline color, radius 12.
- Account selector: leading account_balance icon + trailing expand_more icon.
- Beneficiary search: leading search icon.
- Currency chip: right-aligned next to amount input, min-height 44dp.
- Recent beneficiaries: horizontal scroll, #CDEDA3 bg chips with name + bank sub-label.
- Reference helper text below field.
- Payment type chips: horizontal row, SEPA selected by default.
- Fee banner: full-width, info_outline icon, #CDEDA3 bg, #4C662B border 1dp.
- Continue: full-width, pill-like radius 12, disabled until all required fields filled.

---

## Screen: validating

```
┌─────────────────────────────────────┐
│ ←  Send Money                       │
│  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━  │  ← Linear progress indicator
├─────────────────────────────────────┤
│  [All form fields as in draft]      │
│  [Inputs disabled — greyed out]     │
│                                     │
│  ┌─────────────────────────────┐    │
│  │   ⟳  Validating…           │    │  ← Loading spinner in button
│  └─────────────────────────────┘    │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** All inputs greyed out. Continue button shows circular progress indicator text "Validating…".

---

## Screen: error

```
┌─────────────────────────────────────┐
│ ←  Send Money                       │
├─────────────────────────────────────┤
│  Send Money                         │
│  [Account selector — ok]            │
│                                     │
│  Amount                             │
│  ┌─────────────────────────────┐    │
│  │ £  [     0.00          ]    │    │  ← Border #BA1A1A (error state)
│  └─────────────────────────────┘    │
│  ⚠ Please enter a valid amount      │  ← error text, body_small, #BA1A1A
│    greater than £0.01               │
│                                     │
│  To                                 │
│  ┌─────────────────────────────┐    │
│  │ 🔍                          │    │  ← Border #BA1A1A
│  └─────────────────────────────┘    │
│  ⚠ Please select a valid            │  ← error text, body_small, #BA1A1A
│    beneficiary                      │
│                                     │
│  ┌─────────────────────────────┐    │
│  │ ⚠ Could not process payment │    │  ← Error banner, error_outline icon
│  │   Check connection. [Retry] │    │  ← body_medium + text-button Retry
│  └─────────────────────────────┘    │
│                                     │
│  ┌─────────────────────────────┐    │
│  │         Continue            │    │  ← Disabled
│  └─────────────────────────────┘    │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Field-level errors show below the relevant input with #BA1A1A border on the field. Network error banner shows above Continue with inline Retry action.

---

## Screen: empty

```
┌─────────────────────────────────────┐
│ ←  Send Money                       │
├─────────────────────────────────────┤
│  Send Money                         │
│  [Account selector]                 │
│  [Amount input + GBP chip]          │
│  [Beneficiary search]               │
│                                     │
│  ┌─────────────────────────────┐    │
│  │  No beneficiaries available.│    │  ← body_medium, #44483D
│  │  Add a beneficiary first.   │    │
│  └─────────────────────────────┘    │
│                                     │
│  ┌─────────────────────────────┐    │
│  │         Continue            │    │  ← Disabled
│  └─────────────────────────────┘    │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** No recent beneficiary chips row. Empty state message replaces the chips. Continue disabled.

---

## Design Checklist (Figma / Stitch)

- [ ] M3 TopAppBar with back navigation only; linear progress on loading/validating
- [ ] "From Account" outlined input: leading account_balance icon + trailing expand_more, bg #F9FAEF
- [ ] Amount input: "£" prefix, decimal keyboard type, radius 12
- [ ] Currency chip: "GBP ▾", min-height 44dp, right-aligned row with amount
- [ ] Beneficiary search: leading search icon, placeholder text
- [ ] Recent beneficiary chips: #CDEDA3 bg, radius 12, 2-line (name + bank)
- [ ] Reference input: max 35 chars, helper text below
- [ ] Payment type chips: SEPA selected (#4C662B bg + white text), radius 20dp
- [ ] Fee estimate banner: #CDEDA3 bg, #4C662B border + info icon
- [ ] Continue button: full-width, radius 12, #4C662B — disabled until form complete
- [ ] Error state: #BA1A1A border on errored fields + error text below + network error banner
- [ ] Loading: shimmer on account, amount, beneficiary, recent chips, reference, fee banner
- [ ] No bottom navigation bar — focused form flow
- [ ] 16dp horizontal content padding; 8dp spacing between form elements
