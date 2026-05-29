# MOCKUP — Confirm Payment

**Archetype:** detail_screen
**Shell:** Top app bar ("Confirm Payment") with back arrow. No bottom navigation bar.
**Accent:** #4C662B (Earth-green). Typography: Outfit. Design system: M3.

---

## Screen: review (Primary — payment data loaded)

```
┌─────────────────────────────────────┐
│ ←  Confirm Payment                  │  ← TopAppBar, #F9FAEF bg, Outfit/title_large
├─────────────────────────────────────┤
│                                     │
│  Confirm Payment                    │  ← headline_large, #4C662B
│  Please review the payment details  │  ← body_medium, #44483D
│  before confirming                  │
│                                     │
│  ┌──── Payment Summary ───────────┐ │
│  │           £500.00              │ │  ← display_medium, #4C662B, centered
│  │  ─────────────────────────── │ │
│  │  To         John Smith —      │ │  ← body_medium label #44483D
│  │             Barclays Bank UK  │ │  ← body_large value #1A1C16, w500
│  │  IBAN       GB29 NWBK 6016    │ │  ← monospace body_medium #1A1C16
│  │             1331 9268 19      │ │
│  │  From       Primary Checking  │ │
│  │             (...0130)         │ │
│  │  Reference  Rent August 2026  │ │
│  │  ─────────────────────────── │ │
│  │  Fee                   £0.00  │ │  ← fee_value #386663 teal
│  │  ┌── Total ──── £500.00 ────┐ │ │  ← total_row #F9FAEF bg, title_large #4C662B
│  │  └───────────────────────────┘ │ │
│  └────────────────────────────────┘ │
│                                     │
│  ┌ Scheduled for            [📅] ┐  │  ← outlined input, calendar_today trailing
│  │ Immediate                      │  │
│  └────────────────────────────────┘  │
│                                     │
│  By confirming you authorise this   │  ← body_small #44483D, centered
│  payment per our Terms of Service   │
│                                     │
│  ┌────────────────────────────────┐ │
│  │         Confirm & Send         │ │  ← FilledButton, #4C662B, white text
│  └────────────────────────────────┘ │
│  ┌────────────────────────────────┐ │
│  │          Edit Payment          │ │  ← OutlinedButton, #4C662B border+text
│  └────────────────────────────────┘ │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:**
- 16 dp horizontal padding throughout.
- payment_summary_card: white fill, #CDEDA3 1dp border, 16dp radius, 20dp internal padding.
- Row layout: label (body_medium, #44483D, left) + value (right-aligned or wrapped).
- total_row: #F9FAEF background pill, 8dp radius, bold title_large on both label and value.
- Both buttons full-width, 12dp radius. 16dp gap between terms_text and Confirm button.

---

## Screen: loading (Session initialising)

```
┌─────────────────────────────────────┐
│ ←  Confirm Payment                  │
├─────────────────────────────────────┤
│  ══════════════════════════════     │  ← LinearProgressIndicator top
│                                     │
│  Confirm Payment                    │
│  Please review the payment details  │
│                                     │
│  ┌──── Payment Summary ───────────┐ │
│  │  ████████████  (shimmer)       │ │  ← amount skeleton
│  │  ─────────────────────────── │ │
│  │  To     ████████████████████  │ │  ← to_value shimmer
│  │  IBAN   ████████████████████  │ │  ← iban_value shimmer
│  │  From   ████████████████████  │ │  ← from_value shimmer
│  │  Ref    ████████████████████  │ │  ← reference_value shimmer
│  │  Fee    ████████              │ │  ← fee_value shimmer
│  │  Total  ████████              │ │  ← total shimmer
│  └────────────────────────────────┘ │
│                                     │
│  ┌────────────────────────────────┐ │
│  │         Confirm & Send         │ │  ← disabled, #C5C8BA bg
│  └────────────────────────────────┘ │
│  ┌────────────────────────────────┐ │
│  │          Edit Payment          │ │  ← disabled, #C5C8BA border
│  └────────────────────────────────┘ │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Shimmer animation on all data fields. Buttons disabled (#C5C8BA tint). LinearProgressIndicator below TopAppBar.

---

## Screen: submitting (POST in flight)

```
┌─────────────────────────────────────┐
│ ←  Confirm Payment                  │
├─────────────────────────────────────┤
│  ══════════════════════════════     │  ← LinearProgressIndicator active
│                                     │
│  ┌──── Payment Summary ───────────┐ │
│  │           £500.00              │ │
│  │  To       John Smith           │ │
│  │  Fee      £0.00                │ │
│  │  Total    £500.00              │ │
│  └────────────────────────────────┘ │
│                                     │
│  ┌────────────────────────────────┐ │
│  │    [○] Confirming payment…     │ │  ← loading spinner inside button
│  └────────────────────────────────┘ │
│  ┌────────────────────────────────┐ │
│  │          Edit Payment          │ │  ← disabled
│  └────────────────────────────────┘ │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Summary card remains visible. Confirm button replaces label with circular spinner. Both buttons are non-interactive during submission.

---

## Screen: error (Payment failed)

```
┌─────────────────────────────────────┐
│ ←  Confirm Payment                  │
├─────────────────────────────────────┤
│                                     │
│  ┌─── ⚠  Error ───────────────────┐ │
│  │  Payment could not be           │ │  ← error banner, #FFDAD6 bg, #410002 text
│  │  processed. Please try again.  │ │
│  └────────────────────────────────┘ │
│                                     │
│  ┌──── Payment Summary ───────────┐ │
│  │           £500.00              │ │
│  │  To       John Smith           │ │
│  │  Fee      £0.00                │ │
│  │  Total    £500.00              │ │
│  └────────────────────────────────┘ │
│                                     │
│  ┌────────────────────────────────┐ │
│  │         Confirm & Send         │ │  ← re-enabled, #4C662B
│  └────────────────────────────────┘ │
│  ┌────────────────────────────────┐ │
│  │          Edit Payment          │ │  ← outlined, #4C662B
│  └────────────────────────────────┘ │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Error banner at top of scrollable content. Summary card visible. Confirm & Send re-enabled for retry. Error banner uses #FFDAD6 background, #410002 text, error_outline leading icon.

---

## Screen: empty (No transaction to confirm)

```
┌─────────────────────────────────────┐
│ ←  Confirm Payment                  │
├─────────────────────────────────────┤
│                                     │
│                                     │
│           send                      │  ← M3 outlined icon 48dp, #C5C8BA
│                                     │
│   No transaction to confirm.        │  ← body_large, #1A1C16, centered
│   Start a new payment.              │  ← body_medium, #44483D, centered
│                                     │
│  ┌────────────────────────────────┐ │
│  │          Edit Payment          │ │  ← outlined, #4C662B — navigates to send-money
│  └────────────────────────────────┘ │
│                                     │
└─────────────────────────────────────┘
```

**Layout notes:** Centered icon + messages. Only Edit Payment button shown; Confirm & Send hidden.

---

## Design Checklist (Figma / Stitch)

- [ ] M3 TopAppBar with back navigation icon — title "Confirm Payment"
- [ ] payment_summary_card: white fill, #CDEDA3 1dp border, 16dp radius
- [ ] payment_amount: display_medium (45sp) in #4C662B, center-aligned
- [ ] Label/value rows: body_medium labels in #44483D, values right-aligned or wrapped
- [ ] fee_value: #386663 teal to signal zero-cost
- [ ] total_row: #F9FAEF pill background, both label and value in title_large weight 700
- [ ] scheduled_date_selector: outlined, calendar_today trailing icon
- [ ] Confirm & Send: FilledButton #4C662B, full-width, 12dp radius
- [ ] Edit Payment: OutlinedButton #4C662B border/text, full-width, 12dp radius
- [ ] Loading: shimmer on all data fields, LinearProgressIndicator
- [ ] Submitting: spinner inside Confirm button, both buttons disabled
- [ ] Error: #FFDAD6 banner with error_outline icon and #410002 text
- [ ] Empty: send icon 48dp #C5C8BA, centred message layout
- [ ] All text Outfit typeface
- [ ] 16 dp horizontal content padding throughout
