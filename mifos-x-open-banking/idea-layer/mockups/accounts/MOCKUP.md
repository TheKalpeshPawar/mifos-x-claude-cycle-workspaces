# Visual Specification — My Accounts
**Feature:** accounts | **Flavor:** consumer

---

## Screen Layout

Top-to-bottom composition on a vertical scroll canvas bounded by a 5-tab bottom navigation bar:

```
┌────────────────────────────────────────┐
│  My Accounts                      [?]  │  ← accounts_header (h: 56dp)
├────────────────────────────────────────┤
│  🔍 Search by name, number or label [×]│  ← accounts_search (h: 56dp, 20dp margin)
├────────────────────────────────────────┤
│  🏦 Mifos Bank UK           £10,430.50 │  ← bank_group_1_header
│     2 accounts                         │
├────────────────────────────────────────┤
│ ┌──────────────────────────────────┐   │
│ │▌ Primary Checking    [CHECKING]  │   │  ← account_card_1 (left-border #4C662B)
│ │  £4,250.00                       │   │
│ │  ⊞ DE89 3704 0044 0532 0130 00   │   │
│ └──────────────────────────────────┘   │
│ ┌──────────────────────────────────┐   │
│ │▌ Holiday Savings      [SAVINGS]  │   │  ← account_card_2 (left-border #386663)
│ │  £6,180.50                       │   │
│ │  ⊞ DE89 3704 0044 0532 0131 00   │   │
│ └──────────────────────────────────┘   │
├────────────────────────────────────────┤
│  🏦 Mifos Business UK        £2,050.00 │  ← bank_group_2_header
│     1 account                          │
├────────────────────────────────────────┤
│ ┌──────────────────────────────────┐   │
│ │▌ Business Current   [BUSINESS]   │   │  ← account_card_3 (left-border #E8A317, decorative)
│ │  £2,050.00                       │   │
│ │  ⊞ DE89 3704 0044 0532 0132 00   │   │
│ └──────────────────────────────────┘   │
├────────────────────────────────────────┤
│  Total across 3 accounts   £12,480.50  │  ← total_balance_footer
├────────────────────────────────────────┤
│  [Home] [Accounts★] [Pay] [Cards] [⋯] │  ← bottom nav
└────────────────────────────────────────┘
                              [+] FAB     ← add_account_fab (fixed, bottom-right)
```

---

## Components

### accounts_header
- **Position:** Top of scroll content; padding_horizontal: 20dp, padding_top: 24dp, padding_bottom: 8dp
- **Layout:** Horizontal row, space-between, vertically centred
- **Left:** Text "My Accounts" — Outfit/headline_large (32sp/Regular), color: `#1A1C16`; a11y heading level 1
- **Right:** `help_outline` icon, 24dp, color: `#44483D`; tappable, focusable; on_click: `open_account_help`

### accounts_search
- **Position:** Below header; margin_horizontal: 20dp, padding_vertical: 16dp
- **Variant:** Outlined text field, border_radius: 28dp (pill)
- **Leading icon:** `search` (Material), color: `#44483D`
- **Trailing icon:** `close`, visible when field has input; clears query
- **Placeholder:** "Search by name, number or label" — color: `#44483D`
- **Background:** `#F0F1E6` (surface_container); border: `#C5C8BA` idle, `#4C662B` focused
- **Interaction:** on_click triggers `search_accounts(query)`; a11y role: searchbox
- **States:** idle, hover, focus, focus_visible, disabled, error

### bank_group_1_header — Mifos Bank UK
- **Position:** Below search bar; padding_horizontal: 20dp, padding_top: 24dp, padding_bottom: 8dp
- **Layout:** Horizontal row, space-between
- **Left cluster:** `account_balance` icon 18dp `#4C662B` + vertical stack of "Mifos Bank UK" (Outfit/title_small, `#1A1C16`) and "2 accounts" (Outfit/label_small, `#44483D`), 8dp gap between icon and text stack
- **Right:** Subtotal "£10,430.50" — Outfit/title_medium, color: `#4C662B`
- **A11Y:** heading level 2; full label covers name, count, and subtotal value

### account_card_1 — Primary Checking
- **Background:** `#FFFFFF`, border_radius: 16dp, elevation: 2 (3dp shadow), 4dp left-border `#4C662B`
- **Padding:** 24dp all sides; margin_horizontal: 20dp, margin_bottom: 16dp
- **Header row (space-between):**
  - Left: "Primary Checking" — Outfit/title_medium (16sp/600), color: `#1A1C16`
  - Right: badge box — `#CDEDA3` bg, 6dp radius; "CHECKING" — Outfit/label_small (11sp/500), color: `#4C662B`
- **Balance row:** "£4,250.00" — Outfit/display_small (32sp/600), color: `#4C662B`; padding_bottom: 8dp
- **IBAN row:** `account_box` icon 16dp `#44483D` + "DE89 3704 0044 0532 0130 00" — Outfit/body_small (12sp), `#44483D`, monospace; 8dp gap
- **A11Y:** role button, label: "Primary Checking account, balance four thousand two hundred fifty pounds, tap to view details"
- **On tap:** navigate → account-detail (account_id: acc_checking_primary)
- **States:** idle, hover, focus_visible, pressed

### account_card_2 — Holiday Savings
- **Left-border accent:** 4dp `#386663` (Savings/teal)
- **Balance:** "£6,180.50" — Outfit/display_small, color: `#386663`
- **Badge:** "SAVINGS" — `#CDEDA3` bg, Outfit/label_small, color: `#386663`
- **IBAN:** "DE89 3704 0044 0532 0131 00" monospace `#44483D`
- **On tap:** navigate → account-detail (account_id: acc_savings_goal)
- **A11Y:** "Holiday Savings account, balance six thousand one hundred eighty pounds fifty, tap to view details"

### bank_group_2_header — Mifos Business UK
- **Layout:** Mirrors bank_group_1_header pattern
- **Left cluster:** `account_balance` icon 18dp `#4C662B` + "Mifos Business UK" title_small `#1A1C16` + "1 account" label_small `#44483D`
- **Right:** Subtotal "£2,050.00" — Outfit/title_medium, color: `#4C662B`
- **A11Y:** heading level 2

### account_card_3 — Business Current
- **Left-border accent:** 4dp `#E8A317` (decorative — amber; NOT used on text)
- **Balance:** "£2,050.00" — Outfit/display_small, color: `#44483D` *(A11Y-002 fix: 8.91:1 PASS)*
- **Badge:** "BUSINESS" — `#CDEDA3` bg, Outfit/label_small, color: `#44483D` *(A11Y-002 fix: 7.25:1 PASS)*
- **IBAN:** "DE89 3704 0044 0532 0132 00" monospace `#44483D`
- **On tap:** navigate → account-detail (account_id: acc_business_main)
- **A11Y:** "Business Current account, balance two thousand fifty pounds, tap to view details"

### footer_divider
- **Color:** `#E1E4D5`; margin_horizontal: 20dp, margin_vertical: 4dp
- **A11Y:** role separator

### total_balance_footer
- **Background:** `#F9FAEF`, border_radius: 12dp, padding: 16dp
- **Margin:** horizontal 20dp, top 4dp, bottom 80dp (clears FAB + nav)
- **Row (space-between):**
  - Left: "Total across 3 accounts" — Outfit/body_medium (14sp/Regular), color: `#44483D`
  - Right: "£12,480.50" — Outfit/title_large (22sp/700), color: `#4C662B`
- **A11Y:** role text, "Total: twelve thousand four hundred eighty pounds fifty pence across three accounts"

### add_account_fab
- **Fixed position:** bottom: 80dp, right: 20dp (above bottom nav bar)
- **Size:** 56×56dp, border_radius: 16dp
- **Style:** background: `#4C662B`, `add` icon 24dp color `#FFFFFF`, elevation: 6 (6dp shadow)
- **On tap:** `request_new_account`
- **A11Y:** role button, label: "Request a new account", hint: "Opens the account request form"
- **States:** idle, hover, focus_visible, pressed, disabled

---

## Interaction Patterns

| Target                | Gesture | Outcome                                              |
|-----------------------|---------|------------------------------------------------------|
| accounts_search       | Tap / type | Filter `filteredAccounts` + regroup `groupedByBank`; trailing `close` clears query |
| account_card_1        | Tap     | Navigate → account-detail / acc_checking_primary     |
| account_card_2        | Tap     | Navigate → account-detail / acc_savings_goal         |
| account_card_3        | Tap     | Navigate → account-detail / acc_business_main        |
| add_account_fab       | Tap     | Opens account request form                           |
| accounts_help_icon    | Tap     | Opens account help overlay                           |
| Bottom nav            | Tap     | Replace top-level destination                        |

---

## Loading State (skeleton)

- accounts_header and accounts_search remain visible and interactive
- 3 grey skeleton boxes (120dp tall, `#E1E4D5` bg, 16dp radius, 20dp horizontal margin, 16dp margin between) replace all account cards and bank group headers
- 1 shorter skeleton box (48dp, `#E1E4D5` bg, 12dp radius, 20dp margin) replaces total_balance_footer
- Shimmer animation: `shimmer_duration: short4`; reduced motion fallback: static placeholder

---

## Empty State

- accounts_header visible, search bar hidden
- Centred card: illustration `no_accounts`, title "No accounts found" (Outfit/title_medium), message "You don't have any accounts yet. Request a new account to get started." (Outfit/body_medium), CTA "Request Account" → `request_new_account`

---

## Error State

- accounts_header visible, search bar hidden
- Centred card: icon `error_outline`, title "Could not load accounts", message "We were unable to fetch your account list. Please check your connection and try again.", CTA "Retry" → `retry_load`

---

## Content Data

| Element                   | Value                           |
|---------------------------|---------------------------------|
| Bank group 1 name         | Mifos Bank UK                   |
| Bank group 1 account count| 2 accounts                      |
| Bank group 1 subtotal     | £10,430.50                      |
| Account 1 name            | Primary Checking                |
| Account 1 type            | CHECKING                        |
| Account 1 balance         | £4,250.00                       |
| Account 1 IBAN            | DE89 3704 0044 0532 0130 00     |
| Account 2 name            | Holiday Savings                 |
| Account 2 type            | SAVINGS                         |
| Account 2 balance         | £6,180.50                       |
| Account 2 IBAN            | DE89 3704 0044 0532 0131 00     |
| Bank group 2 name         | Mifos Business UK               |
| Bank group 2 account count| 1 account                       |
| Bank group 2 subtotal     | £2,050.00                       |
| Account 3 name            | Business Current                |
| Account 3 type            | BUSINESS                        |
| Account 3 balance         | £2,050.00                       |
| Account 3 IBAN            | DE89 3704 0044 0532 0132 00     |
| Total balance             | £12,480.50                      |
| Total account count       | 3                               |

---

## Design Notes

- **No filter tabs:** The previous account-type filter chip row has been removed. Discovery and narrowing is now handled via the `accounts_search` free-text field, which searches across name, number, and label in real-time.
- **Bank-grouped layout:** Accounts are grouped into hierarchical sections by institution. Each section header shows bank icon, name, account count, and subtotal, giving instant portfolio-level context before reading individual cards.
- **Color coding:** Left-border accent colours distinguish account types (Checking: `#4C662B`, Savings: `#386663`, Business: `#E8A317` decorative). Text colors on Business cards use the accessible `#44483D` (not amber) per A11Y-002 fix.
- **Typography hierarchy:** headline_large (screen title) > display_small (balance amounts) > title_medium (account names) > title_small (bank institution names) > body_small (IBAN text) — 5 clear levels.
- **Spacing rhythm:** 20dp horizontal gutters on all cards and section headers; 16dp margin below each card; 24dp top padding on section headers.
- **Accessibility:** Every account card has a full-sentence a11y label covering name, balance, and action hint. Bank group headers expose heading level 2. Search field exposes role searchbox. IBAN text is monospace for digit-grouping legibility.
- **Bottom nav:** Accounts tab active (icon: account_balance); FAB clears nav bar with bottom: 80dp positioning.

---

_Generated by /idea export | 2026-06-02_
