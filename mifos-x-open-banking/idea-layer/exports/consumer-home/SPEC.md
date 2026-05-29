# SPEC — Consumer Home

| Field         | Value                    |
|---------------|--------------------------|
| Feature       | consumer-home            |
| Flavor        | consumer                 |
| Status        | designed                 |
| Quality Score | 96                       |
| ViewModel     | ConsumerHomeViewModel    |

---

## Overview

The Consumer Home is the personalised landing dashboard for authenticated consumer users (FR-019). It is the root of the consumer journey and the first screen seen after login. The screen carries no top app bar — instead a full-width earth-green header band (`#4C662B`) containing a personalised greeting ("Good morning, Alex") and a notification bell with unread-count badge. A white balance card floats below the header with a -24dp negative top margin, creating a layered depth effect. The card displays the total GBP balance (£4,250.00), the active account name ("Primary Checking") in a `#CDEDA3` chip, and an income/spend split for the current month (+ £3,200.00 income, - £1,840.00 spent). Four quick-action tiles (Send, Accounts, Standing Orders, Cards) sit below the card in a horizontally evenly-spaced row. A Recent Transactions section follows, showing the three most recent transactions as individual white cards (Coffee Shop - £3.50, Salary + £3,200.00, Supermarket - £42.80) with a "View All Transactions" outlined button. The screen handles four states: `loading` (skeleton shimmer), `content` (full data), `error` (retry card), and `empty` (no-accounts card). Bottom navigation is always visible with Home as the active tab. The screen is responsive: 2-column on tablet (≥600dp), 3-column on desktop (≥840dp).

---

## Screens

| ID            | Name          | Route          | Layout | Scroll   |
|---------------|---------------|----------------|--------|----------|
| consumer-home | Consumer Home | /consumer/home | Column | Vertical |

**Shell:** No top app bar (`show: false`). Bottom navigation bar with 5 items (Home active).

| Nav Item | ID            | Icon            | Target        | Active |
|----------|---------------|-----------------|---------------|--------|
| Home     | nav_home      | home            | consumer-home | true   |
| Accounts | nav_accounts  | account_balance | accounts      | false  |
| Pay      | nav_pay       | send            | send-money    | false  |
| Cards    | nav_cards     | credit_card     | cards         | false  |
| More     | nav_more      | more_horiz      | settings      | false  |

---

## Components

| ID                             | Type    | Description                                                                                                      |
|--------------------------------|---------|------------------------------------------------------------------------------------------------------------------|
| ch_root                        | stack   | Root column; background `#F9FAEF`; hosts all child sections; states: loading, content, error, empty             |
| ch_header_band                 | stack   | Horizontal row; background `#4C662B`; padding-top `spacing.xl` (32dp), padding-bottom `spacing.lg` (24dp)      |
| ch_greeting_text               | text    | "Good morning, Alex" — `Outfit/headline_medium` (28sp/Regular), color `#FFFFFF`; flex:1; data-driven from `greetingName` |
| ch_notification_icon           | button  | `notifications` icon 28dp; white; badge when `unreadNotifications > 0`; tap → notifications; 48×48dp touch target |
| ch_balance_card                | card    | Elevated card; background `#FFFFFF`; border_radius 20dp; elevation 4; margin-top -24dp (overlaps header); 24dp horizontal padding, 24dp vertical padding |
| ch_balance_label               | text    | "Total Balance" — `Outfit/label_medium` (12sp/Medium), color `#757575`                                          |
| ch_balance_amount              | text    | "£4,250.00" — `Outfit/display_small` (32sp/SemiBold), color `#4C662B`; data-driven from `totalBalance`         |
| ch_account_name_chip           | box     | "Primary Checking" — `Outfit/label_small` (11sp/Medium); background `#CDEDA3`; text `#4C662B`; 12dp radius; 10dp horizontal padding, 4dp vertical padding; data-driven from `primaryAccount.label` |
| ch_balance_divider             | divider | Color `#E8E8E8`; `spacing.md` (16dp) vertical margin                                                            |
| ch_balance_sub_row             | stack   | Horizontal row; `justify: space_between`; contains income and expense blocks                                    |
| ch_income_block                | stack   | Column: `ch_income_label` + `ch_income_amount`                                                                  |
| ch_income_label                | text    | "Income this month" — `Outfit/label_small` (11sp/Medium), color `#757575`                                       |
| ch_income_amount               | text    | "+ £3,200.00" — `Outfit/body_large` (16sp/Regular), color `#2E7D32`; medium weight; data-driven from `incomeThisMonth` |
| ch_expense_block               | stack   | Column: `ch_expense_label` + `ch_expense_amount`                                                                |
| ch_expense_label               | text    | "Spent this month" — `Outfit/label_small` (11sp/Medium), color `#757575`                                        |
| ch_expense_amount              | text    | "- £1,840.00" — `Outfit/body_large` (16sp/Regular), color `#C62828`; medium weight; data-driven from `spentThisMonth` |
| ch_quick_actions_row           | stack   | Horizontal row; `justify: space_evenly`; `spacing.lg` (24dp) vertical padding; background `#F9FAEF`            |
| ch_action_send                 | stack   | Column tile: icon + "Send" label; navigates to send-money; 48dp touch target                                    |
| ch_action_accounts             | stack   | Column tile: icon + "Accounts" label; navigates to accounts; 48dp touch target                                  |
| ch_action_standing_orders      | stack   | Column tile: icon + "Standing Orders" label; navigates to standing-orders; 48dp touch target                    |
| ch_action_cards                | stack   | Column tile: icon + "Cards" label; navigates to cards; 48dp touch target                                        |
| ch_recent_transactions_section | stack   | Column; `spacing.md` (16dp) horizontal padding; `spacing.sm` (8dp) top padding                                 |
| ch_transactions_header_row     | stack   | Horizontal; align center; `justify: space_between`; `spacing.sm` (8dp) bottom padding                          |
| ch_transactions_title          | text    | "Recent Transactions" — `Outfit/title_medium` (16sp/Medium), color `#1A1C16`, semibold; heading level 2        |
| ch_see_all_link                | text    | "See all" — `Outfit/label_medium` (12sp/Medium), color `#4C662B`; navigates to transactions                    |
| ch_transaction_item_1          | box     | "Coffee Shop — £3.50"; background `#FFFFFF`; 12dp radius; elevation 1; 16dp padding; navigates to transaction-detail; data-driven |
| ch_transaction_item_2          | box     | "Salary — £3,200.00"; background `#FFFFFF`; 12dp radius; elevation 1; 16dp padding; navigates to transaction-detail; data-driven |
| ch_transaction_item_3          | box     | "Supermarket — £42.80"; background `#FFFFFF`; 12dp radius; elevation 1; 16dp padding; navigates to transaction-detail; data-driven |
| ch_see_all_button              | button  | "View All Transactions"; outlined; border `#4C662B`; text `#4C662B`; 24dp radius; 48dp height; full-width; navigates to transactions |
| ch_error_state                 | stack   | Column; visible only in `error` state; contains error icon, message, and Retry button                           |
| ch_error_icon                  | icon    | `error_outline`; 48dp; color `#D32F2F`; role: presentation                                                     |
| ch_error_text                  | text    | "Could not load your account. Check your connection and try again." — `Outfit/body_medium`, color `#757575`, centered; role: alert |
| ch_retry_button                | button  | "Retry"; filled; background `#4C662B`; text `#FFFFFF`; 24dp radius; 48dp height; action: `retry_load`          |
| ch_empty_state                 | stack   | Column; visible only in `empty` state; contains empty icon and message                                          |
| ch_empty_icon                  | icon    | `account_balance_wallet`; 64dp; color `#CDEDA3`; role: presentation                                            |
| ch_empty_text                  | text    | "No accounts found. Contact your bank to set up your account." — `Outfit/body_medium`, color `#757575`, centered |
| ch_loading_shimmer             | box     | Shimmer placeholder; 200dp height; 20dp radius; visible only in `loading` state; background shimmer from `#E1E4D5` |

---

## States

| ID      | Trigger                        | Description                                                                                                     |
|---------|--------------------------------|-----------------------------------------------------------------------------------------------------------------|
| loading | Screen entry / `RetryLoad`     | Green header + greeting visible; balance card replaced by shimmer (200dp, #E1E4D5, 20dp radius); quick-actions shimmer (72dp); 2 transaction skeleton rows (64dp each, 12dp radius) |
| content | Data load success              | Full screen: header band, balance card with amount + chip + income/spend, four quick-action tiles, three transaction rows, "View All" button, bottom nav |
| error   | Network or auth failure        | Green header + greeting visible; error card with `error_outline` icon, message, and "Retry" filled button       |
| empty   | No accounts returned from API  | Green header + greeting visible; empty state with `account_balance_wallet` icon (64dp, #CDEDA3) and no-accounts message |

---

## State Model

**ViewModel:** `ConsumerHomeViewModel`
**Screen State Type:** `ConsumerHomeScreenState`

| Name                | Type                       | Default       |
|---------------------|----------------------------|---------------|
| isLoading           | Boolean                    | `true`        |
| greetingName        | String                     | `"Alex"`      |
| totalBalance        | BigDecimal?                | `null`        |
| primaryAccount      | AccountSummary?            | `null`        |
| incomeThisMonth     | BigDecimal?                | `null`        |
| spentThisMonth      | BigDecimal?                | `null`        |
| recentTransactions  | List\<TransactionSummary\> | `emptyList()` |
| unreadNotifications | Int                        | `0`           |
| error               | UiError?                   | `null`        |

**State members:** `Loading`, `Content`, `Empty`, `Error`

**Events:** `ScreenOpened`, `RetryLoad`, `OpenNotifications`, `NavigateToSendMoney`, `NavigateToAccounts`, `NavigateToStandingOrders`, `NavigateToCards`, `NavigateToTransactions`, `SelectTransaction`

**Actions:**
- `loadConsumerHome()` — triggers on `ScreenOpened` and `RetryLoad`; calls `obp_get_accounts` + `obp_get_transactions`
- `navigateTo(screen_id)` — dispatches navigation event

**DI Dependencies:** `AccountsRepository`, `TransactionsRepository`, `NotificationsRepository`, `SessionManager`

**Errors:**
- `network_error`: "Could not load your account. Check your connection and try again."
- `auth_error`: "Session expired. Please log in again."
- `unknown_error`: "Something went wrong. Please try again."

---

## Navigation

| From          | To               | Trigger                              | Type |
|---------------|------------------|--------------------------------------|------|
| consumer-home | notifications    | `ch_notification_icon` tap           | push |
| consumer-home | send-money       | `ch_action_send` tile tap            | push |
| consumer-home | accounts         | `ch_action_accounts` tile tap        | push |
| consumer-home | standing-orders  | `ch_action_standing_orders` tile tap | push |
| consumer-home | cards            | `ch_action_cards` tile tap           | push |
| consumer-home | transactions     | `ch_see_all_link` tap                | push |
| consumer-home | transactions     | `ch_see_all_button` tap              | push |
| consumer-home | transaction-detail | `ch_transaction_item_*` tap        | push |
| consumer-home | accounts         | `nav_accounts` bottom tab tap        | tab  |
| consumer-home | send-money       | `nav_pay` bottom tab tap             | tab  |
| consumer-home | cards            | `nav_cards` bottom tab tap           | tab  |
| consumer-home | settings         | `nav_more` bottom tab tap            | tab  |

---

## API Endpoints

| Endpoint                                                                        | Auth        | Tag          | Purpose                                                   |
|---------------------------------------------------------------------------------|-------------|--------------|-----------------------------------------------------------|
| GET /obp/v4.0.0/my/accounts                                                     | DirectLogin | Accounts     | Fetch all consumer accounts; primary used for balance card |
| GET /obp/v4.0.0/banks/{bankId}/accounts/{accountId}/transactions                | DirectLogin | Transactions | Fetch 3 most recent transactions (limit=3, sort=DESC)     |

---

## Design Tokens

| Token                          | Value   | Usage                                                                                         |
|--------------------------------|---------|-----------------------------------------------------------------------------------------------|
| colors.light.primary           | #4C662B | Header band background, balance amount text, account chip text, quick-action row icons, "See all" link, outlined button border+text, retry button background |
| colors.light.primary_container | #CDEDA3 | Account name chip background                                                                  |
| colors.light.background        | #F9FAEF | Screen root background, quick-actions row background                                          |
| colors.light.surface           | #FFFFFF | Balance card background, transaction item card backgrounds                                    |
| colors.light.on_primary        | #FFFFFF | Greeting text, notification icon color                                                        |
| colors.light.on_surface        | #1A1C16 | "Recent Transactions" section title                                                           |
| colors.light.surface_variant   | #E1E4D5 | Loading skeleton shimmer base color                                                           |
| color.semantic.income_green    | #2E7D32 | Income this month amount (not a standard M3 token — inline on income_amount)                 |
| color.semantic.expense_red     | #C62828 | Spent this month amount (not a standard M3 token — inline on expense_amount)                 |
| color.semantic.error_icon      | #D32F2F | Error state icon color                                                                        |
| color.neutral.grey             | #757575 | Balance label, income/expense labels, error text, empty text                                  |
| typography.headline_medium     | Outfit 28sp/Regular   | Greeting text                                                              |
| typography.display_small       | Outfit 32sp/SemiBold  | Balance amount                                                             |
| typography.label_medium        | Outfit 12sp/Medium    | Balance label "Total Balance", "See all" link                              |
| typography.label_small         | Outfit 11sp/Medium    | Account name chip, income/expense labels                                   |
| typography.body_large          | Outfit 16sp/Regular   | Income and expense amounts                                                 |
| typography.title_medium        | Outfit 16sp/Medium    | "Recent Transactions" heading                                              |
| typography.body_medium         | Outfit 14sp/Regular   | Error text, empty state text                                               |
| elevation.level4               | 4dp     | Balance card elevation                                                                        |
| elevation.level1               | 1dp     | Transaction item card elevation                                                               |
| radius.xl                      | 24dp    | Balance card border-radius (ui.yaml: 20dp — nearest token)                                   |
| radius.md                      | 12dp    | Transaction card border-radius, account name chip                                             |
| radius.pill                    | 999dp   | "View All Transactions" outlined button (24dp radius in source — pill treatment)              |
| spacing.xl                     | 32dp    | Header band top padding                                                                       |
| spacing.lg                     | 24dp    | Header band bottom padding, quick-actions vertical padding, balance card padding              |
| spacing.md                     | 16dp    | Horizontal content padding, balance card horizontal padding                                   |

---

_Generated by /idea export | 2026-05-30_
