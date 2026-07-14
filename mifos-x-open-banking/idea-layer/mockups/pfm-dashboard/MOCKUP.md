# PFM Dashboard — Visual Mockup

> Auto-generated from `screens/pfm-dashboard/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-14T00:00:00Z

---

## Screen: My Finances

Canvas: 393×852dp · Top app bar · Bottom nav · Material 3 light theme

---

### State: loading

```
┌─────────────────────────────────────────────┐
│  My Finances                                 │  ← top_app_bar titleMedium #181C20
├─────────────────────────────────────────────┤
│                                              │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │  ← shimmer row 1 height 120dp
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
│                                              │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │  ← shimmer row 2 height 80dp
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
│                                              │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │  ← shimmer row 3 height 200dp
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
│                                              │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │  ← shimmer row 4 height 80dp
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: content

```
┌─────────────────────────────────────────────┐
│  My Finances                                 │
├─────────────────────────────────────────────┤
│                                              │
│  [ 7 days ]  [ 30 days ✓ ]  [ 3 months ]   │  ← period_selector segmented_button
│                                              │
│ ┌─────────────────────────────────────────┐ │
│ │  Net worth                              │ │  ← net_worth_card elevation 2 radius 12dp
│ │  £14,955.45              (primary)      │ │    net_worth_amount displaySmall #266489
│ │  Across 3 accounts                      │ │    subtitle bodySmall #41474D
│ │                                          │ │
│ │  Everyday current  £2,847.63            │ │  ← breakdown_current list_item compact
│ │  Savings           £12,450.00           │ │  ← breakdown_savings
│ │  Credit card       -£342.18             │ │  ← breakdown_credit error #BA1A1A
│ └─────────────────────────────────────────┘ │
│                                              │
│ ┌─── Spending ─────────────┐  ┌── Income ──┐│
│ │  This month              │  │  £2,850    ││  ← spend_card + income_card side by side
│ │  £891.12                 │  │  credit    ││    spend #BA1A1A / income #266489
│ │  Groceries · Transport · │  │  salary    ││
│ └──────────────────────────┘  └────────────┘│
│                                              │
│  Top spending categories                     │  ← section_header titleSmall #181C20
│  ┌──────────────────────────────────────┐   │
│  │ 🛒 Groceries        £324.50  ███     │   │  ← category_row card elevation 0
│  └──────────────────────────────────────┘   │    progress bar primary #266489
│  ┌──────────────────────────────────────┐   │
│  │ ⛽ Transport        £198.00  ██      │   │
│  └──────────────────────────────────────┘   │
│  ┌──────────────────────────────────────┐   │
│  │ ☕ Eating out       £142.80  █       │   │
│  └──────────────────────────────────────┘   │
│                                              │
│  💡 Insight: Groceries spending up 18%      │  ← insight_card elevation 1 outlined
│     vs last month.                          │    icon lightbulb #64597B tertiary
│         [  View details  ]                  │    → spending-by-category
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
top_app_bar/ (title "My Finances")
period_selector/ (segmented_button: 7d / 30d (default) / 3m)
net_worth_card/ (card elevation 2 radius 12dp padding 16dp margin h 16dp)
│  ├── net_worth_label    (labelMedium #50606E): "Net worth"
│  ├── net_worth_amount   (displaySmall #266489): "£14,955.45"
│  ├── net_worth_sub      (bodySmall #41474D): "Across 3 accounts"
│  └── net_worth_breakdown/ (stack vertical)
│       ├── breakdown_current  (list_item compact): "Everyday current  £2,847.63"
│       ├── breakdown_savings  (list_item compact): "Savings  £12,450.00"
│       └── breakdown_credit   (list_item compact, error): "Credit card  -£342.18"
spend_income_row/ (stack horizontal gap 12dp margin h 16dp)
│  ├── spend_card  (card elevation 1 radius 12dp weight 1)
│  │    ├── "This month" labelMedium #41474D
│  │    ├── "£891.12" headlineSmall #BA1A1A
│  │    └── "Groceries · Transport ·" bodySmall #41474D
│  └── income_card (card elevation 1 radius 12dp weight 1)
│       ├── "Income" labelMedium #41474D
│       └── "£2,850" headlineSmall #266489
categories_header/ (section_header titleSmall "Top spending categories")
categories_list/ (list vertical gap 8dp margin h 16dp)
│  └── category_row × N (card elevation 0 outlined radius 8dp padding 12dp)
│       ├── category_icon   (icon md #50606E)
│       ├── category_name   (bodyMedium #181C20): "Groceries"
│       ├── category_amount (bodyMedium #181C20): "£324.50"
│       └── progress_bar    (linear 4dp radius 2dp #266489, width=pct of total)
insight_card/ (card elevation 1 outlined radius 12dp margin h 16dp)
│  ├── icon lightbulb md #64597B
│  ├── insight_text (bodyMedium #181C20): "Groceries spending up 18% vs last month."
│  └── view_details_button (text button → spending-by-category)
BottomNav (always)
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│  My Finances                                 │
├─────────────────────────────────────────────┤
│  [ 7 days ]  [ 30 days ✓ ]  [ 3 months ]   │
│                                              │
│            [bar_chart]                       │  ← icon 48dp #41474D centred
│                                              │
│    No transaction data yet                  │  ← title headlineSmall #181C20
│  Your spending overview will appear         │  ← body bodyMedium #41474D
│  once transactions are loaded.              │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│  My Finances                                 │
├─────────────────────────────────────────────┤
│            [warning_amber]                   │  ← icon 48dp #BA1A1A
│    Could not load finances                  │  ← title headlineSmall #181C20
│  body = pfm_dashboard.error.body             │
│         [  Reload  ]                        │  ← reload_button tonal → reload_finances
└─────────────────────────────────────────────┘
```

---

### Interaction Summary

| Component | Action | Target |
|---|---|---|
| period_selector | select_period | in-place re-compute (7d/30d/3m) |
| category_row | navigate_category_drill | spending-by-category (category filter) |
| view_details_button | navigate_spending | spending-by-category |
| reload_button (error) | reload_finances | in-place retry |

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| net_worth_card | match_parent − 32dp | ~180dp | 12dp |
| spend_card | (50% − 22dp) | ~96dp | 12dp |
| income_card | (50% − 22dp) | ~96dp | 12dp |
| category_row | match_parent − 32dp | 56dp | 8dp |
| progress_bar | variable | 4dp | 2dp |
| insight_card | match_parent − 32dp | ~80dp | 12dp |
