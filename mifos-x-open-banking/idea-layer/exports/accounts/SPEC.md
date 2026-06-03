# SPEC — My Accounts

| Field         | Value              |
|---------------|--------------------|
| Feature       | accounts           |
| Flavor        | consumer           |
| Status        | designed           |
| Quality Score | 100                |
| ViewModel     | AccountsViewModel  |

---

## Overview

The My Accounts screen is the Consumer persona's account list view, accessible via the Accounts tab of the bottom navigation bar. It presents all bank accounts held by the authenticated user under a "My Accounts" headline with a free-text search bar (`accounts_search`) supporting search by name, number, or label. Accounts are **grouped by bank institution** with a per-bank section header showing the bank name, account count, and subtotal balance. The two demo groups are "Mifos Bank UK" (2 accounts, subtotal £10,430.50) and "Mifos Business UK" (1 account, subtotal £2,050.00). Each account card carries a 4dp left-border accent colour per account type (earth-green `#4C662B` for Checking, teal `#386663` for Savings, amber-decorative `#E8A317` border for Business), with account name, coloured type badge, balance in display_small, and IBAN in body_small monospace. A footer divider and total balance row (`£12,480.50` across 3 accounts) anchor the scroll. A FAB at bottom-right triggers account request. Data is loaded via the OBP Accounts endpoint on screen entry and on explicit retry; client-side `searchQuery` filtering applies to `filteredAccounts` without an additional network call; accounts are grouped into `groupedByBank` Map client-side.

**A11Y note (A11Y-002):** The Business Current card balance and badge texts use `#44483D` (8.91:1 / 7.25:1 — WCAG AA PASS) instead of `#E8A317` (2.17:1 / 1.68:1 — FAIL). The left-border accent `#E8A317` is decorative and unchanged.

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

| ID                         | Type       | Description                                                                                                  |
|----------------------------|------------|--------------------------------------------------------------------------------------------------------------|
| accounts_header            | stack      | Horizontal row, space_between, 20dp horizontal padding, 24dp top / 8dp bottom padding                       |
| accounts_title             | text       | "My Accounts" — Outfit/headline_large (32sp/Regular), color `#1A1C16`; heading level 1                      |
| accounts_help_icon         | icon       | `help_outline`, 24dp, color `#44483D`; on_click: `open_account_help`; focusable                             |
| accounts_search            | text_field | Outlined search field, leading `search` icon, trailing `close` icon; placeholder "Search by name, number or label"; border_radius: 28; bg `#F0F1E6`, border `#C5C8BA`, focus border `#4C662B`; 20dp horizontal margin; on_click: `search_accounts`; role: searchbox |
| bank_group_1_header        | stack      | Horizontal, space_between, 20dp padding, 24dp top / 8dp bottom; `account_balance` icon 18dp `#4C662B` + "Mifos Bank UK" title_small + "2 accounts" label_small; subtotal "£10,430.50" title_medium `#4C662B`; heading level 2 |
| account_card_1             | box        | `#FFFFFF` bg, 16dp radius, elevation 2, 4dp left border `#4C662B`; 24dp padding, 20dp horizontal margin, 16dp bottom margin; on_click → account-detail (acc_checking_primary) |
| acct1_label                | text       | "Primary Checking" — Outfit/title_medium (16sp/600), color `#1A1C16`                                        |
| acct1_type_badge           | box        | `#CDEDA3` bg, 6dp radius; text "CHECKING" — Outfit/label_small (11sp/500), color `#4C662B`                  |
| acct1_balance              | text       | "£4,250.00" — Outfit/display_small (32sp/600), color `#4C662B`                                              |
| acct1_iban_icon            | icon       | `account_box`, 16dp, color `#44483D`                                                                         |
| acct1_iban                 | text       | "DE89 3704 0044 0532 0130 00" — Outfit/body_small (12sp), color `#44483D`, monospace                        |
| account_card_2             | box        | `#FFFFFF` bg, 16dp radius, elevation 2, 4dp left border `#386663`; on_click → account-detail (acc_savings_goal) |
| acct2_label                | text       | "Holiday Savings" — Outfit/title_medium (16sp/600), color `#1A1C16`                                         |
| acct2_type_badge           | box        | `#CDEDA3` bg, 6dp radius; text "SAVINGS" — Outfit/label_small, color `#386663`                              |
| acct2_balance              | text       | "£6,180.50" — Outfit/display_small (32sp/600), color `#386663`                                              |
| acct2_iban_icon            | icon       | `account_box`, 16dp, color `#44483D`                                                                         |
| acct2_iban                 | text       | "DE89 3704 0044 0532 0131 00" — Outfit/body_small (12sp), color `#44483D`, monospace                        |
| bank_group_2_header        | stack      | Horizontal, space_between, 20dp padding, 24dp top / 8dp bottom; `account_balance` icon 18dp `#4C662B` + "Mifos Business UK" title_small + "1 account" label_small; subtotal "£2,050.00" title_medium `#4C662B`; heading level 2 |
| account_card_3             | box        | `#FFFFFF` bg, 16dp radius, elevation 2, 4dp left border `#E8A317` (decorative); on_click → account-detail (acc_business_main) |
| acct3_label                | text       | "Business Current" — Outfit/title_medium (16sp/600), color `#1A1C16`                                        |
| acct3_type_badge           | box        | `#CDEDA3` bg, 6dp radius; text "BUSINESS" — Outfit/label_small, color `#44483D` *(A11Y-002)*                |
| acct3_balance              | text       | "£2,050.00" — Outfit/display_small (32sp/600), color `#44483D` *(A11Y-002)*                                 |
| acct3_iban_icon            | icon       | `account_box`, 16dp, color `#44483D`                                                                         |
| acct3_iban                 | text       | "DE89 3704 0044 0532 0132 00" — Outfit/body_small (12sp), color `#44483D`, monospace                        |
| footer_divider             | divider    | `#E1E4D5`, 20dp horizontal margin                                                                            |
| total_balance_footer       | box        | `#F9FAEF` bg, 12dp radius, 16dp padding, 20dp horizontal margin, 4dp top margin, 80dp bottom margin         |
| total_balance_footer_label | text       | "Total across 3 accounts" — Outfit/body_medium (14sp/Regular), color `#44483D`                              |
| total_balance_footer_amount| text       | "£12,480.50" — Outfit/title_large (22sp/700), color `#4C662B`                                               |
| add_account_fab            | button     | FAB — `add` icon, `#4C662B` bg, `#FFFFFF` icon, 56×56dp, 16dp radius, elevation 6; fixed bottom 80dp right 20dp; on_click: `request_new_account` |

---

## States

| ID      | Trigger                                | Description                                                                                                                |
|---------|----------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| loading | Screen entry / RetryLoad event         | Header + search bar visible; 3 skeleton cards (120dp, `#E1E4D5`, 16dp radius) + skeleton footer (48dp) replace content   |
| content | Data load success                      | Header, search bar, both bank group headers, all 3 account cards, footer divider, total balance footer, and FAB visible   |
| empty   | No accounts / search returns no match  | Header only; empty card: illustration `no_accounts`, title "No accounts found", message "You don't have any accounts yet. Request a new account to get started.", CTA "Request Account" → `request_new_account` |
| error   | Network or API failure                 | Header only; error card: icon `error_outline`, title "Could not load accounts", message "We were unable to fetch your account list. Please check your connection and try again.", CTA "Retry" → `retry_load` |

---

## State Model

**ViewModel:** `AccountsViewModel`
**Screen State Type:** `AccountsScreenState`

| Name             | Type                           | Default           |
|------------------|--------------------------------|-------------------|
| isLoading        | `Boolean`                      | `true`            |
| accounts         | `List<BankAccount>`            | `emptyList()`     |
| filteredAccounts | `List<BankAccount>`            | `emptyList()`     |
| groupedByBank    | `Map<String, List<BankAccount>>`| `emptyMap()`      |
| searchQuery      | `String`                       | `""`              |
| totalBalance     | `BigDecimal`                   | `BigDecimal.ZERO` |
| error            | `UiError?`                     | `null`            |

**Events:** `RetryLoad`, `SearchQueryChanged(query: String)`, `AccountSelected(accountId: String)`, `RequestNewAccount`

**Actions:** `loadAccounts()` (triggers: ScreenOpened, RetryLoad), `searchAccounts(query)`, `navigateToDetail(accountId: String)`

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

| Endpoint                                              | Auth        | Tag      | Purpose                              |
|-------------------------------------------------------|-------------|----------|--------------------------------------|
| GET /obp/v3.0.0/banks/{bankId}/accounts               | DirectLogin | Accounts | Fetch all accounts for bank `gh.29.uk` |

---

## Design Tokens

| Token                           | Value                | Usage                                                                         |
|---------------------------------|----------------------|-------------------------------------------------------------------------------|
| colors.light.primary            | `#4C662B`            | Title, Checking card border + balance, bank group icons + subtotals, total footer amount, FAB background |
| colors.light.secondary          | `#386663`            | Savings card left-border accent, Savings balance text, Savings type badge text |
| colors.light.on_surface         | `#1A1C16`            | Account name labels in all cards, search field text                           |
| colors.light.on_surface_variant | `#44483D`            | Help icon, search placeholder + field border, IBAN text, footer label, Business balance + badge (A11Y-002) |
| colors.light.primary_container  | `#CDEDA3`            | Type badge background on all 3 cards                                          |
| colors.light.pending            | `#E8A317`            | Business Current card left-border accent (decorative only)                    |
| colors.light.surface            | `#FFFFFF`            | Account card backgrounds                                                      |
| colors.light.surface_container  | `#F0F1E6`            | Search bar background                                                         |
| colors.light.outline_variant    | `#C5C8BA`            | Search bar border (idle), footer divider                                      |
| colors.light.surface_variant    | `#E1E4D5`            | Footer divider, skeleton card shimmer                                         |
| colors.light.background         | `#F9FAEF`            | Screen background, total balance footer background                            |
| typography.headline_large       | Outfit 32sp/Regular  | "My Accounts" screen title                                                    |
| typography.display_small        | Outfit 32sp/600      | Account balance amounts (all 3 cards)                                         |
| typography.title_large          | Outfit 22sp/700      | Total balance footer amount                                                   |
| typography.title_medium         | Outfit 16sp/600      | Account name label in each card                                               |
| typography.title_small          | Outfit 14sp/500      | Bank group header institution name                                            |
| typography.body_medium          | Outfit 14sp/Regular  | Total footer label "Total across 3 accounts"                                  |
| typography.body_small           | Outfit 12sp/Regular  | IBAN text in all cards (monospace)                                            |
| typography.label_small          | Outfit 11sp/500      | Account type badge text, bank group account count                             |
| radius.lg                       | 16dp                 | Account card corner radius                                                    |
| radius.xl                       | 28dp                 | Search bar border radius                                                      |
| radius.md                       | 12dp                 | Total balance footer corner radius                                            |
| elevation.level2                | 3dp                  | Account card elevation                                                        |
| elevation.level3                | 6dp                  | FAB elevation                                                                 |
| spacing.lg                      | 24dp                 | Card padding, header top padding, bank group header top padding               |
| spacing.md                      | 16dp                 | Card horizontal margin, footer padding                                        |
| spacing.sm                      | 8dp                  | IBAN row icon-text gap, bank group title stack spacing, card bottom margin    |

---

_Generated by /idea export | 2026-06-02_
