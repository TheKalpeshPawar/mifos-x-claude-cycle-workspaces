# Spending by Category — Visual Mockup

> Auto-generated from `screens/spending-by-category/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-14T00:00:00Z

---

## Screen: Spending by Category

Canvas: 393×852dp · Top app bar with back · Bottom nav · Material 3 light theme

---

### State: loading

```
┌─────────────────────────────────────────────┐
│ ← Spending by Category                      │  ← top_app_bar
├─────────────────────────────────────────────┤
│                   ◌                          │  ← circular progress #266489 centred
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: content

```
┌─────────────────────────────────────────────┐
│ ← Spending by Category                      │
├─────────────────────────────────────────────┤
│                                              │
│ (This month ✓) (Last month) (3 months)      │  ← period_selector chip_group h-scroll
│                                              │
│ ┌─────────────────────────────────────────┐ │
│ │        [donut chart or bar chart]       │ │  ← spend_chart card elevation 1
│ │                                          │ │    height ~180dp radius 12dp
│ │  Total spend this month: £891.12        │ │    total_spend headlineMedium #181C20
│ └─────────────────────────────────────────┘ │
│                                              │
│  ┌──────────────────────────────────────┐   │
│  │ 🛒 Groceries                         │   │  ← category_row card elevation 0 outlined
│  │    £324.50  ·  14 transactions       │   │    radius 8dp padding 12dp h 16dp
│  │    ███████████████░░░░  36%          │   │    progress #266489 width=36%
│  └──────────────────────────────────────┘   │
│  ┌──────────────────────────────────────┐   │
│  │ ⛽ Transport                          │   │
│  │    £198.00  ·  8 transactions        │   │
│  │    ████████░░░░░░░░░░  22%           │   │
│  └──────────────────────────────────────┘   │
│  ┌──────────────────────────────────────┐   │
│  │ ☕ Eating out                         │   │
│  │    £142.80  ·  11 transactions       │   │
│  │    ██████░░░░░░░░░░░░  16%           │   │
│  └──────────────────────────────────────┘   │
│  ┌──────────────────────────────────────┐   │
│  │ 🎵 Entertainment                     │   │
│  │    £98.50  ·  5 transactions         │   │
│  │    ████░░░░░░░░░░░░░░  11%           │   │
│  └──────────────────────────────────────┘   │
│  ┌──────────────────────────────────────┐   │
│  │ 🏥 Health & pharmacy                 │   │
│  │    £127.32  ·  3 transactions        │   │
│  └──────────────────────────────────────┘   │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
top_app_bar/ (title "Spending by Category", leading back)
period_selector/ (chip_group single_select h-scroll, visible in all states)
│  ├── period_this_month  "This month" (selected by default)
│  ├── period_last_month  "Last month"
│  └── period_3months     "3 months"
spend_chart_card/ (card elevation 1 radius 12dp padding 16dp margin h 16dp)
│  ├── donut_or_bar_chart (chart component 180dp h)
│  └── total_spend_label  (headlineMedium #181C20): "Total spend this month: £891.12"
categories_list/ (list vertical gap 8dp padding h 16dp, sorted by amount DESC)
└── category_row × N (card outlined elevation 0 radius 8dp padding 12dp)
     ├── category_icon    (icon md #50606E)
     ├── category_name    (bodyMedium #181C20): e.g. "Groceries"
     ├── category_amount  (titleSmall #181C20): "£324.50"
     ├── tx_count         (bodySmall #41474D): "14 transactions"
     └── progress_bar     (linear 4dp radius 2dp bg #DDE3EA fill #266489)
         each row tappable → transactions filtered by category
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│ ← Spending by Category                      │
├─────────────────────────────────────────────┤
│ (This month ✓) (Last month) (3 months)      │
│                                              │
│           [pie_chart_outline]                │  ← icon 48dp #41474D centred
│                                              │
│    No spending data                         │  ← title headlineSmall #181C20
│  No transactions match the selected         │  ← body bodyMedium #41474D
│  period.                                    │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│ ← Spending by Category                      │
├─────────────────────────────────────────────┤
│            [error_outline]                   │  ← icon 48dp #BA1A1A
│    Unable to load categories                │  ← title headlineSmall #181C20
│         [  Try again  ]                     │  ← retry_button filled #266489
└─────────────────────────────────────────────┘
```

---

### Interaction Summary

| Component | Action | Target |
|---|---|---|
| period chips | select_period | in-place re-aggregate |
| category_row | navigate_category_transactions | transactions (category filter) |
| retry_button (error) | retry_load | in-place retry |

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| spend_chart_card | match_parent − 32dp | ~220dp | 12dp |
| category_row | match_parent − 32dp | ~80dp | 8dp |
| progress_bar | match_parent − 24dp | 4dp | 2dp |
| period chip | wrap | 32dp | 9999 |
