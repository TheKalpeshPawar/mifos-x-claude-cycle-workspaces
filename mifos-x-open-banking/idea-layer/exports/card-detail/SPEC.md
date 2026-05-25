# Card Detail — Feature Specification

| Field | Value |
|---|---|
| Feature | card-detail |
| Flavor | consumer |
| Status | enriched |
| Quality Score | 79 |

---

## Overview

The Card Detail screen provides full management controls for a single payment card. It renders an enlarged card visual with masked PAN, a biometric-gated "Show card details" link to reveal full PAN/CVV/expiry, a live active/frozen status toggle, spending limit display and editing, and destructive actions (Freeze, Report Lost/Stolen). The screen also offers a shortcut to view all transactions for that card.

---

## Screens

| Screen ID | Route | Layout | Scroll |
|---|---|---|---|
| card-detail | /cards/{cardId} | detail_screen | vertical |

**Shell:** Back navigation (arrow_back). Top bar "Card Details" with `more_vert` action for overflow menu.

---

## Components

| ID | Type | Description |
|---|---|---|
| card_visual | box | Enlarged card — gradient #1800B1→#4B35E8, 340×210dp, elevation 12, auto-centered |
| card_number_display | text | "•••• •••• •••• 4521", white monospace |
| cardholder_name | text | "ALEX JOHNSON", uppercase #E0DDFF |
| card_expiry | text | "09/29", monospace #C5BFFF |
| card_network_logo | image | Visa logo, 60×22dp, white tinted |
| reveal_card_details_link | link | "Show card details" — underlined, triggers biometric auth |
| card_status_row | stack | Horizontal row with "Card Active" label and toggle switch |
| card_status_label | text | "Card Active", body_large, #111111 medium weight |
| card_status_switch | input | Switch: green when active (#4CAF50), grey when off (#9E9E9E) |
| limits_section | box | White card container for spending limits |
| limits_section_title | text | "Spending Limits", title_medium, semibold |
| daily_limit_row | stack | "Daily limit / £2,500 / edit icon", tappable |
| daily_limit_value | text | "£2,500" |
| daily_limit_edit_icon | icon | `edit` icon, 20dp, #1800B1 |
| monthly_limit_row | stack | "Monthly limit / £10,000 / edit icon", tappable |
| monthly_limit_value | text | "£10,000" |
| monthly_limit_edit_icon | icon | `edit` icon, 20dp, #1800B1 |
| freeze_card_button | button | Outlined "Freeze Card" — orange border/text #FF9800, ac_unit icon |
| report_lost_button | button | Outlined "Report Lost/Stolen" — red border/text #FF5252 |
| view_transactions_button | button | Text variant "View Transactions" — #1800B1, receipt_long icon |

---

## States

| State ID | Trigger | Description |
|---|---|---|
| loading | Screen entry | Skeleton card visual + 4 skeleton fields |
| content | Card data loaded | Full card visual, active status, limits, action buttons |
| frozen | Card status is frozen | Card visual shows grey "FROZEN" overlay, switch off, Freeze button becomes "Unfreeze Card" (green), reveal_card_details_link hidden |
| error | API failure | Error state: credit_card_off icon, "Unable to load card details", retry button |

---

## State Model

**ViewModel:** `CardDetailViewModel`

| Field | Type | Default |
|---|---|---|
| cardId | String | "" |
| cardNumber | String | "" |
| cardholderName | String | "" |
| expiryDate | String | "" |
| cardNetwork | CardNetwork | Visa |
| isActive | Boolean | true |
| isFrozen | Boolean | false |
| dailyLimit | String | "£2,500" |
| monthlyLimit | String | "£10,000" |
| isRevealed | Boolean | false |
| uiState | CardDetailUiState | Loading |

**Events:** CardLoaded, RevealCardDetailsRequested, BiometricAuthSucceeded, BiometricAuthFailed, CardStatusToggled, EditLimitClicked, FreezeCardClicked, ReportLostClicked, ViewTransactionsClicked

**Actions:** reveal_card_details, toggle_card_status, edit_limit, freeze_card, report_lost, navigate, open_card_options_menu

**DI Dependencies:** CardRepository, BiometricAuthUseCase, CardLimitRepository

**Error Codes:**

| Field | Code | Message |
|---|---|---|
| global | LOAD_FAILED | "Unable to load card details. Please try again." |
| freeze | FREEZE_FAILED | "Failed to freeze card. Please contact support." |
| report_lost | REPORT_FAILED | "Failed to report card. Please call 0800 123 456." |

---

## Navigation

| From | To | Trigger | Type |
|---|---|---|---|
| card-detail | cards | Back arrow | pop |
| card-detail | transactions | view_transactions_button tap | push |

---

## API Endpoints

| Endpoint | Auth | Purpose |
|---|---|---|
| GET /obp/v5.1.0/banks/{bankId}/cards/{cardId} | DirectLogin | Load full card details for this screen |

---

## Design Tokens

| Token | Value | Usage |
|---|---|---|
| primary | #1800B1 | Card gradient start, edit icons, view transactions |
| card_gradient_end | #4B35E8 | Card visual gradient end |
| card_text | #FFFFFF | Card PAN, cardholder name |
| card_secondary_text | #E0DDFF | Cardholder name tint |
| card_expiry_text | #C5BFFF | Expiry date |
| active_switch | #4CAF50 | Switch on-state |
| frozen_switch | #9E9E9E | Switch off-state |
| freeze_button | #FF9800 | Freeze Card border and text (warning amber) |
| report_button | #FF5252 | Report Lost border and text (danger red) |
| surface | #FFFFFF | Card status row, limits section background |

---

*Generated by /idea export | 2026-05-25*
