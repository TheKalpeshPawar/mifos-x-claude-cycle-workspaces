# New Standing Order — Visual Specification

| Field     | Value                 |
|-----------|-----------------------|
| Feature   | standing-order-create |
| Flavor    | consumer              |
| Archetype | form_screen           |

---

## Screen Layout

Top-to-bottom hierarchy on a vertically scrolling form under a "New Standing Order" top app bar:

```
[ ← New Standing Order ]                    ← top app bar, back arrow
──────────────────────────────────────────
[ From account                         ⌄ ]  ← soc_source_account_field, read-only
[ Pay to                               ⌄ ]  ← soc_payee_field, read-only
[ Amount                            GBP   ]  ← soc_amount_field, suffix currency
  Amount taken on each payment date          ← supporting text
  Repeats                                    ← soc_frequency_label, label_large
[ (Daily)(Weekly)(Fortnightly)(Monthly●) ]  ← soc_frequency_chips, filter, scroll
[ First payment date                  📅 ]  ← soc_start_date_field, read-only
  Repeats every Monday                       ← soc_recurrence_hint, body_small green
[ End date (optional)                 📅 ]  ← soc_end_date_field, clearable
  Leave empty to pay until cancelled         ← supporting text
  Start date must be after today             ← soc_error_text (conditional, red)
[ Create standing order  (filled #4C662B) ]  ← soc_submit_button, full-width
```

---

## Components

### soc_source_account_field
- Outlined read-only field, "From account", trailing `expand_more`, full-width
- Tap opens soc_account_picker_sheet; switching the account reloads payees

### soc_payee_field
- Outlined read-only field, "Pay to", trailing `expand_more`, 12dp top margin
- Shows "Select payee" until chosen; opens soc_payee_menu dropdown
- Replaced by soc_no_payees_hint ("Add a beneficiary first — standing orders pay an existing payee.") when the account has no beneficiaries

### soc_amount_field
- Outlined text field, currency-code suffix (e.g. "GBP"), supporting text "Amount taken on each payment date"
- Required, rule `amount > 0`; comma normalised to dot

### soc_frequency_label + soc_frequency_chips
- "Repeats" label — `label_large`, `#44483D`
- Horizontal scrollable filter chips: Daily, Weekly, Fortnightly, Monthly, Yearly (default Monthly selected)
- BI-WEEKLY is labelled "Fortnightly"; 8dp chip spacing

### soc_start_date_field + soc_recurrence_hint
- Outlined read-only date field "First payment date", trailing `calendar_today`, supporting "First payment runs on this date"
- Opens an M3 DatePickerDialog restricted to dates strictly after today
- Below it, soc_recurrence_hint in `#4C662B` (`body_small`): "Repeats every Monday" / "Repeats on the 5th of each month" / "Repeats every 1 March" — hidden until a date is chosen

### soc_end_date_field
- Optional outlined read-only date field "End date (optional)", trailing `calendar_today` (clears to close icon when set), supporting "Leave empty to pay until cancelled"
- Picker restricted to dates after the start date

### soc_error_text
- Inline error (`form.error`), `body_small`, `#BA1A1A`, 8dp top margin — e.g. "Start date must be after today"; also fired as a toast; hidden when null

### soc_submit_button
- Filled, `#4C662B` background, `#FFFFFF` text, 12dp radius, full-width, 20dp top margin
- Disabled with label "Creating…" while submitting

### soc_loading
- Centered CircularProgressIndicator on `#F9FAEF`, 32dp padding — shown while the account + beneficiaries load

---

## States

| State      | Visual                                                                                     |
|------------|-------------------------------------------------------------------------------------------|
| loading    | Centered progress (soc_loading); no form visible                                          |
| content    | Full editable form as drawn above; recurrence hint + error appear conditionally           |
| submitting | Same layout; submit button disabled, label "Creating…"                                     |
| error      | soc_error_text shown above the submit button (and a toast); form stays editable           |
| created    | No standalone surface — navigates to payment-authorize-handoff carrying the ConsentId      |

---

## Interaction Patterns

| Interaction          | Component                | Result                                              |
|----------------------|--------------------------|-----------------------------------------------------|
| Tap "From account"   | soc_source_account_field | Account picker sheet opens; payees reload on switch |
| Tap "Pay to"         | soc_payee_field          | Payee dropdown opens                                |
| Tap a frequency chip | soc_frequency_chips      | Selects frequency; updates the recurrence hint      |
| Tap "First payment date"| soc_start_date_field  | DatePicker (after today); sets the recurrence anchor|
| Tap "End date"       | soc_end_date_field       | DatePicker (after start); clearable                 |
| Tap "Create standing order"| soc_submit_button  | Validate → POST consent → "Creating…" → handoff     |

---

## Content Data

| Element          | Value                          |
|------------------|--------------------------------|
| Source account   | Everyday Current (Oliver Bennett)|
| Payee            | British Gas                    |
| Amount           | £92.00                         |
| Frequency        | Monthly                        |
| First payment    | 5 Jul 2026                     |
| Recurrence hint  | Repeats on the 5th of each month|
| Number of payments| 12                            |

> Real OBIE content from demo-data.yaml#/collections/create_domestic_standing_order_consent (GBP 92.00/month to British Gas).

---

## Design Notes

**Progressive disclosure:** The recurrence hint only appears once a first-payment date is chosen — it confirms the user's mental model ("Repeats on the 5th of each month") in plain language derived from frequency + anchor, reducing the cognitive load of OBIE schedule codes.

**Optional end date framing:** The "Leave empty to pay until cancelled" supporting text makes the open-ended nature of a standing order explicit, so an empty field reads as intentional, not incomplete.

**Read-only pickers:** Account, payee, and both dates are read-only fields that open sheets/dialogs rather than free-text inputs — the only typed field is the amount. This keeps every value structurally valid (a real account, a real payee, a real future date).

**Submit-as-consent:** "Create standing order" stages the OBIE consent (AWAU) and hands off to the bank authorise flow — the in-app button does not finalise the order, so its "Creating…" label honestly reflects the consent round-trip, not completion.

*Generated by /idea export | 2026-06-15*
