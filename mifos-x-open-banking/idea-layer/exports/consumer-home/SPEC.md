# SPEC — Consumer Home

| Field         | Value                    |
|---------------|--------------------------|
| Feature       | consumer-home            |
| Flavor        | consumer                 |
| Status        | enriched                 |
| Quality Score | 96                       |
| ViewModel     | ConsumerHomeViewModel    |

---

## Overview

The Consumer Home is the personalised landing dashboard for authenticated consumer users (FR-019). It replaces the generic home screen with a richer, data-driven surface showing total balance, income/spend summary, four quick-action tiles, and the last three recent transactions. The screen uses no top app bar — instead a full-width green header band (`#4C662B`) carries the greeting and a notification bell. A floating white balance card partially overlaps the header (negative top margin of -24dp) to create a layered, modern depth effect. Four quick-action tiles beneath the card navigate to Send Money, Accounts, Standing Orders, and Cards in one tap. Below that, the three most recent transactions are shown as individual cards with a "View All Transactions" outlined button. The screen is responsive (2-column tablet, 3-column desktop). Bottom navigation bar is visible with Home as the active tab.

---

## Screens

| ID            | Name          | Route          | Layout | Scroll   |
|---------------|---------------|----------------|--------|----------|
| consumer-home | Consumer Home | /consumer/home | Column | Vertical |

**Shell:** No top app bar. Bottom navigation bar with 5 items (Home active).

| Nav Item  | ID            | Icon            | Target       |
|-----------|---------------|-----------------|--------------|
| Home      | nav_home      | home            | consumer-home |
| Accounts  | nav_accounts  | account_balance | accounts     |
| Pay       | nav_pay       | send            | send-money   |
| Cards     | nav_cards     | credit_card     | cards        |
| More      | nav_more      | more_horiz      | settings     |

---

## Components

| ID                         | Type         | Description                                                                                          |
|----------------------------|--------------|------------------------------------------------------------------------------------------------------|
| ch_root                    | stack        | Root column; background `#F9FAEF`                                                                    |
| ch_header_band             | stack        | Horizontal row; background `#4C662B`; padding-top `spacing.xl` (32dp); padding-bottom `spacing.lg` (24dp) |
| ch_greeting_text           | text         | "Good morning, Alex" — `headline_medium`, color `#FFFFFF`; flex:1; data-driven from `greetingName` |
| ch_notification_icon       | button       | `notifications` icon 28dp, white; badge when `unreadNotifications > 0`; navigates to notifications  |
| ch_balance_card            | card         | White (`#FFFFFF`), 20dp radius, elevation 4; margin-top -24dp (overlaps header); 24dp horizontal padding |
| ch_balance_label           | text         | "Total Balance" — `label_medium`, color `#757575`                                                   |
| ch_balance_amount          | text         | "£4,250.00" — `display_small` (32sp/SemiBold), color `#4C662B`, bold; data-driven                  |
| ch_account_name_chip       | box          | "Primary Checking" — `label_small`, bg `#CDEDA3`, text `#4C662B`, 12dp radius; data-driven         |
| ch_balance_divider         | divider      | Color `#E8E8E8`; 16dp vertical margin                                                               |
| ch_balance_sub_row         | stack        | Horizontal row; `justify: space_between`                                                            |
| ch_income_block            | stack        | Column: income label + income amount                                                                 |
| ch_income_label            | text         | "Income this month" — `label_small`, color `#757575`                                                |
| ch_income_amount           | text         | "+ £3,200.00" — `body_large`, color `#2E7D32`, medium weight; data-driven                          |
| ch_expense_block           | stack        | Column: spent label + expense amount                                                                 |
| ch_expense_label           | text         | "Spent this month" — `label_small`, color `#757575`                                                 |
| ch_expense_amount          | text         | "- £1,840.00" — `body_large`, color `#C62828`, medium weight; data-driven                          |
| ch_quick_actions_row       | stack        | Horizontal row; `justify: space_evenly`; padding `spacing.lg` vertical; bg `#F9FAEF`               |
| ch_action_send             | stack        | Column tile with icon + label; navigates to send-money; min touch 48dp                              |
| ch_action_accounts         | stack        | Column tile with icon + label; navigates to accounts                                                |
| ch_action_standing_orders  | stack        | Column tile with icon + label; navigates to standing-orders                                         |
| ch_action_cards            | stack        | Column tile with icon + label; navigates to cards                                                   |
| ch_recent_transactions_section | stack   | Column; 16dp horizontal padding                                                                      |
| ch_transactions_title      | text         | "Recent Transactions" — `title_medium`, `#1A1C16`, semibold                                        |
| ch_see_all_link            | text         | "See all" — `label_medium`, color `#4C662B`; navigates to transactions                              |
| ch_transaction_item_1      | box          | "Coffee Shop — £3.50"; white bg, 12dp radius, elevation 1; navigates to transaction-detail          |
| ch_transaction_item_2      | box          | "Salary — £3,200.00"; white bg, 12dp radius, elevation 1; navigates to transaction-detail           |
| ch_transaction_item_3      | box          | "Supermarket — £42.80"; white bg, 12dp radius, elevation 1; navigates to transaction-detail         |
| ch_see_all_button          | button       | "View All Transactions" — outlined, border `#4C662B`, text `#4C662B`, 24dp radius, full-width      |
| ch_error_state             | stack        | Column; `error_outline` icon 48dp `#D32F2F` + message + Retry button; visible in `error` state      |
| ch_error_text              | text         | "Could not load your account. Check your connection and try again." — `body_medium`, `#757575`, centered |
| ch_retry_button            | button       | "Retry" — filled `#4C662B`, white, 24dp radius, 48dp height                                        |
| ch_empty_state             | stack        | Column; `account_balance_wallet` icon 64dp `#CDEDA3` + message; visible in `empty` state            |
| ch_empty_text              | text         | "No accounts found. Contact your bank to set up your account." — `body_medium`, `#757575`, centered |
| ch_loading_shimmer         | box          | Shimmer placeholder 200dp height, 20dp radius; visible in `loading` state                           |

---

## States

| ID      | Trigger                        | Description                                                                                    |
|---------|--------------------------------|------------------------------------------------------------------------------------------------|
| loading | Screen entry / `RetryLoad`     | Green header + greeting visible; skeleton cards for balance (200dp), quick actions (72dp), and 2 transactions (64dp each) with `#E1E4D5` shimmer |
| content | Data load success              | All components visible with real account balance, income/spend, quick actions, and 3 transactions |
| error   | Network or auth failure        | Green header + greeting + error card (icon + message + Retry button)                           |
| empty   | No accounts returned from API  | Green header + greeting + empty state (wallet icon + message)                                  |

---

## State Model

**ViewModel:** `ConsumerHomeViewModel`
**Screen State Type:** `ConsumerHomeScreenState`

| Name                 | Type                        | Default         |
|----------------------|-----------------------------|-----------------|
| isLoading            | Boolean                     | `true`          |
| greetingName         | String                      | `"Alex"`        |
| totalBalance         | BigDecimal?                 | `null`          |
| primaryAccount       | AccountSummary?             | `null`          |
| incomeThisMonth      | BigDecimal?                 | `null`          |
| spentThisMonth       | BigDecimal?                 | `null`          |
| recentTransactions   | List\<TransactionSummary\>  | `emptyList()`   |
| unreadNotifications  | Int                         | `0`             |
| error                | UiError?                    | `null`          |

**State members:** `Loading`, `Content`, `Empty`, `Error`

**Events:** `ScreenOpened`, `RetryLoad`, `OpenNotifications`, `NavigateToSendMoney`, `NavigateToAccounts`, `NavigateToStandingOrders`, `NavigateToCards`, `NavigateToTransactions`, `SelectTransaction`

**Actions:**
- `loadConsumerHome()` — triggers on `ScreenOpened` and `RetryLoad`; calls accounts + transactions APIs
- `navigateTo(screen_id)` — dispatches navigation event

**DI Dependencies:** `AccountsRepository`, `TransactionsRepository`, `NotificationsRepository`, `SessionManager`

**Errors:**
- `network_error`: "Could not load your account. Check your connection and try again."
- `auth_error`: "Session expired. Please log in again."
- `unknown_error`: "Something went wrong. Please try again."

---

## Navigation

| From          | To                | Trigger                              | Type |
|---------------|-------------------|--------------------------------------|------|
| consumer-home | notifications     | `ch_notification_icon` tap           | push |
| consumer-home | send-money        | `ch_action_send` tile tap            | push |
| consumer-home | accounts          | `ch_action_accounts` tile tap        | push |
| consumer-home | standing-orders   | `ch_action_standing_orders` tile tap | push |
| consumer-home | cards             | `ch_action_cards` tile tap           | push |
| consumer-home | transactions      | `ch_see_all_link` tap                | push |
| consumer-home | transactions      | `ch_see_all_button` tap              | push |
| consumer-home | transaction-detail| `ch_transaction_item_*` tap          | push |
| consumer-home | accounts          | `nav_accounts` bottom tab tap        | tab  |
| consumer-home | send-money        | `nav_pay` bottom tab tap             | tab  |
| consumer-home | cards             | `nav_cards` bottom tab tap           | tab  |
| consumer-home | settings          | `nav_more` bottom tab tap            | tab  |

---

## API Endpoints

| Endpoint                                                          | Auth        | Tag          | Purpose                                           |
|-------------------------------------------------------------------|-------------|--------------|---------------------------------------------------|
| GET /obp/v5.1.0/my/accounts                                       | DirectLogin | Accounts     | Fetch primary account balance + account name      |
| GET /obp/v5.1.0/my/banks/{bankId}/accounts/{accountId}/transactions | DirectLogin | Transactions | Fetch 3 most recent transactions (limit=3, sort=DESC) |

---

## Design Tokens

| Token                          | Value   | Usage                                                               |
|--------------------------------|---------|---------------------------------------------------------------------|
| color.light.primary            | #4C662B | Header band background, balance amount, account chip text, quick-action icons, See all link, outlined button, retry button |
| color.light.primary_container  | #CDEDA3 | Account name chip background                                        |
| color.light.background         | #F9FAEF | Screen background, quick-actions row background                     |
| color.light.surface            | #FFFFFF | Balance card background, transaction item cards                     |
| color.light.on_primary         | #FFFFFF | Greeting text, notification icon                                    |
| color.semantic.income_green    | #2E7D32 | Income this month amount                                            |
| color.semantic.expense_red     | #C62828 | Spent this month amount                                             |
| color.semantic.error_icon      | #D32F2F | Error state icon                                                    |
| color.light.on_surface         | #1A1C16 | "Recent Transactions" section title                                 |
| color.neutral.grey             | #757575 | Balance label, income/expense labels, error + empty text            |
| color.light.surface_variant    | #E1E4D5 | Loading skeleton shimmer                                            |
| typography.headline_medium     | —       | Greeting text (28sp/Regular)                                        |
| typography.display_small       | —       | Balance amount (32sp/SemiBold)                                      |
| typography.label_medium        | —       | Balance label, "See all" link                                       |
| typography.label_small         | —       | Account chip, income/expense labels                                 |
| typography.body_large          | —       | Income and expense amounts (16sp/Regular)                           |
| typography.title_medium        | —       | "Recent Transactions" heading (16sp/Medium)                         |
| typography.body_medium         | —       | Error and empty state body text                                     |
| elevation.level4               | 4dp     | Balance card                                                        |
| elevation.level1               | 1dp     | Transaction item cards                                              |
| radius.xl                      | 24dp    | Balance card border-radius                                          |
| radius.md                      | 12dp    | Transaction card border-radius                                      |
| radius.sm                      | 8dp     | Skeleton shimmer blocks                                             |
| spacing.xl                     | 32dp    | Header band top padding                                             |
| spacing.lg                     | 24dp    | Header band bottom padding, quick actions vertical padding          |
| spacing.md                     | 16dp    | Balance card padding, transaction row padding                       |

---

_Generated by /idea export | 2026-05-29_
