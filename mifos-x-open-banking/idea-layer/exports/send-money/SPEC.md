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

Send Money is the payment initiation form for Consumer persona users. It allows users to select a source account (Equity Jijenge Savings — *4521 at KES 87,430.50 or Equity Current — *7803 at KES 23,150.00), enter an amount with currency (default GBP selector), search or select a recent beneficiary (Wycliffe Ochieng at KCB, Naomi Gitau at Co-op Bank, Salim Abdalla at Absa, Margaret Wairimu at Equity), add a payment reference (max 35 characters), pick a payment type (SEPA / Domestic / International), and review an estimated fee before tapping Continue.

The form integrates five OBP endpoints: account listing (v5.1.0), counterparties (v4.0.0), IBAN validation (v4.0.0), funds availability check (v3.1.0), and SEPA transaction request submission (v5.1.0). The Continue button navigates to send-money-confirm after client-side validation passes. No bottom navigation — this is a focused, single-task form flow accessed from the Home or Accounts screens.

Default payment type is SEPA with estimated fee shown as Free. Field-level errors appear for missing amount, invalid beneficiary, missing source account, and overly long reference.

---

## Screens

| ID         | Name       | Route | Layout | Scroll   |
|------------|------------|-------|--------|----------|
| send-money | Send Money | —     | Column | Vertical |

**Shell:** Top app bar ("Send Money", back/arrow_back navigation icon, no action icons). No bottom navigation bar.

---

## Components

| ID                         | Type   | Description                                                                                                                       |
|----------------------------|--------|-----------------------------------------------------------------------------------------------------------------------------------|
| send_money_title           | text   | "Send Money" — Outfit/headline_large, #4C662B, sm bottom padding                                                                 |
| from_account_selector      | input  | "From Account" — outlined variant, leading account_balance icon, trailing expand_more icon; content "Primary Checking — £4,250.00 available"; bg #F9FAEF, radius 12dp |
| amount_input               | input  | "Amount" — number variant, prefix "£", placeholder "0.00", decimal keyboard, radius 12dp                                         |
| currency_selector          | input  | "Currency" — chip/filter variant, content "GBP ▾"; min_height 44dp, radius 8dp, opens currency picker                            |
| beneficiary_search         | input  | "To" — search variant, leading search icon, placeholder "Search beneficiary or enter account…", radius 12dp                      |
| recent_beneficiaries_row   | stack  | Horizontal scroll row (spacing 12dp) — contains recent beneficiary chips; role: list                                             |
| recent_beneficiary_john    | box    | "John Smith · Barclays UK" — #CDEDA3 bg, border #CDEDA3 1dp, radius 12dp, padding 12×8dp; fires select_beneficiary               |
| recent_beneficiary_sarah   | box    | "Sarah Williams · HSBC UK" — #CDEDA3 bg, border #CDEDA3 1dp, radius 12dp, padding 12×8dp; fires select_beneficiary               |
| reference_input            | input  | "Reference" — text variant, placeholder "Payment for invoice #1234", max_length 35, helper "Max 35 characters", radius 12dp     |
| payment_type_selector      | stack  | Horizontal row (spacing 8dp) — groups three payment type chips; role: radio_group                                                |
| payment_type_sepa          | input  | "SEPA" — chip/filter, selected: bg #4C662B, text #FFFFFF; radius 20dp; default selected                                          |
| payment_type_domestic      | input  | "Domestic" — chip/filter, unselected; radius 20dp                                                                                |
| payment_type_international | input  | "International" — chip/filter, unselected; radius 20dp                                                                           |
| fee_estimate_banner        | box    | "Estimated fee: Free (SEPA)" — bg #CDEDA3, border #4C662B 1dp, radius 8dp, leading info_outline icon #4C662B; role: status       |
| continue_button            | button | "Continue" — filled, bg #4C662B, text #FFFFFF, radius 12dp, full width, Outfit/label_large; validates form then navigates to send-money-confirm |

---

## States

| ID          | Trigger                                           | Description                                                                                              |
|-------------|---------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| loading     | Screen entry — accounts + counterparties fetching | Title visible; from_account_selector, amount_input, beneficiary_search, recent rows, fee banner shimmer; linear progress indicator; Continue disabled |
| draft       | Accounts and counterparties loaded                | All 15 components visible; Continue disabled (form incomplete); fee banner "Estimated fee: Free (SEPA)" |
| content     | Alias for draft (default loaded state)            | Same as draft — accounts and beneficiaries loaded, all fields available                                  |
| validating  | User taps Continue — validation in flight         | Continue button shows loading spinner; linear progress indicator; continue_button_loading true            |
| empty       | No counterparties/beneficiaries available         | Title + from_account_selector + amount_input + currency_selector + beneficiary_search + Continue; empty message "No beneficiaries available to send money to. Add a beneficiary first." |
| error       | Validation failed or network error                | Full form visible; amount_input shows "Please enter a valid amount greater than £0.01"; beneficiary_search shows "Please select a valid beneficiary"; network error banner "Could not process payment" with Retry action |

---

## State Model

**ViewModel:** `SendMoneyViewModel`
**Screen State Type:** `SendMoneyUiState`

| Name                 | Type             | Default                                  |
|----------------------|------------------|------------------------------------------|
| selectedAccountId    | String           | ""                                       |
| selectedAccountLabel | String           | "Primary Checking — £4,250.00 available" |
| amount               | String           | ""                                       |
| currency             | String           | "GBP"                                    |
| beneficiaryId        | String           | ""                                       |
| beneficiaryName      | String           | ""                                       |
| reference            | String           | ""                                       |
| paymentType          | PaymentType      | SEPA                                     |
| estimatedFee         | String           | "Free"                                   |
| uiState              | SendMoneyUiState | Draft                                    |

**Events:** `AccountSelected`, `AmountChanged`, `CurrencyChanged`, `BeneficiarySelected`, `ReferenceChanged`, `PaymentTypeChanged`, `ContinueClicked`, `ValidationFailed`, `ValidationSucceeded`

**Actions:** `select_account`, `search_beneficiary`, `select_beneficiary`, `select_currency`, `select_payment_type_sepa`, `select_payment_type_domestic`, `select_payment_type_international`, `validate`, `focus_amount`, `focus_reference`

**DI Dependencies:** `AccountRepository`, `BeneficiaryRepository`, `PaymentRepository`, `FeeCalculatorUseCase`

**Errors:**
- `AMOUNT_REQUIRED`: "Please enter a valid amount greater than £0.01"
- `BENEFICIARY_REQUIRED`: "Please select a valid beneficiary"
- `ACCOUNT_REQUIRED`: "Please select a source account"
- `REFERENCE_TOO_LONG`: "Reference must be 35 characters or fewer"

---

## Navigation

| From       | To                | Trigger                                      | Type |
|------------|-------------------|----------------------------------------------|------|
| send-money | send-money-confirm| Continue tap — validation passes             | push |
| send-money | (back)            | arrow_back navigation icon tap               | pop  |
| send-money | beneficiaries     | "Add a beneficiary" CTA in empty state       | push |

---

## API Endpoints

| Endpoint                                                                                                                       | Auth        | Tag                 | Purpose                                               |
|--------------------------------------------------------------------------------------------------------------------------------|-------------|---------------------|-------------------------------------------------------|
| GET /obp/v5.1.0/banks/{bankId}/accounts                                                                                       | DirectLogin | Accounts            | Populate from_account_selector dropdown               |
| GET /obp/v4.0.0/banks/{bankId}/accounts/{accountId}/{viewId}/counterparties                                                   | DirectLogin | Counterparties      | Populate beneficiary_search results + recent row chips |
| POST /obp/v4.0.0/account/check/scheme/iban                                                                                    | DirectLogin | Account             | Validate IBAN entered manually in beneficiary_search  |
| GET /obp/v3.1.0/banks/{bankId}/accounts/{accountId}/owner/funds-available                                                     | DirectLogin | Account             | Check sufficient funds before Continue is enabled     |
| POST /obp/v5.1.0/banks/{bankId}/accounts/{accountId}/owner/transaction-request-types/SEPA/transaction-requests               | DirectLogin | TransactionRequests | Initiate SEPA payment (triggered from send-money-confirm) |

---

## Design Tokens

| Token                          | Value   | Usage                                                                              |
|--------------------------------|---------|------------------------------------------------------------------------------------|
| colors.light.primary           | #4C662B | Screen title, Continue button bg, SEPA chip selected bg, fee banner border + icon  |
| colors.light.primary_container | #CDEDA3 | Fee estimate banner bg, recent beneficiary chip bg + border                        |
| colors.light.on_primary        | #FFFFFF | Continue button text, SEPA chip selected text                                      |
| colors.light.background        | #F9FAEF | from_account_selector background                                                   |
| colors.light.outline           | #75796C | Outlined input field borders (idle state)                                          |
| colors.light.error             | #BA1A1A | Field error text color (amount, beneficiary)                                       |
| typography.headline_large      | Outfit 32sp/400 | "Send Money" screen title                                               |
| typography.label_large         | Outfit 14sp/500 | Continue button label                                                   |
| typography.body_large          | Outfit 16sp/400 | Input field entered values                                              |
| typography.label_medium        | Outfit 12sp/500 | Currency chip, payment type chip labels                                 |
| typography.body_medium         | Outfit 14sp/400 | Recent beneficiary names, helper text                                   |
| typography.body_small          | Outfit 12sp/400 | Helper text "Max 35 characters"                                         |
| radius.md                      | 12dp    | from_account_selector, amount_input, beneficiary_search, recent chips, Continue    |
| radius.sm                      | 8dp     | Fee estimate banner, currency_selector chip                                        |
| radius.pill                    | 20dp    | Payment type selection chips (SEPA / Domestic / International)                     |
| spacing.sm                     | 8dp     | Payment type chip row spacing                                                      |
| spacing.md                     | 16dp    | Standard section padding                                                           |
| touchTargets.min_touch_target  | 48dp    | currency_selector min_height 44dp (⚠ near minimum — verify in implementation)     |

---

_Generated by /idea export | 2026-05-30_
