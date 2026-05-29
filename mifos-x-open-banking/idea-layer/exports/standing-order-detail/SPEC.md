# SPEC — Standing Order Detail

| Field         | Value                          |
|---------------|--------------------------------|
| Feature       | standing-orders                |
| Flavor        | consumer                       |
| Status        | approved                       |
| Quality Score | 93                             |
| ViewModel     | StandingOrderDetailViewModel   |

---

## Overview

The Standing Order Detail screen shows the complete details of a single standing order — recipient identity (name, IBAN, bank), schedule (frequency, start date, next payment, final date), payment amount with currency badge, and the last 5 execution history entries. The green header card displays the order name and Active/Paused/Cancelled status badge. Two action buttons allow the user to pause/resume the order or permanently cancel it via a confirmation dialog. The edit action in the top app bar navigates to the standing-order-edit form. Error and empty states are full-screen replacements. The screen has no bottom navigation bar — it is reached by tapping a standing order in the standing-orders list.

---

## Screens

| ID                   | Name                 | Route                              | Layout | Scroll   |
|----------------------|----------------------|------------------------------------|--------|----------|
| standing-order-detail | Standing Order Detail | /standing-orders/{standingOrderId} | Column | Vertical |

**Shell:** Top app bar — title "Standing Order", back arrow (`arrow_back`), edit action (`edit` icon). No bottom navigation bar.

| Bar Item    | Icon       | Action                                        |
|-------------|------------|-----------------------------------------------|
| Back arrow  | arrow_back | navigate back to standing-orders list          |
| Edit action | edit       | navigate to standing-order-edit (passes ID)   |

---

## Components

| ID                          | Type      | Description                                                                                                         |
|-----------------------------|-----------|---------------------------------------------------------------------------------------------------------------------|
| sod_root                    | stack     | Full-screen column, background #F9FAEF                                                                              |
| **Header Card**             |           |                                                                                                                     |
| sod_header_card             | card      | #4C662B fill, 0dp radius (full-width flush), pad_horizontal 24, pad_top 24, pad_bottom 32                          |
| sod_order_name_text         | text      | "Rent Payment" — Outfit/headline_medium, #FFFFFF, weight 600; data-driven                                          |
| sod_status_badge            | badge     | "Active" — Outfit/label_medium, #CDEDA3 bg, #4C662B text, radius 20dp, pad_horizontal 16; data-driven             |
| **Beneficiary Card**        |           |                                                                                                                     |
| sod_beneficiary_card        | card      | White, radius 16dp, elevation 4dp, margin_horizontal 24, margin_top -24dp (overlaps header), margin_bottom 16      |
| sod_beneficiary_header      | text      | "RECIPIENT" — Outfit/label_small, #44483D, uppercase, letter-spacing 0.8dp                                         |
| sod_beneficiary_name_row    | stack     | Space-between row: "Name" label + "Landlord Holdings Ltd" value (weight 500)                                       |
| sod_beneficiary_iban_row    | stack     | Space-between row: "IBAN" label + "GB29 NWBK 6016 1331 9268 19" value (monospace body_small)                      |
| sod_beneficiary_bank_row    | stack     | Space-between row: "Bank" label + "NatWest Bank" value (weight 500)                                                |
| **Schedule Card**           |           |                                                                                                                     |
| sod_schedule_card           | card      | White, radius 16dp, elevation 1dp, margin_horizontal 24, margin_bottom 16                                          |
| sod_schedule_header         | text      | "SCHEDULE" — Outfit/label_small, #44483D, uppercase                                                                |
| sod_frequency_row           | stack     | Space-between row: "Frequency" + "Monthly" (weight 500)                                                            |
| sod_start_date_row          | stack     | Space-between row: "Start Date" + "1 Jan 2026" (weight 500)                                                        |
| sod_next_payment_row        | stack     | Space-between row: "Next Payment" + "1 Jun 2026" (color #4C662B, weight 600 — highlighted)                        |
| sod_final_date_row          | stack     | Space-between row: "Final Date" + "31 Dec 2026" (weight 500; shows "Ongoing" when finalDate is null)              |
| **Amount Card**             |           |                                                                                                                     |
| sod_amount_card             | card      | White, radius 16dp, elevation 1dp, margin_horizontal 24, margin_bottom 16                                          |
| sod_amount_header           | text      | "PAYMENT AMOUNT" — Outfit/label_small, #44483D, uppercase                                                          |
| sod_amount_value            | text      | "£1,200.00" — Outfit/display_small, #1A1C16, weight 700; data-driven                                              |
| sod_currency_badge          | badge     | "GBP" — Outfit/label_medium, #F9FAEF bg, #44483D text, radius 6dp; beside amount value                            |
| **Execution History Card**  |           |                                                                                                                     |
| sod_history_card            | card      | White, radius 16dp, elevation 1dp, margin_horizontal 24, margin_bottom 16                                          |
| sod_history_header          | text      | "RECENT EXECUTIONS" — Outfit/label_small, #44483D, uppercase                                                       |
| sod_history_item_1          | list_item | "1 May 2026" + "Completed" (#4C662B) + "£1,200.00" (right-aligned, weight 600)                                    |
| sod_history_item_2          | list_item | "1 Apr 2026" + "Completed" (#4C662B) + "£1,200.00"                                                                |
| sod_history_item_3          | list_item | "1 Mar 2026" + "Completed" (#4C662B) + "£1,200.00"                                                                |
| sod_history_item_4          | list_item | "1 Feb 2026" + "Failed — Insufficient Funds" (#BA1A1A) + "£1,200.00" (#BA1A1A — error color)                      |
| sod_history_item_5          | list_item | "1 Jan 2026" + "Completed" (#4C662B) + "£1,200.00"                                                                |
| **Action Row**              |           |                                                                                                                     |
| sod_pause_resume_button     | button    | "Pause Standing Order" — outlined, border #4C662B, text #4C662B, radius 12dp, leading pause_circle icon           |
| sod_delete_button           | button    | "Cancel Standing Order" — outlined, border #BA1A1A, text #BA1A1A, radius 12dp, leading delete_outline icon        |
| **Delete Dialog**           |           |                                                                                                                     |
| sod_delete_dialog           | dialog    | Alert: "Cancel Standing Order?" — white, radius 28dp, message + Keep + Cancel Order buttons                       |
| sod_delete_dialog_cancel_btn| button    | "Keep" — text variant, #4C662B; dismisses dialog                                                                   |
| sod_delete_dialog_confirm_btn| button   | "Cancel Order" — filled, #BA1A1A bg, white text; triggers DELETE API then navigates to standing-orders             |
| **Error State**             |           |                                                                                                                     |
| sod_error_state             | stack     | Centered column: sync_problem icon (48dp #BA1A1A) + "Standing Order Not Found" + message + Retry button           |
| **Empty State**             |           |                                                                                                                     |
| sod_empty_state             | stack     | Centered column: repeat_off icon (48dp #C5C8BA) + "No details are available" + Back to Standing Orders button     |

---

## States

| ID      | Trigger                             | Description                                                                                      |
|---------|-------------------------------------|--------------------------------------------------------------------------------------------------|
| content | API returns 200 with standing order | Full detail layout — header card, beneficiary, schedule, amount, history, action row visible     |
| loading | Screen entry                        | Full-screen shimmer matching content block structure while GET API resolves                      |
| error   | API 404 or network failure          | Centered error state: sync_problem icon + title + message + Retry button                         |
| empty   | API 200 but null/empty body         | Centered empty state: repeat_off icon + message + Back to Standing Orders button                 |

---

## State Model

**ViewModel:** `StandingOrderDetailViewModel`
**Screen State Type:** `StandingOrderDetailUiState`

| Name                  | Type                         | Default                              |
|-----------------------|------------------------------|--------------------------------------|
| standingOrderId       | String                       | ""                                   |
| beneficiaryName       | String                       | ""                                   |
| beneficiaryIban       | String                       | ""                                   |
| beneficiaryBankName   | String                       | ""                                   |
| amount                | BigDecimal                   | BigDecimal.ZERO                      |
| currency              | String                       | "GBP"                                |
| frequency             | StandingOrderFrequency       | StandingOrderFrequency.MONTHLY       |
| startDate             | LocalDate                    | LocalDate.now()                      |
| nextPaymentDate       | LocalDate                    | LocalDate.now()                      |
| finalDate             | LocalDate?                   | null                                 |
| status                | StandingOrderStatus          | StandingOrderStatus.ACTIVE           |
| executionHistory      | List\<StandingOrderExecution\> | emptyList()                         |
| uiState               | StandingOrderDetailUiState   | StandingOrderDetailUiState.Loading   |
| isDeleteDialogVisible | Boolean                      | false                                |
| isActionInProgress    | Boolean                      | false                                |

**Events:** `RetryLoad`, `PauseClicked`, `ResumeClicked`, `DeleteClicked`, `DeleteConfirmed`, `DeleteDismissed`, `EditClicked`, `NavigateBack`

**Actions:** `loadDetail(standingOrderId)`, `pauseStandingOrder()`, `resumeStandingOrder()`, `deleteStandingOrder()`, `showDeleteDialog()`, `dismissDeleteDialog()`

**DI Dependencies:** `StandingOrderRepository`, `AccountRepository`

**Errors:**

| ID            | Message                                                           |
|---------------|-------------------------------------------------------------------|
| not_found     | "This standing order could not be found."                        |
| network_error | "Network unavailable. Please check your connection."             |
| pause_failed  | "Could not pause this standing order. Please try again."         |
| resume_failed | "Could not resume this standing order. Please try again."        |
| delete_failed | "Could not cancel this standing order. Please try again."        |

---

## Navigation

| ID       | From                  | To                    | Trigger                     |
|----------|-----------------------|-----------------------|-----------------------------|
| nav_back | standing-order-detail | standing-orders       | back arrow tap              |
| nav_edit | standing-order-detail | standing-order-edit   | edit icon in top app bar    |

---

## API Endpoints

| Endpoint                                                                                                    | Method | Auth        | Tag            | Purpose                         |
|-------------------------------------------------------------------------------------------------------------|--------|-------------|----------------|---------------------------------|
| /v4.0.0/banks/{bank_id}/accounts/{account_id}/standing-orders/{standing_order_id}                         | GET    | DirectLogin | Standing-Orders | Load standing order detail      |
| /v4.0.0/banks/{bank_id}/accounts/{account_id}/standing-orders/{standing_order_id}/pause                   | POST   | DirectLogin | Standing-Orders | Pause active standing order     |
| /v4.0.0/banks/{bank_id}/accounts/{account_id}/standing-orders/{standing_order_id}/resume                  | POST   | DirectLogin | Standing-Orders | Resume paused standing order    |
| /v4.0.0/banks/{bank_id}/accounts/{account_id}/standing-orders/{standing_order_id}                         | DELETE | DirectLogin | Standing-Orders | Cancel (soft-delete) order      |

---

## Design Tokens

| Token                           | Value     | Usage                                                                       |
|---------------------------------|-----------|-----------------------------------------------------------------------------|
| colors.light.primary            | #4C662B   | sod_header_card background; next_payment_value; pause button; Keep button  |
| colors.light.on_primary         | #FFFFFF   | sod_order_name_text; Delete Order button text                               |
| colors.light.primary_container  | #CDEDA3   | sod_status_badge (Active) background                                        |
| colors.light.on_primary_container | #4C662B | sod_status_badge (Active) text color                                       |
| colors.light.error              | #BA1A1A   | sod_history_item_4 status and amount; Cancel button border/text; error icon |
| colors.light.on_error           | #FFFFFF   | sod_delete_dialog_confirm_btn text                                          |
| colors.light.background         | #F9FAEF   | Screen root; sod_currency_badge background                                  |
| colors.light.surface            | #FFFFFF   | All four detail cards                                                       |
| colors.light.on_surface         | #1A1C16   | All primary label texts; sod_amount_value                                   |
| colors.light.on_surface_variant | #44483D   | All section headers (uppercase label_small); row field labels               |
| colors.light.outline_variant    | #C5C8BA   | sod_currency_badge text                                                     |
| typography.headline_medium      | 28sp/400  | sod_order_name_text                                                         |
| typography.display_small        | 32sp/600  | sod_amount_value                                                            |
| typography.label_small          | 11sp/500  | Section headers (RECIPIENT, SCHEDULE, PAYMENT AMOUNT, RECENT EXECUTIONS)   |
| typography.label_medium         | 12sp/500  | sod_status_badge, sod_currency_badge                                        |
| typography.body_medium          | 14sp/400  | Row labels and values throughout; execution date/amounts                    |
| typography.body_small           | 12sp/400  | sod_beneficiary_iban_value (monospace); execution status text               |
| typography.label_large          | 14sp/500  | Pause/Cancel button labels                                                  |
| radius.xl                       | 24dp      | sod_beneficiary_card radius                                                 |
| elevation.level4                | 8dp       | sod_beneficiary_card — elevated above header card                          |
| spacing.lg                      | 24dp      | Header card horizontal padding; card margin_horizontal                      |
| spacing.md                      | 16dp      | Card internal padding                                                       |

---

_Generated by /idea export | 2026-05-29_
