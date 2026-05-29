# SPEC — Standing Order Edit

| Field         | Value                        |
|---------------|------------------------------|
| Feature       | standing-orders              |
| Flavor        | consumer                     |
| Status        | designed                     |
| Quality Score | 94                           |
| ViewModel     | StandingOrderEditViewModel   |

---

## Overview

The Standing Order Edit screen allows the user to modify the mutable fields of an existing standing order: payment amount, frequency (Daily/Weekly/Monthly/Yearly), start date, and optional end date. Beneficiary and currency are locked after creation and displayed read-only at the top of the form. The form is pre-filled with the current standing order values passed from standing-order-detail. On save the ViewModel calls the OBP PUT endpoint; on success it navigates back to standing-order-detail, which reloads the updated record. An inline error banner surfaces API or validation failures without leaving the screen. A text "Cancel" button discards edits and returns to detail.

---

## Screens

| ID                  | Name                 | Route                              | Layout | Scroll   |
|---------------------|----------------------|------------------------------------|--------|----------|
| standing-order-edit | Standing Order Edit  | /standing-orders/{standingOrderId}/edit | Column | Vertical |

**Shell:** Top app bar — title "Edit Standing Order", back arrow (`arrow_back`). No bottom navigation bar.

| Bar Item   | Icon       | Action                                  |
|------------|------------|-----------------------------------------|
| Back arrow | arrow_back | discard changes, return to detail        |

---

## Components

| ID                    | Type              | Description                                                                                                                              |
|-----------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| soe_root              | stack             | Full-screen column, background #F9FAEF, padding_horizontal 16, padding_top 24                                                            |
| **Beneficiary (Read-only)**  |          |                                                                                                                                          |
| soe_beneficiary_card  | card              | White, radius 16dp, elevation 1dp, margin_bottom 16; groups read-only recipient info                                                      |
| soe_beneficiary_header| text              | "PAYING TO" — Outfit/label_small, #44483D, uppercase, letter-spacing 0.8dp                                                               |
| soe_beneficiary_icon  | icon              | account_balance, 24dp, #4C662B; presentational only                                                                                       |
| soe_beneficiary_name  | text              | "Landlord Holdings Ltd" — Outfit/body_large, #1A1C16, weight 500; data-driven; read-only                                                |
| soe_beneficiary_iban  | text              | "GB29 NWBK 6016 1331 9268 19 · NatWest Bank" — Outfit/body_small, #44483D, monospace; read-only                                        |
| **Editable Fields**   |                   |                                                                                                                                          |
| soe_amount_input      | input             | Outlined "Amount", prefix £, input_type decimal, placeholder "0.00"; prefill "1200.00"; margin_top 16; helper "Amount taken on each payment date" |
| soe_currency_selector | input             | Outlined "Currency", content "GBP — British Pound", readonly, trailing lock icon; margin_top 8; helper "Matches the source account currency" |
| soe_frequency_selector| input             | Outlined "Frequency", content "Monthly", trailing expand_more + leading repeat icon; tap opens picker (DAILY/WEEKLY/MONTHLY/YEARLY); margin_top 8 |
| soe_start_date_input  | input             | Outlined "Start Date", content "1 Jan 2026", trailing calendar_today; tap opens date picker; margin_top 8                               |
| soe_end_date_input    | input             | Outlined "End Date (optional)", content "Ongoing — no end date", trailing calendar_today; tap opens date picker; margin_top 8            |
| **Error Banner**      |                   |                                                                                                                                          |
| soe_error_banner      | banner            | Error variant — "Couldn't save your changes. Check the amount and try again."; #FFDAD6 bg, #410002 text, error_outline icon; visible in error state only |
| **Action Buttons**    |                   |                                                                                                                                          |
| soe_save_button       | button            | "Save Changes" — filled, #4C662B bg, #FFFFFF text, radius 24dp, min_height 56dp, full-width; margin_top 32dp                            |
| soe_cancel_button     | button            | "Cancel" — text variant, #4C662B text, full-width; margin_top 8dp; navigates back to detail                                             |
| **Loading Overlay**   |                   |                                                                                                                                          |
| soe_saving_indicator  | loading_indicator | Circular, #4C662B, 40dp, centered; shown only in loading state while PUT is in flight                                                   |

---

## States

| ID      | Trigger                               | Description                                                                                         |
|---------|---------------------------------------|-----------------------------------------------------------------------------------------------------|
| content | Screen entry with pre-filled data     | Full form visible: beneficiary card + 4 editable inputs + Save + Cancel; error banner hidden        |
| loading | OnSave — PUT request in flight        | Circular spinner centred on screen; all inputs disabled; save button shows loading indicator        |
| error   | PUT returns non-2xx or validation fail| Form re-shown with inline error banner above action buttons; inputs re-enabled for retry            |

---

## State Model

**ViewModel:** `StandingOrderEditViewModel`
**Screen State Type:** `StandingOrderEditUiState`

| Name            | Type                        | Default                               |
|-----------------|-----------------------------|---------------------------------------|
| standingOrderId | String                      | ""                                    |
| accountId       | String                      | ""                                    |
| beneficiaryName | String                      | ""                                    |
| beneficiaryIban | String                      | ""                                    |
| amount          | BigDecimal                  | BigDecimal.ZERO                       |
| currency        | String                      | "GBP"                                 |
| frequency       | StandingOrderFrequency      | StandingOrderFrequency.MONTHLY        |
| startDate       | LocalDate                   | LocalDate.now()                       |
| endDate         | LocalDate?                  | null                                  |
| amountError     | String?                     | null                                  |
| startDateError  | String?                     | null                                  |
| isSaving        | Boolean                     | false                                 |
| uiState         | StandingOrderEditUiState    | StandingOrderEditUiState.Content      |

**Screen state members:** Content, Saving, Error

**Events:** `OnAmountChange`, `OnCurrencySelect`, `OnFrequencyChange`, `OnStartDateChange`, `OnEndDateChange`, `OnSave`, `OnCancel`, `NavigateBack`, `NavigateToDetail`

**Actions:** `prefillForm(standingOrderId)`, `onAmountChange(amount)`, `onFrequencyChange(frequency)`, `onStartDateChange(startDate)`, `onEndDateChange(endDate)`, `validateForm()`, `saveStandingOrder()`, `cancelEdit()`

**DI Dependencies:** `StandingOrderRepository`, `AccountRepository`

**Errors:**

| ID                | Message                                                          |
|-------------------|------------------------------------------------------------------|
| validation_amount | "Enter an amount greater than £0.00."                           |
| validation_start_date | "Start date can't be in the past."                          |
| save_failed       | "Couldn't save your changes. Check the amount and try again."   |
| already_cancelled | "This standing order has been cancelled and can no longer be edited." |
| network_error     | "Network unavailable. Please check your connection."            |
| not_logged_in     | "Your session expired. Please sign in again."                   |

---

## Navigation

| ID              | From                | To                    | Trigger                            |
|-----------------|---------------------|-----------------------|------------------------------------|
| nav_back        | standing-order-edit | standing-order-detail | back arrow tap or OnCancel         |
| nav_save_success| standing-order-edit | standing-order-detail | PUT 200 — detail reloads record    |

---

## API Endpoints

| Endpoint                                                                                         | Method | Auth        | Tag            | Purpose                         |
|--------------------------------------------------------------------------------------------------|--------|-------------|----------------|---------------------------------|
| /obp/v4.0.0/banks/{bank_id}/accounts/{account_id}/owner/standing-order/{standing_order_id}     | PUT    | DirectLogin | Standing-Orders | Update mutable standing order fields |

---

## Design Tokens

| Token                           | Value     | Usage                                                                 |
|---------------------------------|-----------|-----------------------------------------------------------------------|
| colors.light.primary            | #4C662B   | soe_save_button bg; soe_cancel_button text; soe_beneficiary_icon; Save label |
| colors.light.on_primary         | #FFFFFF   | soe_save_button text                                                  |
| colors.light.background         | #F9FAEF   | Screen root background                                                |
| colors.light.surface            | #FFFFFF   | soe_beneficiary_card background                                       |
| colors.light.on_surface         | #1A1C16   | soe_beneficiary_name; editable field values                           |
| colors.light.on_surface_variant | #44483D   | soe_beneficiary_header (PAYING TO); soe_beneficiary_iban              |
| colors.light.outline            | #75796C   | All outlined input field borders (idle)                               |
| colors.light.primary (focus)    | #4C662B   | Focused input border highlight                                        |
| colors.light.error_container    | #FFDAD6   | soe_error_banner background                                           |
| colors.light.on_error_container | #410002   | soe_error_banner text                                                 |
| typography.label_small          | 11sp/500  | soe_beneficiary_header (uppercase section label)                      |
| typography.body_large           | 16sp/400  | soe_beneficiary_name                                                  |
| typography.body_small           | 12sp/400  | soe_beneficiary_iban                                                  |
| typography.label_large          | 14sp/500  | soe_save_button label, soe_cancel_button label                        |
| radius.xl                       | 24dp      | soe_save_button corner radius (pill-style)                            |
| radius.md                       | 12dp      | Outlined input field corner radius                                    |
| radius.sm                       | 8dp       | soe_error_banner corner radius                                        |
| spacing.xl                      | 32dp      | soe_save_button margin_top                                            |
| spacing.md                      | 16dp      | soe_root padding_horizontal; soe_amount_input margin_top             |
| spacing.sm                      | 8dp       | margin_top between input fields                                       |

---

_Generated by /idea export | 2026-05-29_
