# Payment Sent — Visual Specification

| Field     | Value          |
|-----------|----------------|
| Feature   | payment-result |
| Flavor    | consumer       |
| Archetype | confirmation   |

---

## Screen Layout

Top-to-bottom hierarchy on a vertically scrolling, chrome-free result screen:

```
┌────────────────────────────────────────┐
│   HERO GRADIENT CARD (earth-green)      │  ← gradient_primary, 28dp bottom radius
│                                        │
│            (  ✓  )                     │  ← 92dp white circle, check tint #4C662B
│                                        │
│         Payment sent                   │  ← display_small, #FFFFFF, weight 700
│      £150.00 to James Whitfield        │  ← body_large, #F5FFE6
│        ( ● COMPLETED )                 │  ← white pill @ 0.18 alpha, dot #B6F2C0
└────────────────────────────────────────┘
┌────────────────────────────────────────┐
│  DETAILS CARD (white, elevation 2)     │  ← #FFFFFF, r=16dp, 16dp margin
│  Transaction ID      dp-7a21c9f4-…     │
│  ──────────────────────────────────    │  ← divider #E1E4D5
│  From                Everyday Current   │
│  Charge              £0.00              │
│  Posted              Just now          │
└────────────────────────────────────────┘
[ View transaction  (filled, #4C662B)    ]  ← full-width, r=12dp, 52dp height
[ Done              (text, #4C662B)       ]  ← full-width, text variant
```

---

## Components

### hero_card
- Background: `gradient_primary` (earth-green vertical gradient), text `#FFFFFF`
- Corner radius bottom: 28dp; padding 72dp top / 36dp bottom / 24dp horizontal
- Alignment: centre — anchors the success moment

### success_check
- 92dp white (`#FFFFFF`) circle, `check` glyph tinted `#4C662B` (primary)
- 16dp bottom margin before the headline

### result_title
- "Payment sent" — `display_small`, `#FFFFFF`, weight 700, centre-aligned

### result_summary
- "£150.00 to James Whitfield" — `body_large`, `#F5FFE6`, centre-aligned
- Data-driven: `{currencySymbol(currency)}{amount} to {beneficiaryName}` (falls back to "beneficiary" when blank)

### status_pill
- "● COMPLETED" — pill shape, white fill at 0.18 alpha, white text, dot `#B6F2C0`
- Maps `Data.Status`: ACSC/ACSP → "COMPLETED"

### details_card
- White (`#FFFFFF`), corner radius 16dp, elevation 2, 20dp horizontal + 8dp vertical padding, 16dp margin
- Contains the transaction detail rows as a unified receipt card

### Detail rows (transaction_id_row, from_row, charge_row, posted_row)
- Layout: horizontal stack, `space_between`, 14dp vertical padding per row
- Label side: `body_medium`, `#44483D`
- Value side: `body_medium`, `#1A1C16`
- transaction_id_row shows the shortened DomesticPaymentId (first 13 chars + ellipsis, or "—" when blank)
- charge_row shows the summed `Data.Charges` (`£0.00` when absent)
- details_divider (`#E1E4D5`, 1dp) sits below the transaction-id row

### view_transaction_button
- Filled, `#4C662B` background, `#FFFFFF` label; full-width, corner radius 12dp, 52dp height
- Navigates to transaction-detail

### done_button
- Text variant, `#4C662B` label, full-width
- Navigates to home

---

## Interaction Patterns

| Interaction               | Component                | Result                                            |
|---------------------------|--------------------------|---------------------------------------------------|
| Screen opens              | —                        | Instant paint from nav args, then status read confirms |
| Status read returns ACSC/ACSP | status_pill         | "● COMPLETED" pill renders                         |
| Status read returns RJCT  | —                        | Navigate to payment-declined                       |
| Tap "View transaction"    | view_transaction_button  | Navigate to transaction-detail                     |
| Tap "Done"                | done_button              | Navigate to home                                   |

---

## Content Data

| Element        | Value                       |
|----------------|-----------------------------|
| Headline       | Payment sent                |
| Summary        | £150.00 to James Whitfield  |
| Status         | ● COMPLETED                 |
| Transaction ID | dp-7a21c9f4-…               |
| From           | Everyday Current            |
| Charge         | £0.00                       |
| Posted         | Just now                    |

> Real OBIE content from demo-data.yaml#/collections/get_domestic_payment_status (GBP 150.00 to James Whitfield, ref "Rent June").

---

## Design Notes

**Hero dominance:** The full-bleed gradient hero card with the white check-circle is the screen's emotional payload — the user sees the success before any detail. Chrome (top bar, bottom nav) is intentionally absent so nothing competes.

**Receipt pattern:** The white details card with elevation 2 mimics a printed receipt, listing the transaction id, source, charge and posted time in a scannable two-column layout.

**Status pill:** The translucent white pill with a `#B6F2C0` dot reads cleanly on the gradient without introducing a second accent colour. It is the only place `Data.Status` surfaces verbatim.

**Counterparty rule:** result_summary uses the resolved holder name for `Data.Initiation.CreditorAccount.Name` — never a raw login username (project HARD RULE).

**Action stack:** Primary "View transaction" (filled) sits above secondary "Done" (text) — standard MD3 priority order.

*Generated by /idea export | 2026-06-15*
