# MOCKUP — Standing Order Edit

**Archetype:** form
**Shell:** Top app bar ("Edit Standing Order") with back arrow. No bottom navigation bar.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: content (Form pre-filled — ready to edit)

```
┌─────────────────────────────────────┐
│ ←  Edit Standing Order              │  ← TopAppBar, #F9FAEF bg, Outfit/title_large
├─────────────────────────────────────┤
│                                     │
│  ┌──── PAYING TO ─────────────────┐ │  ← beneficiary_card: white, radius 16, elevation 1
│  │  🏦  Landlord Holdings Ltd     │ │  ← account_balance icon #4C662B + body_large #1A1C16 w500
│  │      GB29 NWBK 6016 1331 9268  │ │  ← monospace body_small #44483D + NatWest Bank
│  │      19 · NatWest Bank         │ │     read-only — cannot be changed
│  └────────────────────────────────┘ │
│                                     │
│  ┌ Amount                        ─┐ │  ← outlined input, prefix £
│  │ £  1200.00                      │ │
│  └────────────────────────────────┘ │
│  Amount taken on each payment date  │  ← helper text body_small #44483D
│                                     │
│  ┌ Currency                     🔒 ┐ │  ← readonly, lock trailing icon
│  │ GBP — British Pound             │ │
│  └────────────────────────────────┘ │
│  Matches the source account currency│
│                                     │
│  ┌ 🔁 Frequency              ▾ ─┐  │  ← repeat leading + expand_more trailing
│  │ Monthly                        │  │
│  └────────────────────────────────┘ │
│  How often the payment repeats      │
│                                     │
│  ┌ Start Date               📅 ─┐  │  ← calendar_today trailing
│  │ 1 Jan 2026                     │  │
│  └────────────────────────────────┘ │
│  First date this payment runs       │
│                                     │
│  ┌ End Date (optional)       📅 ─┐  │
│  │ Ongoing — no end date           │  │
│  └────────────────────────────────┘ │
│  Leave as Ongoing to run indefinitely│
│                                     │
│                                     │
│  ┌────────────────────────────────┐ │
│  │         Save Changes           │ │  ← FilledButton, #4C662B, full-width, radius 24
│  └────────────────────────────────┘ │
│  ┌────────────────────────────────┐ │
│  │             Cancel             │ │  ← TextButton, #4C662B, full-width
│  └────────────────────────────────┘ │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:**
- #F9FAEF background.
- 16 dp horizontal padding on root.
- Beneficiary card: white, radius 16dp, elevation 1dp, margin_bottom 16dp.
- Editable inputs: M3 OutlinedTextField, radius 12dp, #75796C idle border → #4C662B focused border.
- 8 dp gap between consecutive input fields.
- Currency field: read-only (disabled appearance), trailing lock icon.
- Frequency: tappable outlined field — opens ModalBottomSheet picker (DAILY/WEEKLY/MONTHLY/YEARLY).
- Start/End date: tappable — opens M3 DatePickerDialog.
- Helper text: Outfit body_small (12sp) #44483D, 4dp below each field.
- Save Changes: FilledButton, radius 24dp pill, min-height 56dp, full-width, 32dp margin_top above buttons area.
- Cancel: TextButton, #4C662B, full-width, 8dp margin_top below Save.
- 24dp bottom spacer.

---

## Screen: loading (PUT request in flight)

```
┌─────────────────────────────────────┐
│ ←  Edit Standing Order              │
├─────────────────────────────────────┤
│                                     │
│                                     │
│                                     │
│                                     │
│                                     │
│                 (○)                 │  ← CircularProgressIndicator, 40dp, #4C662B, centered
│                                     │
│           Saving changes…           │  ← body_medium #44483D, centered (optional label)
│                                     │
│                                     │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Circular spinner centred in full viewport. All form inputs hidden. Save + Cancel buttons hidden. Back arrow disabled (prevented from exiting mid-save). Progress is indeterminate.

---

## Screen: error (PUT failed — form shown with banner)

```
┌─────────────────────────────────────┐
│ ←  Edit Standing Order              │
├─────────────────────────────────────┤
│                                     │
│  ┌──── PAYING TO ─────────────────┐ │
│  │  🏦  Landlord Holdings Ltd     │ │
│  └────────────────────────────────┘ │
│                                     │
│  ┌ Amount ────────────────────── ─┐ │  ← inputs re-enabled
│  │ £  1200.00                      │ │
│  └────────────────────────────────┘ │
│  … (rest of fields) …               │
│                                     │
│  ┌─── ⚠ ─────────────────────────┐ │
│  │  Couldn't save your changes.   │ │  ← error banner #FFDAD6 bg, #410002 text
│  │  Check the amount and try      │ │     error_outline leading icon
│  │  again.                        │ │
│  └────────────────────────────────┘ │
│                                     │
│  ┌────────────────────────────────┐ │
│  │         Save Changes           │ │  ← re-enabled, #4C662B
│  └────────────────────────────────┘ │
│  ┌────────────────────────────────┐ │
│  │             Cancel             │ │
│  └────────────────────────────────┘ │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Error banner appears between the last input field and the action buttons. Uses #FFDAD6 background (#410002 text) matching M3 error_container tokens. Form is fully editable for retry. Banner uses `role: alert` with `live: assertive` for accessibility.

---

## Design Checklist (Figma / Stitch)

- [ ] M3 TopAppBar with back arrow — title "Edit Standing Order"
- [ ] Beneficiary card: white, radius 16dp, elevation 1dp — read-only, labelled "PAYING TO"
- [ ] account_balance icon 24dp #4C662B beside beneficiary name
- [ ] Beneficiary name: body_large #1A1C16 w500; IBAN line: monospace body_small #44483D
- [ ] Amount: outlined text field with £ prefix, decimal keyboard, helper text
- [ ] Currency: outlined read-only field, trailing lock icon, disabled appearance
- [ ] Frequency: outlined field with repeat leading + expand_more trailing icon; opens picker
- [ ] Start/End date fields: outlined, calendar_today trailing; opens DatePickerDialog
- [ ] Error banner: #FFDAD6 bg, error_outline icon, #410002 text, radius 8dp
- [ ] Save Changes: FilledButton #4C662B, radius 24dp pill, min-height 56dp, full-width
- [ ] Cancel: TextButton #4C662B, full-width
- [ ] Loading state: circular spinner 40dp #4C662B centred, no form elements visible
- [ ] All text Outfit typeface
- [ ] 16 dp horizontal padding throughout
