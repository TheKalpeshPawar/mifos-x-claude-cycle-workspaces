# SPEC — Standing Order Edit

| Field         | Value                      |
|---------------|----------------------------|
| Feature       | standing-order-edit        |
| Flavor        | consumer                   |
| Status        | designed                   |
| Quality Score | 94                         |
| ViewModel     | StandingOrderEditViewModel |

---

## Overview

The Standing Order Edit screen allows the Consumer persona user to modify the mutable fields of an existing standing order: payment amount, frequency (DAILY / WEEKLY / MONTHLY / YEARLY), start date, and an optional final date. The beneficiary (Landlord Holdings Ltd — IBAN GB29 NWBK 6016 1331 9268 19, NatWest Bank) and currency (GBP) are immutable after creation and are shown read-only at the top of the form for context. The form is pre-filled from navigation arguments `standingOrderId` (SO-2026-0001) and `accountId` (acc-alex-gbp-current-001) passed by the standing-order-detail screen. On save the ViewModel calls the OBP PUT endpoint; on HTTP 200 it pops back to standing-order-detail, which reloads the updated record. Client-side validation enforces amount > £0.00 and start date not in the past before the API call is dispatched. A circular progress overlay (soe_saving_indicator) replaces the form content while the PUT is in flight. An inline error banner (soe_error_banner, #FFDAD6 / #410002) surfaces 400 / 409 / network failures without leaving the screen, keeping the form editable for retry. A text "Cancel" button discards edits and navigates back to standing-order-detail without saving.

---

## Screens

| ID                  | Name                | Route                                       | Layout | Scroll   |
|---------------------|---------------------|---------------------------------------------|--------|----------|
| standing-order-edit | Standing Order Edit | /standing-orders/{standingOrderId}/edit     | Column | Vertical |

**Shell:** Top app bar — title "Edit Standing Order", navigation icon `arrow_back` (navigate_back action). No bottom navigation bar.

| Bar Item   | Icon       | Action          |
|------------|------------|-----------------|
| Back arrow | arrow_back | navigate_back   |

---

## Components

| ID                     | Type              | Description                                                                                                                               |
|------------------------|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| soe_root               | stack (column)    | Root scrollable column; background #F9FAEF; padding_horizontal spacing.md (16dp); padding_top spacing.lg (24dp)                           |
| **Beneficiary (read-only)** |              |                                                                                                                                           |
| soe_beneficiary_card   | card (filled)     | Grouped read-only recipient block; #FFFFFF fill, radius 16dp, padding 16dp, margin_bottom 16dp, elevation 1dp; a11y group role             |
| soe_beneficiary_header | text              | "PAYING TO" — Outfit/label_small (11sp/500), #44483D, letter-spacing 0.8dp, uppercase, padding_bottom spacing.sm (8dp)                    |
| soe_beneficiary_row    | stack (row)       | Horizontal; center_start alignment; spacing spacing.sm (8dp); children: icon + info column                                                |
| soe_beneficiary_icon   | icon              | `account_balance`, 24dp, #4C662B; role: presentation (decorative)                                                                        |
| soe_beneficiary_info   | stack (column)    | Column containing name + IBAN; spacing 2dp                                                                                                |
| soe_beneficiary_name   | text              | "Landlord Holdings Ltd" — Outfit/body_large (16sp/500), #1A1C16; data-driven; read-only                                                  |
| soe_beneficiary_iban   | text              | "GB29 NWBK 6016 1331 9268 19 · NatWest Bank" — Outfit/body_small (12sp/400), #44483D, monospace; data-driven; read-only                  |
| **Editable Fields**    |                   |                                                                                                                                           |
| soe_amount_input       | input (outlined)  | Label "Amount"; prefix "£"; placeholder "0.00"; pre-filled "1200.00"; input_type decimal; radius 12dp; margin_top 16dp; helper "Amount taken on each payment date"; states: idle / hover / focus_visible / pressed / error |
| soe_currency_selector  | input (outlined)  | Label "Currency"; content "GBP — British Pound"; readonly; trailing icon `lock`; radius 12dp; margin_top 8dp; helper "Matches the source account currency"; states: idle / disabled |
| soe_frequency_selector | input (outlined)  | Label "Frequency"; content "Monthly"; leading icon `repeat`; trailing icon `expand_more`; tap opens frequency picker (DAILY / WEEKLY / MONTHLY / YEARLY); radius 12dp; margin_top 8dp; helper "How often the payment repeats"; states: idle / hover / focus_visible / pressed |
| soe_start_date_input   | input (outlined)  | Label "Start Date"; content "1 Jan 2026"; trailing icon `calendar_today`; tap opens date picker; radius 12dp; margin_top 8dp; helper "First date this payment runs"; states: idle / hover / focus_visible / pressed / error |
| soe_end_date_input     | input (outlined)  | Label "End Date (optional)"; content "Ongoing — no end date"; trailing icon `calendar_today`; tap opens date picker; radius 12dp; margin_top 8dp; helper "Leave as Ongoing to run indefinitely"; states: idle / hover / focus_visible / pressed / error |
| **Error Banner**       |                   |                                                                                                                                           |
| soe_error_banner       | banner (error)    | "Couldn't save your changes. Check the amount and try again."; background #FFDAD6; text #410002; leading icon `error_outline`; radius 8dp; margin_top 16dp; visible in error state only; a11y role: alert, live: assertive |
| **Action Buttons**     |                   |                                                                                                                                           |
| soe_save_button        | button (filled)   | Label "Save Changes"; background #4C662B; text #FFFFFF; radius 24dp; min_height 56dp; width fill; margin_top spacing.xl (32dp); Outfit/label_large; on tap: save_standing_order → navigates to standing-order-detail on success |
| soe_cancel_button      | button (text)     | Label "Cancel"; color #4C662B; Outfit/label_large; width fill; margin_top spacing.sm (8dp); on tap: navigate_back → standing-order-detail without saving |
| soe_bottom_spacer      | spacer            | Height 24dp — ensures content clears on-screen keyboard / safe area                                                                       |
| **Loading Overlay**    |                   |                                                                                                                                           |
| soe_saving_indicator   | loading_indicator | Circular; color #4C662B; alignment center; padding spacing.xl (32dp); a11y role: progressbar, label "Saving your standing order changes"; visible in loading state only while PUT is in flight |

---

## States

| ID      | Trigger                                          | Description                                                                                                |
|---------|--------------------------------------------------|------------------------------------------------------------------------------------------------------------|
| content | Screen entry (form pre-filled from nav args)     | All form components visible: beneficiary card + amount + currency + frequency + start date + end date + Save + Cancel; error banner hidden |
| loading | OnSave event — PUT request in flight             | soe_saving_indicator visible and centred; all form inputs hidden; save and cancel buttons hidden           |
| error   | PUT returns 400 / 409 / network / timeout        | Full form re-shown; soe_error_banner visible between last input and action buttons; inputs re-enabled for retry |

*empty: not_applicable — edit form is always pre-loaded from navigation args; there is no empty list state.*

---

## State Model

**ViewModel:** `StandingOrderEditViewModel`
**Screen State Type:** `StandingOrderEditUiState`

| Field             | Type                     | Default                           |
|-------------------|--------------------------|-----------------------------------|
| standingOrderId   | String                   | ""                                |
| accountId         | String                   | ""                                |
| beneficiaryName   | String                   | ""                                |
| beneficiaryIban   | String                   | ""                                |
| amount            | BigDecimal               | BigDecimal.ZERO                   |
| currency          | String                   | "GBP"                             |
| frequency         | StandingOrderFrequency   | StandingOrderFrequency.MONTHLY    |
| startDate         | LocalDate                | LocalDate.now()                   |
| endDate           | LocalDate?               | null                              |
| amountError       | String?                  | null                              |
| startDateError    | String?                  | null                              |
| isSaving          | Boolean                  | false                             |
| uiState           | StandingOrderEditUiState | StandingOrderEditUiState.Content  |

**Screen State Members:** `Content`, `Saving`, `Error`

**Events:** `OnAmountChange`, `OnCurrencySelect`, `OnFrequencyChange`, `OnStartDateChange`, `OnEndDateChange`, `OnSave`, `OnCancel`, `NavigateBack`, `NavigateToDetail`

**Actions:**

| Action                     | Trigger              | Description                                                   |
|----------------------------|----------------------|---------------------------------------------------------------|
| `prefillForm(standingOrderId)` | ScreenOpened     | Loads existing standing order values into form state          |
| `onAmountChange(amount)`   | OnAmountChange       | Updates amount; clears amountError                            |
| `onFrequencyChange(frequency)` | OnFrequencyChange | Updates frequency enum selection                             |
| `onStartDateChange(startDate)` | OnStartDateChange | Updates start date; clears startDateError                    |
| `onEndDateChange(endDate)` | OnEndDateChange      | Sets or clears endDate (null = indefinite)                    |
| `validateForm()`           | Before OnSave        | Checks amount > 0 and startDate >= today; sets error fields   |
| `saveStandingOrder()`      | OnSave               | Dispatches PUT; sets isSaving=true; handles success/failure   |
| `cancelEdit()`             | OnCancel             | Emits NavigateBack without saving                             |

**DI Dependencies:** `StandingOrderRepository`, `AccountRepository`

**Errors:**

| ID                    | Message                                                                  |
|-----------------------|--------------------------------------------------------------------------|
| validation_amount     | "Enter an amount greater than £0.00."                                   |
| validation_start_date | "Start date can't be in the past."                                      |
| save_failed           | "Couldn't save your changes. Check the amount and try again."           |
| already_cancelled     | "This standing order has been cancelled and can no longer be edited."   |
| network_error         | "Network unavailable. Please check your connection."                    |
| not_logged_in         | "Your session expired. Please sign in again."                           |

---

## Navigation

| ID               | From                | To                    | Trigger                                                    | Type |
|------------------|---------------------|-----------------------|------------------------------------------------------------|------|
| nav_back         | standing-order-edit | standing-order-detail | soe_cancel_button tap (OnCancel) or top app bar back arrow | pop  |
| nav_save_success | standing-order-edit | standing-order-detail | PUT 200 — standing-order-detail reloads updated record     | pop  |

**Route Parameters (StandingOrderEditRoute):**

| Name             | Type   | Required | Demo Value                   |
|------------------|--------|----------|------------------------------|
| standingOrderId  | String | true     | SO-2026-0001                 |
| accountId        | String | true     | acc-alex-gbp-current-001     |

---

## API Endpoints

| Endpoint                                                                                                              | Method | Auth        | Tag             | Purpose                                          |
|-----------------------------------------------------------------------------------------------------------------------|--------|-------------|-----------------|--------------------------------------------------|
| PUT /obp/v4.0.0/banks/{bank_id}/accounts/{account_id}/owner/standing-order/{standing_order_id}                       | PUT    | DirectLogin | Standing-Orders | Update amount, frequency, start date, final date |

---

## Design Tokens

| Token                           | Value          | Usage                                                                              |
|---------------------------------|----------------|------------------------------------------------------------------------------------|
| colors.light.primary            | #4C662B        | soe_save_button background; soe_cancel_button + back arrow text; soe_beneficiary_icon; soe_saving_indicator |
| colors.light.on_primary         | #FFFFFF        | soe_save_button label text                                                         |
| colors.light.error_container    | #FFDAD6        | soe_error_banner background                                                        |
| colors.light.on_error_container | #410002        | soe_error_banner text color                                                        |
| colors.light.background         | #F9FAEF        | soe_root screen background                                                         |
| colors.light.surface            | #FFFFFF        | soe_beneficiary_card fill                                                          |
| colors.light.on_surface         | #1A1C16        | soe_beneficiary_name; editable field entered values                                |
| colors.light.on_surface_variant | #44483D        | soe_beneficiary_header; soe_beneficiary_iban; field helper text                   |
| colors.light.outline            | #75796C        | Outlined input field idle border                                                   |
| typography.label_small          | Outfit 11sp/500 | soe_beneficiary_header uppercase section label                                    |
| typography.body_large           | Outfit 16sp/400 | soe_beneficiary_name (weight 500); editable field pre-filled values               |
| typography.body_small           | Outfit 12sp/400 | soe_beneficiary_iban + bank name; field helper text                               |
| typography.label_large          | Outfit 14sp/500 | soe_save_button and soe_cancel_button labels                                      |
| radius.lg                       | 16dp           | soe_beneficiary_card corner radius                                                 |
| radius.md                       | 12dp           | All outlined input field corner radius                                             |
| radius.sm                       | 8dp            | soe_error_banner corner radius                                                     |
| radius.pill (24dp)              | 24dp           | soe_save_button corner radius (pill-style at 56dp height)                         |
| spacing.sm (8dp)                | 8dp            | Gap between beneficiary icon and info; between consecutive input fields; Cancel top margin |
| spacing.md (16dp)               | 16dp           | soe_root horizontal padding; soe_amount_input top margin; soe_error_banner horizontal padding |
| spacing.lg (24dp)               | 24dp           | soe_root top padding; soe_bottom_spacer height                                    |
| spacing.xl (32dp)               | 32dp           | soe_save_button top margin; soe_saving_indicator padding                          |
| elevation.level1                | 1dp            | soe_beneficiary_card elevation                                                    |

---

_Generated by /idea export | 2026-05-30_
