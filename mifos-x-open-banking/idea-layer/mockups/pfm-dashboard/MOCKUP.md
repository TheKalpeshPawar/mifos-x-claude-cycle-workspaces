# Visual Specification — Spending Insights (PFM Dashboard)

| Field | Value |
|---|---|
| Feature | pfm-dashboard |
| Flavor | consumer |
| Archetype | dashboard |
| Status | designed |

---

## Screen Layout

Top app bar: "Spending Insights" title, back arrow (left), tune icon (right). Bottom navigation: Home | Accounts | **Insights** (active, #1800B1) | Cards | More. Page background: #FCF8FF (very light lavender). Main content is a vertically scrollable column:

```
┌─────────────────────────────────────┐
│ ← Spending Insights           [⚙]  │  ← Top app bar
├─────────────────────────────────────┤
│  Spending Insights                   │  headline_large #1800B1 bold
│                                     │
│  [This Month] [Last Month] [Last 3] │  ← Period chip row (horizontal scroll)
│  [Custom]                           │
│  May 2026                           │  body_medium #888888
│                                     │
│  ┌───────────────────────────────┐  │
│  │ This Month              >     │  │  ← Summary card (white, radius 20)
│  │ Total Spent  Total Rec.  Net  │  │
│  │ £1,029.80   £3,200.00  +£2,170│  │
│  │  (red)       (green)   (indigo)│  │
│  └───────────────────────────────┘  │
│                                     │
│  ┌───────────────────────────────┐  │
│  │ Monthly Budget       68% used │  │  ← Overall budget card (#F8F4FF bg)
│  │ £1,029.80 spent    £470.20 left│  │
│  │ ████████████████░░░░░░░░░░░░  │  │  amber fill 68%
│  │ of £1,500.00 monthly budget   │  │
│  └───────────────────────────────┘  │
│                                     │
│  Spending by Category               │  title_medium semi-bold
│  ┌───────────────────────────────┐  │
│  │         [Pie chart]           │  │  ← 220dp chart card (white, radius 20)
│  │  ● Bills 43.7%                │  │
│  │  ● Food & Dining 31.1%        │  │
│  │  ● Transport 12.1%            │  │
│  │  ● Shopping 8.7%              │  │
│  │  ● Entertainment 4.4%         │  │
│  └───────────────────────────────┘  │
│  ● Food & Dining           £320.50  │  ← Legend rows (tappable → transactions)
│  ● Transport               £125.00  │
│  ● Shopping                 £89.30  │
│  ● Bills                   £450.00  │
│  ● Entertainment             £45.00  │
│                                     │
│  Budget Progress                    │  title_medium semi-bold
│  ┌────────────────────────────────┐ │
│  │ Food & Dining    £320.50/£350  │ │  ← Budget card (white, radius 16)
│  │ ██████████████████████████░░  │ │  red 92%
│  └────────────────────────────────┘ │
│  ┌────────────────────────────────┐ │
│  │ Transport        £125.00/£200  │ │
│  │ ████████████░░░░░░░░░░░░░░░░  │ │  amber 63%
│  └────────────────────────────────┘ │
│  ┌────────────────────────────────┐ │
│  │ Shopping          £89.30/£150  │ │
│  │ ███████████░░░░░░░░░░░░░░░░░  │ │  amber 60%
│  └────────────────────────────────┘ │
│  ┌────────────────────────────────┐ │
│  │ Bills            £450.00/£500  │ │
│  │ █████████████████████████░░░  │ │  red 90%
│  └────────────────────────────────┘ │
│  ┌────────────────────────────────┐ │
│  │ Entertainment     £45.00/£100  │ │
│  │ ████████░░░░░░░░░░░░░░░░░░░░  │ │  green 45%
│  └────────────────────────────────┘ │
│       [Manage Budgets]              │  outlined button, centered
│                                     │
│  Top Merchants                      │  title_medium semi-bold
│  ┌────────────────────────────────┐ │
│  │ [🏪] Tesco           £142.30   │ │  storefront icon, 8 transactions
│  │      8 transactions            │ │
│  ├────────────────────────────────┤ │
│  │ [🚇] Transport for London £78  │ │  subway icon, 23 transactions
│  │      23 transactions           │ │
│  ├────────────────────────────────┤ │
│  │ [▶] Netflix            £17.99  │ │  play_circle icon (red)
│  │     1 transaction              │ │
│  ├────────────────────────────────┤ │
│  │ [♪] Spotify            £11.99  │ │  music_note icon (green)
│  │     1 transaction              │ │
│  └────────────────────────────────┘ │
│       [View All Transactions]       │  text button, centered, #1800B1
├─────────────────────────────────────┤
│  Home  Accounts  Insights  Cards  More │  ← Bottom nav
└─────────────────────────────────────┘
```

---

## Period Chip Selector

**Position:** Below page title, horizontally scrollable row (padding H20, spacing 8).

| Chip | Default State | Color When Selected | Color When Unselected |
|---|---|---|---|
| This Month | Selected | bg #1800B1, text #FFFFFF | bg #F0EDFF, text #1800B1 |
| Last Month | Unselected | bg #1800B1, text #FFFFFF | bg #F0EDFF, text #1800B1 |
| Last 3 Months | Unselected | bg #1800B1, text #FFFFFF | bg #F0EDFF, text #1800B1 |
| Custom | Unselected | bg #1800B1, text #FFFFFF | bg #F0EDFF, text #1800B1 |

All chips: corner_radius 20, padding H16 V8, typography label_medium. "Custom" tap → date range picker bottom sheet.

---

## Overall Budget Progress Card

**Style:** bg #F8F4FF (lavender), border #E8E0FF 1dp, radius 20, elevation 1, padding H20 V18, margin H20 B20.

**Header row:**
- Left: "Monthly Budget" title_small semi-bold #1800B1
- Right: "68% used" label_medium semi-bold #FF9800

**Amounts row:**
- Left: "£1,029.80 spent" body_medium semi-bold #111111
- Right: "£470.20 left" body_medium semi-bold #4CAF50

**Progress bar:**
- Track: bg #E0E0E0, height 10dp, radius 6, full width
- Fill: bg #FF9800 (amber — approaching threshold), width 68%, height 10dp, radius 6

**Footer:** "of £1,500.00 monthly budget" label_small #888888

**Interaction:** Tap anywhere → manage_budgets bottom sheet

---

## Category Breakdown

### Pie Chart Card

**Style:** white bg, radius 20, elevation 2, height 220dp, padding H16 V16, margin H20. Tap → full-screen chart modal.

Pie segments (clockwise from top):
- Bills — #1800B1 — 43.7%
- Food & Dining — #FF6B6B — 31.1%
- Transport — #4ECDC4 — 12.1%
- Shopping — #A8E6CF — 8.7%
- Entertainment — #FFD93D — 4.4%

### Category Legend Rows

Each row: horizontal stack, space_between, padding V6. Tap row → filter_by_category → transactions.

| Row | Dot Color | Label | Amount |
|---|---|---|---|
| Food & Dining | #FF6B6B | "Food & Dining" | £320.50 |
| Transport | #4ECDC4 | "Transport" | £125.00 |
| Shopping | #A8E6CF | "Shopping" | £89.30 |
| Bills | #1800B1 | "Bills" | £450.00 |
| Entertainment | #FFD93D | "Entertainment" | £45.00 |

Dot size: 12x12dp, radius 6. Amount: body_medium semi-bold #111111.

---

## Per-Category Budget Cards

**Card style:** white bg, radius 16, elevation 1, border #F0F0F0 1dp, padding H16 V14, margin H20 B10. Tap → edit_budget bottom sheet.

**Header row:** category name (body_medium semi-bold #111111) | spent/limit amount (body_medium, colored).
**Progress bar:** height 8dp, radius 4.

### Budget Progress Colors

| Utilisation | Fill Color | Amount Color | Status |
|---|---|---|---|
| ≥ 90% | #FF5252 | #FF5252 semi-bold | Critical — at limit |
| 60–89% | #FF9800 | #555555 | Approaching |
| < 60% | #4CAF50 | #555555 | Healthy |

### Food & Dining (92% — Critical)
- Header: "Food & Dining" | "£320.50 / £350.00" #FF5252 semi-bold
- Progress: #FF5252 fill, width 92%

### Transport (63% — Approaching)
- Header: "Transport" | "£125.00 / £200.00" #555555
- Progress: #FF9800 fill, width 63%

### Shopping (60% — Approaching)
- Header: "Shopping" | "£89.30 / £150.00" #555555
- Progress: #FF9800 fill, width 60%

### Bills (90% — Critical)
- Header: "Bills" | "£450.00 / £500.00" #FF5252 semi-bold
- Progress: #FF5252 fill, width 90%

### Entertainment (45% — Healthy)
- Header: "Entertainment" | "£45.00 / £100.00" #555555
- Progress: #4CAF50 fill, width 45%

### Manage Budgets Button
- Outlined variant, border #1800B1, text #1800B1, radius 12, label_large
- align_self center, margin H20, top 8, bottom 24
- Tap → manage_budgets bottom sheet

---

## Top Merchants

**Card style:** white bg, radius 20, elevation 2, border #F0F0F0 1dp, padding H16 V8, margin H20 B24.

Each merchant row: list_item with leading icon (40dp circle background), merchant name + transaction count sub-label, amount right-aligned. Tap → view_merchant_transactions → transactions. Divider between rows (none on last).

| Merchant | Icon | Icon Color | Icon Bg | Amount | Transactions |
|---|---|---|---|---|---|
| Tesco | storefront | #1800B1 | #F0EDFF | £142.30 | 8 transactions |
| Transport for London | directions_subway | #003688 | #E8EDFF | £78.50 | 23 transactions |
| Netflix | play_circle | #E50914 | #FFF0F0 | £17.99 | 1 transaction |
| Spotify | music_note | #1DB954 | #F0FFF4 | £11.99 | 1 transaction |

**View All Transactions button:** text variant, #1800B1, label_large, centered, padding V12, margin B32. Tap → navigate_to_transactions.

---

## State Descriptions

### loading

Visible: page title, period chip row (chips inert), period label. Below: 5 skeleton cards (rounded, shimmer animation, height 120dp each, margin H20, spacing 12dp).

```
Spending Insights
[This Month] [Last Month] [Last 3 Months] [Custom]
May 2026
▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓  (skeleton 1)
▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓  (skeleton 2)
▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓  (skeleton 3)
▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓  (skeleton 4)
▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓  (skeleton 5)
```

### populated

Full dashboard as per layout above. All sections visible: summary card, overall budget, category chart + legend, per-category budgets, top merchants.

### empty

Visible: page title, period chips. Full-screen empty state below chips:

```
Spending Insights
[This Month] [Last Month] [Last 3 Months] [Custom]
May 2026

         [receipt_long icon, 64dp, #CCCCCC]
    No transaction history yet
    Your spending insights will appear
    once you have transactions in the
       selected period.

           [View Accounts]         ← tonal button
```

- Icon: `receipt_long` 64dp #CCCCCC
- Title: title_medium semi-bold #111111
- Body: body_medium #888888, centered, padding H32
- CTA: "View Accounts" → navigate_to_accounts

### no_budget_set

Visible: summary card + category chart/legend (transactions exist, so spending data is shown). Budget progress section replaced by amber banner:

```
┌─────────────────────────────────────┐
│  No budget set                       │  title_small semi-bold #E65100
│  Set a monthly budget to track how  │  body_small #BF360C
│  much you spend against your target.│
│                                     │
│         [Set Budget Now]            │  filled #1800B1
└─────────────────────────────────────┘
```

Banner: bg #FFF8E1, border #FFE082 1dp, radius 16, padding H20 V16, margin H20 B16. Tap banner → manage_budgets.

Top merchants section still visible below banner.

---

## Interaction Summary

| Component | Gesture | Result |
|---|---|---|
| period_chip_this_month | Tap | select_period action → reload data |
| period_chip_last_month | Tap | select_period action → reload data |
| period_chip_last_3_months | Tap | select_period action → reload data |
| period_chip_custom | Tap | open_custom_date_picker → date picker sheet |
| this_month_summary_card | Tap | navigate_to_transactions |
| overall_budget_card | Tap | manage_budgets bottom sheet |
| category_pie_chart | Tap | open_chart_detail full-screen modal |
| category_row_* | Tap | filter_by_category → transactions with category filter |
| budget_food_dining | Tap | edit_budget bottom sheet (Food & Dining) |
| budget_transport | Tap | edit_budget bottom sheet (Transport) |
| budget_shopping | Tap | edit_budget bottom sheet (Shopping) |
| budget_bills | Tap | edit_budget bottom sheet (Bills) |
| budget_entertainment | Tap | edit_budget bottom sheet (Entertainment) |
| manage_budgets_button | Tap | manage_budgets bottom sheet |
| merchant_row_tesco | Tap | view_merchant_transactions → transactions |
| merchant_row_tfl | Tap | view_merchant_transactions → transactions |
| merchant_row_netflix | Tap | view_merchant_transactions → transactions |
| merchant_row_spotify | Tap | view_merchant_transactions → transactions |
| view_all_transactions_button | Tap | navigate_to_transactions |
| top app bar back | Tap | navigate_back → home |
| top app bar tune | Tap | open_pfm_settings |

---

## Design Notes

**Progress bar traffic-light system:** Fill colour signals urgency without text — green (< 60%) is calm, amber (60–89%) prompts attention, red (≥ 90%) demands action. The overall budget bar is fixed amber at 68% to distinguish it from per-category bars.

**Summary card amount hierarchy:** title_large bold ensures £ amounts read at a glance. Labels (label_small with letter_spacing 0.4) recede visually. Spent (red) vs. Received (green) creates immediate income/outflow distinction without iconography.

**Overall budget card lavender background (#F8F4FF):** Visually separates the aggregated budget view from per-category cards below. The indigo primary border (#E8E0FF) ties it to the brand colour without heavy saturation.

**Merchant icon circles:** 40dp background circles use a desaturated tint of each brand's colour — Tesco (indigo #F0EDFF), Netflix (rose #FFF0F0), Spotify (mint #F0FFF4), TfL (sky #E8EDFF) — providing brand recognition without literal logos.

**no_budget_set amber banner:** Uses Material Design warning semantics (#FFF8E1 bg, #FFE082 border, #E65100 title, #BF360C body) — alerts without alarming. The "Set Budget Now" CTA in primary indigo provides clear resolution.

*Generated by /idea export | 2026-05-25*
