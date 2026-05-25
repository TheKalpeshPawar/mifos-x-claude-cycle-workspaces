# Confirm Payment — Visual Specification

| Field | Value |
|---|---|
| Feature | send-money-confirm |
| Flavor | consumer |
| Archetype | detail_screen |

---

## Screen Layout

Top-to-bottom component hierarchy on a vertically scrolling confirmation screen:

```
[ Top App Bar: "Confirm Payment"  ← back ]
──────────────────────────────────────────
[ Headline: "Confirm Payment"            ]  ← #1800B1, headline_large
[ Subtitle: "Please review the payment   ]  ← body_medium, #666666
  details before confirming"             ]
┌────────────────────────────────────────┐
│  PAYMENT SUMMARY CARD (elevation 2)    │  ← white, border #E8E8FF, r=16dp
│                                        │
│        £500.00                         │  ← display_medium, #1800B1, center
│  ──────────────────────────────────    │
│  To           John Smith — Barclays    │
│               Bank UK                 │
│  IBAN         GB29 NWBK 6016 1331     │  ← monospace font
│               9268 19                 │
│  From         Primary Checking        │
│               (...0130)               │
│  Reference    Rent August 2026        │
│  ──────────────────────────────────    │
│  Fee          £0.00                   │  ← teal #008B8B
│  ┌──────────────────────────────────┐ │
│  │  Total           £500.00         │ │  ← bg #F5F5FF, bold, r=8dp
│  └──────────────────────────────────┘ │
└────────────────────────────────────────┘
[ Scheduled for: [Immediate   📅]        ]  ← outlined, trailing calendar icon
[ "By confirming you authorise this      ]  ← body_small, #888888, centered
   payment per our Terms of Service"    ]
[ Confirm & Send  (filled, #1800B1)      ]  ← full-width, r=12dp, 16dp padding
[ Edit Payment    (outlined, #1800B1)    ]  ← full-width, r=12dp, 14dp padding
──────────────────────────────────────────
```

---

## Components

### confirm_title
- Typography: `headline_large`
- Color: `#1800B1`
- Padding bottom: 4dp

### review_subtitle
- Typography: `body_medium`
- Color: `#666666`
- Padding bottom: 16dp

### payment_summary_card
- Background: `#FFFFFF`, corner radius: 16dp, elevation: 2
- Border: `#E8E8FF`, 1dp
- Padding: 20dp horizontal, 20dp vertical
- Contains all detail rows as a visually unified receipt card

### payment_amount
- Content: "£500.00"
- Typography: `display_medium` (45sp, Roboto)
- Color: `#1800B1`
- Text align: center
- Dominant visual element — immediately communicates the financial commitment

### Detail rows (to_row, iban_row, from_row, reference_row)
- Layout: horizontal stack with `space_between` justification
- Label side: `body_medium`, color `#888888` (muted)
- Value side: `body_large` or `body_medium`, color `#111111` or `#333333`
- IBAN value uses `font_family: monospace` for readability
- Padding vertical: 10dp per row

### fee_row
- Fee label: `body_medium`, `#888888`
- Fee value "£0.00": `body_medium`, `#008B8B` (teal) — signals zero cost prominently

### total_row
- Background: `#F5F5FF`, corner radius: 8dp, padding 12dp horizontal
- "Total" label: `title_large`, `#111111`, bold
- "£500.00" value: `title_large`, `#1800B1`, bold
- Visual weight communicates finality

### scheduled_date_selector
- Variant: outlined, trailing `calendar_today` icon
- Content: "Immediate"
- Corner radius: 12dp
- Padding top: 16dp above card

### confirm_send_button
- Variant: filled, background `#1800B1`, text `#FFFFFF`
- Full-width, corner radius 12dp, padding vertical 16dp
- Loading state: spinner replaces label, both buttons disabled

### edit_payment_button
- Variant: outlined, border `#1800B1`, text `#1800B1`
- Full-width, corner radius 12dp, padding vertical 14dp
- Navigates back to send-money screen (pop)

---

## Interaction Patterns

| Interaction | Component | Result |
|---|---|---|
| Tap "Scheduled for" | scheduled_date_selector | Date picker dialog opens |
| Tap "Confirm & Send" | confirm_send_button | State → submitting, API call fires |
| Tap "Edit Payment" | edit_payment_button | Navigate back to send-money |
| Payment succeeds | — | Snackbar "Payment of £500.00 sent to John Smith", navigate home |
| Payment fails | — | Error banner, confirm re-enabled |

---

## Content Data

| Element | Value |
|---|---|
| Amount | £500.00 |
| Recipient | John Smith — Barclays Bank UK |
| IBAN | GB29 NWBK 6016 1331 9268 19 |
| Source account | Primary Checking (...0130) |
| Reference | Rent August 2026 |
| Fee | £0.00 |
| Total | £500.00 |
| Schedule | Immediate |
| Success snackbar | "Payment of £500.00 sent to John Smith" |

---

## Design Notes

**Hierarchy:** The `display_medium` amount at the top of the card anchors the confirmation visually — users see the financial impact before reading the details.

**Receipt pattern:** The white card with subtle border and elevation 2 mimics a printed receipt, reinforcing the "review before finalise" mental model.

**Fee teal color #008B8B:** Distinct from primary and from error. Draws attention to the zero-cost SEPA path without alarm.

**Total row highlight:** `#F5F5FF` background — slight brand tint on the total row separates it from other rows, preventing it from being skipped.

**Button stack:** Primary action (filled) sits above secondary action (outlined) — standard MD3 two-button layout. 2dp gap ensures tap targets do not bleed.

**Accessibility:** `display_medium` amount carries `content_description: "Payment amount: five hundred pounds"` — screen readers receive the spelled-out value. IBAN announced character-group by character-group per `content_description`.

*Generated by /idea export | 2026-05-25*
