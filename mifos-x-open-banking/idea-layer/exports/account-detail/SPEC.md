# SPEC — Account Detail

| Field         | Value                     |
|---------------|---------------------------|
| Feature       | account-detail            |
| Flavor        | consumer                  |
| Status        | approved                  |
| Quality Score | 94                        |
| ViewModel     | AccountDetailViewModel    |

---

## Overview

The Account Detail screen provides a deep-dive view of a single bank account. A full-width green hero header displays the account label ("Primary Checking"), balance ("£4,250.00"), currency badge ("GBP"), and account type badge ("CHECKING"). Below the header, an elevated white card overlapping the hero shows the IBAN (DE89 3704 0044 0532 0130 00) and BIC/SWIFT (COBADEFFXXX) with one-tap copy icons. A three-button action row offers "Send Money", "Request", and "Statement" tonal/outlined buttons. Below that, a "Recent Transactions" section lists the 5 most recent transactions with merchant name, date, category icon, and signed amount. A bottom navigation bar keeps the Consumer shell accessible at all times.

---

## Screens

| ID                     | Name           | Route                   | Layout | Scroll   |
|------------------------|----------------|-------------------------|--------|----------|
| account_detail_content | Account Detail | /accounts/{accountId}   | Column | Vertical |

**Shell:** Top app bar, title "Account Details", back arrow. Bottom navigation bar with 5 items (Accounts active).

| Nav Item | ID           | Icon            | Target      |
|----------|--------------|-----------------|-------------|
| Home     | nav_home     | home            | home        |
| Accounts | nav_accounts | account_balance | accounts    |
| Pay      | nav_pay      | send            | send-money  |
| Cards    | nav_cards    | credit_card     | cards       |
| More     | nav_more     | more_horiz      | settings    |

---

## Components

| ID                         | Type    | Description                                                                                              |
|----------------------------|---------|----------------------------------------------------------------------------------------------------------|
| account_header_card        | box     | Full-width hero, `#4C662B` bg, no radius, 24dp H padding; contains label, balance, and currency/type badges |
| account_header_label       | text    | "Primary Checking" — label_large (14sp/Medium), color `#FFFFFFB3` (70% white opacity)                   |
| account_header_balance     | text    | "£4,250.00" — display_large (57sp/Bold), color `#FFFFFF`; data-driven                                   |
| account_currency_badge     | box     | `#FFFFFF1A` bg, 6dp radius, 8dp H pad / 4dp V pad; contains "GBP" label                                 |
| account_currency_label     | text    | "GBP" — label_small (11sp/Medium), color `#FFFFFF`                                                      |
| account_type_badge         | box     | `#FFFFFF1A` bg, 6dp radius; contains "CHECKING" label                                                   |
| account_type_label         | text    | "CHECKING" — label_small (11sp/Medium), color `#FFFFFF`                                                  |
| account_info_card          | box     | Elevated white card, 16dp radius, 20dp padding, 20dp H margin, -16dp top margin (overlap hero), elevation 3 |
| iban_label                 | text    | "IBAN" — label_small (11sp/Medium), color `#44483D`, letter_spacing 0.5                                 |
| iban_value                 | text    | "DE89 3704 0044 0532 0130 00" — body_medium monospace, color `#1A1C16`                                   |
| copy_iban_button           | icon    | `content_copy`, 22dp, color `#4C662B`; on_click copies IBAN to clipboard                                |
| info_divider_1             | divider | `#F9FAEF` separator between IBAN and BIC rows                                                            |
| bic_label                  | text    | "BIC / SWIFT" — label_small (11sp/Medium), color `#44483D`, letter_spacing 0.5                          |
| bic_value                  | text    | "COBADEFFXXX" — body_medium monospace, color `#1A1C16`                                                   |
| copy_bic_button            | icon    | `content_copy`, 22dp, color `#4C662B`; on_click copies BIC to clipboard                                 |
| action_row                 | stack   | Horizontal row of 3 action buttons, 20dp H padding                                                      |
| btn_send_money             | button  | "Send Money" — tonal `#CDEDA3` bg / `#4C662B` text, 12dp radius, `send` icon; navigates to send-money  |
| btn_request_payment        | button  | "Request" — outlined `#4C662B` border/text, 12dp radius, `request_quote` icon; triggers request_payment |
| btn_download_statement     | button  | "Statement" — outlined `#4C662B` border/text, 12dp radius, `download` icon; triggers download_statement |
| section_divider            | divider | `#E1E4D5` section separator, 20dp H margin                                                              |
| recent_transactions_title  | text    | "Recent Transactions" — title_large (22sp/Regular), color `#1A1C16`; heading level 2                    |
| view_all_transactions_link | link    | "View All" — label_medium (12sp/Medium), color `#4C662B`; navigates to transactions                     |
| detail_txn_row_1           | box     | Tesco Supermarket — `shopping_basket` icon (#BA1A1A on #CDEDA3 pill) / -£42.50 (#BA1A1A) / 23 May 2026 |
| detail_txn_row_2           | box     | Salary Payment — `payments` icon (#4C662B on #CDEDA3 pill) / +£3,200.00 (#4C662B) / 22 May 2026        |
| detail_txn_row_3           | box     | EDF Energy — `bolt` icon (#44483D on #CDEDA3 pill) / -£94.20 (#BA1A1A) / 20 May 2026                   |
| detail_txn_row_4           | box     | Amazon Prime — `subscriptions` icon (#4C662B on #CDEDA3 pill) / -£8.99 (#BA1A1A) / 18 May 2026         |
| detail_txn_row_5           | box     | Costa Coffee — `local_cafe` icon (#44483D on #CDEDA3 pill) / -£3.75 (#BA1A1A) / 17 May 2026            |

---

## States

| ID      | Trigger                                   | Description                                                                                           |
|---------|-------------------------------------------|-------------------------------------------------------------------------------------------------------|
| loading | Screen entry / RetryLoad                  | Green hero skeleton + info card skeleton + action row skeleton + 1 transaction skeleton visible       |
| content | Data load success                         | Full hero, info card, action row, 5 transaction rows all visible                                      |
| error   | Network or API failure                    | Error card: "Could not load account" + message + Retry button; hero and cards hidden                  |
| empty   | Account data unavailable or account closed| Empty card: "No account details available" + "Go to Accounts" CTA; hero and cards hidden              |

---

## State Model

**ViewModel:** `AccountDetailViewModel`
**Screen State Type:** `AccountDetailScreenState`

| Name                  | Type                        | Default        |
|-----------------------|-----------------------------|----------------|
| isLoading             | `Boolean`                   | `true`         |
| account               | `BankAccount?`              | `null`         |
| recentTransactions    | `List<TransactionSummary>`  | `emptyList()`  |
| error                 | `UiError?`                  | `null`         |
| ibanCopied            | `Boolean`                   | `false`        |
| bicCopied             | `Boolean`                   | `false`        |
| isDownloadingStatement| `Boolean`                   | `false`        |

**Events:** `RetryLoad`, `CopyIban`, `CopyBic`, `RequestPayment`, `DownloadStatement`, `NavigateToSendMoney`, `NavigateToTransactions`

**Actions:** `loadAccountDetail(accountId)` (triggers: ScreenOpened, RetryLoad), `copyToClipboard(text)`, `downloadStatement()`, `navigateTo(screen_id)`

**DI Dependencies:** `AccountsRepository`, `TransactionsRepository`, `ClipboardManager`, `StatementDownloader`

**Errors:**
- `network_error`: "Network unavailable. Please check your connection."
- `not_found`: "Account no longer available."
- `statement_download_failed`: "Statement download failed. Please try again."

---

## Navigation

| From           | To           | Trigger                              | Type |
|----------------|--------------|--------------------------------------|------|
| account-detail | send-money   | btn_send_money tap                   | push |
| account-detail | transactions | view_all_transactions_link tap       | push |
| account-detail | accounts     | nav_accounts bottom tab tap          | tab  |
| account-detail | home         | nav_home bottom tab tap              | tab  |
| account-detail | send-money   | nav_pay bottom tab tap               | tab  |
| account-detail | cards        | nav_cards bottom tab tap             | tab  |
| account-detail | settings     | nav_more bottom tab tap              | tab  |
| account-detail | (back)       | Top app bar back arrow               | pop  |

---

## API Endpoints

| Endpoint                                                                   | Auth        | Tag          | Purpose                                           |
|----------------------------------------------------------------------------|-------------|--------------|---------------------------------------------------|
| GET /obp/v5.1.0/banks/{bankId}/accounts/{accountId}/owner/account          | DirectLogin | Accounts     | Fetch full account details including IBAN, BIC    |
| GET /obp/v5.1.0/my/banks/{bankId}/accounts/{accountId}/transactions        | DirectLogin | Transactions | Fetch 5 most recent transactions DESC             |

---

## Design Tokens

| Token                           | Value       | Usage                                                         |
|---------------------------------|-------------|---------------------------------------------------------------|
| colors.light.primary            | `#4C662B`   | Hero card background, copy icons, action buttons, View All link|
| colors.light.on_primary         | `#FFFFFF`   | Balance amount, currency/type badges on hero                  |
| colors.light.primary_container  | `#CDEDA3`   | Transaction icon pill background                              |
| colors.light.on_surface         | `#1A1C16`   | IBAN/BIC values, transaction merchant names                   |
| colors.light.on_surface_variant | `#44483D`   | IBAN/BIC labels, transaction dates, utilities icon color      |
| colors.light.error              | `#BA1A1A`   | Debit amount text, debit transaction icon                     |
| colors.light.surface            | `#FFFFFF`   | Info card and transaction row backgrounds                     |
| colors.light.surface_variant    | `#E1E4D5`   | Section divider                                               |
| colors.light.background         | `#F9FAEF`   | Screen and info card internal divider                         |
| typography.display_large        | 57sp/Bold   | Account balance in hero                                       |
| typography.title_large          | 22sp/Regular| "Recent Transactions" section header                          |
| typography.label_large          | 14sp/Medium | Account label in hero                                         |
| typography.label_medium         | 12sp/Medium | Action button labels, "View All" link                         |
| typography.label_small          | 11sp/Medium | Currency and type badges; IBAN/BIC field labels               |
| typography.body_medium          | 14sp/Regular| IBAN/BIC values, transaction merchant names                   |
| typography.body_small           | 12sp/Regular| Transaction dates                                             |
| typography.body_large           | 16sp/Regular| Transaction amounts                                           |
| radius.lg                       | 16dp        | Info card corner radius                                       |
| radius.md                       | 12dp        | Transaction row corner radius, action button radius           |
| elevation.level3                | 6dp         | Info card overlap elevation                                   |

---

_Generated by /idea export | 2026-05-29_
