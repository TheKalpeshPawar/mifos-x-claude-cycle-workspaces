# Direct Debits — Visual Specification

| Field | Value |
|---|---|
| Feature | direct-debits |
| Flavor | consumer |
| Archetype | index_list |

---

## Screen Layout

Top-to-bottom layout on a vertically scrolling list screen with FAB:

```
[ Top App Bar: "Direct Debits"  ←  ⋮  ]  ← back + more_vert
────────────────────────────────────────
[ Direct Debits       [2 active]        ]  ← headline_large #1800B1 bold + green chip
────────────────────────────────────────
┌──────────────────────────────────────┐
│  London Borough of Hackney  [Active] │  ← white card, elevation 2, r=16dp
│  £148.00 / month         Next: 1 Jun │  ← #1800B1 semibold | body_small #888888
└──────────────────────────────────────┘  ← margin 20dp horizontal, 12dp bottom

┌──────────────────────────────────────┐
│  BT Broadband               [Active] │  ← white card, elevation 2
│  £42.99 / month          Next: 15 Jun│
└──────────────────────────────────────┘

                         [+ Set Up DD  ]  ← FAB bottom-right, #1800B1
────────────────────────────────────────
```

---

## Components

### title_count_row
- Horizontal stack, alignment center, spacing 12dp
- Padding: 20dp horizontal, 16dp top and bottom
- Separates app bar from the list content

### direct_debits_title
- Content: "Direct Debits"
- Typography: `headline_large`, color `#1800B1`, font_weight bold
- Fills available width, chip sits to the right

### active_count_chip
- Content: "2 active"
- Background: `#E8F5E9`, corner radius: 12dp
- Padding: 10dp horizontal, 4dp vertical
- Typography: `label_medium`, color `#4CAF50`, semibold
- Consistent chip pattern with standing-orders screen

### direct_debit_council_tax
- Background: `#FFFFFF`, corner radius: 16dp, elevation: 2
- Border: `#F0F0F0`, 1dp
- Margin: 20dp horizontal (inset from screen edge), 12dp bottom
- Padding: 16dp horizontal and vertical

### council_tax_header_row
- Horizontal stack, `space_between`, padding bottom 8dp
- Left: "London Borough of Hackney" — `title_medium`, `#111111`, semibold
- Right: Active badge

### council_tax_active_badge
- Background: `#E8F5E9`, corner radius 10dp
- Padding: 8dp horizontal, 3dp vertical
- Typography: `label_small`, color `#4CAF50`

### council_tax_amount_row
- Horizontal stack, `space_between`, align center, padding top 4dp
- Left: "£148.00 / month" — `body_large`, `#1800B1`, semibold
- Right: "Next: 1 Jun 2026" — `body_small`, `#888888`

### direct_debit_broadband (same structure as council_tax)
- "BT Broadband" — `title_medium`, `#111111`, semibold
- Active badge: same green chip
- "£42.99 / month" — `body_large`, `#1800B1`, semibold
- "Next: 15 Jun 2026" — `body_small`, `#888888`

### setup_direct_debit_fab
- Position: floating_action_button (bottom-right, standard MD3 position)
- Background: `#1800B1`, text: `#FFFFFF`
- Label: "Set Up Direct Debit"
- Leading icon: `add`
- Corner radius: 16dp (extended FAB shape), elevation: 6

---

## Interaction Patterns

| Interaction | Component | Result |
|---|---|---|
| Tap council tax card | direct_debit_council_tax | Opens direct debit detail bottom sheet |
| Tap broadband card | direct_debit_broadband | Opens direct debit detail bottom sheet |
| Tap FAB | setup_direct_debit_fab | Opens new direct debit setup sheet |
| Tap "⋮" overflow | more_vert (top bar) | Opens options menu (e.g., manage mandate) |
| Tap back arrow | arrow_back | Navigate to accounts screen |
| Pull to refresh | scroll area | RefreshTriggered event |
| Tap retry (error state) | retry_button | RetryLoad event |

---

## Content Data

| Element | Value |
|---|---|
| Active count | 2 active |
| Direct debit 1 payee | London Borough of Hackney |
| Direct debit 1 amount | £148.00 / month |
| Direct debit 1 next | Next: 1 Jun 2026 |
| Direct debit 1 status | Active |
| Direct debit 2 payee | BT Broadband |
| Direct debit 2 amount | £42.99 / month |
| Direct debit 2 next | Next: 15 Jun 2026 |
| Direct debit 2 status | Active |
| Empty state icon | account_balance_wallet |
| Empty state title | "No direct debits set up" |
| Empty state message | "Authorise merchants to collect payments automatically on agreed dates" |

---

## Design Notes

**Horizontal card inset:** Unlike standing orders (which have zero horizontal margin on cards), direct debit cards use 20dp horizontal margin — this is defined in the YAML as `margin_horizontal: 20`. This creates a visual breathing room that subtly differentiates the two list screens when users navigate between them.

**No delete/edit action icons on rows:** Direct debits differ from standing orders in that they are controlled by the payee, not the payer. Cancellation requires contacting the payee or going through a detail view. The card's tap-to-view-detail pattern reflects this asymmetry — there are no quick delete icons at the row level.

**Only "Active" status shown:** The two real-world mandates (Council Tax, BT Broadband) are both active. No "Paused" or "Cancelled" examples. The absence of grey/muted cards keeps the list clean; any cancelled mandates would be excluded from the active list.

**FAB label "Set Up Direct Debit":** Uses "Set Up" (not "Create") to reflect that direct debits require a merchant authorisation flow, not just a simple form fill. The language sets correct user expectations.

**Empty state message:** "Authorise merchants to collect payments automatically on agreed dates" — explains the concept (merchant authorisation) rather than the feature. Helpful for users who don't know what a direct debit is.

**Overflow menu on top bar:** `more_vert` opens options not surfaced at row level (e.g., view cancelled mandates, bulk management). Design reserves this space for power-user actions.

*Generated by /idea export | 2026-05-25*
