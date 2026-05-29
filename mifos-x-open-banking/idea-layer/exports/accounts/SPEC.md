# SPEC — My Accounts

| Field         | Value              |
|---------------|--------------------|
| Feature       | accounts           |
| Flavor        | consumer           |
| Status        | approved           |
| Quality Score | 94                 |
| ViewModel     | AccountsViewModel  |

---

## Overview

The My Accounts screen is the Consumer persona's account list view, accessible via the Accounts tab of the bottom navigation bar. It presents all bank accounts held by the authenticated user under a "My Accounts" headline with a horizontally scrollable type filter tab row (ALL selected by default, plus CHECKING, SAVINGS, BUSINESS). Each account is rendered as a vertically stacked card with a 4dp left-border accent colour per account type: earth-green (`#4C662B`) for Checking, teal (`#386663`) for Savings, and amber-outlined (`#E8A317` border) for Business. Every card shows the account label in title_medium, a coloured type badge, the balance in display_small, and the IBAN in body_small monospace. Tapping any card navigates to the Account Detail screen. A footer row on `#F9FAEF` aggregates the total balance across all accounts. A FAB fixed at bottom-right allows the user to request a new account. Data is loaded via the OBP Accounts endpoint on screen entry and on explicit retry; client-side filter applies to `filteredAccounts` without a new network request.

**A11Y note (A11Y-002, applied in ui.yaml):** The Business Current card balance text and type badge text were updated from `#E8A317` (contrast ratio 2.17:1 / 1.68:1 — WCAG AA FAIL) to `#44483D` (8.91:1 / 7.25:1 — WCAG AA PASS). The left-border accent colour `#E8A317` is decorative and remains unchanged.

---

## Screens

| ID               | Name        | Route     | Layout | Scroll   |
|------------------|-------------|-----------|--------|----------|
| accounts_content | My Accounts | /accounts | Column | Vertical |

**Shell:** Consumer bottom navigation bar with 5 items. Accounts tab active.

| Nav Item | ID           | Icon            | Target     | Active |
|----------|--------------|-----------------|------------|--------|
| Home     | nav_home     | home            | home       | false  |
| Accounts | nav_accounts | account_balance | accounts   | true   |
| Pay      | nav_pay      | send            | send-money | false  |
| Cards    | nav_cards    | credit_card     | cards      | false  |
| More     | nav_more     | more_horiz      | settings   | false  |

---

## Components

| ID                         | Type    | Description                                                                                               |
|----------------------------|---------|-----------------------------------------------------------------------------------------------------------|
| accounts_header            | stack   | Horizontal row, space_between, 20dp horizontal padding, 24dp top / 8dp bottom padding                    |
| accounts_title             | text    | "My Accounts" — Outfit/headline_large (32sp/Regular), color `#1A1C16`; heading level 1                   |
| accounts_help_icon         | icon    | `help_outline`, 24dp, color `#44483D`; on_click: `open_account_help`; focusable                          |
| account_type_tabs          | stack   | Horizontal scroll, 8dp spacing, 20dp horizontal / 16dp vertical padding; tablist role                     |
| tab_all                    | button  | "ALL" — filled `#4C662B` bg / `#FFFFFF` text, 20dp pill radius, selected; on_click: `filter_accounts(all)` |
| tab_checking               | button  | "CHECKING" — outlined `#E1E4D5` border / `#44483D` text, 20dp pill radius; on_click: `filter_accounts(checking)` |
| tab_savings                | button  | "SAVINGS" — outlined `#E1E4D5` border / `#44483D` text, 20dp pill radius; on_click: `filter_accounts(savings)` |
| tab_business               | button  | "BUSINESS" — outlined `#E1E4D5` border / `#44483D` text, 20dp pill radius; on_click: `filter_accounts(business)` |
| account_card_1             | box     | `#FFFFFF` bg, 16dp radius, elevation 2, 4dp left border `#4C662B`; 24dp padding, 20dp margin, 16dp bottom margin; on_click → account-detail (acc_checking_primary) |
| acct1_label                | text    | "Primary Checking" — Outfit/title_medium (16sp/600), color `#1A1C16`                                     |
| acct1_type_badge           | box     | `#CDEDA3` bg, 6dp radius; text "CHECKING" — Outfit/label_small (11sp/500), color `#4C662B`               |
| acct1_balance              | text    | "£4,250.00" — Outfit/display_small (32sp/600), color `#4C662B`                                           |
| acct1_iban_icon            | icon    | `account_box`, 16dp, color `#44483D`                                                                      |
| acct1_iban                 | text    | "DE89 3704 0044 0532 0130 00" — Outfit/body_small (12sp), color `#44483D`, monospace                     |
| account_card_2             | box     | `#FFFFFF` bg, 16dp radius, elevation 2, 4dp left border `#386663`; on_click → account-detail (acc_savings_goal) |
| acct2_label                | text    | "Holiday Savings" — Outfit/title_medium (16sp/600), color `#1A1C16`                                      |
| acct2_type_badge           | box     | `#CDEDA3` bg, 6dp radius; text "SAVINGS" — Outfit/label_small, color `#386663`                           |
| acct2_balance              | text    | "£6,180.50" — Outfit/display_small (32sp/600), color `#386663`                                           |
| acct2_iban_icon            | icon    | `account_box`, 16dp, color `#44483D`                                                                      |
| acct2_iban                 | text    | "DE89 3704 0044 0532 0131 00" — Outfit/body_small (12sp), color `#44483D`, monospace                     |
| account_card_3             | box     | `#FFFFFF` bg, 16dp radius, elevation 2, 4dp left border `#E8A317`; on_click → account-detail (acc_business_main) |
| acct3_label                | text    | "Business Current" — Outfit/title_medium (16sp/600), color `#1A1C16`                                     |
| acct3_type_badge           | box     | `#CDEDA3` bg, 6dp radius; text "BUSINESS" — Outfit/label_small, color `#44483D` *(A11Y-002 fix: was #E8A317)* |
| acct3_balance              | text    | "£2,050.00" — Outfit/display_small (32sp/600), color `#44483D` *(A11Y-002 fix: was #E8A317)*             |
| acct3_iban_icon            | icon    | `account_box`, 16dp, color `#44483D`                                                                      |
| acct3_iban                 | text    | "DE89 3704 0044 0532 0132 00" — Outfit/body_small (12sp), color `#44483D`, monospace                     |
| footer_divider             | divider | `#E1E4D5`, 20dp horizontal margin                                                                         |
| total_balance_footer       | box     | `#F9FAEF` bg, 12dp radius, 16dp padding, 20dp horizontal margin, 4dp top margin, 80dp bottom margin       |
| total_balance_footer_label | text    | "Total across 3 accounts" — Outfit/body_medium (14sp/Regular), color `#44483D`                           |
| total_balance_footer_amount| text    | "£12,480.50" — Outfit/title_large (22sp/700), color `#4C662B`                                            |
| add_account_fab            | button  | FAB — `add` icon, `#4C662B` bg, `#FFFFFF` icon, 56×56dp, 16dp radius, elevation 6; fixed bottom 80dp right 20dp; on_click: `request_new_account` |

---

## States

| ID      | Trigger                                   | Description                                                                                          |
|---------|-------------------------------------------|------------------------------------------------------------------------------------------------------|
| loading | Screen entry / RetryLoad event            | Header row + filter tabs visible; 3 skeleton cards (120dp, `#E1E4D5`, 16dp radius) replace account cards; skeleton total footer (48dp) |
| content | Data load success                         | All 3 account cards, footer divider, total balance footer, and FAB visible; filter tabs operative     |
| empty   | No accounts match filter / no accounts    | Header only; empty card: illustration `no_accounts`, title "No accounts found", message "You don't have any accounts matching this filter. Try a different category or request a new account.", CTA "Request Account" → `request_new_account` |
| error   | Network or API failure                    | Header only; error card: icon `error_outline`, title "Could not load accounts", message "We were unable to fetch your account list. Please check your connection and try again.", CTA "Retry" → `retry_load` |

---

## State Model

**ViewModel:** `AccountsViewModel`
**Screen State Type:** `AccountsScreenState`

| Name             | Type                  | Default                 |
|------------------|-----------------------|-------------------------|
| isLoading        | `Boolean`             | `true`                  |
| accounts         | `List<BankAccount>`   | `emptyList()`           |
| filteredAccounts | `List<BankAccount>`   | `emptyList()`           |
| activeFilter     | `AccountTypeFilter`   | `AccountTypeFilter.ALL` |
| totalBalance     | `BigDecimal`          | `BigDecimal.ZERO`       |
| error            | `UiError?`            | `null`                  |

**Events:** `RetryLoad`, `FilterChanged(filter: AccountTypeFilter)`, `AccountSelected(accountId: String)`, `RequestNewAccount`

**Actions:** `loadAccounts()` (triggers: ScreenOpened, RetryLoad), `filterAccounts(AccountTypeFilter)`, `navigateToDetail(accountId: String)`

**DI Dependencies:** `AccountsRepository`, `SessionManager`

**Errors:**
- `network_error`: "Network unavailable. Please try again."
- `auth_error`: "Session expired. Please log in again."

---

## Navigation

| From     | To             | Trigger                                          | Type |
|----------|----------------|--------------------------------------------------|------|
| accounts | account-detail | account_card_1 tap (acc_checking_primary)        | push |
| accounts | account-detail | account_card_2 tap (acc_savings_goal)            | push |
| accounts | account-detail | account_card_3 tap (acc_business_main)           | push |
| accounts | home           | nav_home bottom tab tap                          | tab  |
| accounts | send-money     | nav_pay bottom tab tap                           | tab  |
| accounts | cards          | nav_cards bottom tab tap                         | tab  |
| accounts | settings       | nav_more bottom tab tap                          | tab  |

---

## API Endpoints

| Endpoint                                        | Auth        | Tag      | Purpose                                         |
|-------------------------------------------------|-------------|----------|-------------------------------------------------|
| GET /obp/v5.1.0/banks/{bankId}/accounts         | DirectLogin | Accounts | Fetch all accounts for bank `gh.29.uk`          |

---

## Design Tokens

| Token                           | Value        | Usage                                                                        |
|---------------------------------|--------------|------------------------------------------------------------------------------|
| colors.light.primary            | `#4C662B`    | "My Accounts" title, Checking card border + balance + tab pill, total footer amount, FAB background |
| colors.light.secondary          | `#386663`    | Savings card left-border accent, Savings balance text, Savings type badge text |
| colors.light.on_surface         | `#1A1C16`    | Account name text in all cards                                                |
| colors.light.on_surface_variant | `#44483D`    | Help icon, unselected tab text, IBAN text, total footer label, Business balance + badge (A11Y-002) |
| colors.light.primary_container  | `#CDEDA3`    | Type badge background on all 3 cards                                          |
| colors.light.pending            | `#E8A317`    | Business Current card left-border accent (decorative only)                    |
| colors.light.surface            | `#FFFFFF`    | Account card backgrounds                                                      |
| colors.light.surface_variant    | `#E1E4D5`    | Footer divider, unselected tab borders, skeleton card shimmer                 |
| colors.light.background         | `#F9FAEF`    | Screen background, total balance footer background                            |
| typography.headline_large       | Outfit 32sp/Regular  | "My Accounts" screen title                                          |
| typography.display_small        | Outfit 32sp/600      | Account balance amounts (all 3 cards)                               |
| typography.title_large          | Outfit 22sp/700      | Total balance footer amount                                         |
| typography.title_medium         | Outfit 16sp/600      | Account name label in each card                                     |
| typography.body_medium          | Outfit 14sp/Regular  | Total footer label "Total across 3 accounts"                        |
| typography.body_small           | Outfit 12sp/Regular  | IBAN text in all cards (monospace)                                  |
| typography.label_medium         | Outfit 12sp/500      | Tab button labels (ALL, CHECKING, SAVINGS, BUSINESS)                |
| typography.label_small          | Outfit 11sp/500      | Account type badge text in each card                                |
| radius.lg                       | 16dp         | Account card corner radius                                                    |
| radius.md                       | 12dp         | Total balance footer corner radius                                            |
| elevation.level2                | 3dp          | Account card elevation                                                        |
| elevation.level3                | 6dp          | FAB elevation                                                                 |
| spacing.lg                      | 24dp         | Card padding, header top padding                                              |
| spacing.md                      | 16dp         | Card horizontal margin, tab vertical padding, footer padding                  |
| spacing.sm                      | 8dp          | IBAN row icon-text gap, tab horizontal spacing, card bottom margin            |

---

_Generated by /idea export | 2026-05-30_
