# Feature Specification — Transaction Detail
**Feature:** transaction-detail | **Flavor:** consumer | **Status:** enriched | **Quality Score:** 82

---

## Overview

The Transaction Detail screen delivers a full-fidelity receipt view for a single bank transaction. A full-bleed deep-purple hero section displays the signed amount prominently alongside a completion status badge. Overlapping the hero, a merchant card surfaces the counterparty name, logo, and spending category. A structured detail card itemises date/time, reference number (copyable), transaction type, source account, and destination beneficiary. Users can download a PDF receipt or report a dispute through in-screen CTAs. The screen has no bottom navigation, keeping the user focused on the transaction context.

---

## Screens

| Screen ID | Label | Route | Layout | Scroll |
|---|---|---|---|---|
| transaction_detail_content | Transaction Detail | /transactions/{transactionId} | Vertical scroll, top app bar with back + share | vertical |

---

## Components

| ID | Type | Description |
|---|---|---|
| amount_hero_section | box | Full-bleed #1800B1 hero: signed amount (-£42.50) + "Completed" status badge |
| amount_hero_value | text | "-£42.50" — display_large, #FF8A80 (soft red on dark), weight 700, center-aligned |
| status_badge | box | "Completed" pill — #4CAF5033 bg, #69F0AE text, check_circle icon |
| merchant_card | box | Overlaps hero (margin_top -20); merchant logo (56px) + name + category badge |
| merchant_name | text | "Tesco Supermarket" — title_large, #1A1A1A, weight 600 |
| category_badge | box | "Groceries" chip — #E8F5E9 bg, #2E7D32 text, label_small |
| details_card | box | Structured field rows: Date & Time / Reference / Transaction Type / From Account / To Beneficiary |
| detail_date_value | text | "25 May 2026, 14:32" — body_medium, #1A1A1A, weight 500 |
| detail_reference_value | text | "SEPA-2026051500123" — body_small, monospace |
| copy_reference_icon | icon | content_copy 16px, #1800B1 — copies reference to clipboard |
| detail_type_value | text | "SEPA Credit Transfer" — body_medium, #1A1A1A, weight 500 |
| detail_from_account_name | text | "Primary Checking" + "...0130" IBAN suffix |
| detail_to_name | text | "Tesco PLC" + "DE89 3704...0044" masked IBAN |
| download_receipt_button | button | Outlined #1800B1, download icon, "Download Receipt", full-width minus margins |
| report_issue_row | stack | flag icon (#FF5252) + "Report an Issue" link (#FF5252) — centered |

---

## States

| ID | Trigger | Description |
|---|---|---|
| loading | ScreenOpened / RetryLoad | Skeleton: hero block (160px) + merchant card overlap + details card (300px) + actions bar |
| content | Transaction loaded | Full hero, merchant card, details card, download + report CTAs |
| error | Not found / network failure | Error card: "Transaction not found", CTA "Go Back" (navigate_back) |

---

## State Model

**ViewModel:** `TransactionDetailViewModel`
**ScreenState:** `TransactionDetailScreenState`

| Field | Type | Default |
|---|---|---|
| isLoading | Boolean | true |
| transaction | TransactionDetail? | null |
| error | UiError? | null |
| isDownloadingReceipt | Boolean | false |
| referenceCopied | Boolean | false |

**Events:** RetryLoad · DownloadReceipt · OpenDisputeForm · CopyReference · ShareTransaction · NavigateBack

**Actions:** loadTransactionDetail(transactionId, triggers: ScreenOpened/RetryLoad) · downloadReceipt · copyReferenceToClipboard · openDisputeForm · shareTransaction

**DI:** TransactionsRepository · ClipboardManager · ReceiptDownloader · DisputeFormLauncher

---

## Navigation

| From | To | Trigger | Type |
|---|---|---|---|
| transaction-detail | transactions | Top app bar back arrow | pop |
| transaction-detail | (share sheet) | Top app bar share icon | system sheet |
| transaction-detail | (dispute form) | Tap "Report an Issue" | push / bottom sheet |

---

## API Endpoints

| Endpoint | Auth | Purpose |
|---|---|---|
| GET /obp/v5.1.0/banks/{bankId}/accounts/{accountId}/owner/transactions/{transactionId}/transaction | DirectLogin | Fetch full transaction with counterparty, routing, and metadata |

---

## Design Tokens

| Token | Value | Usage |
|---|---|---|
| color.primary | #1800B1 | Hero background, outlined button border/text, copy icon |
| color.debit_on_dark | #FF8A80 | Debit amount on dark hero (lightened for contrast) |
| color.status_success_bg | #4CAF5033 | Status badge background (20% green) |
| color.status_success_text | #69F0AE | Status badge text and icon (light green on dark) |
| color.surface | #FFFFFF | Merchant card + details card backgrounds |
| color.error | #FF5252 | "Report an Issue" text and flag icon |
| color.groceries_badge | #E8F5E9 / #2E7D32 | Category badge |
| color.secondary_text | #666666 | Detail field labels |
| color.mono_text | #1A1A1A | Detail field values |
| typography.display_large | — | Hero amount |
| typography.title_large | — | Merchant name |
| typography.body_medium | — | Detail field values |
| typography.body_small / monospace | — | Reference number, masked IBANs |
| typography.label_medium | — | Status badge label, "Report an Issue" |
| elevation.merchant_card | 4 | Merchant card overlap shadow |

---

_Generated by /idea export | 2026-05-25_
