# SPEC — Home Dashboard

| Field         | Value         |
|---------------|---------------|
| Feature       | home          |
| Flavor        | consumer      |
| Status        | approved      |
| Quality Score | 95            |
| ViewModel     | HomeViewModel |

---

## Overview

The Home Dashboard is the primary landing screen for Consumer persona users after authentication. It shows a personalized greeting ("Good morning, Alex"), today's date, a hero primary checking account card (#4C662B fill) with the £4,250.00 balance, masked IBAN (•••• 0130), and three quick action buttons (Send Money, Beneficiaries, View Cards). A total balance chip (#CDEDA3) aggregates all 3 accounts to £12,480.50. Below this, a Recent Transactions section lists the 3 most recent entries: Tesco Supermarket (−£42.50 debit), Salary Payment (+£3,200.00 credit), EDF Energy (−£94.20 debit), each with a coloured icon container, merchant name, date/category, amount, and DEBIT/CREDIT badge. A Services section at the bottom provides tiles for Standing Orders, ATM & Branches, and FX Rates. The screen uses a 5-tab bottom navigation bar. Data is fetched from OBP Accounts and Transactions endpoints on screen entry and retry.

---

## Screens

| ID           | Name           | Route | Layout | Scroll   |
|--------------|----------------|-------|--------|----------|
| home_content | Home Dashboard | /home | Column | Vertical |

**Shell:** Bottom navigation bar with 5 items (Home active by default).

| Nav Item | ID           | Icon            | Target    | Active |
|----------|--------------|-----------------|-----------|--------|
| Home     | nav_home     | home            | home      | true   |
| Accounts | nav_accounts | account_balance | accounts  | false  |
| Pay      | nav_pay      | send            | send-money| false  |
| Cards    | nav_cards    | credit_card     | cards     | false  |
| More     | nav_more     | more_horiz      | settings  | false  |

---

## Components

| ID                          | Type   | Description                                                                                          |
|-----------------------------|--------|------------------------------------------------------------------------------------------------------|
| greeting_text               | text   | "Good morning, Alex" — Outfit/headline_medium, #4C662B, lg top padding, md horizontal padding       |
| greeting_date               | text   | "Monday, 25 May 2026" — Outfit/body_medium, #44483D, md horizontal padding                         |
| primary_account_card        | box    | #4C662B fill, 20dp radius, lg padding, md horizontal margin, 4dp elevation                         |
| account_card_label          | text   | "Primary Checking" — Outfit/label_large, #FFFFFF                                                    |
| account_card_balance        | text   | "£4,250.00" — Outfit/display_small, #FFFFFF, sm top pad, xs bottom pad                             |
| account_card_iban           | text   | "•••• •••• •••• 0130" — Outfit/body_medium, #FFFFFF, md bottom pad                                |
| quick_actions_row           | stack  | Horizontal, 8dp spacing — contains 3 quick action buttons                                           |
| btn_send_money              | button | "Send Money" — filled, #FFFFFF fill + #4C662B text, 12dp radius, sm padding, Outfit/label_medium    |
| btn_add_beneficiary         | button | "Beneficiaries" — outlined, #FFFFFF border + text, 12dp radius, sm padding                         |
| btn_view_cards              | button | "View Cards" — outlined, #FFFFFF border + text, 12dp radius, sm padding                            |
| total_balance_chip          | box    | #CDEDA3 fill, 12dp radius, md horizontal + 10dp vertical padding, md horizontal margin              |
| total_balance_icon          | icon   | account_balance_wallet, 16dp, #4C662B                                                               |
| total_balance_text          | text   | "Total across 3 accounts: £12,480.50" — Outfit/label_medium, #4C662B                               |
| recent_transactions_header  | stack  | Horizontal, space-between, md padding — title + "View All" link                                     |
| recent_transactions_title   | text   | "Recent Transactions" — Outfit/title_large, #1A1C16, heading level 2                               |
| view_all_link               | link   | "View All" — Outfit/label_medium, #4C662B → navigates to transactions                              |
| transaction_row_1           | box    | Tesco Supermarket: white card, 12dp radius, 1dp elevation; shopping_cart icon on #CDEDA3 circle    |
| txn1_merchant               | text   | "Tesco Supermarket" — Outfit/body_large, #1A1C16                                                   |
| txn1_date                   | text   | "23 May 2026 · Groceries" — Outfit/body_small, #44483D                                              |
| txn1_amount                 | text   | "−£42.50" — Outfit/body_large, #BA1A1A, bold                                                       |
| txn1_badge                  | box    | "DEBIT" badge — #CDEDA3 fill, 4dp radius, Outfit/label_small, #BA1A1A text                         |
| transaction_row_2           | box    | Salary Payment: white card; payments icon on #CDEDA3 circle                                         |
| txn2_merchant               | text   | "Salary Payment" — Outfit/body_large, #1A1C16                                                      |
| txn2_date                   | text   | "22 May 2026 · Income" — Outfit/body_small, #44483D                                                 |
| txn2_amount                 | text   | "+£3,200.00" — Outfit/body_large, #4C662B, bold                                                    |
| txn2_badge                  | box    | "CREDIT" badge — #CDEDA3 fill, 4dp radius, Outfit/label_small, #4C662B text                        |
| transaction_row_3           | box    | EDF Energy: white card; bolt icon on #CDEDA3 circle                                                 |
| txn3_merchant               | text   | "EDF Energy" — Outfit/body_large, #1A1C16                                                          |
| txn3_date                   | text   | "20 May 2026 · Utilities" — Outfit/body_small, #44483D                                              |
| txn3_amount                 | text   | "−£94.20" — Outfit/body_large, #BA1A1A, bold                                                       |
| txn3_badge                  | box    | "DEBIT" badge — #CDEDA3 fill, 4dp radius, Outfit/label_small, #BA1A1A text                         |
| services_section_title      | text   | "Services" — Outfit/title_large, #1A1C16, heading level 2                                          |
| services_grid               | stack  | Horizontal, 12dp spacing, md horizontal pad, flex_wrap — 3 service tiles                           |
| service_standing_orders     | box    | #CDEDA3 fill, 16dp radius, 16dp pad — repeat icon (#4C662B) + "Standing Orders" label              |
| service_atm_locator         | box    | #DCE7C8 fill, 16dp radius, 16dp pad — location_on icon (#386663) + "ATM & Branches" label          |
| service_fx_rates            | box    | #CDEDA3 fill, 16dp radius, 16dp pad — currency_exchange icon (#386663) + "FX Rates" label          |

---

## States

| ID      | Trigger                       | Description                                                                                   |
|---------|-------------------------------|-----------------------------------------------------------------------------------------------|
| loading | Screen entry / RetryLoad      | Greeting + date visible; account card replaced by skeleton box (200dp); 2 skeleton txn rows  |
| content | Data load success             | Full screen: account card + balance chip + 3 transactions + services grid + bottom nav        |
| error   | Network or auth failure       | Greeting + date + error card ("Could not load your account") with retry button                |
| empty   | Account data returns empty    | Greeting + date + empty card ("No accounts yet") with "Set Up Account" CTA                   |

---

## State Model

**ViewModel:** `HomeViewModel`
**Screen State Type:** `HomeScreenState`

| Name               | Type                       | Default     |
|--------------------|----------------------------|-------------|
| isLoading          | Boolean                    | true        |
| primaryAccount     | AccountSummary?            | null        |
| totalBalance       | BigDecimal?                | null        |
| totalAccountCount  | Int                        | 0           |
| recentTransactions | List\<TransactionSummary\> | emptyList() |
| error              | UiError?                   | null        |
| greetingName       | String                     | "Alex"      |

**Events:** `RetryLoad`, `NavigateToTransactions`, `NavigateToSendMoney`, `NavigateToAccounts`, `NavigateToBeneficiaries`, `NavigateToCards`

**Actions:** `loadDashboardData()` (triggers: RetryLoad, ScreenOpened), `navigateTo(screen_id)`

**DI Dependencies:** `AccountsRepository`, `TransactionsRepository`, `SessionManager`

**Errors:**
- `network_error`: "Could not connect to banking services. Please try again."
- `auth_error`: "Session expired. Please log in again."
- `unknown_error`: "Something went wrong. Please try again."

---

## Navigation

| From | To             | Trigger                           | Type |
|------|----------------|-----------------------------------|------|
| home | send-money     | btn_send_money tap                | push |
| home | beneficiaries  | btn_add_beneficiary tap           | push |
| home | cards          | btn_view_cards tap                | push |
| home | transactions   | view_all_link tap                 | push |
| home | standing-orders| service_standing_orders tap       | push |
| home | atm-locator    | service_atm_locator tap           | push |
| home | fx-rates       | service_fx_rates tap              | push |
| home | accounts       | nav_accounts bottom tab tap       | tab  |
| home | send-money     | nav_pay bottom tab tap            | tab  |
| home | cards          | nav_cards bottom tab tap          | tab  |
| home | settings       | nav_more bottom tab tap           | tab  |

---

## API Endpoints

| Endpoint                                                                  | Auth        | Tag          | Purpose                                         |
|---------------------------------------------------------------------------|-------------|--------------|-------------------------------------------------|
| GET /obp/v3.0.0/banks/{bankId}/accounts                                   | DirectLogin | Accounts     | Fetch accounts for bank gh.29.uk                |
| GET /obp/v3.0.0/banks/{bankId}/accounts/{accountId}/owner/transactions    | DirectLogin | Transactions | Fetch 5 most recent transactions DESC (limit=5) |
| GET /obp/v3.0.0/my/accounts                                               | DirectLogin | Accounts     | Cross-bank aggregation for total balance chip   |

---

## Design Tokens

| Token                          | Value     | Usage                                                               |
|--------------------------------|-----------|---------------------------------------------------------------------|
| colors.light.primary           | #4C662B   | Account card fill, greeting text, total balance chip text+icon, "View All" link, credit amounts, service tile icons |
| colors.light.primary_container | #CDEDA3   | Total balance chip fill, txn icon containers, DEBIT/CREDIT badge fill, Standing Orders + FX tile fill |
| colors.light.nav_active_indicator | #DCE7C8 | ATM tile fill                                                      |
| colors.light.secondary         | #386663   | ATM + FX service tile icon + label color                            |
| colors.light.error             | #BA1A1A   | Debit amounts (−£42.50, −£94.20), DEBIT badge text                |
| colors.light.surface           | #FFFFFF   | Transaction row card fill, Send Money button fill                   |
| colors.light.background        | #F9FAEF   | Screen base                                                         |
| colors.light.on_surface        | #1A1C16   | Merchant names, section headers                                     |
| colors.light.on_surface_variant| #44483D   | Date/category text (23 May 2026 · Groceries), bolt icon (a11y fix)  |
| typography.headline_medium     | Outfit 28sp | Greeting text                                                     |
| typography.display_small       | Outfit 32sp/600 | Account balance                                               |
| typography.title_large         | Outfit 22sp | "Recent Transactions" + "Services" section headers              |
| typography.label_large         | Outfit 14sp/500 | Account card type label "Primary Checking"                  |
| typography.label_medium        | Outfit 12sp/500 | Total balance chip, quick action button labels              |
| typography.body_large          | Outfit 16sp/400 | Transaction merchant names, amounts                         |
| typography.body_medium         | Outfit 14sp/400 | Greeting date, account IBAN                                 |
| typography.body_small          | Outfit 12sp/400 | Transaction date/category lines                             |
| typography.label_small         | Outfit 11sp/500 | DEBIT / CREDIT badge labels                                 |
| radius.sm                      | 8dp       | Bottom nav active pill indicator                                    |
| radius.md                      | 12dp      | Quick action buttons, total balance chip, transaction cards         |
| radius.lg                      | 16dp      | Service tiles, FAB                                                  |
| elevation.level1               | 1dp       | Transaction cards                                                   |
| elevation.level2               | 3dp       | Account card (specified as 4dp in source)                          |

---

_Generated by /idea export | 2026-06-02 (API endpoints resynced to v3.0.0 owner-transactions paths per api.yaml)_
