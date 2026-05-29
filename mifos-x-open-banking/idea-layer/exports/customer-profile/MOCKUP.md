# MOCKUP — Customer Profile

**Archetype:** detail_screen
**Shell:** Top app bar with back arrow ("Customer Information"). No bottom navigation on detail screens.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: loading

```
┌─────────────────────────────────────┐
│ ← Customer Information              │  ← Top app bar: title_large, #F9FAEF bg
├─────────────────────────────────────┤
│                                     │
│  Personal Information               │  ← title_large, #4C662B (visible during load)
│                                     │
│  ┌───────────────────────────────┐  │
│  │ ████████████  ██████████████ │  │  ← Skeleton: full_name_row (200ms shimmer)
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │ ████████████  ██████████████ │  │  ← Skeleton: dob_row
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │ ████████████  ██████████████ │  │  ← Skeleton: national_id_row
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │ ████████████  ██████████████ │  │  ← Skeleton: tax_pin_row
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │ ████████████  ██████████████ │  │  ← Skeleton: phone_row
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │ ████████████  ██████████████ │  │  ← Skeleton: email_row
│  └───────────────────────────────┘  │
│                                     │
│  ─────────────────────────────────  │  ← #E1E4D5 divider
│                                     │
│  Address                            │  ← title_large, #4C662B (visible during load)
│                                     │
│  ┌───────────────────────────────┐  │
│  │ ████████████████████████████ │  │  ← Skeleton: address_street_row
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │ ████████████████████████████ │  │  ← Skeleton: address_county_row
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │ ████████████████████████████ │  │  ← Skeleton: address_postcode_row
│  └───────────────────────────────┘  │
│                                     │
│  ─────────────────────────────────  │  ← #E1E4D5 divider
│                                     │
│  Employment                         │  ← title_large, #4C662B (visible during load)
│                                     │
│  ┌───────────────────────────────┐  │
│  │ ████████████  ██████████████ │  │  ← Skeleton: employer_row
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │ ████████████  ██████████████ │  │  ← Skeleton: income_row
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │ ████████████  ██████████████ │  │  ← Skeleton: employment_type_row
│  └───────────────────────────────┘  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Section headings and dividers are visible during loading (structural chrome). All data rows shimmer with `#E1E4D5` skeleton blocks, `8dp` radius, matching row height. `short4` (200ms) shimmer duration; `reduced_motion_fallback: static_placeholder`. Edit Information button hidden during loading.

---

## Screen: content

```
┌─────────────────────────────────────┐
│ ← Customer Information              │  ← title_large, #F9FAEF bg, 56dp height
├─────────────────────────────────────┤
│                                     │
│  Personal Information               │  ← title_large, #4C662B; 20dp top, 8dp bottom
│                                     │
│  ┌───────────────────────────────┐  │  ← full_name_row: #FFFFFF, 8dp radius, 12dp v-pad
│  │ Full Name     Wanjiru Kamau   │  │  ← label: body_medium #44483D | value: body_large #1A1C16 w600
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │  ← dob_row
│  │ Date of Birth  22 Mar 1988    │  │
│  │               (Age: 38)       │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │  ← national_id_row
│  │ National ID    28456789       │  │  ← value: monospace
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │  ← tax_pin_row
│  │ Tax PIN (KRA)  A987654321W    │  │  ← value: monospace
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │  ← phone_row
│  │ Phone    +254 712 345 678     │  │  ← link: body_large, #4C662B, underline; tap → dialler
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │  ← email_row
│  │ Email  wanjiru.kamau@gmail.com│  │  ← link: body_large, #4C662B, underline; tap → mail
│  └───────────────────────────────┘  │
│                                     │
│  ─────────────────────────────────  │  ← address_divider: #E1E4D5, 16dp v-margin
│                                     │
│  Address                            │  ← title_large, #4C662B, 8dp bottom
│                                     │
│  ┌───────────────────────────────┐  │  ← address_street_row: #FFFFFF, 8dp radius, 10dp v-pad
│  │ 26 Westlands Road, Westlands  │  │  ← body_large, #1A1C16
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │  ← address_county_row
│  │ Nairobi County, Kenya         │  │  ← body_large, #1A1C16
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │  ← address_postcode_row
│  │ Postcode: 00100               │  │  ← body_large, #1A1C16
│  └───────────────────────────────┘  │
│                                     │
│  ─────────────────────────────────  │  ← employment_divider: #E1E4D5, 16dp v-margin
│                                     │
│  Employment                         │  ← title_large, #4C662B, 8dp bottom
│                                     │
│  ┌───────────────────────────────┐  │  ← employer_row
│  │ Employer       Safaricom PLC  │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │  ← income_row
│  │ Monthly Income  KES 85,000    │  │  ← value: monospace
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │  ← employment_type_row
│  │ Employment Type  Permanent    │  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │  ← edit_info_button: outlined, #4C662B border+text
│  │      Edit Information         │  │  ← pill radius, fill-width, 8dp top margin
│  └───────────────────────────────┘  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:**
- All rows: `#FFFFFF` fill, `8dp` radius, `16dp` horizontal padding, `12dp` vertical padding (address rows 10dp v-pad), `2dp` margin-bottom between rows.
- Label column: body_medium (14sp/400), `#44483D`, weight 500. Value column: body_large (16sp/400), `#1A1C16`.
- phone_link and email_link: body_large, `#4C662B`, text-decoration underline; 48dp touch target.
- National ID, Tax PIN, Monthly Income values: monospace font-family.
- Section headings use title_large (22sp/400), `#4C662B`.
- Dividers: `1dp` height, `#E1E4D5`, `16dp` vertical margin.
- Edit Information button: outlined variant, `#4C662B` border colour and text, pill radius (999dp), fills content width.
- Screen background: `#F9FAEF`. 16dp horizontal content padding.

---

## Screen: editing

```
┌─────────────────────────────────────┐
│ ← Customer Information              │
├─────────────────────────────────────┤
│                                     │
│  Personal Information               │  ← title_large, #4C662B
│                                     │
│  ┌───────────────────────────────┐  │
│  │ Full Name    [Wanjiru Kamau  ]│  │  ← text field, editable; #75796C border, 4dp radius
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │ Phone    [+254 712 345 678  ] │  │  ← text field, editable; keyboard: phone type
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │ Email  [wanjiru.kamau@gmail  ]│  │  ← text field, editable; keyboard: email type
│  └───────────────────────────────┘  │
│                                     │
│  (National ID, Tax PIN, DOB —       │
│   read-only in editing mode;        │
│   same display as content state)    │
│                                     │
│  ─────────────────────────────────  │
│                                     │
│  (Address and Employment sections   │
│   read-only in editing mode)        │
│                                     │
│  ┌───────────────────────────────┐  │  ← save button: filled, #4C662B, pill radius
│  │       Save Changes            │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │  ← cancel: text button, #4C662B
│  │         Cancel                │  │
│  └───────────────────────────────┘  │
│                                     │
│     ┌──────────────────────────┐    │  ← Keyboard visible (showKeyboard: true)
└─────┘                          └────┘
```

**Layout notes:** Only editable fields (legal_name, mobile_phone_number, email) become TextFields. Read-only fields (DOB, National ID, Tax PIN) remain as label-value rows. Save Changes is a filled `#4C662B` button; Cancel is a text button. Appropriate keyboard types shown per field.

---

## Screen: saving

```
┌─────────────────────────────────────┐
│ ← Customer Information              │
├─────────────────────────────────────┤
│                                     │
│  (Full content as per editing       │
│   state — fields populated with     │
│   draft values)                     │
│                                     │
│  ┌─────────────────────────────┐    │
│  │  ◌ Saving changes...        │    │  ← Progress overlay: semi-transparent scrim +
│  └─────────────────────────────┘    │     circular progress indicator, #4C662B
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Full-screen semi-transparent scrim (`#000000` at 32% opacity) with centred circular progress indicator (`#4C662B`). Screen remains scrollable underneath but all inputs are disabled.

---

## Screen: error

```
┌─────────────────────────────────────┐
│ ← Customer Information              │
├─────────────────────────────────────┤
│                                     │
│  Personal Information               │
│                                     │
│  ┌───────────────────────────────┐  │  ← Error banner (per row): #FFDAD6 fill
│  │ ⚠ Could not load customer     │  │    body_medium, #410002 text
│  │   profile. Please try again.  │  │    error_outline icon 20dp
│  │              [ Retry ]        │  │  ← text button, #4C662B
│  └───────────────────────────────┘  │
│                                     │
│  ─────────────────────────────────  │
│                                     │
│  Address                            │
│                                     │
│  ┌───────────────────────────────┐  │  ← Same banner shown for address rows
│  │ ⚠ Customer address            │  │
│  │   information unavailable.    │  │
│  │              [ Retry ]        │  │
│  └───────────────────────────────┘  │
│                                     │
│  (Employment section similarly      │
│   shows banner with retry)          │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Each section shows a retry banner (`#FFDAD6` fill, `error_outline` icon, body_medium text, outlined Retry button). Banners replace the skeleton rows for that section. Section headings and dividers remain visible. Edit Information button hidden during error state.

---

## Screen: empty

```
┌─────────────────────────────────────┐
│ ← Customer Information              │
├─────────────────────────────────────┤
│                                     │
│  Personal Information               │
│                                     │
│  ┌───────────────────────────────┐  │
│  │ Full Name    [person_outline] │  │  ← empty box: icon + "Customer name not available."
│  │              Customer name    │  │
│  │              not available.   │  │
│  └───────────────────────────────┘  │
│  ┌───────────────────────────────┐  │
│  │ Date of Birth [calendar_today]│  │  ← "Date of birth not recorded."
│  │              Date of birth    │  │
│  │              not recorded.    │  │
│  └───────────────────────────────┘  │
│  ...                                │
│  (Each absent field shows its       │
│   contextual icon + empty message)  │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Per-field empty state shows: icon (24dp, `#44483D`), body_medium message in `#44483D`. Icons are field-contextual: `person_outline` (name), `calendar_today` (DOB), `badge` (national ID), `receipt_long` (tax PIN), `phone_disabled` (phone), `mail_off` (email), `location_off` (address), `business` (employer), `payments` (income), `work_outline` (employment type).

---

## Design Checklist (Figma / Stitch)

- [ ] Top app bar: "Customer Information" title, title_large (22sp), `#F9FAEF` background, 56dp height, back arrow icon 24dp
- [ ] Screen background: `#F9FAEF`; 16dp horizontal content padding throughout
- [ ] Section headings: title_large (22sp/400), `#4C662B`; Personal Information 20dp top, 8dp bottom; Address + Employment 8dp bottom
- [ ] Dividers: `1dp` height, `#E1E4D5`, 16dp vertical margin — between Personal Info/Address and Address/Employment sections
- [ ] Data rows: `#FFFFFF` fill, `8dp` radius, `16dp` h-pad, `12dp` v-pad (address rows `10dp`), `2dp` bottom margin
- [ ] Row layout: horizontal stack, `space-between`, align-center, full-width
- [ ] Label text: body_medium (14sp/400), `#44483D`, weight 500
- [ ] Value text: body_large (16sp/400), `#1A1C16`; full_name_value weight 600
- [ ] Monospace values: national_id_value, tax_pin_value, income_value — monospace font-family
- [ ] phone_link: body_large (16sp), `#4C662B`, text-underline; 48dp touch target; `call_customer` action
- [ ] email_link: body_large (16sp), `#4C662B`, text-underline; 48dp touch target; `email_customer` action
- [ ] Edit Information button: outlined, `#4C662B` border + text, pill radius (999dp), fills content width, 8dp top margin, 24dp bottom margin
- [ ] Loading skeletons: `#E1E4D5` fill, `8dp` radius, matching row heights, short4 (200ms) shimmer
- [ ] Error banners: `#FFDAD6` background, `error_outline` icon (20dp), body_medium `#410002` text, retry text button `#4C662B`
- [ ] Empty states: contextual icon 24dp `#44483D` + body_medium `#44483D` message per field
- [ ] Saving overlay: `#000000` 32% scrim + circular progress `#4C662B`, all inputs disabled
- [ ] All typography: Outfit typeface exclusively. Touch targets minimum 48dp on interactive elements.
- [ ] No bottom navigation bar on this detail screen

---

_Generated by /idea export | 2026-05-30_
