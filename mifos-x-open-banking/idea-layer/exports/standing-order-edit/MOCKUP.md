# MOCKUP — Standing Order Edit

**Archetype:** form
**Shell:** Top app bar — title "Edit Standing Order", `arrow_back` navigation icon. No bottom navigation bar.
**Accent:** #4C662B (Earth-green primary). Typography: Outfit. Design system: Material Design 3.

---

## Screen: content (form pre-filled — ready to edit)

```
┌─────────────────────────────────────────┐
│ ←  Edit Standing Order                  │  ← M3 TopAppBar, #F9FAEF bg, Outfit/title_large
├─────────────────────────────────────────┤
│                                         │
│  ┌─────────────────────────────────┐    │  ← soe_beneficiary_card
│  │  PAYING TO                      │    │  ← label_small (11sp/500), #44483D, uppercase
│  │                                 │    │
│  │  🏦  Landlord Holdings Ltd      │    │  ← account_balance icon #4C662B 24dp
│  │      GB29 NWBK 6016 1331        │    │     body_large (16sp/500) #1A1C16
│  │      9268 19 · NatWest Bank     │    │  ← body_small (12sp) #44483D monospace
│  └─────────────────────────────────┘    │     white card, radius 16dp, elevation 1dp
│                                         │
│  ┌─ Amount ───────────────────────────┐ │  ← soe_amount_input, outlined, radius 12dp
│  │  £  1200.00                        │ │     prefix "£", decimal keyboard
│  └────────────────────────────────────┘ │
│  Amount taken on each payment date      │  ← helper text, body_small #44483D
│                                         │
│  ┌─ Currency ───────────────────── 🔒 ┐ │  ← soe_currency_selector, readonly, lock icon
│  │  GBP — British Pound               │ │
│  └────────────────────────────────────┘ │
│  Matches the source account currency    │
│                                         │
│  ┌─ 🔁 Frequency ───────────────── ▾ ┐ │  ← soe_frequency_selector, repeat + expand_more
│  │  Monthly                           │ │     tap → frequency picker (DAILY/WEEKLY/MONTHLY/YEARLY)
│  └────────────────────────────────────┘ │
│  How often the payment repeats          │
│                                         │
│  ┌─ Start Date ────────────────── 📅 ┐ │  ← soe_start_date_input, calendar_today trailing
│  │  1 Jan 2026                        │ │     tap → M3 DatePickerDialog
│  └────────────────────────────────────┘ │
│  First date this payment runs           │
│                                         │
│  ┌─ End Date (optional) ──────── 📅  ┐ │  ← soe_end_date_input, calendar_today trailing
│  │  Ongoing — no end date             │ │     tap → DatePickerDialog; null = indefinite
│  └────────────────────────────────────┘ │
│  Leave as Ongoing to run indefinitely   │
│                                         │
│                                         │
│  ┌──────────────────────────────────┐   │  ← soe_save_button: FilledButton
│  │          Save Changes            │   │     #4C662B fill, #FFFFFF text
│  └──────────────────────────────────┘   │     radius 24dp, min-height 56dp, full-width
│  ┌──────────────────────────────────┐   │  ← soe_cancel_button: TextButton
│  │              Cancel              │   │     #4C662B text, full-width
│  └──────────────────────────────────┘   │
│                                         │
└─────────────────────────────────────────┘
```

**Layout notes:**
- Background: #F9FAEF throughout (colors.light.background).
- Root padding: 16dp horizontal (spacing.md), 24dp top (spacing.lg).
- Beneficiary card: #FFFFFF fill, radius 16dp, elevation 1dp, 16dp bottom margin. Cannot be tapped — read-only group.
- Editable inputs: M3 OutlinedTextField, radius 12dp; idle border #75796C → focused border #4C662B.
- 8dp vertical gap between consecutive input fields.
- Currency field: disabled/readonly appearance, trailing lock icon, not focusable.
- Frequency field: tappable — opens a ModalBottomSheet picker (DAILY / WEEKLY / MONTHLY / YEARLY); pre-selected MONTHLY.
- Start Date / End Date: tappable — open M3 DatePickerDialog; End Date defaults to null (shown as "Ongoing — no end date").
- Helper text: Outfit body_small (12sp/400), #44483D, 4dp below each field.
- Save Changes: FilledButton — radius 24dp (pill), min-height 56dp, full-width, 32dp margin_top.
- Cancel: TextButton — #4C662B, full-width, 8dp margin_top below Save.
- 24dp bottom spacer to clear keyboard / safe area.

---

## Screen: loading (PUT request in flight)

```
┌─────────────────────────────────────────┐
│ ←  Edit Standing Order                  │
├─────────────────────────────────────────┤
│                                         │
│                                         │
│                                         │
│                                         │
│                  (  ○  )                │  ← soe_saving_indicator: CircularProgressIndicator
│                                         │     40dp, #4C662B, indeterminate, centered
│           Saving changes…               │  ← optional body_medium label, #44483D, centered
│                                         │
│                                         │
│                                         │
│                                         │
└─────────────────────────────────────────┘
```

**Layout notes:**
- Circular spinner centred in the full viewport. All form components (beneficiary card, inputs, buttons) hidden.
- Top app bar back arrow is non-interactive during save to prevent partial-save navigation.
- Progress is indeterminate — spinner color #4C662B (colors.light.primary).
- Accessibility: `role: progressbar`, label "Saving your standing order changes" (assertive live region).

---

## Screen: error (PUT failed — form re-shown with error banner)

```
┌─────────────────────────────────────────┐
│ ←  Edit Standing Order                  │
├─────────────────────────────────────────┤
│                                         │
│  ┌─────────────────────────────────┐    │  ← beneficiary card — re-shown, read-only
│  │  PAYING TO                      │    │
│  │  🏦  Landlord Holdings Ltd      │    │
│  │      GB29 NWBK ... NatWest Bank │    │
│  └─────────────────────────────────┘    │
│                                         │
│  ┌─ Amount ───────────────────────────┐ │  ← inputs re-enabled for retry
│  │  £  1200.00                        │ │
│  └────────────────────────────────────┘ │
│  Amount taken on each payment date      │
│                                         │
│  ┌─ Currency ───────────────────── 🔒 ┐ │
│  │  GBP — British Pound               │ │
│  └────────────────────────────────────┘ │
│                                         │
│  ┌─ 🔁 Frequency ───────────────── ▾ ┐ │
│  │  Monthly                           │ │
│  └────────────────────────────────────┘ │
│                                         │
│  ┌─ Start Date ────────────────── 📅 ┐ │
│  │  1 Jan 2026                        │ │
│  └────────────────────────────────────┘ │
│                                         │
│  ┌─ End Date (optional) ──────── 📅  ┐ │
│  │  Ongoing — no end date             │ │
│  └────────────────────────────────────┘ │
│                                         │
│  ┌─ ⚠ ──────────────────────────────┐  │  ← soe_error_banner
│  │  Couldn't save your changes.      │  │     #FFDAD6 background (error_container)
│  │  Check the amount and try again.  │  │     #410002 text (on_error_container)
│  └───────────────────────────────────┘  │     error_outline leading icon; radius 8dp
│                                         │     role: alert, live: assertive
│  ┌──────────────────────────────────┐   │
│  │          Save Changes            │   │  ← re-enabled #4C662B FilledButton
│  └──────────────────────────────────┘   │
│  ┌──────────────────────────────────┐   │
│  │              Cancel              │   │
│  └──────────────────────────────────┘   │
│                                         │
└─────────────────────────────────────────┘
```

**Layout notes:**
- Full form content restored identically to content state.
- soe_error_banner injected between the last input field (soe_end_date_input) and the action buttons.
- Error banner: #FFDAD6 fill (M3 error_container), #410002 text (on_error_container), `error_outline` leading icon, radius 8dp, horizontal padding 16dp, vertical padding 8dp.
- Accessibility: `role: alert`, `live: assertive` — screen readers announce immediately.
- All inputs remain editable; Save button is re-enabled for retry.
- Validation field errors (amountError, startDateError) display inline below their own fields as M3 `supportingText` in error color #BA1A1A — distinct from the save-failed banner.

---

## Design Checklist (Figma / Stitch)

- [ ] M3 TopAppBar, title "Edit Standing Order", back `arrow_back` navigation icon — no bottom nav
- [ ] Screen background: #F9FAEF (colors.light.background); 16dp horizontal padding
- [ ] soe_beneficiary_card: white (#FFFFFF), radius 16dp, elevation 1dp, 16dp bottom margin
- [ ] "PAYING TO" label: Outfit label_small (11sp/500), #44483D, uppercase, letter-spacing 0.8dp
- [ ] `account_balance` icon: 24dp, #4C662B, beside beneficiary name (decorative role)
- [ ] Beneficiary name: Outfit body_large (16sp/500), #1A1C16 — read-only
- [ ] IBAN line: Outfit body_small (12sp/400), #44483D, monospace — "GB29 NWBK 6016 1331 9268 19 · NatWest Bank" — read-only
- [ ] soe_amount_input: M3 OutlinedTextField, radius 12dp, "£" prefix, decimal keyboard, pre-filled "1200.00"
- [ ] soe_currency_selector: M3 OutlinedTextField, readonly, trailing lock icon, "GBP — British Pound" — disabled appearance
- [ ] soe_frequency_selector: M3 OutlinedTextField, leading `repeat` icon, trailing `expand_more`; tap → ModalBottomSheet picker (DAILY/WEEKLY/MONTHLY/YEARLY)
- [ ] soe_start_date_input: M3 OutlinedTextField, trailing `calendar_today`; tap → M3 DatePickerDialog; pre-filled "1 Jan 2026"
- [ ] soe_end_date_input: M3 OutlinedTextField, trailing `calendar_today`; tap → DatePickerDialog; shows "Ongoing — no end date" when null
- [ ] All helper text: Outfit body_small (12sp/400), #44483D, 4dp below each field
- [ ] Outlined field idle border: #75796C; focused border: #4C662B
- [ ] soe_error_banner: #FFDAD6 background, `error_outline` icon, #410002 text, radius 8dp; visible in error state only
- [ ] soe_save_button: FilledButton, #4C662B fill, #FFFFFF text, Outfit label_large, radius 24dp pill, min-height 56dp, full-width, 32dp top margin
- [ ] soe_cancel_button: TextButton, #4C662B color, Outfit label_large, full-width, 8dp top margin
- [ ] 24dp bottom spacer below cancel button
- [ ] soe_saving_indicator: circular, #4C662B, 40dp, indeterminate, centred — visible in loading state only; form hidden
- [ ] Loading: back arrow non-interactive during save
- [ ] Error: error banner role="alert" live="assertive" for screen reader announcement
- [ ] All text: Outfit typeface. Touch targets minimum 48dp (M3 standard).

---

_Generated by /idea export | 2026-05-30_
