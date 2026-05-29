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

The My Accounts screen is the Consumer persona's account list view, accessible via the Accounts tab of the bottom navigation bar. It displays all bank accounts held by the authenticated user, organized under a "My Accounts" headline with a type filter tab row (ALL, CHECKING, SAVINGS, BUSINESS). Each account appears as a vertically-stacked card with a left border accent color per account type, showing the account label, type badge, balance in display_small, and IBAN. Tapping any card navigates to the Account Detail screen. A footer aggregates the total balance across all 3 accounts (£12,480.50). A FAB in the bottom-right allows requesting a new account. Data is fetched from the OBP Accounts endpoint and filtered client-side.

---

## Screens

| ID               | Name        | Route     | Layout | Scroll   |
|------------------|-------------|-----------|--------|----------|
| accounts_content | My Accounts | /accounts | Column | Vertical |

**Shell:** Consumer bottom navigation bar with 5 items (Accounts active).

| Nav Item | ID           | Icon            | Target      |
|----------|--------------|-----------------|-------------|
| Home     | nav_home     | home            | home        |
| Accounts | nav_accounts | account_balance | accounts    |
| Pay      | nav_pay      | send            | send-money  |
| Cards    | nav_cards    | credit_card     | cards       |
| More     | nav_more     | more_horiz      | settings    |

---

## Components

| ID                        | Type   | Description                                                                                           |
|---------------------------|--------|-------------------------------------------------------------------------------------------------------|
| accounts_title            | text   | "My Accounts" — headline_large (32sp), color `#1A1C16`; heading level 1                              |
| accounts_help_icon        | icon   | `help_outline`, 24dp, color `#44483D`; on_click opens account help                                   |
| account_type_tabs         | stack  | Horizontal scrollable tab row: ALL (selected), CHECKING, SAVINGS, BUSINESS                            |
| tab_all                   | button | "ALL" — filled `#4C662B`/white, pill radius 20dp, selected state                                     |
| tab_checking              | button | "CHECKING" — outlined `#E1E4D5` border / `#44483D` text, unselected                                  |
| tab_savings               | button | "SAVINGS" — outlined `#E1E4D5` border / `#44483D` text, unselected                                   |
| tab_business              | button | "BUSINESS" — outlined `#E1E4D5` border / `#44483D` text, unselected                                  |
| account_card_1            | box    | White card, radius 16dp, elevation 2, left border 4dp `#4C662B` — Primary Checking, £4,250.00        |
| acct1_label               | text   | "Primary Checking" — title_medium (16sp/SemiBold), color `#1A1C16`                                   |
| acct1_type_badge          | box    | `#CDEDA3` bg, 6dp radius; text "CHECKING" label_small `#4C662B`                                      |
| acct1_balance             | text   | "£4,250.00" — display_small (32sp/SemiBold), color `#4C662B`                                         |
| acct1_iban                | text   | "DE89 3704 0044 0532 0130 00" — body_small monospace, color `#44483D`                                 |
| account_card_2            | box    | White card, radius 16dp, elevation 2, left border 4dp `#386663` — Holiday Savings, £6,180.50         |
| acct2_label               | text   | "Holiday Savings" — title_medium (16sp/SemiBold), color `#1A1C16`                                    |
| acct2_type_badge          | box    | `#CDEDA3` bg, 6dp radius; text "SAVINGS" label_small `#386663` (secondary)                           |
| acct2_balance             | text   | "£6,180.50" — display_small (32sp/SemiBold), color `#386663`                                         |
| acct2_iban                | text   | "DE89 3704 0044 0532 0131 00" — body_small monospace, color `#44483D`                                 |
| account_card_3            | box    | White card, radius 16dp, elevation 2, left border 4dp `#E8A317` — Business Current, £2,050.00        |
| acct3_label               | text   | "Business Current" — title_medium (16sp/SemiBold), color `#1A1C16`                                   |
| acct3_type_badge          | box    | `#CDEDA3` bg, 6dp radius; text "BUSINESS" label_small `#44483D` (a11y-corrected)                     |
| acct3_balance             | text   | "£2,050.00" — display_small (32sp/SemiBold), color `#44483D` (a11y-corrected)                        |
| acct3_iban                | text   | "DE89 3704 0044 0532 0132 00" — body_small monospace, color `#44483D`                                 |
| footer_divider            | divider| `#E1E4D5` separator above total footer                                                               |
| total_balance_footer      | box    | `#F9FAEF` bg, 12dp radius, 16dp padding — aggregated total across 3 accounts                         |
| total_balance_footer_label| text   | "Total across 3 accounts" — body_medium (14sp), color `#44483D`                                      |
| total_balance_footer_amount| text  | "£12,480.50" — title_large (22sp/Bold), color `#4C662B`                                              |
| add_account_fab           | button | FAB `add` icon — `#4C662B` fill, white icon, 56×56dp, 16dp radius; fixed bottom-right               |

---

## States

| ID      | Trigger                                | Description                                                                                     |
|---------|----------------------------------------|-------------------------------------------------------------------------------------------------|
| loading | Screen entry / RetryLoad               | Header + filter tabs visible; 3 skeleton cards (120dp each) in place of account cards          |
| content | Data load success                      | All 3 account cards, footer, FAB visible; filter tabs operative                                 |
| empty   | No accounts match filter or none exist | Empty card: "No accounts found" + "Request Account" CTA button                                 |
| error   | Network or API failure                 | Error card: "Could not load accounts" + retry button                                            |

---

## State Model

**ViewModel:** `AccountsViewModel`
**Screen State Type:** `AccountsScreenState`

| Name             | Type                  | Default                  |
|------------------|-----------------------|--------------------------|
| isLoading        | `Boolean`             | `true`                   |
| accounts         | `List<BankAccount>`   | `emptyList()`            |
| filteredAccounts | `List<BankAccount>`   | `emptyList()`            |
| activeFilter     | `AccountTypeFilter`   | `AccountTypeFilter.ALL`  |
| totalBalance     | `BigDecimal`          | `BigDecimal.ZERO`        |
| error            | `UiError?`            | `null`                   |

**Events:** `RetryLoad`, `FilterChanged(filter: AccountTypeFilter)`, `AccountSelected(accountId: String)`, `RequestNewAccount`

**Actions:** `loadAccounts()` (triggers: ScreenOpened, RetryLoad), `filterAccounts(AccountTypeFilter)`, `navigateToDetail(accountId)`

**DI Dependencies:** `AccountsRepository`, `SessionManager`

**Errors:**
- `network_error`: "Network unavailable. Please try again."
- `auth_error`: "Session expired. Please log in again."

---

## Navigation

| From     | To             | Trigger                              | Type |
|----------|----------------|--------------------------------------|------|
| accounts | account-detail | account_card_1 tap (acc_checking_primary) | push |
| accounts | account-detail | account_card_2 tap (acc_savings_goal)     | push |
| accounts | account-detail | account_card_3 tap (acc_business_main)    | push |
| accounts | home           | nav_home bottom tab tap              | tab  |
| accounts | send-money     | nav_pay bottom tab tap               | tab  |
| accounts | cards          | nav_cards bottom tab tap             | tab  |
| accounts | settings       | nav_more bottom tab tap              | tab  |

---

## API Endpoints

| Endpoint                                     | Auth        | Tag      | Purpose                                          |
|----------------------------------------------|-------------|----------|--------------------------------------------------|
| GET /obp/v5.1.0/banks/{bankId}/accounts       | DirectLogin | Accounts | Fetch all accounts for bank gh.29.uk             |

---

## Design Tokens

| Token                           | Value     | Usage                                                             |
|---------------------------------|-----------|-------------------------------------------------------------------|
| colors.light.primary            | `#4C662B` | Accounts title, Checking card accent + balance + tab pill, total balance amount, FAB |
| colors.light.secondary          | `#386663` | Savings card left-border accent, Savings balance + type badge text|
| colors.light.on_surface         | `#1A1C16` | Account name text in all cards                                    |
| colors.light.on_surface_variant | `#44483D` | Help icon, tab unselected text, IBAN text, total label, Business balance (a11y) |
| colors.light.primary_container  | `#CDEDA3` | Account type badge background on all cards                        |
| colors.light.pending            | `#E8A317` | Business Current card left-border accent                          |
| colors.light.surface            | `#FFFFFF` | Account card backgrounds                                          |
| colors.light.surface_variant    | `#E1E4D5` | Footer divider, unselected tab borders                            |
| colors.light.background         | `#F9FAEF` | Screen background, total footer background                        |
| typography.headline_large       | 32sp/Regular | "My Accounts" screen title                                    |
| typography.display_small        | 32sp/SemiBold | Account balance amounts                                      |
| typography.title_large          | 22sp/Bold    | Total balance footer amount                                    |
| typography.title_medium         | 16sp/SemiBold| Account name in cards                                         |
| typography.body_medium          | 14sp/Regular | Total footer label                                            |
| typography.body_small           | 12sp/Regular | IBAN text in cards                                            |
| typography.label_medium         | 12sp/Medium  | Tab button labels                                             |
| typography.label_small          | 11sp/Medium  | Account type badge text                                       |
| radius.lg                       | 16dp      | Account card corner radius                                        |
| radius.md                       | 12dp      | Total footer corner radius, FAB radius                            |
| elevation.level2                | 3dp       | Account card elevation                                            |
| spacing.lg                      | 24dp      | Accounts header top padding                                       |
| spacing.md                      | 16dp      | Card horizontal margin, tab horizontal padding                    |

---

_Generated by /idea export | 2026-05-29_
