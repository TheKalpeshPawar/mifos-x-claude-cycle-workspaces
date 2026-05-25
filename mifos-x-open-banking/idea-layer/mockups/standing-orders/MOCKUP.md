# Standing Orders — Visual Specification

| Field | Value |
|---|---|
| Feature | standing-orders |
| Flavor | consumer |
| Archetype | index_list |

---

## Screen Layout

Top-to-bottom layout on a vertically scrolling list screen with FAB:

```
[ Top App Bar: "Standing Orders"  ← ⚙️ ]  ← filter_list action
────────────────────────────────────────
[ Standing Orders     [3 active]        ]  ← headline_large #1800B1 + green chip
────────────────────────────────────────
┌──────────────────────────────────────┐
│  Rent Payment            [Active ✓]  │  ← white card, elevation 2, r=16dp
│  To: Landlord Holdings Ltd           │  ← body_medium, #666666
│  £1,200 / month        Next: 1 Jun   │  ← #1800B1 bold | body_small #888888
│                      [✏️]  [🗑️]      │  ← edit #1800B1 | delete #FF5252
└──────────────────────────────────────┘

┌──────────────────────────────────────┐
│  Netflix Subscription    [Active ✓]  │  ← white card, elevation 2
│  (no beneficiary label shown)        │
│  £15.99 / month       Next: 7 Jun   │
│                      [✏️]  [🗑️]      │
└──────────────────────────────────────┘

┌──────────────────────────────────────┐  ← dimmed: #FAFAFA bg, #E0E0E0 border
│  Gym Membership         [Paused]     │  ← grey text #888888 | grey badge
│  £45.00 / month  Next: 15 Jun (Paused)│ ← #9E9E9E amount | #BBBBBB date
│                      [✏️]  [🗑️]      │
└──────────────────────────────────────┘

                              [+ Create ]  ← FAB bottom-right, #1800B1, r=16dp
────────────────────────────────────────
```

---

## Components

### title_count_row
- Horizontal stack, alignment center, spacing 12dp
- Padding bottom: 16dp, separates header from first card

### standing_orders_title
- Content: "Standing Orders"
- Typography: `headline_large`, color `#1800B1`
- Flex-grows to fill space left of chip

### active_count_chip
- Content: "3 active"
- Background: `#E8F5E9`, corner radius: 12dp
- Padding: 10dp horizontal, 4dp vertical
- Text: `label_medium`, color `#4CAF50`, semibold
- Communicates health at a glance — green = active count, not warning

### Standing order cards (Active: standing_order_rent, standing_order_netflix)
- Background: `#FFFFFF`, corner radius: 16dp, elevation: 2
- Border: `#F0F0F0`, 1dp, margin bottom: 12dp
- Padding: 16dp horizontal and vertical
- Header row: `space_between` — title left, status badge right
- Beneficiary text: `body_medium`, `#666666`, prefix "To: "
- Amount row: `space_between` — amount left (#1800B1 semibold) | next date right (body_small #888888)
- Actions row: `flex_end` — edit icon then delete icon, 8dp spacing

### Paused card (standing_order_gym)
- Background: `#FAFAFA` (lighter than active), corner radius: 16dp, elevation: 1
- Border: `#E0E0E0`, 1dp (slightly more visible = paused border)
- Title text: `#888888` (dimmed vs active #111111)
- Badge: "Paused" — background `#F5F5F5`, text `#9E9E9E`
- Amount: `#9E9E9E` (dimmed primary)
- Date: `#BBBBBB` — "Next: 15 Jun 2026 (Paused)" with literal "(Paused)" suffix

### Active badge
- Background `#E8F5E9`, corner radius 10dp, padding 8dp × 3dp
- Text: `label_small`, color `#4CAF50`

### Paused badge
- Background `#F5F5F5`, corner radius 10dp
- Text: `label_small`, color `#9E9E9E`

### Action icons (edit, delete)
- Edit: `edit_outlined`, size 22dp, color `#1800B1`, 8dp padding
- Delete: `delete_outlined`, size 22dp, color `#FF5252`, 8dp padding
- Actions row: `justify: flex_end`, padding top 12dp

### create_standing_order_fab
- Position: floating_action_button (bottom-right)
- Background: `#1800B1`, text: `#FFFFFF`
- Leading icon: `add`, corner radius 16dp, elevation 6

---

## Interaction Patterns

| Interaction | Component | Result |
|---|---|---|
| Tap order card | standing_order_* | Opens standing order detail bottom sheet |
| Tap edit icon | *_edit_icon | Opens edit standing order sheet |
| Tap delete icon | *_delete_icon | Confirmation dialog: "Delete this standing order?" [Delete] [Cancel] |
| Confirm delete | — | DELETE_FAILED if error; success removes from list |
| Tap FAB | create_standing_order_fab | Opens create standing order form bottom sheet |
| Tap filter icon | filter_list (top bar) | Filter bottom sheet: All / Active / Paused |
| Pull to refresh | scroll area | RefreshTriggered event → reload list |

---

## Content Data

| Order | Beneficiary | Amount | Frequency | Next Date | Status |
|---|---|---|---|---|---|
| Rent Payment | Landlord Holdings Ltd | £1,200 | Monthly | 1 Jun 2026 | Active |
| Netflix Subscription | (Netflix) | £15.99 | Monthly | 7 Jun 2026 | Active |
| Gym Membership | (Gym) | £45.00 | Monthly | 15 Jun 2026 | Paused |
| Active count chip | — | — | — | — | "3 active" |

---

## Design Notes

**Active vs Paused visual differentiation:** Active cards use pure white (#FFFFFF) background; paused use off-white (#FAFAFA). Active text uses full-contrast #111111; paused uses muted #888888. This passive dimming communicates "paused" without requiring users to read the badge text — the card "looks inactive."

**Amount in primary color:** £ amounts use `#1800B1` (primary) for active orders, `#9E9E9E` for paused — the brand color acts as a visual "this is moving money" signal.

**Delete in red, edit in blue:** Icon color assignment at the row level ensures accidental taps result in an edit (reversible) not a delete (irreversible). Edit is on the left, delete on the right — matching the standard swipe-to-delete direction.

**FAB placement:** Bottom-right per MD3 FAB spec, elevation 6, always visible in content, empty, and error states — creation is always available.

**Empty state copy:** "Set up recurring payments to automate your regular bills" — benefit-oriented language, not feature-describing. Pairs with `repeat_off` icon for context.

*Generated by /idea export | 2026-05-25*
