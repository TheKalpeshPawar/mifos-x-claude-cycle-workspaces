# Send Money — Feature Specification

| Field | Value |
|---|---|
| Feature | send-money |
| Flavor | consumer |
| Status | enriched |
| Quality Score | 82 |

---

## Overview

The Send Money screen is the primary payment initiation surface in the Mifos X Open Banking consumer app. Users select a source account, enter an amount and currency, choose or search for a beneficiary, enter a payment reference, and select a payment type (SEPA, Domestic, or International). The screen performs real-time fee estimation and IBAN/funds validation before routing to the confirmation step.

---

## Screens

| Screen ID | Route | Layout | Scroll |
|---|---|---|---|
| send-money | /send-money | form | vertical |

---

## Components

| ID | Type | Description |
|---|---|---|
| send_money_title | text | Headline "Send Money" in primary #1800B1 |
| from_account_selector | input | Outlined dropdown — "Primary Checking — £4,250.00 available" |
| amount_input | input | Decimal number field with £ prefix, placeholder "0.00" |
| currency_selector | input | Filter chip — "GBP ▾", opens currency picker |
| beneficiary_search | input | Search field — "Search beneficiary or enter account..." |
| recent_beneficiaries_row | stack | Horizontal scroll row of recent beneficiary chips |
| recent_beneficiary_john | box | Chip — "John Smith · Barclays UK" |
| recent_beneficiary_sarah | box | Chip — "Sarah Williams · HSBC UK" |
| reference_input | input | Text field, max 35 chars, placeholder "Payment for invoice #1234" |
| payment_type_selector | stack | Horizontal radio-chip group |
| payment_type_sepa | input | Filter chip — "SEPA", selected by default (#1800B1) |
| payment_type_domestic | input | Filter chip — "Domestic", unselected |
| payment_type_international | input | Filter chip — "International", unselected |
| fee_estimate_banner | box | Green info banner — "Estimated fee: Free (SEPA)" |
| continue_button | button | Filled primary button — "Continue" → send-money-confirm |

---

## States

| State ID | Trigger | Description |
|---|---|---|
| draft | Screen load | Empty form, all fields ready, continue disabled, recent beneficiaries visible |
| validating | User taps Continue | Continue button shows loading indicator, linear progress bar shown |
| error | Validation fails | Inline field errors on amount / beneficiary, continue disabled |

---

## State Model

**ViewModel:** `SendMoneyViewModel`

| Field | Type | Default |
|---|---|---|
| selectedAccountId | String | "" |
| selectedAccountLabel | String | "Primary Checking — £4,250.00 available" |
| amount | String | "" |
| currency | String | "GBP" |
| beneficiaryId | String | "" |
| beneficiaryName | String | "" |
| reference | String | "" |
| paymentType | PaymentType | SEPA |
| estimatedFee | String | "Free" |
| uiState | SendMoneyUiState | Draft |

**Events:** AccountSelected, AmountChanged, CurrencyChanged, BeneficiarySelected, ReferenceChanged, PaymentTypeChanged, ContinueClicked, ValidationFailed, ValidationSucceeded

**Actions:** select_account, search_beneficiary, select_beneficiary, select_currency, select_payment_type_sepa, select_payment_type_domestic, select_payment_type_international, validate, focus_amount, focus_reference

**DI Dependencies:** AccountRepository, BeneficiaryRepository, PaymentRepository, FeeCalculatorUseCase

**Validation Errors:**

| Field | Code | Message |
|---|---|---|
| amount | AMOUNT_REQUIRED | "Please enter a valid amount greater than £0.01" |
| beneficiary | BENEFICIARY_REQUIRED | "Please select a valid beneficiary" |
| account | ACCOUNT_REQUIRED | "Please select a source account" |
| reference | REFERENCE_TOO_LONG | "Reference must be 35 characters or fewer" |

---

## Navigation

| From | To | Trigger | Type |
|---|---|---|---|
| send-money | send-money-confirm | continue_button tap (after validation) | push |

---

## API Endpoints

| Endpoint | Auth | Purpose |
|---|---|---|
| GET /obp/v5.1.0/banks/{bankId}/accounts | DirectLogin | Load user accounts for "From" selector |
| GET /obp/v4.0.0/banks/{bankId}/accounts/{accountId}/{viewId}/counterparties | DirectLogin | Load beneficiary list for search |
| POST /obp/v5.1.0/banks/{bankId}/accounts/{accountId}/owner/transaction-request-types/SEPA/transaction-requests | DirectLogin | Initiate SEPA payment request |
| POST /obp/v4.0.0/account/check/scheme/iban | DirectLogin | Validate IBAN before payment |
| GET /obp/v3.1.0/banks/{bankId}/accounts/{accountId}/owner/funds-available | DirectLogin | Check sufficient funds pre-submission |

---

## Design Tokens

| Token | Value | Usage |
|---|---|---|
| primary | #1800B1 | Title, SEPA chip selected, continue button |
| background | #FCF8FF | Screen background |
| surface | #F5F5FF | Account selector background |
| success | #4CAF50 | Fee banner border and icon |
| fee_banner_bg | #E8F5E9 | Fee estimate banner background |
| recent_chip_bg | #F0F0FF | Recent beneficiary chip background |
| error | #BA1A1A | Field validation error text |

---

*Generated by /idea export | 2026-05-25*
