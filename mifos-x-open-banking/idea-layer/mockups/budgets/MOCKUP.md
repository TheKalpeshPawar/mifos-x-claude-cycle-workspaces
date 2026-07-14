# Budgets — Visual Mockup

> Auto-generated from `screens/budgets/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-14T00:00:00Z

---

## Screen: Budgets

Canvas: 393×852dp · Top app bar with back · Bottom nav · Material 3 light theme

---

### State: loading

```
┌─────────────────────────────────────────────┐
│ ← Budgets                                   │  ← top_app_bar titleMedium #181C20
├─────────────────────────────────────────────┤
│                                              │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │  ← budgets_skeleton shimmer radius 12dp
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │    rows × 3, 96dp each
│                                              │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
│                                              │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: content

```
┌─────────────────────────────────────────────┐
│ ← Budgets                                   │
├─────────────────────────────────────────────┤
│                                              │
│  Monthly budgets — July 2026                 │  ← month_header titleSmall #181C20
│                                              │
│ ┌─────────────────────────────────────────┐ │
│ │ 🛒 Groceries                            │ │  ← budget_card elevation 1 radius 12dp
│ │    Spent: £324.50 / £400.00             │ │    spent / limit bodyMedium #181C20
│ │    ████████████░░░░░░░░░   81%          │ │    progress primary #266489 (≤100%)
│ │    [delete]                             │ │    delete icon_button trailing
│ └─────────────────────────────────────────┘ │
│ ┌─────────────────────────────────────────┐ │
│ │ ⛽ Transport                             │ │
│ │    Spent: £198.00 / £150.00             │ │  ← over budget: progress error #BA1A1A
│ │    ████████████████████  🚨 Over budget │ │    badge chip tonal error "Over budget"
│ │    [delete]                             │ │
│ └─────────────────────────────────────────┘ │
│ ┌─────────────────────────────────────────┐ │
│ │ ☕ Eating out                            │ │
│ │    Spent: £142.80 / £200.00             │ │
│ │    ██████████░░░░░░░░░░    71%          │ │    progress primary #266489
│ │    [delete]                             │ │
│ └─────────────────────────────────────────┘ │
│                                              │
│ ┌─────────────────────────────────────────┐ │
│ │  + Add a budget category                │ │  ← add_budget_row card outlined
│ └─────────────────────────────────────────┘ │    or FAB (if spec uses FAB)
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
top_app_bar/ (title "Budgets", leading back)
month_header/ (text titleSmall #181C20, padding h 16dp): "Monthly budgets — July 2026"
budgets_list/ (list vertical gap 8dp padding h 16dp)
└── budget_card × N (card elevation 1 radius 12dp padding 16dp)
     ├── category_icon     (icon md #50606E)
     ├── category_name     (titleSmall #181C20): "Groceries"
     ├── spend_vs_limit    (bodyMedium #181C20): "Spent: £324.50 / £400.00"
     ├── progress_bar      (linear 6dp radius 3dp, under_budget=#266489, over=#BA1A1A)
     ├── pct_label         (labelSmall #41474D): "81%"
     ├── over_budget_chip  (chip tonal error, visible_when over_budget)
     └── delete_button     (icon_button delete trailing 48dp tap target)
add_budget_card/ (card outlined dashed-border elevation 0 radius 12dp)
│  └── add_label (bodyMedium #266489): "+ Add a budget category"
   on_click → show add_budget_form (bottom sheet)
BottomNav (always)
```

### Add Budget Bottom Sheet

```
┌─────────────────────────────────────────────┐
│  ▬ ─────────────────────────────────────    │  ← drag handle
│                                              │
│  Add budget                                 │  ← title headlineSmall #181C20
│                                              │
│  Category                                    │  ← category_dropdown label
│  ┌─────────────────────────────────────────┐│
│  │ Shopping                        ▼       ││  ← exposed dropdown
│  └─────────────────────────────────────────┘│
│                                              │
│  Monthly limit                               │
│  ┌─────────────────────────────────────────┐│
│  │ £  300.00                               ││  ← amount_field text_field numeric
│  └─────────────────────────────────────────┘│
│                                              │
│         [  Save budget  ]                   │  ← save_button filled #266489
│         [  Cancel       ]                   │  ← cancel_button text
│                                              │
└─────────────────────────────────────────────┘
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│ ← Budgets                                   │
├─────────────────────────────────────────────┤
│                                              │
│            [savings]                         │  ← icon 48dp #41474D
│                                              │
│    No budgets set                           │  ← title headlineSmall #181C20
│  Set monthly spending limits for each       │  ← body bodyMedium #41474D
│  category to track your habits.             │
│                                              │
│      [  Create your first budget  ]         │  ← CTA filled → open add_budget sheet
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home    ◫ Accounts    ☰ PFM    ⚙ More   │
└─────────────────────────────────────────────┘
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│ ← Budgets                                   │
├─────────────────────────────────────────────┤
│            [warning_amber]                   │  ← icon 48dp #BA1A1A
│    Could not load budgets                   │  ← title headlineSmall #181C20
│         [  Try again  ]                     │  ← retry tonal → budgets_load
└─────────────────────────────────────────────┘
```

---

### Interaction Summary

| Component | Action | Target |
|---|---|---|
| add_budget_card | open_add_budget_form | bottom sheet |
| save_button (sheet) | save_budget | DataStore persist, list refresh |
| cancel_button (sheet) | dismiss_sheet | → content |
| delete_button (card) | delete_budget | immediate persist + list refresh |
| retry_load_button (error) | budgets_load | in-place retry |
| create_first_budget_cta (empty) | open_add_budget_form | bottom sheet |

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| budget_card | match_parent − 32dp | ~96dp | 12dp |
| progress_bar | match_parent − 16dp | 6dp | 3dp |
| add_budget_card | match_parent − 32dp | 56dp | 12dp |
| amount_field | match_parent − 32dp | 48dp | 4dp |
| save_button | match_parent − 32dp | 48dp | 12dp |
