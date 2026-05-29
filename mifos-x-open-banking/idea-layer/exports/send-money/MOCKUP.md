# MOCKUP — Send Money

**Archetype:** form
**Shell:** Top app bar ("Send Money", arrow_back navigation icon, no action icons). No bottom navigation bar.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│ ←  Send Money                       │  ← M3 TopAppBar, arrow_back icon, bg #F9FAEF
│  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━  │  ← Linear progress indicator, #4C662B
├─────────────────────────────────────┤
│                                     │
│  Send Money                         │  ← headline_large (32sp/400), #4C662B
│                                     │
│  ████████████████████████████████   │  ← from_account_selector skeleton (#E1E4D5, r12)
│  ████████████████████████████████   │  ← amount_input skeleton
│  ████████████████████████████████   │  ← beneficiary_search skeleton
│                                     │
│  ████████████████  ████████████████ │  ← recent beneficiary chips skeleton
│                                     │
│  ████████████████████████████████   │  ← reference_input skeleton
│  ████████████████████████████████   │  ← fee_estimate_banner skeleton
│                                     │
│  ┌─────────────────────────────┐    │
│  │         Continue            │    │  ← Filled, #4C662B, disabled
│  └─────────────────────────────┘    │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Title visible immediately. Shimmer (#E1E4D5) on from_account_selector, amount_input, beneficiary_search, both recent beneficiary chips, reference_input, and fee_estimate_banner. Continue disabled. currency_selector and payment_type chips hidden during loading.

---

## Screen: draft / content

```
┌─────────────────────────────────────┐
│ ←  Send Money                       │  ← TopAppBar, #F9FAEF bg
├─────────────────────────────────────┤
│                                     │
│  Send Money                         │  ← headline_large (32sp/400), #4C662B
│                                     │
│  From Account                       │  ← label_medium, #44483D
│  ┌─────────────────────────────┐    │
│  │🏦 Primary Checking—£4,250 ▾ │    │  ← account_balance + expand_more icons
│  └─────────────────────────────┘    │  ← outlined, bg #F9FAEF, border #75796C, r12
│                                     │    Demo: "Equity Jijenge Savings — *4521"
│  Amount                             │  ← label_medium, #44483D
│  ┌────────────────────┐  [GBP ▾]   │
│  │ £    0.00          │             │  ← prefix "£", placeholder 0.00, r12
│  └────────────────────┘             │  ← currency chip: filter, r8, min-h 44dp
│                                     │
│  To                                 │  ← label_medium, #44483D
│  ┌─────────────────────────────┐    │
│  │🔍 Search beneficiary…       │    │  ← leading search icon, r12
│  └─────────────────────────────┘    │
│                                     │
│  ←─── horizontal scroll ────────→   │  ← recent_beneficiaries_row
│  ┌───────────────┐ ┌─────────────┐  │
│  │ John Smith    │ │Sarah Williams│  │  ← #CDEDA3 bg, #CDEDA3 border, r12
│  │ Barclays UK   │ │ HSBC UK     │  │  ← body_medium, name+bank 2-line layout
│  └───────────────┘ └─────────────┘  │    Demo: Wycliffe Ochieng/KCB, Naomi Gitau/Co-op
│                                     │
│  Reference                          │  ← label_medium, #44483D
│  ┌─────────────────────────────┐    │
│  │ Payment for invoice #1234   │    │  ← placeholder, max_length 35, r12
│  └─────────────────────────────┘    │
│  Max 35 characters                  │  ← helper, body_small (12sp), #75796C
│                                     │
│  Payment Type                       │  ← label_medium, #44483D
│  [● SEPA]  [ Domestic]  [International] │
│    ↑ selected: bg #4C662B, text #FFF    ← r20dp, filter chips, spacing 8dp
│                                     │
│  ┌─────────────────────────────┐    │
│  │ ℹ  Estimated fee: Free (SEPA)│   │  ← bg #CDEDA3, border #4C662B 1dp, r8
│  └─────────────────────────────┘    │  ← info_outline icon #4C662B, body_medium
│                                     │
│  ┌─────────────────────────────┐    │
│  │           Continue          │    │  ← filled, bg #4C662B, text #FFF, r12
│  └─────────────────────────────┘    │  ← full width, label_large, disabled
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:**
- 16dp horizontal content padding throughout.
- All outlined inputs: bg #F9FAEF, border #75796C (outline), radius 12dp, height 56dp.
- from_account_selector: leading account_balance icon + trailing expand_more — pre-filled with first account. Demo data: "Equity Jijenge Savings — *4521 / KES 87,430.50".
- currency_selector chip floats right of amount_input in a horizontal row; min-height 44dp (⚠ below 48dp M3 minimum — verify padding compensation in implementation).
- Recent beneficiary chips: horizontal scroll, 12dp spacing, #CDEDA3 bg, radius 12dp. Component labels: John Smith (Barclays UK) / Sarah Williams (HSBC UK). Current demo data maps to: Wycliffe Ochieng (KCB) / Naomi Gitau (Co-op Bank) — chips are dynamic; component IDs remain the same.
- Reference helper text: body_small (12sp/400), #75796C, placed 4dp below input.
- Payment type chips: horizontal row, spacing 8dp; SEPA default selected — bg #4C662B, text #FFFFFF; unselected chips have outline style.
- Fee banner: full-width, info_outline icon left, padding 16×12dp, radius 8dp, #4C662B border 1dp.
- Continue: full-width, radius 12dp, disabled until selectedAccountId + amount + beneficiaryId are non-empty.

---

## Screen: validating

```
┌─────────────────────────────────────┐
│ ←  Send Money                       │
│  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━  │  ← Linear progress indicator, #4C662B
├─────────────────────────────────────┤
│  Send Money                         │
│  [from_account_selector — filled]   │
│  [amount_input — filled]  [GBP ▾]  │
│  [beneficiary_search — filled]      │
│  [reference_input — filled]         │
│  [Payment type chips — disabled]    │
│  [fee_estimate_banner]              │
│                                     │
│  ┌─────────────────────────────┐    │
│  │   ⟳   Validating…          │    │  ← Circular progress in button, text grey
│  └─────────────────────────────┘    │  ← bg #4C662B, full width
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** All inputs show as disabled/greyed (surface_variant fill). Linear progress at top of screen. Continue button shows CircularProgressIndicator replacing label text. Recent beneficiary chips hidden (same as validating state in ui.yaml).

---

## Screen: error

```
┌─────────────────────────────────────┐
│ ←  Send Money                       │
├─────────────────────────────────────┤
│  Send Money                         │
│                                     │
│  From Account                       │
│  ┌─────────────────────────────┐    │
│  │🏦 Primary Checking — £4,250 ▾│   │  ← OK — no error on account
│  └─────────────────────────────┘    │
│                                     │
│  Amount                             │
│  ┌─────────────────────────────┐    │
│  │ £   0.00                    │    │  ← Border #BA1A1A (error state)
│  └─────────────────────────────┘    │
│  ⚠ Please enter a valid amount      │  ← body_small (12sp), #BA1A1A
│    greater than £0.01               │
│                                     │
│  To                                 │
│  ┌─────────────────────────────┐    │
│  │ 🔍                          │    │  ← Border #BA1A1A
│  └─────────────────────────────┘    │
│  ⚠ Please select a valid            │  ← body_small, #BA1A1A
│    beneficiary                      │
│                                     │
│  [Payment type chips — visible]     │
│  [fee_estimate_banner]              │
│                                     │
│  ┌─────────────────────────────┐    │
│  │ ⚠ Could not process payment │    │  ← error_outline icon, title_sm, #1A1C16
│  │   Check your connection and │    │
│  │   try again.    [ Retry ]   │    │  ← text button, #4C662B
│  └─────────────────────────────┘    │  ← error_container bg #FFDAD6, r8
│                                     │
│  ┌─────────────────────────────┐    │
│  │           Continue          │    │  ← Filled #4C662B, disabled
│  └─────────────────────────────┘    │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Field-level errors show directly below the errored input with #BA1A1A border on the field and error_container (#FFDAD6) highlight. Network error banner uses error_outline icon and inline Retry text button. Continue remains disabled until errors are resolved.

---

## Screen: empty

```
┌─────────────────────────────────────┐
│ ←  Send Money                       │
├─────────────────────────────────────┤
│  Send Money                         │
│                                     │
│  From Account                       │
│  ┌─────────────────────────────┐    │
│  │🏦 Equity Jijenge Savings ▾  │    │  ← Accounts loaded OK
│  └─────────────────────────────┘    │
│                                     │
│  Amount                             │
│  ┌──────────────┐  [GBP ▾]         │
│  │ £  0.00      │                   │
│  └──────────────┘                   │
│                                     │
│  To                                 │
│  ┌─────────────────────────────┐    │
│  │ 🔍 Search beneficiary…      │    │
│  └─────────────────────────────┘    │
│                                     │
│  ┌─────────────────────────────┐    │
│  │  No beneficiaries available │    │  ← body_medium, #1A1C16, center
│  │  to send money to. Add a    │    │
│  │  beneficiary first.         │    │  ← body_small, #44483D
│  └─────────────────────────────┘    │
│                                     │
│  ┌─────────────────────────────┐    │
│  │           Continue          │    │  ← Filled #4C662B, disabled
│  └─────────────────────────────┘    │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** No recent_beneficiaries_row or chips rendered. Empty state message block replaces the chips area. reference_input, payment_type_selector, and fee_estimate_banner also hidden in this state (per ui.yaml empty state visible_components). Continue disabled.

---

## Design Checklist (Figma / Stitch)

- [ ] M3 TopAppBar — arrow_back navigation icon only, no action icons; bg #F9FAEF; title "Send Money" (title_large)
- [ ] Linear progress indicator (#4C662B) at top of screen during loading and validating states
- [ ] "Send Money" headline: Outfit headline_large (32sp/400), #4C662B, sm bottom padding
- [ ] "From Account" outlined input: account_balance leading icon + expand_more trailing; bg #F9FAEF; radius 12dp; border #75796C
- [ ] Amount input: "£" prefix text, placeholder "0.00", decimal keyboard type, radius 12dp; height 56dp
- [ ] Currency chip ("GBP ▾"): filter chip style, radius 8dp, min-height 44dp, right-aligned in amount row
- [ ] "To" beneficiary search: leading search icon, placeholder "Search beneficiary or enter account...", radius 12dp
- [ ] Recent beneficiary chips: horizontal scroll row, spacing 12dp; each chip bg #CDEDA3, border #CDEDA3 1dp, radius 12dp, padding 12×8dp; 2-line (name + bank)
- [ ] Reference input: placeholder "Payment for invoice #1234", max 35 chars, helper text "Max 35 characters" below (body_small #75796C)
- [ ] Payment type chips (SEPA / Domestic / International): horizontal row spacing 8dp; SEPA selected default — bg #4C662B, text #FFFFFF; others unselected outline; radius 20dp
- [ ] Fee estimate banner: bg #CDEDA3, border #4C662B 1dp, radius 8dp, info_outline icon #4C662B; content "Estimated fee: Free (SEPA)"
- [ ] Continue button: full-width, bg #4C662B, text #FFFFFF, label_large (14sp/500), radius 12dp, padding_vertical 16dp; disabled until required fields filled
- [ ] Loading: shimmer (#E1E4D5) on account selector, amount, beneficiary search, recent chips, reference, fee banner
- [ ] Error fields: border #BA1A1A; error text body_small #BA1A1A directly below field
- [ ] Network error banner: error_outline icon, #FFDAD6 bg, radius 8dp, inline Retry text button #4C662B
- [ ] Empty state: no chips row, no reference/payment-type/fee-banner; message "No beneficiaries available..."
- [ ] No bottom navigation bar — focused form flow (shell.bottom_nav: false)
- [ ] 16dp horizontal content padding; 8dp vertical spacing between form sections
- [ ] All text: Outfit typeface. Touch targets 48dp minimum (check currency chip at 44dp)
- [ ] Dark mode: primary #B2D188, primary_container #354E16, background #12140E

---

_Generated by /idea export | 2026-05-30_
