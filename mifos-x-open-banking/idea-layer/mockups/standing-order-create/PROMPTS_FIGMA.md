# Figma Prompts — New Standing Order (Standing Order Create)

**Feature:** standing-order-create
**Archetype:** form_screen (top app bar, no bottom nav)
**Design System:** Material 3 — Earth-green palette, Outfit typeface

---

## Screen: content

Design a full-screen Android mobile screen (390×844dp) for the "New Standing Order" creation form in the HSBC Open Banking app.

**Top app bar:** small M3 app bar, `#F9FAEF` surface, title "New Standing Order" (Outfit 22sp `#1A1C16`) with a leading `arrow_back` icon. No actions. No bottom navigation bar.

**Background:** `#F9FAEF`. Content is a vertically scrolling column, 16dp horizontal padding, 16dp top padding, 12dp gap between fields.

1. **From-account field** — outlined read-only text field, full-width, 12dp radius, label "From account", trailing `expand_more` icon, value "Everyday Current" (Outfit 16sp `#1A1C16`).
2. **Pay-to field** — outlined read-only text field, label "Pay to", trailing `expand_more`, value "British Gas".
3. **Amount field** — outlined text field, label "Amount", trailing suffix "GBP" (Outfit 14sp `#44483D`), value "92.00", supporting text "Amount taken on each payment date" (Outfit 12sp `#44483D`).
4. **Repeats label** — "Repeats", Outfit 14sp weight 500, `#44483D`.
5. **Frequency chip row** — five M3 filter chips, horizontal scroll, 8dp gap: "Daily", "Weekly", "Fortnightly", "Monthly" (selected: `#CDEDA3` fill `#102000` label), "Yearly" (unselected outline).
6. **First-payment-date field** — outlined read-only text field, label "First payment date", trailing `calendar_today` icon, value "5 Jul 2026", supporting text "First payment runs on this date".
7. **Recurrence hint** — "Repeats on the 5th of each month" — Outfit 12sp `#4C662B`, just below the date field.
8. **End-date field** — outlined read-only text field, label "End date (optional)", trailing `calendar_today`, empty value, supporting text "Leave empty to pay until cancelled".
9. **Submit button** — filled, full-width, `#4C662B` fill, `#FFFFFF` label "Create standing order" (Outfit 16sp weight 500), 12dp radius, 52dp height, 20dp top margin.

**DO NOT add:** a bottom navigation bar, free-text inputs for account/payee/date (those are read-only pickers), or a confirm/summary card.

---

## Screen: loading

Same top app bar and `#F9FAEF` background. The form is replaced by a single centred 40dp circular indeterminate progress indicator `#4C662B`, vertically centred. No fields, no button.

---

## Screen: submitting

Identical to `content`, with one change: the "Create standing order" button is disabled (60% opacity `#4C662B` fill), label reads "Creating…", and shows a small white circular spinner before the label. All form fields remain visible but non-interactive.

---

## Screen: error

Identical to `content`, with one addition: an inline error line appears directly above the submit button — "Start date must be after today" — Outfit 12sp `#BA1A1A`, 8dp top margin. The form fields stay fully editable. No full-screen error illustration — this is an inline-validation form error.

---
