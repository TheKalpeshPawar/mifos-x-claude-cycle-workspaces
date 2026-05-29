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

The Confirm Payment screen is the final authorisation gate in the consumer payment flow. Reached from the Send Money form, it displays a complete read-only summary of the payment — amount (£500.00 at display_medium scale), recipient name and bank (John Smith — Barclays Bank UK), IBAN (GB29 NWBK 6016 1331 9268 19), source account (Primary Checking ...0130), payment reference (Rent August 2026), transaction fee (£0.00), and a highlighted total row (£500.00). An outlined date-selector field allows scheduling the payment (default: Immediate). A legal notice precedes the two action buttons: "Confirm & Send" (filled primary) submits the OBP SEPA transaction request; "Edit Payment" (outlined) navigates back to the send-money entry screen. On success the screen is replaced by Home and a snackbar confirms "Payment of £500.00 sent to John Smith". The screen is mobile-only (390px baseline) with no bottom navigation bar — the top app bar (title "Confirm Payment", back arrow) is the sole chrome.

---

## Screens

| ID                  | Name             | Route               | Layout | Scroll   |
|---------------------|------------------|---------------------|--------|----------|
| send-money-confirm  | Confirm Payment  | /send-money/confirm | Column | Vertical |

**Shell:** Top app bar only — title "Confirm Payment", navigation_icon `arrow_back`. No bottom navigation bar.

| Bar Item   | Icon       | Action                      |
|------------|------------|-----------------------------|
| Back arrow | arrow_back | navigate back to send-money |

---

## Components

| ID                       | Type    | Description                                                                                                                            |
|--------------------------|---------|----------------------------------------------------------------------------------------------------------------------------------------|
| confirm_title            | text    | "Confirm Payment" — Outfit/headline_large, #4C662B, xs bottom padding; a11y role: heading                                             |
| review_subtitle          | text    | "Please review the payment details before confirming" — Outfit/body_medium, #44483D, md bottom padding                                |
| payment_summary_card     | box     | White (#FFFFFF) card — 16dp radius, elevation 2, 20dp horizontal + vertical padding, 1dp #CDEDA3 border; wraps all detail rows        |
| payment_amount           | text    | "£500.00" — Outfit/display_medium, #4C662B, center-aligned; sm top + md bottom padding; data-driven from `amount` state field         |
| amount_divider           | divider | #E1E4D5, 1dp — separates hero amount from detail rows                                                                                  |
| to_row                   | stack   | Horizontal, space-between, 10dp vertical padding — groups to_label + to_value                                                         |
| to_label                 | text    | "To" — Outfit/body_medium, #44483D (9.37:1 on #FFFFFF — WCAG AA pass; A11Y-002 fix applied)                                          |
| to_value                 | text    | "John Smith — Barclays Bank UK" — Outfit/body_large, #1A1C16, weight 500; data-driven from beneficiaryName + beneficiaryBank           |
| iban_row                 | stack   | Horizontal, space-between, 10dp vertical padding — groups iban_label + iban_value                                                     |
| iban_label               | text    | "IBAN" — Outfit/body_medium, #44483D                                                                                                   |
| iban_value               | text    | "GB29 NWBK 6016 1331 9268 19" — Outfit/body_medium, #1A1C16, monospace font family; data-driven                                       |
| from_row                 | stack   | Horizontal, space-between, 10dp vertical padding — groups from_label + from_value                                                     |
| from_label               | text    | "From" — Outfit/body_medium, #44483D                                                                                                   |
| from_value               | text    | "Primary Checking (...0130)" — Outfit/body_medium, #1A1C16; data-driven from fromAccountLabel                                         |
| reference_row            | stack   | Horizontal, space-between, 10dp vertical padding — groups reference_label + reference_value                                           |
| reference_label          | text    | "Reference" — Outfit/body_medium, #44483D                                                                                              |
| reference_value          | text    | "Rent August 2026" — Outfit/body_medium, #1A1C16; data-driven                                                                         |
| fee_divider              | divider | #E1E4D5, 1dp — separates detail rows from fee/total summary section                                                                   |
| fee_row                  | stack   | Horizontal, space-between, 10dp vertical padding — groups fee_label + fee_value                                                       |
| fee_label                | text    | "Fee" — Outfit/body_medium, #44483D                                                                                                    |
| fee_value                | text    | "£0.00" — Outfit/body_medium, #386663 (secondary teal — signals zero cost); data-driven                                               |
| total_row                | stack   | Horizontal, space-between, sm vertical + sm horizontal padding; #F9FAEF fill, 8dp radius — highlighted total summary band              |
| total_label              | text    | "Total" — Outfit/title_large, #1A1C16, weight 700                                                                                     |
| total_value              | text    | "£500.00" — Outfit/title_large, #4C662B, weight 700; data-driven from total state field                                               |
| scheduled_date_selector  | input   | Outlined "Scheduled for: Immediate", trailing icon calendar_today, 12dp radius, 16dp top padding; on_click: select_schedule_date       |
| terms_text               | text    | "By confirming you authorise this payment per our Terms of Service" — Outfit/body_small, #44483D, center-aligned, sm vertical padding  |
| confirm_send_button      | button  | "Confirm & Send" — filled, #4C662B bg, #FFFFFF text, 12dp radius, md vertical padding, full-width, Outfit/label_large; on_click: submit|
| edit_payment_button      | button  | "Edit Payment" — outlined, #4C662B border + text, 12dp radius, 14dp vertical padding, full-width; on_click: navigate → send-money     |

---

## States

| ID         | Trigger                                    | Description                                                                                                      |
|------------|--------------------------------------------|------------------------------------------------------------------------------------------------------------------|
| loading    | Screen entry while payment data resolves   | Shimmer over payment_amount, to_value, iban_value, from_value, reference_value, fee_value, total_value; both buttons disabled; linear progress bar at top |
| review     | Data loaded — awaiting user action         | Full summary card with all rows populated; confirm_send_button enabled; terms_text visible                       |
| content    | Alias for review (default loaded state)    | Same visible layout as review; confirm_send_button enabled                                                       |
| submitting | ConfirmClicked event                       | confirm_send_button shows loading spinner + disabled; edit_payment_button disabled; linear progress indicator     |
| success    | PaymentSucceeded event                     | Visible components cleared; snackbar "Payment of £500.00 sent to John Smith"; auto-navigate to home (replace)    |
| error      | PaymentFailed event / network failure      | Inline error banner "Payment could not be processed. Please try again."; confirm_send_button re-enabled          |
| empty      | No transaction context available           | Empty state: title + "No transaction to confirm. Start a new payment." message; only edit_payment_button shown   |

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

| From               | To         | Trigger                               | Type    |
|--------------------|------------|---------------------------------------|---------|
| send-money-confirm | home       | PaymentSucceeded — auto after success | replace |
| send-money-confirm | send-money | edit_payment_button tap               | pop     |
| send-money-confirm | send-money | top app bar back arrow tap            | pop     |

---

## API Endpoints

| Endpoint                                                                                                                                   | Method | Auth        | Tag                 | Purpose                       |
|--------------------------------------------------------------------------------------------------------------------------------------------|--------|-------------|---------------------|-------------------------------|
| /obp/v5.1.0/banks/{bankId}/accounts/{accountId}/owner/transaction-request-types/SEPA/transaction-requests                                  | POST   | DirectLogin | TransactionRequests | Submit confirmed SEPA payment |

---

## Design Tokens

| Token                           | Value        | Usage                                                                                    |
|---------------------------------|--------------|------------------------------------------------------------------------------------------|
| colors.light.primary            | #4C662B      | confirm_title, payment_amount, total_value, confirm_send_button bg, edit_payment_button border+text |
| colors.light.on_primary         | #FFFFFF      | confirm_send_button label text                                                           |
| colors.light.secondary          | #386663      | fee_value text (zero-cost teal signal)                                                   |
| colors.light.primary_container  | #CDEDA3      | payment_summary_card border colour                                                       |
| colors.light.surface            | #FFFFFF      | payment_summary_card background                                                          |
| colors.light.background         | #F9FAEF      | screen base, total_row highlight fill                                                    |
| colors.light.on_surface         | #1A1C16      | to_value, iban_value, from_value, reference_value, total_label                           |
| colors.light.on_surface_variant | #44483D      | review_subtitle, all row label texts (To/IBAN/From/Reference/Fee), terms_text            |
| colors.light.surface_variant    | #E1E4D5      | amount_divider and fee_divider colour                                                    |
| colors.light.outline            | #75796C      | scheduled_date_selector border (outlined variant)                                        |
| typography.display_medium       | Outfit 45sp/400 | payment_amount (hero amount)                                                          |
| typography.headline_large       | Outfit 32sp/400 | confirm_title                                                                         |
| typography.title_large          | Outfit 22sp/400 | total_label, total_value                                                              |
| typography.body_large           | Outfit 16sp/400 | to_value                                                                              |
| typography.body_medium          | Outfit 14sp/400 | review_subtitle, to_label, iban_label, iban_value, from_label, from_value, reference_label, reference_value, fee_label, fee_value |
| typography.body_small           | Outfit 12sp/400 | terms_text                                                                            |
| typography.label_large          | Outfit 14sp/500 | confirm_send_button label, edit_payment_button label                                  |
| radius.lg                       | 16dp         | payment_summary_card corner radius                                                       |
| radius.md                       | 12dp         | confirm_send_button, edit_payment_button, scheduled_date_selector corner radius          |
| radius.sm                       | 8dp          | total_row highlight container corner radius                                              |
| elevation.level2                | 3dp          | payment_summary_card elevation                                                           |
| spacing.xs                      | 4dp          | confirm_title bottom padding, divider vertical padding                                   |
| spacing.sm                      | 8dp          | total_row padding, terms_text vertical padding                                           |
| spacing.md                      | 16dp         | scheduled_date_selector top padding, confirm_send_button vertical padding                |

---

_Generated by /idea export | 2026-05-30_
