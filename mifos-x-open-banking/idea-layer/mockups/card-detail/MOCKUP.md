# Card Detail — Visual Specification

| Field | Value |
|---|---|
| Feature | card-detail |
| Flavor | consumer |
| Archetype | detail_screen |

---

## Screen Layout

Top-to-bottom hierarchy on a vertically scrolling detail screen:

```
[ Top App Bar: "Card Details"  ←  ⋮  ]  ← back + more_vert overflow
───────────────────────────────────────
┌────────────────────────────────────┐
│ Mifos Debit Visa           VISA   │  ← gradient #1800B1→#4B35E8
│                                    │     340×210dp, elevation 12
│ ●●●● ●●●● ●●●● 4521               │  ← white monospace, letter-spacing 4
│ ALEX JOHNSON               09/29  │  ← #E0DDFF uppercase | #C5BFFF expiry
└────────────────────────────────────┘  ← corner radius 20dp, auto-centered
       [ Show card details ]            ← underlined link, #1800B1, centered
───────────────────────────────────────
┌──────────────────────────────────────┐
│  Card Active                    ●─  │  ← white surface, elevation 1, r=12dp
└──────────────────────────────────────┘  ← switch: green #4CAF50 on
┌──────────────────────────────────────┐
│  Spending Limits                     │  ← white surface, elevation 1
│  ─────────────────────────────────  │
│  Daily limit          £2,500   ✏️   │  ← body_medium label | body_large value
│  ─────────────────────────────────  │
│  Monthly limit        £10,000  ✏️   │
└──────────────────────────────────────┘
[ ❄️  Freeze Card      (outlined orange) ]  ← #FF9800 border+text, full-width
[ ⚠️  Report Lost/Stolen (outlined red) ]  ← #FF5252 border+text, full-width
[ 🧾  View Transactions  (text #1800B1) ]  ← full-width, receipt_long icon
───────────────────────────────────────
```

---

## Components

### card_visual
- Dimensions: 340dp wide × 210dp tall
- Gradient: diagonal, start `#1800B1`, end `#4B35E8`
- Corner radius: 20dp, elevation: 12 (prominent shadow)
- Padding: 24dp all sides
- Horizontal margin: auto-centered
- Margin top: 8dp from top bar, margin bottom: 24dp

### card_number_display
- Content: "•••• •••• •••• 4521"
- Typography: `title_large`, color `#FFFFFF`
- Font family: monospace, letter-spacing: 4
- Positioned over card visual, middle area

### cardholder_name
- Content: "ALEX JOHNSON"
- Typography: `body_large`, color `#E0DDFF`, text_transform uppercase
- Letter spacing: 1, bottom-left of card visual

### card_expiry
- Content: "09/29"
- Typography: `body_medium`, color `#C5BFFF`, monospace
- Bottom-right of card visual, below network logo

### reveal_card_details_link
- Content: "Show card details"
- Typography: `label_large`, color `#1800B1`, underline decoration
- Text align: center, padding vertical: 4dp
- Triggers biometric prompt before revealing full PAN/CVV

### card_status_row
- Horizontal stack, `space_between`, background `#FFFFFF`, elevation 1
- Corner radius 12dp, padding: 16dp vertical, 20dp horizontal
- "Card Active" label: `body_large`, `#111111`, medium weight
- Switch: checked color `#4CAF50`, unchecked color `#9E9E9E`

### limits_section
- Background `#FFFFFF`, corner radius 12dp, elevation 1
- Border: `#F0F0F0`, 1dp
- Padding: 20dp horizontal, 16dp vertical, margin top 12dp

### limits rows (daily_limit_row, monthly_limit_row)
- Horizontal stack, `space_between`, align center
- Label: `body_medium`, `#888888` — "Daily limit" / "Monthly limit"
- Value: `body_large`, `#111111`, medium weight — "£2,500" / "£10,000"
- Edit icon: `edit`, 20dp, `#1800B1` — tapping opens edit limit sheet
- Divider between rows: `#F0F0F0`, 1dp

### freeze_card_button
- Variant: outlined, full-width
- Border + text: `#FF9800` (amber — caution without alarm)
- Leading icon: `ac_unit` (snowflake)
- Corner radius 12dp, padding vertical 14dp

### report_lost_button
- Variant: outlined, full-width
- Border + text: `#FF5252` (red — irreversible danger signal)
- Leading icon: `report_problem`
- Corner radius 12dp, padding vertical 14dp

### view_transactions_button
- Variant: text, full-width
- Text color: `#1800B1`, leading icon: `receipt_long`
- Typography: `label_large`, padding vertical 12dp

---

## Interaction Patterns

| Interaction | Component | Result |
|---|---|---|
| Tap "Show card details" | reveal_card_details_link | Biometric prompt → reveals PAN/CVV for 30s |
| Toggle switch ON→OFF | card_status_switch | Card deactivated, state → frozen |
| Toggle switch OFF→ON | card_status_switch | Card reactivated, state → content |
| Tap "£2,500" row | daily_limit_row | Opens daily limit edit bottom sheet |
| Tap "£10,000" row | monthly_limit_row | Opens monthly limit edit bottom sheet |
| Tap "Freeze Card" | freeze_card_button | Confirmation dialog → freeze API → frozen state |
| Tap "Report Lost/Stolen" | report_lost_button | Confirmation dialog → hot-list API → card permanently blocked |
| Tap "View Transactions" | view_transactions_button | Navigate to transactions screen filtered by this card |
| Tap overflow "⋮" | more_vert top bar | Opens card options menu |

---

## Content Data

| Element | Value |
|---|---|
| Card PAN (masked) | •••• •••• •••• 4521 |
| Cardholder | ALEX JOHNSON |
| Expiry | 09/29 |
| Card type | Mifos Debit Visa |
| Card network | VISA |
| Card status | Active (switch on, green) |
| Daily limit | £2,500 |
| Monthly limit | £10,000 |

---

## Design Notes

**Frozen state visual diff:** When `isFrozen: true`, the card_visual gets a 50%-opacity grey overlay with "FROZEN" watermark text. The switch flips off (grey). Freeze button re-labels to "Unfreeze Card" with `lock_open` icon and green (#4CAF50) border/text. The "Show card details" link is hidden — frozen cards cannot be revealed.

**Destructive action gradient:** Three buttons at screen bottom use intentional severity escalation: text (View Transactions, neutral) → outlined amber (Freeze, reversible warning) → outlined red (Report Lost, irreversible). Visual weight guides users toward the correct action level.

**Edit pencil icon on limit rows:** Inline edit affordance using MD3 `edit` icon in primary color. The entire row is tappable (not just the icon), with 10dp vertical padding for 44dp+ touch target.

**Elevation hierarchy:** card_visual (elevation 12) > payment_summary_card on other screens (elevation 2) > limits section (elevation 1). This places the card image as the most prominent element, consistent with physical wallet UX paradigm.

**Biometric reveal timer:** 30-second auto-mask after reveal. The `isRevealed: Boolean` field controls masking — never stored in persistent state.

*Generated by /idea export | 2026-05-25*
