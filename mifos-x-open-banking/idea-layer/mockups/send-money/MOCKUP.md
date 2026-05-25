# Send Money — Visual Specification

| Field | Value |
|---|---|
| Feature | send-money |
| Flavor | consumer |
| Archetype | form |

---

## Screen Layout

Top-to-bottom component hierarchy on a vertically scrolling form screen:

```
[ Top App Bar: "Send Money"  ← back arrow ]
─────────────────────────────────────────
[ Headline: "Send Money"                 ]  ← #1800B1, headline_large
[ From Account selector (outlined)       ]  ← account_balance icon + expand_more
  "Primary Checking — £4,250.00 available"
[ Amount field (outlined) + Currency chip]  ← £ prefix, decimal keyboard | GBP ▾ chip
[ Beneficiary search field (outlined)    ]  ← search icon leading
  "Search beneficiary or enter account..."
[ ── Recent Beneficiaries (horiz scroll) ]
  [ John Smith · Barclays UK ]  [ Sarah Williams · HSBC UK ]
[ Reference field (outlined)             ]  ← max 35 chars, helper text
  placeholder: "Payment for invoice #1234"
[ Payment Type chip row                  ]
  [ SEPA (selected #1800B1) ] [ Domestic ] [ International ]
[ Fee estimate banner (green)            ]
  info_outline  "Estimated fee: Free (SEPA)"
─────────────────────────────────────────
[ Continue  (filled, full-width, #1800B1)]
─────────────────────────────────────────
```

---

## Components

### send_money_title
- Typography: `headline_large` (32sp, Roboto/Inter)
- Color: `#1800B1` (Mifos primary)
- Padding bottom: 8dp
- Role: section heading for screen identity

### from_account_selector
- Variant: outlined text field, corner radius 12dp
- Leading icon: `account_balance` (bank icon)
- Trailing icon: `expand_more` (dropdown affordance)
- Background: `#F5F5FF`
- Content: "Primary Checking — £4,250.00 available"
- Tapping opens account picker bottom sheet

### amount_input + currency_selector
- Amount field: outlined, decimal keyboard, £ prefix, placeholder "0.00"
- Corner radius: 12dp
- Currency chip: filter chip variant, "GBP ▾", corner radius 8dp
- Both laid out in a horizontal row — amount fills remaining width, chip is trailing

### beneficiary_search
- Variant: outlined with leading `search` icon
- Placeholder: "Search beneficiary or enter account..."
- Corner radius: 12dp
- Triggers debounce search against counterparties API

### recent_beneficiaries_row
- Orientation: horizontal with spacing 12dp, horizontally scrollable
- Each chip: background `#F0F0FF`, border `#E0E0FF` 1dp, corner radius 12dp
- Chip content: name + bank name (e.g., "John Smith · Barclays UK")
- Padding: 8dp vertical, 12dp horizontal per chip

### payment_type chips
- SEPA: selected state — background `#1800B1`, text `#FFFFFF`, corner radius 20dp, padding 16dp×8dp
- Domestic / International: unselected — outlined chip, corner radius 20dp
- Row spacing: 8dp, horizontal orientation

### fee_estimate_banner
- Background: `#E8F5E9`, border: `#4CAF50` 1dp, corner radius 8dp
- Leading icon: `info_outline` in `#4CAF50`
- Text: "Estimated fee: Free (SEPA)" — body_medium, #111111
- Padding: 16dp horizontal, 12dp vertical

### continue_button
- Variant: filled, full-width
- Background: `#1800B1`, text: `#FFFFFF`
- Corner radius: 12dp, padding vertical: 16dp
- Typography: `label_large` (14sp, medium weight)
- Disabled state: 38% opacity
- Loading state: linear progress indicator overlaid

---

## Interaction Patterns

| Interaction | Component | Result |
|---|---|---|
| Tap From Account | from_account_selector | Opens account picker bottom sheet |
| Tap amount field | amount_input | Numeric decimal keyboard appears |
| Tap GBP chip | currency_selector | Opens currency picker |
| Type in search | beneficiary_search | Debounce search, results appear below |
| Tap recent beneficiary | recent_beneficiary_john/sarah | Auto-fills beneficiary, validates IBAN |
| Tap SEPA/Domestic/International | payment_type chips | Switches selection, updates fee banner |
| Tap fee banner | fee_estimate_banner | Shows fee detail sheet |
| Tap Continue | continue_button | Triggers validation → validating state → navigation |

---

## Content Data

| Element | Value |
|---|---|
| Default account | "Primary Checking — £4,250.00 available" |
| Default currency | "GBP" |
| Recent beneficiary 1 | "John Smith · Barclays UK" |
| Recent beneficiary 2 | "Sarah Williams · HSBC UK" |
| Reference placeholder | "Payment for invoice #1234" |
| Default payment type | SEPA (selected) |
| Fee estimate | "Estimated fee: Free (SEPA)" |

---

## Design Notes

**Colors:**
- Primary `#1800B1` used on: title, selected payment chip, continue button, account selector icon
- `#F0F0FF` / `#E0E0FF` for recent beneficiary chips — maintains brand without competing with primary inputs
- Green `#E8F5E9` fee banner signals zero-cost SEPA path, encouraging SEPA selection

**Typography:**
- `headline_large` (32sp) for screen title — sets visual hierarchy
- `label_large` on Continue button — MD3 standard for primary CTA
- Helper text `body_small` on reference field — 35-char cap callout

**Spacing:**
- Form fields: 12dp vertical gap between each field
- Recent beneficiaries strip: 8dp top/bottom padding, 12dp chip gap
- Payment type chips: 8dp gap, flush left
- Continue button: 16dp vertical padding, adheres to 48dp minimum touch target

**Accessibility:**
- All inputs carry `content_description` describing current value
- Payment type chips declare `role: radio_button` and `assert_selected` state
- Fee banner uses `role: status` for live region announcement
- Continue button `assert_enabled: true` — disabled state must announce "greyed out, form incomplete"

*Generated by /idea export | 2026-05-25*
