# Visual Specification — Transaction History
**Feature:** transactions | **Flavor:** consumer

---

## Screen Layout

Vertical scroll with top app bar ("Transactions" + back + filter_list action icon):

```
┌────────────────────────────────────┐
│ ← Transactions               [≡]  │  ← top app bar
├────────────────────────────────────┤
│ 🔍 Search by merchant, amount, date│  ← search_bar (bg #F5F5F5)
├────────────────────────────────────┤
│ 📅 Last 30 Days              ▼     │  ← date_range_picker
├────────────────────────────────────┤
│ [All] [Debit] [Credit] [Pending]   │  ← filter_chips_row
├────────────────────────────────────┤
│ ┌──────────────────────────────┐   │
│ │  Spent this month │ Received │   │  ← monthly_summary_card (#F8F4FF)
│ │  £1,240.30        │ £3,200.00│   │
│ └──────────────────────────────┘   │
├────────────────────────────────────┤
│  25 May 2026                       │  ← transactions_date_group_header
│ ┌──────────────────────────────┐   │
│ │ [T] Tesco Supermarket        │   │
│ │     25 May 2026 · [Groceries]│  -£42.50 │  ← txn_list_row_1
│ └──────────────────────────────┘   │
│  24 May 2026                       │
│ ┌──────────────────────────────┐   │
│ │ [💰] Salary Payment          │   │
│ │     24 May 2026 · [Income]   │ +£3,200.00 │  ← txn_list_row_2
│ └──────────────────────────────┘   │
│  23 May 2026                       │
│ ┌──────────────────────────────┐   │
│ │ [E] EDF Energy               │   │
│ │     23 May 2026 · [Utilities]│  -£94.20 │  ← txn_list_row_3
│ └──────────────────────────────┘   │
│        Load More Transactions      │  ← load_more_button
├────────────────────────────────────┤
│  [Home] [Accounts*] [Pay] [Cards] [More] │
└────────────────────────────────────┘
```

---

## Components

### search_bar
- **Style:** variant=search, background: #F5F5F5, border_radius: 12
- **Padding:** horizontal 16, vertical 12; margin_horizontal 20, margin_top 16
- **Leading icon:** search (24px, #666666)
- **Trailing icon:** mic (24px, #666666)
- **Placeholder:** "Search by merchant, amount, date..." — #888888

### date_range_picker
- **Style:** background: #F5F5F5, border_radius: 12, padding h/v 16/12, margin_horizontal 20
- **Row layout:** horizontal, space-between
- **Left:** date_range icon (18px, #1800B1) + "Last 30 Days" text (body_medium, #1A1A1A)
- **Right:** expand_more icon (20px, #666666)
- Entire component is tappable (opens date range dialog)

### filter_chips_row
- **Horizontal scroll, spacing 8, padding_horizontal 20**
- **Active chip (All):** filled, background #1800B1, text #FFFFFF, border_radius 20, padding h/v 16/8
- **Inactive chips (Debit, Credit, Pending):** outlined, border #CCCCCC, text #666666, same radius/padding
- Role: radio group (a11y)

### monthly_summary_card
- **Background:** #F8F4FF (light purple tint), border_radius 16, padding 16, margin_horizontal 20
- **Two columns separated by 1px×40px vertical divider (#DDDDDD):**
  - **Left (spent_col):** "Spent this month" label (label_small, #666666, letter_spacing 0.4) above "£1,240.30" (title_large, #FF5252, weight 700)
  - **Right (received_col):** "Received" label above "£3,200.00" (title_large, #4CAF50, weight 700)

### transactions_date_group_header
- **"25 May 2026"** — label_medium, #666666, letter_spacing 0.5, padding_horizontal 20

### Transaction Row (txn_list_row_1 — Tesco Supermarket)
- **Background:** #FFFFFF, border_radius 12, padding 14, margin_horizontal 20, elevation 1
- **Layout:** horizontal, align center, spacing 12
- **Merchant logo:** 40×40 circle, background #E8F5E9 (Tesco green tint)
- **Info stack (flex 1):**
  - "Tesco Supermarket" — body_medium, #1A1A1A, weight 500
  - Meta row: "25 May 2026" (body_small, #888888) + "·" separator + "Groceries" badge (#E8F5E9 bg, #2E7D32 text, label_small)
- **Amount:** "-£42.50" — body_large, #FF5252, weight 600

### Transaction Row (txn_list_row_2 — Salary Payment)
- **Merchant logo:** 40×40 circle, background #E8F5E9
- **Name:** "Salary Payment", **Date:** "24 May 2026"
- **Category badge:** "Income" — #E8F5E9 bg, #2E7D32 text
- **Amount:** "+£3,200.00" — body_large, #4CAF50, weight 600

### Transaction Row (txn_list_row_3 — EDF Energy)
- **Merchant logo:** 40×40 circle, background #FFF3E0 (orange tint)
- **Name:** "EDF Energy", **Date:** "23 May 2026"
- **Category badge:** "Utilities" — #FFF3E0 bg, #E65100 text
- **Amount:** "-£94.20" — body_large, #FF5252, weight 600

### load_more_button
- **Variant:** text, text_color #1800B1, typography label_medium
- **Alignment:** center (align_self: center), padding_vertical 16

---

## Interaction Patterns

| Target | Gesture | Outcome |
|---|---|---|
| search_bar | Tap / type | isSearching=true; skeleton rows during search; results replace list |
| date_range_picker | Tap | Opens date range dialog; DateRangeChanged event on confirm |
| filter_all | Tap | activeFilter=ALL; all transactions shown |
| filter_debit | Tap | activeFilter=DEBIT; re-fetches with type=DEBIT |
| filter_credit | Tap | activeFilter=CREDIT; re-fetches with type=CREDIT |
| filter_pending | Tap | activeFilter=PENDING; re-fetches with type=PENDING |
| txn_list_row_1 | Tap | Navigate → /transactions/txn_20260525_001 |
| txn_list_row_2 | Tap | Navigate → /transactions/txn_20260524_001 |
| txn_list_row_3 | Tap | Navigate → /transactions/txn_20260523_001 |
| load_more_button | Tap | LoadMore event; currentPage++ ; appends next 20 transactions |
| Top app bar filter icon | Tap | open_advanced_filter (date + type sheet) |

---

## Content Data

| Element | Value |
|---|---|
| Date range | Last 30 Days |
| Spent this month | £1,240.30 |
| Received this month | £3,200.00 |
| Txn 1 | Tesco Supermarket / Groceries / -£42.50 / 25 May 2026 |
| Txn 2 | Salary Payment / Income / +£3,200.00 / 24 May 2026 |
| Txn 3 | EDF Energy / Utilities / -£94.20 / 23 May 2026 |
| Transaction IDs | txn_20260525_001, txn_20260524_001, txn_20260523_001 |
| Page size | 20 per load |

---

## Design Notes

- **Summary card color:** #F8F4FF is a 3% purple tint of the primary #1800B1 — creates brand warmth without distracting from transaction content below.
- **Category badge system:** Each category has a unique background tint derived from its semantic color — Groceries (#E8F5E9 green), Utilities (#FFF3E0 orange), Income (#E8F5E9 green). These are inline chips in the meta row, not icons, making them scannable at small sizes.
- **Date group headers:** label_medium with letter_spacing 0.5 and #666666 — clearly separated from card content without a background divider, keeping the list light.
- **Search + filter combo:** The search bar, date picker, and filter chips are all persistent across states (visible in loading, content, and searching), so users can immediately refine without waiting for results.
- **Load more vs infinite scroll:** Explicit "Load More" button chosen over infinite scroll to give users control over data loading, important for metered mobile connections.
- **a11y:** Each transaction row has a full sentence a11y label read by TalkBack: "Tesco Supermarket, debit forty-two pounds fifty, Groceries, 25 May 2026. Tap for details." Filter chips use role=radio with selected state.

---

_Generated by /idea export | 2026-05-25_
