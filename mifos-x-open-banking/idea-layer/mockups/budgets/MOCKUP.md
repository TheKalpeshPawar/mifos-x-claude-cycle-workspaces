# Budgets — Visual Mockup

> Auto-generated from `screens/budgets/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-16T00:00:00Z

---

## Screen: Budgets

Canvas: 393×852dp (Pixel 5) · Top app bar visible (back leading, title "Budgets") · Bottom navigation visible · No FAB · Roboto font · Material 3 light theme · Background #F7F9FF

Shell (from `app-shell.yaml`): Bottom navigation — Home | Accounts | Transactions | More.
Top app bar variant: small, leading: back arrow, title: "Budgets" (per `ui.yaml#shell`).
FAB disabled per `ui.yaml#shell.fab_visible: false`.

---

### State: loading

```
┌─────────────────────────────────────────────┐
│ ← Budgets                                   │  ← top_app_bar h 56dp bg #F7F9FF
│                                              │    title titleMedium 16sp w500 #181C20
│                                              │    leading back_arrow icon 24dp #181C20
├─────────────────────────────────────────────┤
│                                              │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │  ← budgets_skeleton row 1: 361×88dp
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │    shimmer fill #DDE3EA, radius 12dp
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │    margin horizontal 16dp
│                                              │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │  ← budgets_skeleton row 2: 361×88dp
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │    gap 8dp between rows
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │
│                                              │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │  ← budgets_skeleton row 3: 361×88dp
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░   │
│                                              │
│  [reduce-motion: static fill, no animation] │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│  ← bottom_nav bg #F7F9FF h 80dp
└─────────────────────────────────────────────┘
```

### Component Hierarchy — loading

```
Screen: Budgets (BudgetsUiState.Loading)
│
top_app_bar/ (small variant, bg #F7F9FF, elevation 0 scrolled → 2)
├── leading back_arrow  (icon arrow_back 24dp #181C20, min touch 48dp)
└── title               (titleMedium 16sp/24sp w500 #181C20): "Budgets"

LazyColumn padding top 16dp horizontal 16dp bottom 16dp, gap 8dp:
│
budgets_skeleton/ (loading placeholder for 3 budget card rows)
│   accessibility_label: "Loading budgets" (#DDE3EA shimmer, reduce-motion: static fill)
│
├── skeleton_row[0]  (shimmer variant:card, 88dp h, radius 12dp, #DDE3EA pulse 1.5s)
├── skeleton_row[1]  (shimmer variant:card, 88dp h, radius 12dp, #DDE3EA pulse 1.5s)
└── skeleton_row[2]  (shimmer variant:card, 88dp h, radius 12dp, #DDE3EA pulse 1.5s)

BottomNav/ (persistent, always rendered)
├── tab Home         (icon:home,          label:"Home",         default,  tint #41474D)
├── tab Accounts     (icon:account_balance,label:"Accounts",    default,  tint #41474D)
├── tab Transactions (icon:receipt_long,  label:"Transactions", default,  tint #41474D)
└── tab More         (icon:more_horiz,    label:"More",         default,  tint #41474D)
```

---

### State: content

```
┌─────────────────────────────────────────────┐
│ ← Budgets                                   │  ← top_app_bar h 56dp bg #F7F9FF
├─────────────────────────────────────────────┤
│ Set budget                                   │  ← set_budget_header labelLarge 14sp w500
│                                              │    #181C20, padding h 16dp top 16dp bottom 8dp
│ ┌─────────────────────────────────────────┐ │  ← set_budget_card bg #EBEEF3 elevation 1
│ │ Category                               ▼│ │    radius 12dp padding 16dp margin h 16dp
│ │ Groceries                               │ │  ← budget_category_dropdown exposed_dropdown
│ │                                         │ │    label labelSmall 11sp #41474D
│ │ Monthly limit (£)                       │ │    selected value bodyLarge 16sp #181C20
│ │ ┌─────────────────────────────────────┐ │ │  ← budget_amount_field text_field
│ │ │                                     │ │ │    label labelSmall 11sp #41474D
│ │ │  0.00                               │ │ │    placeholder bodyLarge 16sp #72787E
│ │ └─────────────────────────────────────┘ │ │    keyboard: decimal, outline #72787E
│ │                                         │ │
│ │    [        Set Budget        ]         │ │  ← save_budget_button filled h 40dp
│ └─────────────────────────────────────────┘ │    bg #266489 text #FFFFFF radius 9999
│                                              │    min-touch 48dp
│  Budgets are stored locally on your device. │  ← budgets_storage_hint bodySmall 12sp
│                                              │    #41474D padding h 16dp bottom 8dp
│ June 2026                                   │  ← budgets_header labelLarge 14sp w500
│                                              │    #181C20 padding h 16dp bottom 8dp
│ ┌─────────────────────────────────────────┐ │  ← budget_card[Groceries] elevation 1
│ │ Groceries                  £201.50 left │ │    bg #EBEEF3 radius 12dp padding 16dp
│ │ £198.50 of £400.00                      │ │  ← list_item label titleSmall 14sp w500
│ │ ████████████░░░░░░░░░░░░░  50%          │ │    #181C20 trailing bodySmall 12sp #41474D
│ │ [View transactions]  [Delete]           │ │  ← progress primary #266489 fraction 0.496
│ └─────────────────────────────────────────┘ │    actions row gap 8dp
│                                              │
│ ┌─────────────────────────────────────────┐ │  ← budget_card[Dining] over budget
│ │ Dining                     £18.00 over  │ │    bg #EBEEF3 radius 12dp
│ │ £168.00 of £150.00                      │ │    trailing text #BA1A1A "£18.00 over"
│ │ ████████████████████████  100%          │ │  ← progress error #BA1A1A fraction 1.0
│ │ Over budget by £18.00                   │ │  ← over_budget_alert labelSmall 11sp
│ │ [View transactions]  [Delete]           │ │    #BA1A1A visible: true
│ └─────────────────────────────────────────┘ │
│                                              │
│ ┌─────────────────────────────────────────┐ │  ← budget_card[Transport] elevation 1
│ │ Transport                  £38.80 left  │ │    bg #EBEEF3 radius 12dp
│ │ £41.20 of £80.00                        │ │
│ │ ████████████░░░░░░░░░░░░░  52%          │ │  ← progress primary #266489 fraction 0.515
│ │ [View transactions]  [Delete]           │ │
│ └─────────────────────────────────────────┘ │
│                                              │
│ ┌─────────────────────────────────────────┐ │  ← budget_card[Bills] elevation 1
│ │ Bills                      £22.60 left  │ │
│ │ £197.40 of £220.00                      │ │
│ │ █████████████████████░░░░  90%          │ │  ← progress primary #266489 fraction 0.897
│ │ [View transactions]  [Delete]           │ │
│ └─────────────────────────────────────────┘ │
│                                              │
│ ┌─────────────────────────────────────────┐ │  ← budget_card[Shopping] over budget
│ │ Shopping                  £24.99 over   │ │    trailing text #BA1A1A
│ │ £124.99 of £100.00                      │ │
│ │ ████████████████████████  100%          │ │  ← progress error #BA1A1A fraction 1.0
│ │ Over budget by £24.99                   │ │  ← over_budget_alert labelSmall #BA1A1A
│ │ [View transactions]  [Delete]           │ │
│ └─────────────────────────────────────────┘ │
│                                              │
│ ┌─────────────────────────────────────────┐ │  ← budget_card[Subscriptions] elevation 1
│ │ Subscriptions              £12.00 left  │ │
│ │ £63.00 of £75.00                        │ │
│ │ ████████████████████░░░░░  84%          │ │  ← progress primary #266489 fraction 0.84
│ │ [View transactions]  [Delete]           │ │
│ └─────────────────────────────────────────┘ │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│
└─────────────────────────────────────────────┘
```

### Component Hierarchy — content

```
Screen: Budgets (BudgetsUiState.Content)
│
top_app_bar/ (small variant, bg #F7F9FF, elevation 0 scrolled → 2)
├── leading back_arrow  (icon arrow_back 24dp #181C20, min touch 48dp)
└── title               (titleMedium 16sp/24sp w500 #181C20): "Budgets"

LazyColumn padding top 8dp horizontal 16dp bottom 16dp, gap 12dp:
│
set_budget_header/ (section_header, padding bottom 4dp)
└── label (labelLarge 14sp/20sp w500 #181C20): "Set budget"

set_budget_card/ (card bg #EBEEF3, elevation 1, radius 12dp, padding 16dp, margin bottom 4dp)
│  stack vertical gap 12dp:
├── budget_category_dropdown/ (ExposedDropdownMenuBox)
│   ├── label        (labelSmall 11sp/16sp w500 #41474D): "Category"
│   ├── selected     (bodyLarge 16sp/24sp w400 #181C20): "Groceries"  ← demo-data form.category
│   └── trailing     (icon arrow_drop_down 24dp #41474D)
│   on_click → selectBudgetCategory(category) → transform_state: form.category updated
│   options: ["Groceries", "Transport", "Dining", "Bills", "Shopping", "Subscriptions", "Income"]
│
├── budget_amount_field/ (OutlinedTextField, keyboard_type: decimal)
│   ├── label        (labelSmall 11sp/16sp w500 #41474D): "Monthly limit (£)"
│   ├── value        (bodyLarge 16sp/24sp w400 #181C20): "" (empty — demo: form.amount)
│   ├── placeholder  (bodyLarge 16sp/24sp w400 #72787E): "0.00"
│   └── error_msg    (labelSmall 11sp/16sp w400 #BA1A1A, visible on validation failure)
│   on_change → updateBudgetAmountField(amount) → transform_state: form.amount + inline validation
│   validation: required, numeric, min 0.01
│
└── save_budget_button/ (Button variant:filled, h 40dp, radius 9999, min touch 48dp)
    bg #266489, label-color #FFFFFF
    label: "Set Budget" (labelLarge 14sp w500)
    enabled_when: form.category != null AND form.amount valid
    on_click → saveBudget() → persist_db: upserts BudgetEntry to DataStore, resets form on success

budgets_storage_hint/ (text bodySmall 12sp/16sp w400 #41474D, padding h 0 bottom 4dp)
  value: "Budgets are stored locally on your device."

budgets_header/ (section_header, padding top 8dp bottom 4dp)
└── label (labelLarge 14sp/20sp w500 #181C20): "June 2026"  ← demo-data current_month_label

budgets_list/ (list vertical gap 8dp items_source: budgets[6])
│
├── budget_card[Groceries]/ (card bg #EBEEF3, elevation 1, radius 12dp, padding 16dp)
│   stack vertical gap 8dp:
│   ├── list_item (stack horizontal alignment center_vertical):
│   │   ├── label        (titleSmall 14sp/20sp w500 #181C20): "Groceries"
│   │   ├── supporting   (bodySmall 12sp/16sp w400 #41474D): "£198.50 of £400.00"
│   │   └── trailing     (bodySmall 12sp/16sp w400 #41474D): "£201.50 left"
│   │   a11y: "Groceries: spent £198.50 of £400.00 budget"
│   ├── budget_progress_bar (LinearProgressIndicator, value 0.496, color #266489,
│   │   trackColor #DDE3EA, h 6dp, radius 3dp, match_parent)
│   │   a11y: "Groceries budget: 50% used"
│   ├── over_budget_alert  (labelSmall 11sp/16sp w500 #BA1A1A, visibility: GONE — not over budget)
│   └── budget_card_actions/ (row horizontal gap 0):
│       ├── view_category_spend_button (text button labelMedium 12sp #266489): "View transactions"
│       │   a11y: "View transactions for Groceries"
│       │   on_click → navigateSpendingByCategory(category:"Groceries") → navigate: spending-by-category
│       └── delete_budget_button (text button labelMedium 12sp #BA1A1A): "Delete"
│           a11y: "Delete budget for Groceries"
│           on_click → deleteBudget(category:"Groceries") → delete: removes from DataStore
│
├── budget_card[Dining]/ (card bg #EBEEF3, elevation 1, radius 12dp, padding 16dp)
│   stack vertical gap 8dp:
│   ├── list_item:
│   │   ├── label        (titleSmall 14sp/20sp w500 #181C20): "Dining"
│   │   ├── supporting   (bodySmall 12sp/16sp w400 #41474D): "£168.00 of £150.00"
│   │   └── trailing     (bodySmall 12sp/16sp w400 #BA1A1A): "£18.00 over"   ← error colour
│   │   a11y: "Dining: spent £168.00 of £150.00 budget"
│   ├── budget_progress_bar (value 1.0 clamped, color #BA1A1A ← error, trackColor #FFDAD6)
│   │   a11y: "Dining budget: 100% used"
│   ├── over_budget_alert  (labelSmall 11sp/16sp w500 #BA1A1A, VISIBLE):
│   │   "Over budget by £18.00"
│   └── budget_card_actions/
│       ├── view_category_spend_button → navigateSpendingByCategory(category:"Dining")
│       └── delete_budget_button → deleteBudget(category:"Dining")
│
├── budget_card[Transport]/ (card elevation 1, radius 12dp)
│   ├── list_item label "Transport" + supporting "£41.20 of £80.00" + trailing "£38.80 left"
│   ├── budget_progress_bar (value 0.515, color #266489)
│   ├── over_budget_alert  (GONE)
│   └── actions → navigateSpendingByCategory("Transport") / deleteBudget("Transport")
│
├── budget_card[Bills]/ (card elevation 1, radius 12dp)
│   ├── list_item label "Bills" + supporting "£197.40 of £220.00" + trailing "£22.60 left"
│   ├── budget_progress_bar (value 0.897, color #266489)
│   ├── over_budget_alert  (GONE)
│   └── actions → navigateSpendingByCategory("Bills") / deleteBudget("Bills")
│
├── budget_card[Shopping]/ (card elevation 1, radius 12dp — OVER BUDGET)
│   ├── list_item label "Shopping" + supporting "£124.99 of £100.00" + trailing #BA1A1A "£24.99 over"
│   ├── budget_progress_bar (value 1.0 clamped, color #BA1A1A, trackColor #FFDAD6)
│   ├── over_budget_alert  (VISIBLE, #BA1A1A): "Over budget by £24.99"
│   └── actions → navigateSpendingByCategory("Shopping") / deleteBudget("Shopping")
│
└── budget_card[Subscriptions]/ (card elevation 1, radius 12dp)
    ├── list_item label "Subscriptions" + supporting "£63.00 of £75.00" + trailing "£12.00 left"
    ├── budget_progress_bar (value 0.84, color #266489)
    ├── over_budget_alert  (GONE)
    └── actions → navigateSpendingByCategory("Subscriptions") / deleteBudget("Subscriptions")

BottomNav/ (persistent)
├── tab Home         (icon:home,          label:"Home",         default,  tint #41474D)
├── tab Accounts     (icon:account_balance,label:"Accounts",    default,  tint #41474D)
├── tab Transactions (icon:receipt_long,  label:"Transactions", default,  tint #41474D)
└── tab More         (icon:more_horiz,    label:"More",         default,  tint #41474D)
```

---

### State: empty

```
┌─────────────────────────────────────────────┐
│ ← Budgets                                   │  ← top_app_bar h 56dp bg #F7F9FF
├─────────────────────────────────────────────┤
│ Set budget                                   │  ← set_budget_header visible in empty too
│                                              │    labelLarge 14sp w500 #181C20 padding h 16dp
│ ┌─────────────────────────────────────────┐ │  ← set_budget_card visible in empty state
│ │ Category                               ▼│ │    bg #EBEEF3 elevation 1 radius 12dp
│ │ Groceries                               │ │    padding 16dp margin h 16dp
│ │                                         │ │
│ │ Monthly limit (£)                       │ │
│ │ ┌─────────────────────────────────────┐ │ │
│ │ │ 0.00                                │ │ │
│ │ └─────────────────────────────────────┘ │ │
│ │                                         │ │
│ │    [        Set Budget        ]         │ │  ← save_budget_button same as content state
│ └─────────────────────────────────────────┘ │
│                                              │
│  Budgets are stored locally on your device. │  ← budgets_storage_hint bodySmall #41474D
│                                              │
│                                              │
│              [savings]                       │  ← empty_state icon 48dp #41474D centred
│                                              │    icon: savings (M3 material symbol)
│    No budgets yet                           │  ← title headlineSmall 24sp/32sp w400
│                                              │    #181C20 centred
│    Set monthly spending limits for each     │
│    category to track your habits against    │  ← body bodyMedium 14sp/20sp w400
│    your real Open Banking transactions.     │    #41474D centred padding h 32dp
│                                              │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│
└─────────────────────────────────────────────┘
```

### Component Hierarchy — empty

```
Screen: Budgets (BudgetsUiState.Empty)
│
top_app_bar/ (same as content state — small variant, leading back, title "Budgets")

LazyColumn padding top 8dp horizontal 16dp bottom 16dp, gap 12dp:
│
set_budget_header/ (identical to content state — visible in empty)
└── label (labelLarge 14sp/20sp w500 #181C20): "Set budget"

set_budget_card/ (identical to content state — visible in empty, allows creating first budget)
│  stack vertical gap 12dp:
├── budget_category_dropdown/ (same form fields as content)
├── budget_amount_field/
└── save_budget_button/ → saveBudget() — on success transitions Empty → Content

budgets_storage_hint/ (text bodySmall 12sp/16sp w400 #41474D)
  value: "Budgets are stored locally on your device."

empty_state/ (empty_state component, vertically centered, padding horizontal 32dp, top 48dp)
│   accessibility_label: "No budgets yet — use the form above to create your first budget"
├── icon  (savings 48dp #41474D, decorative:false,
│          contentDescription: "No budgets set")
├── title (headlineSmall 24sp/32sp w400 #181C20 center):
│         "No budgets yet"
└── body  (bodyMedium 14sp/20sp w400 #41474D center):
          "Set monthly spending limits for each category to track your habits against your real Open Banking transactions."

BottomNav/ (persistent — same as content)
```

---

### State: error

```
┌─────────────────────────────────────────────┐
│ ← Budgets                                   │  ← top_app_bar h 56dp bg #F7F9FF
├─────────────────────────────────────────────┤
│                                              │
│                                              │
│              [error_outline]                 │  ← icon 48dp #BA1A1A centred
│                                              │
│    Couldn't load budgets                    │  ← budgets_error title headlineSmall 24sp
│                                              │    #181C20 centred
│  Something went wrong reading your saved    │
│  budget data. Please try again.             │  ← message bodyMedium 14sp #41474D centred
│                                              │    padding h 32dp
│                                              │
│      [       Try again       ]              │  ← retry_load_button variant:tonal h 48dp
│                                              │    bg #D3E5F5 text #266489 radius 9999
│                                              │    min touch 48dp
│                                              │    triggers: retryLoad() action
│                                              │
│                                              │
├─────────────────────────────────────────────┤
│  ⌂ Home  ◫ Accounts  ≡ Transactions  ⊕ More│
└─────────────────────────────────────────────┘
```

### Component Hierarchy — error

```
Screen: Budgets (BudgetsUiState.Error — EC-BUD-004: DataStore IOException on mount)
│
top_app_bar/ (same as other states)

error_state/ (vertically centered, padding horizontal 32dp)
│   accessibility_label: "Couldn't load budgets"
│   id: budgets_error
├── icon   (error_outline 48dp #BA1A1A, decorative:false,
│           contentDescription: "Error loading budgets")
├── title  (headlineSmall 24sp/32sp w400 #181C20 center):
│          "Couldn't load budgets"
├── body   (bodyMedium 14sp/20sp w400 #41474D center):
│          "Something went wrong reading your saved budget data. Please try again."
└── retry_load_button/ (Button variant:tonal, h 48dp, radius 9999, min touch 48dp)
    bg #D3E5F5, text-color #266489
    label: "Try again" (labelLarge 14sp w500)
    on_click → retryLoad() → transform_state: re-runs budgets_load from loading state
    a11y: "Try again"

BottomNav/ (persistent)
```

---

### Interaction Summary

| Component | Action | Effect | Target / Behaviour |
|---|---|---|---|
| budget_category_dropdown | select_budget_category | transform_state | Updates form.category from dropdown selection; re-evaluates save-enabled state |
| budget_amount_field | update_budget_amount_field | transform_state | Updates form.amount + inline validation (numeric, min 0.01); shows field-level error if invalid |
| save_budget_button | save_budget | persist_db | Validates form, upserts BudgetEntry to DataStore keyed by category; overwrites existing entry for same category; resets form on success (androidx.datastore, kotlinx-serialization) |
| view_category_spend_button | navigate_spending_by_category | navigate | spending-by-category screen (param: category = item.category) — pre-filters transaction list to that budget category |
| delete_budget_button | delete_budget | delete | Removes BudgetEntry for item.category from DataStore (androidx.datastore); refreshes list; transitions to empty state if list becomes empty |
| retry_load_button (error) | retry_load | transform_state | Re-runs budgets_load from loading state: reads BudgetEntry records from DataStore and recomputes per-category used/limit fractions (kotlinx-coroutines) |

### Dimensions Table

| Component | Width | Height | Corner Radius |
|---|---|---|---|
| top_app_bar | match_parent | 56dp | 0 |
| set_budget_card | match_parent | wrap (~180dp) | 12dp |
| budget_category_dropdown | match_parent | 56dp | 4dp (outlined) |
| budget_amount_field | match_parent | 56dp | 4dp (outlined) |
| save_budget_button | match_parent | 40dp (touch 48dp) | 9999dp (full pill) |
| budgets_storage_hint | match_parent | 16dp | 0 |
| budget_card | match_parent | wrap (~120dp) | 12dp |
| budget_progress_bar | match_parent | 6dp | 3dp |
| view_category_spend_button | hug | 36dp (touch 48dp) | 4dp |
| delete_budget_button | hug | 36dp (touch 48dp) | 4dp |
| retry_load_button | match_parent − 64dp | 48dp | 9999dp (full pill) |
| bottom_nav | match_parent | 80dp | 0 |
