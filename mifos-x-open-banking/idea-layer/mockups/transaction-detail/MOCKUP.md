# Visual Specification — Transaction Detail
**Feature:** transaction-detail | **Flavor:** consumer

---

## Screen Layout

Vertical scroll with top app bar ("Transaction Details" + back + share); no bottom navigation:

```
┌────────────────────────────────────┐
│ ← Transaction Details        [↗]  │  ← top app bar
├────────────────────────────────────┤
│                                    │
│           -£42.50                  │  ← amount_hero_section (bg #1800B1)
│        ✓ Completed                 │  ← status_badge (green pill)
│                                    │
├────────────────────────────────────┤
│ ┌──────────────────────────────┐   │
│ │ [Tesco Logo] Tesco Supermarket│  │  ← merchant_card (elevation 4,
│ │             [Groceries]       │  │    margin_top -20 overlap)
│ └──────────────────────────────┘   │
│                                    │
│ ┌──────────────────────────────┐   │
│ │ Date & Time    25 May 2026, 14:32│ ← details_card
│ │──────────────────────────────│   │
│ │ Reference      SEPA-202605.. [⎘]│
│ │──────────────────────────────│   │
│ │ Transaction Type  SEPA Credit Transfer │
│ │──────────────────────────────│   │
│ │ From Account   Primary Checking │ │
│ │                ...0130          │ │
│ │──────────────────────────────│   │
│ │ To Beneficiary    Tesco PLC     │ │
│ │                DE89 3704...0044 │ │
│ └──────────────────────────────┘   │
│                                    │
│ [Download Receipt]                 │  ← outlined button #1800B1
│      🚩 Report an Issue            │  ← #FF5252 link
└────────────────────────────────────┘
```

---

## Components

### amount_hero_section — Hero
- **Background:** #1800B1, full width, padding h/v: 24/28 top, 36 bottom, align: center
- **amount_hero_value:** "-£42.50" — typography: display_large, color: #FF8A80 (soft red on dark for contrast), font_weight: 700, text_align: center
- **status_badge_row:** centered horizontally below amount
  - Pill: background #4CAF5033 (20% green), border_radius 20, padding h/v 16/6
  - Inner row: check_circle icon (14px, #69F0AE) + "Completed" text (label_medium, #69F0AE)

### merchant_card
- **Position:** margin_horizontal 20, margin_top -20 (overlaps hero), margin_bottom 16
- **Style:** background #FFFFFF, border_radius 20, padding 20, elevation 4
- **merchant_row (horizontal, spacing 16):**
  - **merchant_logo:** 56×56 circle, background #E8F5E9, border_radius 28 — Tesco logo image
  - **merchant_info (vertical, flex 1):**
    - "Tesco Supermarket" — title_large, #1A1A1A, weight 600
    - category_badge: "Groceries" chip — background #E8F5E9, border_radius 6, padding h/v 8/4, text label_small, color #2E7D32, align_self flex_start, margin_top 4

### details_card
- **Style:** background #FFFFFF, border_radius 16, padding 20, margin_horizontal 20, elevation 1
- **Each field row:** horizontal layout, space-between, padding_bottom 16 (except last row)
- **Between each row:** #F0F0F0 divider, margin_bottom 16
- **Label style:** label_small, #666666, letter_spacing 0.4
- **Value style:** body_medium, #1A1A1A, weight 500

| Row | Label | Value |
|---|---|---|
| detail_date_row | "Date & Time" | "25 May 2026, 14:32" |
| detail_reference_row | "Reference" | "SEPA-2026051500123" (monospace, body_small) + copy icon |
| detail_type_row | "Transaction Type" | "SEPA Credit Transfer" |
| detail_from_row | "From Account" | "Primary Checking" (weight 500) + "...0130" (body_small, #888888, monospace) |
| detail_to_row | "To Beneficiary" | "Tesco PLC" (weight 500) + "DE89 3704...0044" (body_small, #888888, monospace) |

### download_receipt_button
- **Style:** variant=outlined, border_color #1800B1, text_color #1800B1, border_radius 12
- **Padding:** vertical 14, margin_horizontal 20, margin_bottom 12
- **Label:** "Download Receipt", typography label_large
- **Leading icon:** download

### report_issue_row
- **Layout:** horizontal, centered, padding_bottom 24
- **flag icon:** 16px, #FF5252, padding_right 6
- **"Report an Issue" link:** label_medium, #FF5252 — taps open dispute form

---

## Interaction Patterns

| Target | Gesture | Outcome |
|---|---|---|
| Top app bar back | Tap | NavigateBack event → pop to transactions |
| Top app bar share icon | Tap | ShareTransaction event → system share sheet |
| copy_reference_icon | Tap | CopyReference event; referenceCopied=true (brief snackbar "Copied") |
| download_receipt_button | Tap | DownloadReceipt event; isDownloadingReceipt=true → PDF download progress |
| report_issue_link | Tap | OpenDisputeForm event → dispute form screen / bottom sheet |

---

## Content Data

| Element | Value |
|---|---|
| Transaction amount | -£42.50 |
| Status | Completed |
| Merchant | Tesco Supermarket |
| Category | Groceries |
| Date & Time | 25 May 2026, 14:32 |
| Reference | SEPA-2026051500123 |
| Transaction type | SEPA Credit Transfer |
| From account | Primary Checking (IBAN: ...0130) |
| To beneficiary | Tesco PLC (IBAN: DE89 3704...0044) |

---

## Design Notes

- **Amount color on hero:** #FF8A80 (a lighter red) is used instead of #FF5252 on the #1800B1 dark background to meet WCAG AA contrast (ratio ~4.8:1 vs ~3.1:1 for the darker red).
- **Hero overlap pattern:** merchant_card uses margin_top -20 to float above the hero bottom edge — the elevation 4 shadow makes it feel physically lifted off the hero. This is the same technique used on account-detail for visual continuity across the banking flow.
- **Status badge:** Translucent green (#4CAF5033) pill with #69F0AE (Material Design "tertiary" on dark) gives a "payment cleared" signal without harsh full-saturation green on the brand purple.
- **Reference monospace:** SEPA-2026051500123 displayed in monospace body_small allows digit grouping to read as a code, distinct from prose text.
- **Masked IBANs:** Source shows "...0130" (last 4 chars), destination shows "DE89 3704...0044" — partial disclosure protects counterparty privacy while giving enough context for recognition.
- **No bottom nav:** This is a leaf screen — removing the nav bar maximises vertical space for the structured details and signals there is no lateral navigation from this context.
- **Loading skeleton:** Hero stays purple (background persists); merchant card and details card replaced by grey blocks to prevent layout jump on data arrival.

---

_Generated by /idea export | 2026-05-25_
