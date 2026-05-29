# MOCKUP — Confirm Payment

**Archetype:** detail_screen
**Shell:** Top app bar — title "Confirm Payment", back arrow (`arrow_back`). No bottom navigation bar.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: review (Primary — payment data loaded)

```
┌─────────────────────────────────────┐
│ ←  Confirm Payment                  │  ← TopAppBar, #F9FAEF bg, Outfit/title_large 22sp
├─────────────────────────────────────┤
│                                     │
│  Confirm Payment                    │  ← headline_large 32sp, #4C662B (confirm_title)
│  Please review the payment details  │  ← body_medium 14sp, #44483D (review_subtitle)
│  before confirming                  │
│                                     │
│  ┌──────────────────────────────────┐│  ← payment_summary_card: #FFFFFF, 16dp radius,
│  │                                  ││    1dp #CDEDA3 border, 2dp elevation, 20dp pad
│  │          £500.00                 ││  ← display_medium 45sp, #4C662B, centred (payment_amount)
│  │  ────────────────────────────── ││  ← amount_divider #E1E4D5
│  │  To          John Smith —       ││  ← to_label: body_medium #44483D
│  │              Barclays Bank UK   ││  ← to_value: body_large 16sp, #1A1C16, w500
│  │  IBAN        GB29 NWBK 6016    ││  ← iban_label: body_medium #44483D
│  │              1331 9268 19      ││  ← iban_value: body_medium, #1A1C16, monospace
│  │  From        Primary Checking  ││  ← from_label/value: body_medium #44483D / #1A1C16
│  │              (...0130)         ││
│  │  Reference   Rent August 2026  ││  ← reference_label/value: body_medium #44483D / #1A1C16
│  │  ────────────────────────────── ││  ← fee_divider #E1E4D5
│  │  Fee                    £0.00  ││  ← fee_label #44483D / fee_value #386663 teal
│  │  ┌────────────────────────────┐ ││
│  │  │  Total           £500.00  │ ││  ← total_row: #F9FAEF fill, 8dp radius
│  │  │  (title_large 22sp, w700) │ ││  ← total_label #1A1C16 / total_value #4C662B
│  │  └────────────────────────────┘ ││
│  └──────────────────────────────────┘│
│                                     │
│  ┌──────────────────────────── [📅] │  ← scheduled_date_selector: outlined, calendar_today
│  │  Scheduled for: Immediate        │     trailing icon, 12dp radius, 16dp top margin
│  └──────────────────────────────────┘
│                                     │
│  By confirming you authorise this   │  ← terms_text: body_small 12sp, #44483D, centred
│  payment per our Terms of Service   │
│                                     │
│  ┌──────────────────────────────────┐│
│  │         Confirm & Send           ││  ← FilledButton, #4C662B bg, #FFFFFF text
│  └──────────────────────────────────┘│  ← Outfit/label_large 14sp, 12dp radius, full-width
│  ┌──────────────────────────────────┐│
│  │          Edit Payment            ││  ← OutlinedButton, #4C662B border+text
│  └──────────────────────────────────┘│  ← Outfit/label_large 14sp, 12dp radius, full-width
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:**
- 16dp horizontal content padding throughout.
- payment_summary_card: #FFFFFF fill, 1dp #CDEDA3 border, 16dp radius, 2dp elevation, 20dp horizontal + vertical padding.
- Detail rows (to/iban/from/reference/fee): horizontal stack, space-between, 10dp vertical padding; label body_medium #44483D left, value right-aligned.
- to_value uses body_large (#1A1C16, weight 500); iban_value uses monospace font family.
- total_row: #F9FAEF fill, 8dp radius, sm padding on all sides; both label and value Outfit/title_large 22sp weight 700.
- fee_value colour #386663 (secondary teal) to signal zero-cost at a glance.
- scheduled_date_selector: outlined variant, trailing calendar_today icon, 12dp radius.
- terms_text centered above action buttons, sm vertical padding.
- Both CTA buttons full-width, 12dp radius, md vertical padding. 8dp vertical gap between them.

---

## Screen: loading (Session initialising / data resolving)

```
┌─────────────────────────────────────┐
│ ←  Confirm Payment                  │
├─────────────────────────────────────┤
│  ══════════════════════════════     │  ← LinearProgressIndicator (indeterminate)
│                                     │
│  Confirm Payment                    │  ← confirm_title visible
│  Please review the payment details  │  ← review_subtitle visible
│                                     │
│  ┌──────────────────────────────────┐│
│  │  ████████████████████ (shimmer)  ││  ← payment_amount skeleton (#E1E4D5)
│  │  ────────────────────────────── ││
│  │  To     ████████████████████    ││  ← to_value shimmer
│  │  IBAN   ████████████████████    ││  ← iban_value shimmer
│  │  From   ████████████████        ││  ← from_value shimmer
│  │  Ref    ████████████████████    ││  ← reference_value shimmer
│  │  Fee    ████████                ││  ← fee_value shimmer
│  │  Total  ████████                ││  ← total_value shimmer
│  └──────────────────────────────────┘│
│                                     │
│  ┌──────────────────────────────────┐│
│  │         Confirm & Send           ││  ← disabled, #C5C8BA bg (outline_variant)
│  └──────────────────────────────────┘│
│  ┌──────────────────────────────────┐│
│  │          Edit Payment            ││  ← disabled, #C5C8BA border
│  └──────────────────────────────────┘│
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Shimmer animation (skeleton_shimmer: true) over payment_amount, to_value, iban_value, from_value, reference_value, fee_value, total_value using surface_variant (#E1E4D5) base. LinearProgressIndicator renders below TopAppBar. confirm_title and review_subtitle remain visible. Both buttons disabled with outline_variant (#C5C8BA) tint.

---

## Screen: submitting (POST in flight)

```
┌─────────────────────────────────────┐
│ ←  Confirm Payment                  │
├─────────────────────────────────────┤
│  ══════════════════════════════     │  ← LinearProgressIndicator (active)
│                                     │
│  Confirm Payment                    │
│                                     │
│  ┌──────────────────────────────────┐│
│  │          £500.00                 ││  ← payment_amount visible
│  │  To      John Smith — Barclays   ││  ← to_value visible
│  │  Fee     £0.00                   ││  ← fee_value visible
│  │  Total   £500.00                 ││  ← total_value visible
│  └──────────────────────────────────┘│
│                                     │
│  ┌──────────────────────────────────┐│
│  │   [◉] Confirming payment…        ││  ← confirm_send_button: loading spinner replacing label
│  └──────────────────────────────────┘│  ← disabled, #4C662B (spinner uses on_primary #FFFFFF)
│  ┌──────────────────────────────────┐│
│  │          Edit Payment            ││  ← disabled, #C5C8BA border
│  └──────────────────────────────────┘│
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Reduced component set visible (amount, to_value, fee, total). Confirm button replaces text label with circular loading spinner; background remains #4C662B but text/spinner #FFFFFF. Edit Payment disabled. LinearProgressIndicator active.

---

## Screen: error (PaymentFailed)

```
┌─────────────────────────────────────┐
│ ←  Confirm Payment                  │
├─────────────────────────────────────┤
│                                     │
│  ┌── ⚠  Payment Error ─────────────┐│  ← error banner: #FFDAD6 bg, #410002 text
│  │  Payment could not be processed. ││    error_outline icon 24dp #BA1A1A leading
│  │  Please try again.              ││
│  └──────────────────────────────────┘│
│                                     │
│  Confirm Payment                    │
│                                     │
│  ┌──────────────────────────────────┐│
│  │          £500.00                 ││  ← payment_amount visible
│  │  To      John Smith — Barclays   ││
│  │  Fee     £0.00                   ││
│  │  Total   £500.00                 ││
│  │  Terms of Service notice         ││  ← terms_text visible
│  └──────────────────────────────────┘│
│                                     │
│  ┌──────────────────────────────────┐│
│  │         Confirm & Send           ││  ← re-enabled, #4C662B (user may retry)
│  └──────────────────────────────────┘│
│  ┌──────────────────────────────────┐│
│  │          Edit Payment            ││  ← outlined, #4C662B (navigate back to fix details)
│  └──────────────────────────────────┘│
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Error banner at top of scrollable content — #FFDAD6 background (error_container), #410002 text (on_error_container), error_outline icon 24dp #BA1A1A leading. Summary card visible with partial component set. confirm_send_button re-enabled for retry. edit_payment_button also active to allow corrections.

---

## Screen: empty (No transaction context)

```
┌─────────────────────────────────────┐
│ ←  Confirm Payment                  │
├─────────────────────────────────────┤
│                                     │
│                                     │
│                                     │
│            [  send  ]               │  ← send icon 48dp (icon-2xl), #C5C8BA
│                                     │
│   No transaction to confirm.        │  ← body_large 16sp, #1A1C16, centred
│   Start a new payment.              │  ← body_medium 14sp, #44483D, centred
│                                     │
│                                     │
│  ┌──────────────────────────────────┐│
│  │          Edit Payment            ││  ← outlined, #4C662B — navigates to send-money
│  └──────────────────────────────────┘│
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Icon + text stack vertically centred in available space. Only edit_payment_button shown; confirm_send_button hidden. confirm_title visible. Empty state message uses real copy from ui.yaml.

---

## Design Checklist (Figma / Stitch)

- [ ] M3 TopAppBar — title "Confirm Payment", arrow_back navigation icon, #F9FAEF background, 56dp height
- [ ] confirm_title: Outfit headline_large (32sp/400), #4C662B
- [ ] review_subtitle: Outfit body_medium (14sp/400), #44483D
- [ ] payment_summary_card: #FFFFFF fill, 1dp #CDEDA3 border, 16dp corner radius, 2dp elevation, 20dp h+v padding
- [ ] payment_amount: Outfit display_medium (45sp/400), #4C662B, horizontally centred, sm top pad + md bottom pad
- [ ] amount_divider and fee_divider: #E1E4D5, 1dp, xs vertical padding
- [ ] Detail row labels (To/IBAN/From/Reference/Fee): Outfit body_medium (14sp/400), #44483D (9.37:1 contrast — A11Y-002 fix)
- [ ] to_value: Outfit body_large (16sp/400), #1A1C16, weight 500
- [ ] iban_value: Outfit body_medium (14sp/400), #1A1C16, monospace font family
- [ ] from_value / reference_value: Outfit body_medium (14sp/400), #1A1C16
- [ ] fee_value: #386663 (secondary teal) to signal zero-cost — NOT #44483D
- [ ] total_row: #F9FAEF background, 8dp corner radius, sm padding; label + value Outfit title_large (22sp) weight 700; label #1A1C16, value #4C662B
- [ ] scheduled_date_selector: outlined variant, trailing calendar_today icon 24dp, 12dp radius
- [ ] terms_text: Outfit body_small (12sp/400), #44483D, centred, sm vertical padding
- [ ] Confirm & Send: FilledButton #4C662B bg / #FFFFFF text, Outfit/label_large (14sp/500), 12dp radius, full-width, md vertical padding
- [ ] Edit Payment: OutlinedButton #4C662B border + text, Outfit/label_large, 12dp radius, full-width, 14dp vertical padding
- [ ] Loading: shimmer (#E1E4D5) on all dynamic fields; LinearProgressIndicator below TopAppBar; both buttons disabled
- [ ] Submitting: spinner inside Confirm button (#FFFFFF on #4C662B); both buttons disabled; linear progress active
- [ ] Error: #FFDAD6 banner (error_container), #410002 text (on_error_container), error_outline icon; Confirm re-enabled
- [ ] Empty: send icon 48dp #C5C8BA; "No transaction to confirm. Start a new payment." centred; only Edit Payment shown
- [ ] All text: Outfit typeface exclusively. Touch targets 48dp minimum. 16dp horizontal content padding. 8dp gap between adjacent buttons.

---

_Generated by /idea export | 2026-05-30_
