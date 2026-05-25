# SPEC — Home Dashboard

| Field         | Value         |
|---------------|---------------|
| Feature       | home          |
| Flavor        | consumer      |
| Status        | enriched      |
| Quality Score | 82            |
| ViewModel     | HomeViewModel |

---

## Overview

The Home Dashboard is the primary landing screen for Consumer persona users after authentication. It displays a personalized greeting, a hero account card showing the primary checking account balance and quick actions, a total balance chip aggregating across all accounts, a recent transactions list (up to 5 entries), and a services grid with quick-access tiles for Standing Orders, ATM & Branches, and FX Rates. The screen has a bottom navigation bar with five tabs: Home, Accounts, Pay, Cards, and More. Data is fetched from OBP APIs on screen entry and on retry.

---

## Screens

| ID           | Name           | Route | Layout | Scroll   |
|--------------|----------------|-------|--------|----------|
| home_content | Home Dashboard | /home | Column | Vertical |

**Shell:** Bottom navigation bar with 5 items (Home active by default)

| Nav Item    | ID            | Icon              | Target       |
|-------------|---------------|-------------------|--------------|
| Home        | nav_home      | home              | home         |
| Accounts    | nav_accounts  | account_balance   | accounts     |
| Pay         | nav_pay       | send              | send-money   |
| Cards       | nav_cards     | credit_card       | cards        |
| More        | nav_more      | more_horiz        | more         |

---

## Components

| ID                        | Type  | Description                                                                            |
|---------------------------|-------|----------------------------------------------------------------------------------------|
| greeting_text             | text  | "Good morning, Alex" — headline_medium, color #1800B1; data-driven from greetingName  |
| greeting_date             | text  | "Monday, 25 May 2026" — body_medium, color #666666                                    |
| primary_account_card      | box   | Deep purple hero card (#1800B1, border-radius 20, elevation 4) containing account info + quick actions |
| account_card_label        | text  | "Primary Checking" — label_large, color #FFFFFFB3                                     |
| account_card_balance      | text  | "£4,250.00" — display_small, color #FFFFFF; data-driven                               |
| account_card_iban         | text  | "•••• •••• •••• 0130" — body_medium, color #FFFFFFB3; masked account number           |
| quick_actions_row         | stack | Horizontal row of 3 quick action buttons inside account card                          |
| btn_send_money            | button| "Send Money" — filled white; navigates to send-money                                  |
| btn_add_beneficiary       | button| "Beneficiaries" — outlined white; navigates to beneficiaries                          |
| btn_view_cards            | button| "View Cards" — outlined white; navigates to cards                                     |
| total_balance_chip        | box   | Light purple chip (#E8E4FF, border-radius 12) showing total across 3 accounts         |
| total_balance_icon        | icon  | account_balance_wallet, 16 dp, color #1800B1                                          |
| total_balance_text        | text  | "Total across 3 accounts: £12,480.50" — label_medium, color #1800B1                  |
| recent_transactions_header| stack | Row: "Recent Transactions" heading + "View All" link                                   |
| recent_transactions_title | text  | "Recent Transactions" — title_large, color #1A1A1A                                    |
| view_all_link             | link  | "View All" — label_medium, color #1800B1; navigates to transactions                   |
| transaction_row_1         | box   | "Tesco Supermarket" debit card — shopping_cart icon (#4CAF50), -£42.50 (#FF5252)      |
| transaction_row_2         | box   | "Salary Payment" credit card — payments icon (#4CAF50), +£3,200.00 (#4CAF50)         |
| transaction_row_3         | box   | "EDF Energy" debit card — bolt icon (#FF9800), -£94.20 (#FF5252)                      |
| services_section_title    | text  | "Services" — title_large, color #1A1A1A                                               |
| services_grid             | stack | Horizontal row of 3 service tiles                                                      |
| service_standing_orders   | box   | Purple tile (#F5F0FF) — repeat icon (#1800B1) + "Standing Orders" label              |
| service_atm_locator       | box   | Teal tile (#E0F7F7) — location_on icon (#008B8B) + "ATM & Branches" label            |
| service_fx_rates          | box   | Amber tile (#FFF3E0) — currency_exchange icon (#E65100) + "FX Rates" label           |

---

## States

| ID      | Trigger                        | Description                                                                            |
|---------|--------------------------------|----------------------------------------------------------------------------------------|
| loading | Screen entry / RetryLoad       | Greeting visible; account card and transaction rows replaced by skeleton shimmer boxes |
| content | Data load success              | All components visible with real account and transaction data                          |
| error   | Network or auth failure        | Greeting visible; error card shown with retry button                                   |
| empty   | Account data returns empty     | Greeting visible; empty state card with "Set Up Account" CTA                           |

---

## State Model

**ViewModel:** `HomeViewModel`
**Screen State Type:** `HomeScreenState`

| Name                | Type                    | Default      |
|---------------------|-------------------------|--------------|
| isLoading           | Boolean                 | true         |
| primaryAccount      | AccountSummary?         | null         |
| totalBalance        | BigDecimal?             | null         |
| totalAccountCount   | Int                     | 0            |
| recentTransactions  | List\<TransactionSummary\> | emptyList() |
| error               | UiError?                | null         |
| greetingName        | String                  | "Alex"       |

**Events:** `RetryLoad`, `NavigateToTransactions`, `NavigateToSendMoney`, `NavigateToAccounts`, `NavigateToBeneficiaries`, `NavigateToCards`

**Actions:** `loadDashboardData()` (triggers: RetryLoad, ScreenOpened), `navigateTo(screen_id)`

**DI Dependencies:** `AccountsRepository`, `TransactionsRepository`, `SessionManager`

**Errors:**
- `network_error`: "Could not connect to banking services. Please try again."
- `auth_error`: "Session expired. Please log in again."
- `unknown_error`: "Something went wrong. Please try again."

---

## Navigation

| From | To             | Trigger                          | Type     |
|------|----------------|----------------------------------|----------|
| home | send-money     | btn_send_money tap               | push     |
| home | beneficiaries  | btn_add_beneficiary tap          | push     |
| home | cards          | btn_view_cards tap               | push     |
| home | transactions   | view_all_link tap                | push     |
| home | standing-orders| service_standing_orders tap      | push     |
| home | atm-locator    | service_atm_locator tap          | push     |
| home | fx-rates       | service_fx_rates tap             | push     |
| home | accounts       | nav_accounts bottom tab tap      | tab      |
| home | send-money     | nav_pay bottom tab tap           | tab      |
| home | cards          | nav_cards bottom tab tap         | tab      |
| home | more           | nav_more bottom tab tap          | tab      |

---

## API Endpoints

| Endpoint                                                              | Auth         | Tag          | Purpose                                           |
|-----------------------------------------------------------------------|--------------|--------------|---------------------------------------------------|
| GET /obp/v5.1.0/banks/{bankId}/accounts                              | DirectLogin  | Accounts     | Fetch accounts for bank gh.29.uk                 |
| GET /obp/v5.1.0/my/banks/{bankId}/accounts/{accountId}/transactions  | DirectLogin  | Transactions | Fetch recent 5 transactions DESC for primary account |
| GET /obp/v3.0.0/my/accounts                                          | DirectLogin  | Accounts     | Cross-bank account aggregation for total balance  |

---

## Design Tokens

| Token                       | Value     | Usage                                                         |
|-----------------------------|-----------|---------------------------------------------------------------|
| color.light.primary         | #1800B1   | Greeting text, account card background, quick action text, total balance chip text/icon, view all link, service tile icons |
| color.surface.white         | #FFFFFF   | Transaction row cards, quick action (Send Money) button background |
| color.light.background      | #FCF8FF   | Page background (inherited)                                   |
| color.account_card.text     | #FFFFFFB3 | Card label and IBAN (70% white opacity)                       |
| color.balance.chip          | #E8E4FF   | Total balance chip background (light purple)                  |
| color.debit.default         | #FF5252   | Debit transaction amounts and badge text                      |
| color.debit.surface         | #FFEBEE   | Debit badge background                                        |
| color.credit.default        | #4CAF50   | Credit transaction amounts, badge text, and shopping/payment icons |
| color.credit.surface        | #E8F5E9   | Credit badge background and icon containers                   |
| color.utility.amber         | #FF9800   | Utilities category icon (EDF Energy)                          |
| color.utility.surface       | #FFF3E0   | Utilities icon container background                           |
| color.standing_orders.surface| #F5F0FF  | Standing Orders service tile background                       |
| color.atm.surface           | #E0F7F7   | ATM & Branches service tile background                        |
| color.fx.icon               | #E65100   | FX Rates icon and label color                                 |
| color.fx.surface            | #FFF3E0   | FX Rates service tile background                              |
| typography.headline_medium  | —         | Greeting text                                                 |
| typography.display_small    | —         | Account balance                                               |
| typography.title_large      | —         | Section headers (Recent Transactions, Services)               |
| typography.label_large      | —         | Account card type label                                       |
| typography.label_medium     | —         | Total balance chip, quick action buttons, View All link       |
| typography.body_large       | —         | Transaction merchant names                                    |
| typography.body_medium      | —         | Greeting date, account IBAN                                   |
| typography.body_small       | —         | Transaction date/category                                     |
| typography.label_small      | —         | DEBIT / CREDIT badge labels                                   |

---

_Generated by /idea export | 2026-05-25_
