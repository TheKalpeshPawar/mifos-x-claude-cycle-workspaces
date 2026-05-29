# SPEC — Send Money

| Field         | Value               |
|---------------|---------------------|
| Feature       | send-money          |
| Flavor        | consumer            |
| Status        | approved            |
| Quality Score | 95                  |
| ViewModel     | SendMoneyViewModel  |

---

## Overview

Send Money is the payment initiation form for Consumer persona users. It allows users to select a source account, enter an amount with currency, choose a beneficiary (via search or recent beneficiaries), add a payment reference, pick a payment type (SEPA / Domestic / International), and see an estimated fee before proceeding to confirmation.

The form integrates four OBP endpoints: account listing (v5.1.0), counterparties (v4.0.0), IBAN validation (v4.0.0), funds availability check (v3.1.0), and SEPA transaction request submission (v5.1.0). The Continue button navigates to send-money-confirm after client-side validation passes. No bottom navigation — this is a focused form flow.

Pre-filled account: Primary Checking — £4,250.00 available. Recent beneficiaries: John Smith (Barclays UK) and Sarah Williams (HSBC UK). Default payment type: SEPA. Default fee estimate: Free.

---

## Screens

| ID         | Name       | Route | Layout | Scroll   |
|------------|------------|-------|--------|----------|
| send-money | Send Money | —     | Column | Vertical |

**Shell:** Top app bar ("Send Money", back arrow, no actions). No bottom navigation bar.

---

## Components

| ID                        | Type   | Description                                                                                       |
|---------------------------|--------|---------------------------------------------------------------------------------------------------|
| send_money_title          | text   | "Send Money" — Outfit/headline_large, #4C662B                                                   |
| from_account_selector     | input  | "From Account" — outlined, leading account_balance icon, trailing expand_more; pre-filled "Primary Checking — £4,250.00 available"; bg #F9FAEF, radius 12 |
| amount_input              | input  | "Amount" — number variant, prefix "£", placeholder "0.00", decimal keyboard, radius 12           |
| currency_selector         | input  | "Currency" — chip style, "GBP ▾"; opens currency picker; min_height 44dp                        |
| beneficiary_search        | input  | "To" — search variant, leading search icon, placeholder "Search beneficiary or enter account…", radius 12 |
| recent_beneficiaries_row  | stack  | Horizontal scroll row — recent beneficiary chips                                                  |
| recent_beneficiary_john   | box    | "John Smith · Barclays UK" — #CDEDA3 bg, radius 12; fires select_beneficiary                    |
| recent_beneficiary_sarah  | box    | "Sarah Williams · HSBC UK" — #CDEDA3 bg, radius 12; fires select_beneficiary                    |
| reference_input           | input  | "Reference" — text variant, placeholder "Payment for invoice #1234", max_length 35, helper "Max 35 characters", radius 12 |
| payment_type_selector     | stack  | Horizontal row of 3 payment type chips                                                           |
| payment_type_sepa         | input  | "SEPA" — chip, selected: bg #4C662B text #FFFFFF, radius 20; default selected                   |
| payment_type_domestic     | input  | "Domestic" — chip, unselected, radius 20                                                         |
| payment_type_international| input  | "International" — chip, unselected, radius 20                                                    |
| fee_estimate_banner       | box    | "Estimated fee: Free (SEPA)" — bg #CDEDA3, border #4C662B, radius 8, leading info_outline icon #4C662B |
| continue_button           | button | "Continue" — filled, bg #4C662B, text #FFFFFF, radius 12, full width, Outfit/label_large; navigates to send-money-confirm after validation |

---

## States

| ID          | Trigger                                 | Description                                                                              |
|-------------|-----------------------------------------|------------------------------------------------------------------------------------------|
| loading     | Screen entry — accounts + beneficiaries being fetched | Title + form skeleton; Continue disabled; linear progress indicator     |
| draft       | Accounts and beneficiaries loaded       | All form fields visible; Continue disabled (form incomplete); fee: "Free (SEPA)"        |
| content     | Alias for draft (default loaded state)  | Same as draft                                                                            |
| validating  | User taps Continue — validation in flight | Continue button loading spinner; linear progress indicator; inputs disabled             |
| empty       | No beneficiaries available              | Form with accounts; empty state message "No beneficiaries… Add a beneficiary first."     |
| error       | Validation failed / network error       | Field-level error messages on amount + beneficiary; network error banner with Retry      |

---

## State Model

**ViewModel:** `SendMoneyViewModel`
**Screen State Type:** `SendMoneyUiState`

| Name                  | Type          | Default                                    |
|-----------------------|---------------|--------------------------------------------|
| selectedAccountId     | String        | ""                                         |
| selectedAccountLabel  | String        | "Primary Checking — £4,250.00 available"   |
| amount                | String        | ""                                         |
| currency              | String        | "GBP"                                      |
| beneficiaryId         | String        | ""                                         |
| beneficiaryName       | String        | ""                                         |
| reference             | String        | ""                                         |
| paymentType           | PaymentType   | SEPA                                       |
| estimatedFee          | String        | "Free"                                     |
| uiState               | SendMoneyUiState | Draft                                   |

**Events:** `AccountSelected`, `AmountChanged`, `CurrencyChanged`, `BeneficiarySelected`, `ReferenceChanged`, `PaymentTypeChanged`, `ContinueClicked`, `ValidationFailed`, `ValidationSucceeded`

**DI Dependencies:** `AccountRepository`, `BeneficiaryRepository`, `PaymentRepository`, `FeeCalculatorUseCase`

**Errors:**
- `AMOUNT_REQUIRED`: "Please enter a valid amount greater than £0.01"
- `BENEFICIARY_REQUIRED`: "Please select a valid beneficiary"
- `ACCOUNT_REQUIRED`: "Please select a source account"
- `REFERENCE_TOO_LONG`: "Reference must be 35 characters or fewer"

---

## Navigation

| From       | To                | Trigger                                | Type  |
|------------|-------------------|----------------------------------------|-------|
| send-money | send-money-confirm| Continue tap + validation passes       | push  |
| send-money | (back)            | Back arrow tap                         | pop   |
| send-money | beneficiaries     | Add beneficiary (empty state CTA)      | push  |

---

## API Endpoints

| Endpoint                                                                                   | Auth        | Tag                 | Purpose                                  |
|--------------------------------------------------------------------------------------------|-------------|---------------------|------------------------------------------|
| GET /obp/v5.1.0/banks/{bankId}/accounts                                                   | DirectLogin | Accounts            | Populate from_account_selector           |
| GET /obp/v4.0.0/banks/{bankId}/accounts/{accountId}/{viewId}/counterparties               | DirectLogin | Counterparties      | Populate beneficiary_search + recents    |
| POST /obp/v4.0.0/account/check/scheme/iban                                                | DirectLogin | Account             | Validate IBAN entered by user            |
| GET /obp/v3.1.0/banks/{bankId}/accounts/{accountId}/owner/funds-available                 | DirectLogin | Account             | Check sufficient funds before Continue   |
| POST /obp/v5.1.0/banks/{bankId}/accounts/{accountId}/owner/transaction-request-types/SEPA/transaction-requests | DirectLogin | TransactionRequests | Initiate SEPA payment (on confirm screen)|

---

## Design Tokens

| Token                           | Value   | Usage                                                            |
|---------------------------------|---------|------------------------------------------------------------------|
| colors.light.primary            | #4C662B | Screen title, Continue button bg, SEPA chip bg, fee banner border+icon, recent beneficiary border |
| colors.light.primary_container  | #CDEDA3 | Fee estimate banner bg, recent beneficiary chip bg               |
| colors.light.on_primary         | #FFFFFF | Continue button text, SEPA chip text                             |
| colors.light.background         | #F9FAEF | Account selector bg, amount input bg                             |
| colors.light.outline            | #75796C | Input field borders (default state)                              |
| colors.light.surface_container  | #F0F1E6 | —                                                                |
| typography.headline_large       | —       | "Send Money" title                                               |
| typography.body_large           | —       | Input field values                                               |
| typography.label_large          | —       | Continue button text                                             |
| typography.label_medium         | —       | Currency selector, payment type chips                            |
| typography.body_medium          | —       | Recent beneficiary names, reference placeholder                  |
| radius.md                       | 12dp    | Account selector, amount input, beneficiary search, recent beneficiary chips, Continue button |
| radius.sm                       | 8dp     | Fee estimate banner                                              |
| radius.pill                     | 20dp    | Payment type selection chips                                     |

---

_Generated by /idea export | 2026-05-29_
