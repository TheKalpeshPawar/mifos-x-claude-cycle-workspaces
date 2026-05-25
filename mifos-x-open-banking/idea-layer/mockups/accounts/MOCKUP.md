# Visual Specification — My Accounts
**Feature:** accounts | **Flavor:** consumer

---

## Screen Layout

Top-to-bottom composition on a vertical scroll canvas bounded by a 5-tab bottom navigation bar:

```
┌────────────────────────────────────┐
│  My Accounts              [?]      │  ← accounts_header (h: 56px)
├────────────────────────────────────┤
│  [ALL] [CHECKING] [SAVINGS] [BUSI] │  ← account_type_tabs (h: 44px, h-scroll)
├────────────────────────────────────┤
│ ┌────────────────────────────────┐ │
│ │▌ Primary Checking    [CHECKING]│ │  ← account_card_1 (left-border #1800B1)
│ │  £4,250.00                     │ │
│ │  ⊞ DE89 3704 0044 0532 0130 00 │ │
│ └────────────────────────────────┘ │
│ ┌────────────────────────────────┐ │
│ │▌ Holiday Savings     [SAVINGS] │ │  ← account_card_2 (left-border #008B8B)
│ │  £6,180.50                     │ │
│ │  ⊞ DE89 3704 0044 0532 0131 00 │ │
│ └────────────────────────────────┘ │
│ ┌────────────────────────────────┐ │
│ │▌ Business Current   [BUSINESS] │ │  ← account_card_3 (left-border #FF9800)
│ │  £2,050.00                     │ │
│ │  ⊞ DE89 3704 0044 0532 0132 00 │ │
│ └────────────────────────────────┘ │
├────────────────────────────────────┤
│  Total across 3 accounts  £12,480.50│ ← total_balance_footer
├────────────────────────────────────┤
│  [Home] [Accounts*] [Pay] [Cards] [More]│ ← bottom nav
└────────────────────────────────────┘
                          [+] FAB      ← add_account_fab (fixed, bottom-right)
```

---

## Components

### accounts_header
- **Position:** Top of scroll content, padding_horizontal: 20, padding_top: 24
- **Layout:** Horizontal row, space-between
- **Left:** Text "My Accounts" — typography: headline_large, color: #1A1A1A
- **Right:** help_outline icon, 24px, color: #666666 — tappable

### account_type_tabs
- **Position:** Below header, horizontally scrollable
- **Active tab (ALL):** filled button, background: #1800B1, text: #FFFFFF, border_radius: 20
- **Inactive tabs:** outlined, border: #CCCCCC, text: #666666, border_radius: 20
- **Spacing:** 8px between tabs, padding_horizontal: 20

### account_card_1 — Primary Checking
- **Background:** #FFFFFF, border_radius: 16, elevation: 2
- **Left accent bar:** 4px solid #1800B1
- **Header row:** "Primary Checking" (title_medium, #1A1A1A, weight 600) + "CHECKING" badge (#E8E4FF background, #1800B1 text, label_small)
- **Balance:** "£4,250.00" — typography: display_small, color: #1800B1
- **IBAN row:** account_box icon (16px, #666666) + "DE89 3704 0044 0532 0130 00" — body_small, monospace, #666666

### account_card_2 — Holiday Savings
- **Left accent bar:** 4px solid #008B8B
- **Badge:** "SAVINGS" on #E0F2F1 background, color #008B8B
- **Balance:** "£6,180.50" — display_small, color: #008B8B
- **IBAN:** "DE89 3704 0044 0532 0131 00"

### account_card_3 — Business Current
- **Left accent bar:** 4px solid #FF9800
- **Badge:** "BUSINESS" on #FFF3E0 background, color #E65100
- **Balance:** "£2,050.00" — display_small, color: #E65100
- **IBAN:** "DE89 3704 0044 0532 0132 00"

### total_balance_footer
- **Background:** #F5F5F5, border_radius: 12, padding: 16, margin_horizontal: 20
- **Left:** "Total across 3 accounts" — body_medium, #666666
- **Right:** "£12,480.50" — title_large, #1800B1, font_weight: 700

### add_account_fab
- **Fixed position:** bottom: 80, right: 20 (above bottom nav)
- **Size:** 56×56, border_radius: 16
- **Style:** background: #1800B1, add icon in #FFFFFF, elevation: 6

---

## Interaction Patterns

| Target | Gesture | Outcome |
|---|---|---|
| account_card_1 | Tap | Navigate → /accounts/acc_checking_primary |
| account_card_2 | Tap | Navigate → /accounts/acc_savings_goal |
| account_card_3 | Tap | Navigate → /accounts/acc_business_main |
| tab_all / tab_checking / tab_savings / tab_business | Tap | Filter filteredAccounts, active chip switches to filled #1800B1 |
| add_account_fab | Tap | Opens account request form |
| accounts_help_icon | Tap | Opens account help overlay |
| Bottom nav | Tap any item | Replace top-level destination |

---

## Content Data

| Element | Value |
|---|---|
| Account 1 name | Primary Checking |
| Account 1 balance | £4,250.00 |
| Account 1 IBAN | DE89 3704 0044 0532 0130 00 |
| Account 2 name | Holiday Savings |
| Account 2 balance | £6,180.50 |
| Account 2 IBAN | DE89 3704 0044 0532 0131 00 |
| Account 3 name | Business Current |
| Account 3 balance | £2,050.00 |
| Account 3 IBAN | DE89 3704 0044 0532 0132 00 |
| Total balance | £12,480.50 |
| Account count | 3 |

---

## Design Notes

- **Color coding:** Each account type carries a distinct accent color applied consistently to the left border, balance text, and type badge — Checking: #1800B1, Savings: #008B8B, Business: #FF9800/#E65100. This allows instant visual identification without reading labels.
- **Typography hierarchy:** headline_large (title) > display_small (balance) > title_medium (account name) > body_small (IBAN) — 4 clear levels.
- **Spacing rhythm:** 20px horizontal gutters on all cards; 12px margin between cards; 24px top padding on header.
- **Accessibility:** Every account card has a full-sentence a11y label covering name, balance, and action hint. Filter chips expose role=tab with selected state. IBAN text uses monospace to aid digit grouping legibility.
- **Bottom nav:** Accounts tab is active (icon: account_balance); FAB clears bottom nav bar by positioning at bottom: 80.
- **Loading skeleton:** 3 grey boxes (120px × full width minus 40px) replace cards, maintaining spatial layout so no content jump on load.

---

_Generated by /idea export | 2026-05-25_
