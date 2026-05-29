# SPEC — Transaction Detail

| Field         | Value                          |
|---------------|--------------------------------|
| Feature       | transaction-detail             |
| Flavor        | consumer                       |
| Status        | approved                       |
| Quality Score | 93                             |
| ViewModel     | TransactionDetailViewModel     |

---

## Overview

The Transaction Detail screen delivers a full-fidelity receipt view for a single bank transaction. A full-bleed earth-green hero section (`#4C662B`) displays the signed amount prominently in Outfit/display_large alongside a completion status badge. Overlapping the hero via negative margin-top, a merchant card surfaces the counterparty name (Tesco Supermarket), logo, and spending category chip (Groceries, `#CDEDA3`). A structured details card itemises date/time, a copyable reference number, transaction type, source account, and destination beneficiary IBAN. Users can download a PDF receipt (OutlinedButton) or report a dispute (red link) via in-screen CTAs. The screen uses a top app bar with share action. No bottom navigation — focused receipt context.

---

## Screens

| ID                       | Name               | Route                       | Layout | Scroll   |
|--------------------------|--------------------|-----------------------------|--------|----------|
| transaction_detail_content | Transaction Detail | /transactions/{transactionId} | Column | Vertical |

**Shell:** Top app bar with back arrow + share action. No bottom navigation bar.

| Element         | Value                      |
|-----------------|----------------------------|
| Title           | "Transaction Details"      |
| Navigation icon | arrow_back                 |
| Navigation action | navigate_back            |
| Action 1        | share → share_transaction  |

---

## Components

| ID                      | Type    | Description                                                                                                    |
|-------------------------|---------|----------------------------------------------------------------------------------------------------------------|
| amount_hero_section     | box     | Full-width hero, background `#4C662B`, padding H 24dp/V 28-36dp, centred                                     |
| amount_hero_value       | text    | "-£42.50" — Outfit/display_large 700-weight, `#BA1A1A` (debit red on green hero)                             |
| status_badge_row        | stack   | Horizontal centred row containing status_badge; padding_top 8dp                                               |
| status_badge            | box     | Semi-transparent pill, background `#4C662B33`, radius 20, padding H 16dp / V 6dp                             |
| status_badge_inner      | stack   | Row: status_icon + status_label, align center, spacing 6dp                                                    |
| status_icon             | icon    | check_circle 14dp, `#4C662B` (on white pill reads as green on light, or accent on dark hero)                  |
| status_label            | text    | "Completed" — Outfit/label_medium, `#4C662B`                                                                  |
| merchant_card           | box     | White card, radius 20, elevation 4, padding 20, margin H 20dp, margin_top -20dp (overlaps hero)               |
| merchant_row            | stack   | Horizontal: merchant_logo + merchant_info, spacing 16dp, align center                                         |
| merchant_logo           | image   | merchant_tesco_large 56×56dp, radius 28dp, background `#CDEDA3`                                               |
| merchant_name           | text    | "Tesco Supermarket" — Outfit/title_large 600-weight, `#1A1C16`                                               |
| category_badge          | box     | background `#CDEDA3`, radius 6dp, padding H 8dp / V 4dp, align_self flex_start, margin_top 4dp               |
| category_label          | text    | "Groceries" — Outfit/label_small, `#4C662B`                                                                   |
| details_card            | box     | White card, radius 16, elevation 1, padding 20, margin H 20dp                                                 |
| detail_date_row         | stack   | Row: "Date & Time" label + "25 May 2026, 14:32" value (space_between)                                        |
| detail_date_label       | text    | "Date & Time" — Outfit/label_small, `#44483D`, tracking 0.4                                                  |
| detail_date_value       | text    | "25 May 2026, 14:32" — Outfit/body_medium 500-weight, `#1A1C16`                                              |
| detail_div_1            | divider | `#F9FAEF` divider, margin_bottom 16dp                                                                         |
| detail_reference_row    | stack   | Row: "Reference" label + reference value + copy icon (space_between)                                          |
| detail_reference_label  | text    | "Reference" — Outfit/label_small, `#44483D`                                                                   |
| detail_reference_value  | text    | "SEPA-2026051500123" — Outfit/body_small monospace, `#1A1C16`                                                |
| copy_reference_icon     | icon    | content_copy 16dp, `#4C662B`; tappable → copy_reference action                                               |
| detail_div_2            | divider | `#F9FAEF` divider                                                                                              |
| detail_type_row         | stack   | Row: "Transaction Type" label + "SEPA Credit Transfer" value                                                   |
| detail_type_label       | text    | "Transaction Type" — Outfit/label_small, `#44483D`                                                           |
| detail_type_value       | text    | "SEPA Credit Transfer" — Outfit/body_medium 500-weight, `#1A1C16`                                            |
| detail_div_3            | divider | `#F9FAEF` divider                                                                                              |
| detail_from_row         | stack   | Row: "From Account" label + "Primary Checking / ...0130" value (space_between, align flex_start)              |
| detail_from_label       | text    | "From Account" — Outfit/label_small, `#44483D`                                                               |
| detail_from_account_name| text    | "Primary Checking" — Outfit/body_medium 500-weight, `#1A1C16`                                                |
| detail_from_iban        | text    | "...0130" — Outfit/body_small monospace, `#44483D`                                                           |
| detail_div_4            | divider | `#F9FAEF` divider                                                                                              |
| detail_to_row           | stack   | Row: "To Beneficiary" label + "Tesco PLC / DE89 3704...0044" value                                            |
| detail_to_label         | text    | "To Beneficiary" — Outfit/label_small, `#44483D`                                                             |
| detail_to_name          | text    | "Tesco PLC" — Outfit/body_medium 500-weight, `#1A1C16`                                                       |
| detail_to_iban          | text    | "DE89 3704...0044" — Outfit/body_small monospace, `#44483D`                                                  |
| download_receipt_button | button  | "Download Receipt" — outlined, border `#4C662B`, text `#4C662B`, radius 12dp, icon: download, margin H 20dp |
| report_issue_row        | stack   | Horizontal centred row: report_issue_icon + report_issue_link                                                  |
| report_issue_icon       | icon    | flag 16dp, `#BA1A1A`, padding_right 6dp                                                                       |
| report_issue_link       | link    | "Report an Issue" — Outfit/label_medium, `#BA1A1A`; opens dispute form                                       |

---

## States

| ID      | Trigger                     | Description                                                                                       |
|---------|-----------------------------|---------------------------------------------------------------------------------------------------|
| loading | ScreenOpened / RetryLoad    | 4 skeleton blocks: green hero (160dp), merchant card (100dp), details card (300dp), actions (52dp)|
| content | loadTransactionDetail success | Full hero + merchant card + details card + download button + report link                        |
| error   | not_found / network_error   | Error card: "Transaction not found", message, "Go Back" action, navigate_back trigger            |
| empty   | No detail record available  | Empty card: "Transaction details not available", message, "Go Back" action                       |

---

## State Model

**ViewModel:** `TransactionDetailViewModel`
**Screen State Type:** `TransactionDetailScreenState`

| Name                 | Type              | Default |
|----------------------|-------------------|---------|
| isLoading            | Boolean           | true    |
| transaction          | TransactionDetail?| null    |
| error                | UiError?          | null    |
| isDownloadingReceipt | Boolean           | false   |
| referenceCopied      | Boolean           | false   |

**Events:** `RetryLoad`, `DownloadReceipt`, `OpenDisputeForm`, `CopyReference`, `ShareTransaction`, `NavigateBack`

**Actions:** `loadTransactionDetail(transactionId)`, `downloadReceipt()`, `copyReferenceToClipboard()`, `openDisputeForm()`, `shareTransaction()`

**DI Dependencies:** `TransactionsRepository`, `ClipboardManager`, `ReceiptDownloader`, `DisputeFormLauncher`

**Errors:**
- `not_found`: "This transaction could not be found."
- `network_error`: "Network unavailable. Please check your connection."
- `receipt_download_failed`: "Receipt download failed. Please try again."
- `dispute_unavailable`: "Dispute form is temporarily unavailable."

---

## Navigation

| From               | To                 | Trigger                      | Type |
|--------------------|--------------------|------------------------------|------|
| transaction-detail | transaction-tags   | (deep-link from detail view) | push |
| transaction-detail | transactions       | NavigateBack                 | pop  |

---

## API Endpoints

| Endpoint                                                                                              | Auth        | Tag          | Purpose                               |
|-------------------------------------------------------------------------------------------------------|-------------|--------------|---------------------------------------|
| GET /obp/v5.1.0/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/transaction    | DirectLogin | Transactions | Fetch full transaction record by ID   |

---

## Design Tokens

| Token                          | Value   | Usage                                                              |
|--------------------------------|---------|--------------------------------------------------------------------|
| color.light.primary            | #4C662B | Hero background, copy icon, category label, download button text   |
| color.light.primary_container  | #CDEDA3 | Merchant logo background, category badge background                |
| color.light.error              | #BA1A1A | Debit amount color, report issue icon + link color                 |
| color.light.surface            | #FFFFFF | Merchant card, details card backgrounds                            |
| color.light.background         | #F9FAEF | Screen background, divider color                                   |
| color.light.on_surface         | #1A1C16 | Merchant name, detail values                                       |
| color.light.on_surface_variant | #44483D | Detail row labels, supporting metadata                             |
| typography.display_large       | —       | Hero amount "-£42.50" (57sp/700)                                   |
| typography.title_large         | —       | Merchant name "Tesco Supermarket" (22sp/600)                       |
| typography.body_medium         | —       | Detail row values (14sp/400–500)                                   |
| typography.label_medium        | —       | Status badge "Completed", report link (12sp/500)                   |
| typography.label_small         | —       | Detail row labels, category chip (11sp/500)                        |
| typography.body_small          | —       | IBAN / reference monospace values (12sp/400)                       |
| typography.label_large         | —       | Download Receipt button text (14sp/500)                            |
| radius.xl                      | 24dp    | Merchant card corner radius (spec: 20dp)                           |
| radius.lg                      | 16dp    | Details card corner radius                                         |
| radius.md                      | 12dp    | Download button, category badge radius                             |
| elevation.level4               | 8dp     | Merchant card elevation                                            |
| elevation.level1               | 1dp     | Details card elevation                                             |
| spacing.lg                     | 24dp    | Hero horizontal padding                                            |
| spacing.md                     | 16dp    | Section margins                                                    |

---

_Generated by /idea export | 2026-05-29_
