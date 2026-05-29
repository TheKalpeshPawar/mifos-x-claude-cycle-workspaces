# SPEC — Confirm Payment

| Field         | Value                        |
|---------------|------------------------------|
| Feature       | send-money-confirm           |
| Flavor        | consumer                     |
| Status        | approved                     |
| Quality Score | 93                           |
| ViewModel     | SendMoneyConfirmViewModel    |

---

## Overview

The Confirm Payment screen is the final authorisation gate in the consumer payment flow. Reached from the Send Money form, it displays a complete read-only summary of the payment — amount, recipient name and bank, IBAN, source account, payment reference, transaction fee, and total debit — before the user taps "Confirm & Send". An optional scheduled-date selector allows deferring an immediate payment. On confirmation the ViewModel posts to the OBP SEPA transaction-request endpoint; on success the screen is replaced by Home and a snackbar confirms "Payment of £500.00 sent to John Smith". An "Edit Payment" outlined button returns the user to the send-money form without losing state. No bottom navigation is shown — this screen is part of a focused payment journey.

---

## Screens

| ID                  | Name             | Route               | Layout | Scroll   |
|---------------------|------------------|---------------------|--------|----------|
| send-money-confirm  | Confirm Payment  | /send-money/confirm | Column | Vertical |

**Shell:** Top app bar only — title "Confirm Payment", back arrow (`arrow_back`). No bottom navigation bar.

| Bar Item   | Icon       | Action                      |
|------------|------------|-----------------------------|
| Back arrow | arrow_back | navigate back to send-money |

---

## Components

| ID                       | Type    | Description                                                                                                                            |
|--------------------------|---------|----------------------------------------------------------------------------------------------------------------------------------------|
| confirm_title            | text    | "Confirm Payment" — Outfit/headline_large, color #4C662B                                                                               |
| review_subtitle          | text    | "Please review the payment details before confirming" — Outfit/body_medium, color #44483D                                              |
| payment_summary_card     | box     | White card (border #CDEDA3 1dp, radius 16dp, elevation 2, pad_horizontal 20, pad_vertical 20) wrapping all detail rows                 |
| payment_amount           | text    | "£500.00" — Outfit/display_medium, color #4C662B, center-aligned; data-driven from `amount` state field                               |
| amount_divider           | divider | #E1E4D5, 1dp — separates amount from detail rows                                                                                       |
| to_row                   | stack   | Horizontal space-between, pad_vertical 10dp                                                                                            |
| to_label                 | text    | "To" — Outfit/body_medium, color #44483D                                                                                               |
| to_value                 | text    | "John Smith — Barclays Bank UK" — Outfit/body_large, color #1A1C16, weight 500; data-driven                                           |
| iban_row                 | stack   | Horizontal space-between, pad_vertical 10dp                                                                                            |
| iban_label               | text    | "IBAN" — Outfit/body_medium, color #44483D                                                                                             |
| iban_value               | text    | "GB29 NWBK 6016 1331 9268 19" — Outfit/body_medium, #1A1C16, font_family monospace; data-driven                                       |
| from_row                 | stack   | Horizontal space-between, pad_vertical 10dp                                                                                            |
| from_label               | text    | "From" — Outfit/body_medium, color #44483D                                                                                             |
| from_value               | text    | "Primary Checking (...0130)" — Outfit/body_medium, #1A1C16; data-driven                                                               |
| reference_row            | stack   | Horizontal space-between, pad_vertical 10dp                                                                                            |
| reference_label          | text    | "Reference" — Outfit/body_medium, color #44483D                                                                                        |
| reference_value          | text    | "Rent August 2026" — Outfit/body_medium, #1A1C16; data-driven                                                                         |
| fee_divider              | divider | #E1E4D5, 1dp — separates detail rows from fee/total summary                                                                           |
| fee_row                  | stack   | Horizontal space-between, pad_vertical 10dp                                                                                            |
| fee_label                | text    | "Fee" — Outfit/body_medium, color #44483D                                                                                              |
| fee_value                | text    | "£0.00" — Outfit/body_medium, color #386663 (teal — signals zero cost)                                                                |
| total_row                | stack   | Horizontal space-between, background #F9FAEF, radius 8, pad_horizontal 8, pad_vertical 8                                              |
| total_label              | text    | "Total" — Outfit/title_large, color #1A1C16, weight 700                                                                               |
| total_value              | text    | "£500.00" — Outfit/title_large, color #4C662B, weight 700; data-driven                                                                |
| scheduled_date_selector  | input   | Outlined "Scheduled for: Immediate", trailing icon calendar_today, radius 12, pad_top 16; opens date picker on tap                    |
| terms_text               | text    | "By confirming you authorise this payment per our Terms of Service" — Outfit/body_small, #44483D, center-aligned, pad_vertical 8      |
| confirm_send_button      | button  | "Confirm & Send" — filled, bg #4C662B, text #FFFFFF, radius 12, full-width, Outfit/label_large; disabled while loading/submitting     |
| edit_payment_button      | button  | "Edit Payment" — outlined, border #4C662B, text #4C662B, radius 12, full-width, Outfit/label_large; navigates back to send-money      |

---

## States

| ID         | Trigger                                    | Description                                                                                       |
|------------|--------------------------------------------|---------------------------------------------------------------------------------------------------|
| loading    | Screen entry while payment data resolves   | Shimmer on amount, to_value, iban_value, from_value, reference_value, fee_value, total_value; both buttons disabled; linear progress bar |
| review     | Data loaded — awaiting user action         | Full summary card with all rows populated; Confirm & Send enabled                                 |
| content    | Alias for review (default loaded state)    | Same layout as review                                                                             |
| submitting | ConfirmClicked                             | Confirm button shows loading spinner; both buttons disabled; linear progress top                  |
| success    | PaymentSucceeded event                     | Snackbar "Payment of £500.00 sent to John Smith"; auto-navigate to home (replace stack)           |
| error      | PaymentFailed event                        | Inline error banner "Payment could not be processed. Please try again."; Confirm re-enabled       |
| empty      | No transaction data to confirm             | Empty-state message "No transaction to confirm. Start a new payment."; Edit Payment button only  |

---

## State Model

**ViewModel:** `SendMoneyConfirmViewModel`
**Screen State Type:** `ConfirmPaymentUiState`

| Name              | Type                  | Default       |
|-------------------|-----------------------|---------------|
| amount            | String                | ""            |
| currency          | String                | "GBP"         |
| beneficiaryName   | String                | ""            |
| beneficiaryBank   | String                | ""            |
| iban              | String                | ""            |
| fromAccountLabel  | String                | ""            |
| reference         | String                | ""            |
| fee               | String                | "£0.00"       |
| total             | String                | ""            |
| scheduledDate     | String                | "Immediate"   |
| uiState           | ConfirmPaymentUiState | Review        |

**Events:** `ScheduleDateSelected`, `ConfirmClicked`, `EditClicked`, `PaymentSucceeded`, `PaymentFailed`

**Actions:** `submit`, `navigate`, `select_schedule_date`

**DI Dependencies:** `PaymentRepository`, `TransactionRequestUseCase`, `AccountRepository`

**Errors:**

| Code                 | Message                                                      |
|----------------------|--------------------------------------------------------------|
| PAYMENT_FAILED       | "Payment could not be processed. Please try again."         |
| INSUFFICIENT_FUNDS   | "Insufficient funds in your account."                       |
| INVALID_BENEFICIARY  | "The beneficiary account details are invalid."              |
| DAILY_LIMIT_EXCEEDED | "This payment exceeds your daily transfer limit."           |

---

## Navigation

| From               | To         | Trigger                              | Type    |
|--------------------|------------|--------------------------------------|---------|
| send-money-confirm | home       | PaymentSucceeded — auto after success| replace |
| send-money-confirm | send-money | edit_payment_button tap              | pop     |
| send-money-confirm | home       | back arrow tap (if not in progress)  | pop     |

---

## API Endpoints

| Endpoint                                                                                                                     | Method | Auth        | Tag                 | Purpose                      |
|------------------------------------------------------------------------------------------------------------------------------|--------|-------------|---------------------|------------------------------|
| /obp/v5.1.0/banks/{bankId}/accounts/{accountId}/owner/transaction-request-types/SEPA/transaction-requests | POST   | DirectLogin | TransactionRequests | Submit confirmed SEPA payment |

---

## Design Tokens

| Token                           | Value     | Usage                                                                            |
|---------------------------------|-----------|----------------------------------------------------------------------------------|
| colors.light.primary            | #4C662B   | confirm_title, payment_amount, total_value, confirm_send_button background       |
| colors.light.on_primary         | #FFFFFF   | confirm_send_button text                                                          |
| colors.light.secondary          | #386663   | fee_value text (teal — zero-cost signal)                                         |
| colors.light.primary_container  | #CDEDA3   | payment_summary_card border color                                                |
| colors.light.on_surface         | #1A1C16   | to_value, iban_value, from_value, reference_value, total_label                  |
| colors.light.on_surface_variant | #44483D   | review_subtitle, row label texts (To/IBAN/From/Reference/Fee), terms_text        |
| colors.light.surface_variant    | #E1E4D5   | amount_divider, fee_divider                                                      |
| colors.light.background         | #F9FAEF   | total_row highlight background                                                   |
| colors.light.outline            | #75796C   | scheduled_date_selector border                                                   |
| typography.display_medium       | 45sp/400  | payment_amount                                                                   |
| typography.title_large          | 22sp/400  | total_label, total_value                                                         |
| typography.headline_large       | 32sp/400  | confirm_title                                                                    |
| typography.body_large           | 16sp/400  | to_value                                                                         |
| typography.body_medium          | 14sp/400  | review_subtitle, row labels and values (IBAN/From/Reference/Fee)                |
| typography.body_small           | 12sp/400  | terms_text                                                                       |
| typography.label_large          | 14sp/500  | button labels                                                                    |
| radius.md                       | 12dp      | confirm_send_button and edit_payment_button corner radius                        |
| radius.xl                       | 16dp      | payment_summary_card corner radius                                               |
| radius.sm                       | 8dp       | total_row corner radius                                                          |
| spacing.md                      | 16dp      | horizontal padding, scheduled_date_selector margin_top                           |
| spacing.sm                      | 8dp       | total_row padding, terms_text padding_vertical                                   |

---

_Generated by /idea export | 2026-05-29_
