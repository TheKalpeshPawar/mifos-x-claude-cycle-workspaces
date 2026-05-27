# MOCKUP.md — direct-debit-detail

Design system: Material 3 · Typography: Outfit · Accent: #4C662B (Earth-green)
Canvas: 390 × 844 px (iPhone 14 base)

---

## State: loading

```
┌─────────────────────────────────────────┐
│ ← [TopAppBar]  Direct Debit Detail      │  height: 64dp, surface color
├─────────────────────────────────────────┤
│                                         │
│  ┌───────────────────────────────────┐  │
│  │ ░░░░░░░░░░░░░░░░░░  ░░░░░░░░░░   │  │  skeleton: counterparty name line
│  │ ░░░░░░░    ░░░░░░░░░░░░░░░░░░░   │  │  skeleton: status chip + amount
│  └───────────────────────────────────┘  │  card: 16dp margin, 12dp radius
│                                         │
│  ░░░░░░░░░░░░░░░  ░░░░░░░░░░░░░░░░░░   │  skeleton: meta row 1
│  ░░░░░░░░░░░░░    ░░░░░░░░░░░░░░░░░░   │  skeleton: meta row 2
│  ░░░░░░░░░░░░░░░░ ░░░░░░░░░░░░░░░░░░   │  skeleton: meta row 3
│  ░░░░░░░░░░░      ░░░░░░░░░░░░░░░░░░   │  skeleton: meta row 4
│                                         │
│  ── Recent Payments ──────────────────  │  section divider skeleton
│                                         │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │  skeleton: payment row 1
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │  skeleton: payment row 2
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │  skeleton: payment row 3
│                                         │
└─────────────────────────────────────────┘
Shimmer animation: left-to-right gradient sweep, 1200ms loop
```

---

## State: content

```
┌─────────────────────────────────────────┐
│ ←  Direct Debit Detail           [⋮]   │  TopAppBar, surface, Outfit Medium 18sp
├─────────────────────────────────────────┤
│                                         │
│  ┌───────────────────────────────────┐  │
│  │  Thames Water Utilities Ltd       │  │  titleLarge Outfit 22sp, onSurface
│  │  ┌──────────┐          £ 48.50   │  │  status chip (left) + amount (right)
│  │  │ ● Active │          GBP       │  │  chip: #4C662B fill, white text 12sp
│  └───────────────────────────────────┘  │  card elevation 1dp, cornerRadius 12dp
│                                         │  16dp horizontal margin
│  ─────────────────────────────────────  │  divider
│                                         │
│  Frequency          Monthly            │  labelMedium / bodyMedium, 56dp row
│  Start Date         15 Jan 2024        │  labelMedium / bodyMedium, 56dp row
│  Next Payment       15 Jun 2026        │  labelMedium / bodyMedium, 56dp row
│  Reference          WATER-ACC-TW-99102 │  labelMedium / bodyMedium, 56dp row
│                                         │
│  ─────────────────────────────────────  │  divider
│                                         │
│  Recent Payments                        │  titleSmall Outfit SemiBold, #4C662B
│                                         │
│  ┌─────────────────────────────────┐   │
│  │  15 May 2026    £48.50   ✓      │   │  payment row: date + amount + status dot
│  ├─────────────────────────────────┤   │  ✓ completed = #4C662B
│  │  15 Apr 2026    £48.50   ✓      │   │  ✗ failed = #BA1A1A
│  ├─────────────────────────────────┤   │  ○ pending = #757575
│  │  15 Mar 2026    £48.50   ✓      │   │
│  └─────────────────────────────────┘   │  list card, 12dp corner, 16dp margin
│                                         │
│  ┌───────────────────────────────────┐  │
│  │      Cancel Direct Debit          │  │  OutlinedButton, border #BA1A1A
│  └───────────────────────────────────┘  │  text #BA1A1A, Outfit Medium, 16dp margin
│                                         │  visible only when status = active/pending
└─────────────────────────────────────────┘
```

### Cancel Confirmation Dialog (overlay on content)

```
┌─────────────────────────────────────────┐
│  ████████████████████████████████████   │  scrim 54% black
│  █                                  █   │
│  █  ┌──────────────────────────┐   █   │
│  █  │  Cancel Direct Debit?    │   █   │  AlertDialog
│  █  │                          │   █   │  titleLarge Outfit 20sp
│  █  │  This will permanently   │   █   │
│  █  │  cancel your standing    │   █   │  bodyMedium 14sp onSurfaceVariant
│  █  │  order with Thames       │   █   │
│  █  │  Water Utilities Ltd.    │   █   │
│  █  │                          │   █   │
│  █  │  [Dismiss]  [Cancel DD]  │   █   │  text buttons: Dismiss (neutral)
│  █  └──────────────────────────┘   █   │  Cancel DD: #BA1A1A destructive
│  ████████████████████████████████████   │
└─────────────────────────────────────────┘
```

---

## State: error

```
┌─────────────────────────────────────────┐
│ ←  Direct Debit Detail                  │  TopAppBar
├─────────────────────────────────────────┤
│                                         │
│              [!] icon                   │  error_outline 64dp, #BA1A1A
│                                         │
│      Something went wrong               │  titleMedium Outfit, center
│                                         │
│  We couldn't load the mandate detail.   │  bodyMedium, center, onSurfaceVariant
│  Please check your connection           │
│  and try again.                         │
│                                         │
│       ┌──────────────────┐              │
│       │      Retry       │              │  FilledButton #4C662B
│       └──────────────────┘              │
│                                         │
└─────────────────────────────────────────┘
404 variant: icon = search_off, text = "Mandate not found", no Retry button
```

---

## State: empty

```
┌─────────────────────────────────────────┐
│ ←  Direct Debit Detail                  │  TopAppBar
├─────────────────────────────────────────┤
│                                         │
│        [illustration]                   │  empty_inbox 96dp SVG, #4C662B tint
│                                         │
│      No Mandate Found                   │  titleMedium Outfit, center
│                                         │
│  This direct debit no longer exists     │  bodyMedium, center, onSurfaceVariant
│  or may have been removed.              │
│                                         │
└─────────────────────────────────────────┘
```

---

## Design Tokens

| Token | Value | Usage |
|---|---|---|
| accent | #4C662B | Buttons, status chip, section headers, active status |
| error | #BA1A1A | Cancel button, failed payments, error state |
| surface | #FFFBFF | Card backgrounds |
| onSurfaceVariant | #44483E | Secondary text, meta labels |
| outlineVariant | #C3C8BC | Dividers, card outlines |
| typography-title | Outfit SemiBold | Screen title, card counterparty name |
| typography-body | Outfit Regular | Meta values, payment rows |
| typography-label | Outfit Medium | Meta field labels, chip text |
| card-corner-radius | 12dp | All cards |
| card-elevation | 1dp | MandateHeaderCard |
| horizontal-margin | 16dp | All content |
| row-height | 56dp | Meta section rows |

---

## Figma Layer Naming

```
direct-debit-detail/
  states/
    loading/
      TopAppBar
      MandateHeaderCard_skeleton
      MetaSection_skeleton
      RecentPayments_skeleton
    content/
      TopAppBar
      MandateHeaderCard
        counterparty_name
        status_chip
        amount_label
      MandateMetaSection
        row_frequency
        row_start_date
        row_next_payment
        row_reference
      RecentPaymentsList
        PaymentRow × n
      CancelMandateButton
    content_dialog/
      [content layers]
      CancelConfirmDialog
        dialog_title
        dialog_body
        btn_dismiss
        btn_confirm_cancel
    error/
      TopAppBar
      ErrorState
        error_icon
        error_title
        error_body
        btn_retry
    empty/
      TopAppBar
      EmptyState
        empty_illustration
        empty_title
        empty_body
```
