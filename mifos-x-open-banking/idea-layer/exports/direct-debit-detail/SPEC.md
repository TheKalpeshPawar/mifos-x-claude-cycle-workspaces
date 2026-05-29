# SPEC — Direct Debit Detail

| Field         | Value                           |
|---------------|---------------------------------|
| Feature       | direct-debit-detail             |
| Flavor        | consumer                        |
| Status        | approved                        |
| Quality Score | 95                              |
| ViewModel     | DirectDebitDetailViewModel      |

---

## Overview

Direct Debit Detail is a consumer-facing detail screen showing the full mandate record for a single direct debit. It presents a merchant hero card at the top (green #4C662B background, merchant logo, merchant name, mandate status badge, amount + frequency), followed by a Mandate Details card (next payment date, linked account, mandate reference, start date) and a Recent Payments card (last 3 collected/failed payment rows with dates and amounts). At the bottom an action row provides Cancel Mandate (outlined error button) and Edit Mandate (filled teal button). The screen has a top app bar with a back arrow and a More Options overflow menu. The loading state shows a detail-screen skeleton. An error state with icon, message, and retry button is shown on API failure. The empty state covers the case where a mandate ID resolves but returns no data.

---

## Screens

| ID                  | Name               | Route                    | Layout | Scroll   |
|---------------------|--------------------|--------------------------|--------|----------|
| direct-debit-detail | Direct Debit Detail| /direct-debit/{mandateId}| Column | Vertical |

**Shell:** Top app bar ("Direct Debit", back arrow, more_vert overflow). No bottom navigation — detail screen.

| Element       | Config                                              |
|---------------|-----------------------------------------------------|
| top_app_bar   | show: true; title "Direct Debit"; nav_icon arrow_back; action more_vert → open_mandate_options |
| bottom_nav    | false                                               |

---

## Components

| ID                         | Type     | Description                                                                                            |
|----------------------------|----------|--------------------------------------------------------------------------------------------------------|
| ddd_root                   | stack    | Column root container, #F9FAEF bg, pad spacing.lg (24dp)                                               |
| ddd_merchant_hero          | box      | #4C662B bg, pad H24/T32/B36, radius-bottom 24dp; contains logo + name + badge + amount                |
| ddd_merchant_logo          | image    | 56×56dp merchant logo, radius 12dp, #FFFFFF bg; fallback to initials avatar on load error             |
| ddd_merchant_name          | text     | "Netflix Entertainment" — Outfit/headline_small, #FFFFFF, centered                                    |
| ddd_mandate_status_badge   | badge    | "Active" — #CDEDA3 bg, #4C662B text, Outfit/label_small, radius 20dp, pad H12/V4; centered            |
| ddd_mandate_amount_value   | text     | "£15.99" — Outfit/display_small, #FFFFFF, centered, weight 700                                        |
| ddd_mandate_frequency_text | text     | "Monthly" — Outfit/body_medium, #CDEDA3, centered                                                     |
| ddd_mandate_details_card   | card     | #FFFFFF bg, radius 12dp, pad 16dp; contains next payment, account, ref, start date rows               |
| ddd_details_header         | text     | "Mandate Details" — Outfit/title_medium, #4C662B                                                      |
| ddd_next_payment_row       | stack    | Row: "Next Payment" label + "15 Jun 2026" value, space-between, pad V8                                |
| ddd_next_payment_label     | text     | "Next Payment" — Outfit/body_medium, #44483D                                                          |
| ddd_next_payment_value     | text     | "15 Jun 2026" — Outfit/body_medium, #1A1C16, weight 600                                               |
| ddd_divider_1              | divider  | #E1E4D5, margin V4                                                                                     |
| ddd_account_row            | stack    | Row: "Account" label + right-aligned account name + masked number column                               |
| ddd_account_label          | text     | "Account" — Outfit/body_medium, #44483D                                                                |
| ddd_account_name           | text     | "Current Account" — Outfit/body_medium, #1A1C16, weight 600                                           |
| ddd_account_number         | text     | "****4521" — Outfit/body_small, #44483D                                                                |
| ddd_divider_2              | divider  | #E1E4D5, margin V4                                                                                     |
| ddd_mandate_ref_row        | stack    | Row: "Mandate Ref" label + "MDT-2024-00947" value                                                     |
| ddd_mandate_ref_label      | text     | "Mandate Ref" — Outfit/body_medium, #44483D                                                            |
| ddd_mandate_ref_value      | text     | "MDT-2024-00947" — Outfit/body_medium, #1A1C16, monospace                                              |
| ddd_divider_3              | divider  | #E1E4D5, margin V4                                                                                     |
| ddd_start_date_row         | stack    | Row: "Start Date" label + "12 Jan 2024" value                                                          |
| ddd_start_date_label       | text     | "Start Date" — Outfit/body_medium, #44483D                                                             |
| ddd_start_date_value       | text     | "12 Jan 2024" — Outfit/body_medium, #1A1C16, weight 600                                               |
| ddd_payment_history_card   | card     | #FFFFFF bg, radius 12dp, pad 16dp; contains history header row + 3 payment items + 2 dividers         |
| ddd_history_header_row     | stack    | Row: "Recent Payments" heading + "View all" link, space-between                                        |
| ddd_history_header         | text     | "Recent Payments" — Outfit/title_medium, #4C662B                                                       |
| ddd_history_view_all_link  | link     | "View all" — Outfit/label_medium, #386663; navigates to transactions                                   |
| ddd_history_item_1         | stack    | Row: date+status column + amount; 15 May 2026 / Collected / −£15.99                                    |
| ddd_history_item_1_date    | text     | "15 May 2026" — Outfit/body_medium, #1A1C16                                                            |
| ddd_history_item_1_status  | text     | "Collected" — Outfit/body_small, #4C662B                                                               |
| ddd_history_item_1_amount  | text     | "−£15.99" — Outfit/body_medium, #1A1C16, weight 600                                                    |
| ddd_history_item_2         | stack    | Row: 15 Apr 2026 / Collected / −£15.99                                                                 |
| ddd_history_item_2_date    | text     | "15 Apr 2026" — Outfit/body_medium, #1A1C16                                                            |
| ddd_history_item_2_status  | text     | "Collected" — Outfit/body_small, #4C662B                                                               |
| ddd_history_item_2_amount  | text     | "−£15.99" — Outfit/body_medium, #1A1C16, weight 600                                                    |
| ddd_history_item_3         | stack    | Row: 15 Mar 2026 / Failed / −£15.99 (all in error color)                                               |
| ddd_history_item_3_date    | text     | "15 Mar 2026" — Outfit/body_medium, #1A1C16                                                            |
| ddd_history_item_3_status  | text     | "Failed" — Outfit/body_small, #BA1A1A                                                                  |
| ddd_history_item_3_amount  | text     | "−£15.99" — Outfit/body_medium, #BA1A1A, weight 600                                                    |
| ddd_action_row             | stack    | Row: Cancel + Edit buttons, space-between, pad T16, spacing 16dp                                       |
| ddd_cancel_button          | button   | Outlined error "Cancel Mandate" — #BA1A1A border+text, radius 12dp, pad H24                            |
| ddd_edit_button            | button   | Filled "Edit Mandate" — #386663 bg, #FFFFFF text, radius 12dp, pad H24                                 |
| ddd_loading_skeleton       | skeleton | Detail-screen shimmer skeleton — #F9FAEF bg, pad 24dp                                                  |
| ddd_error_state            | stack    | Column centered: error_outline icon 48dp #BA1A1A + error message + retry button                        |
| ddd_error_icon             | icon     | error_outline, 48dp, #BA1A1A                                                                            |
| ddd_error_message          | text     | "Couldn't load mandate details. Please try again." — Outfit/body_medium, #44483D, centered             |
| ddd_retry_button           | button   | Filled "Try Again" — #4C662B bg, #FFFFFF text, radius 12dp, pad H32                                    |

---

## States

| ID      | Trigger                              | Description                                                                                   |
|---------|--------------------------------------|-----------------------------------------------------------------------------------------------|
| loading | Screen entry / OnRetryClicked        | Full detail-screen skeleton shimmer; no interactive elements                                   |
| content | API load success                     | Merchant hero + mandate details card + payment history card + action row all rendered          |
| error   | API failure / network error          | Error icon + "Couldn't load mandate details. Please try again." + Try Again retry button       |
| empty   | mandateId resolves but no data       | Event_busy icon + "Mandate details not available" + "Back to Direct Debits" action button     |

---

## State Model

**ViewModel:** `DirectDebitDetailViewModel`
**Screen State Type:** `DirectDebitDetailUiState`

| Name                | Type                      | Default     |
|---------------------|---------------------------|-------------|
| mandateId           | String                    | ""          |
| merchantName        | String?                   | null        |
| merchantLogoUrl     | String?                   | null        |
| mandateStatus       | String?                   | null        |
| mandateAmount       | String?                   | null        |
| mandateFrequency    | String?                   | null        |
| nextPaymentDate     | String?                   | null        |
| linkedAccountName   | String?                   | null        |
| linkedAccountMasked | String?                   | null        |
| mandateReference    | String?                   | null        |
| mandateStartDate    | String?                   | null        |
| recentPayments      | List\<PaymentHistoryItem\>| emptyList() |
| isLoading           | Boolean                   | true        |
| errorMessage        | String?                   | null        |

**Events:** `LoadMandate`, `OnCancelClicked`, `OnEditClicked`, `OnRetryClicked`

**Actions:** `loadMandate(mandateId)`, `onCancelClicked()`, `onEditClicked()`, `onRetryClicked()`

**DI Dependencies:** `DirectDebitRepository`, `AccountRepository`

**Errors:**
- `NETWORK_ERROR`: "Couldn't load mandate details. Please try again."
- `MANDATE_NOT_FOUND`: "This direct debit mandate could not be found."
- `CANCEL_FAILED`: "Unable to cancel mandate. Please try again."

---

## Navigation

| From                | To            | Trigger                            | Type  |
|---------------------|---------------|------------------------------------|-------|
| direct-debit-detail | direct-debits | back arrow / ddd_cancel_button     | pop   |
| direct-debit-detail | accounts      | nav_to_accounts                    | push  |
| direct-debit-detail | transactions  | ddd_history_view_all_link          | push  |
| direct-debit-detail | direct-debits | ddd_edit_button                    | pop   |
| direct-debit-detail | direct-debits | empty state "Back to Direct Debits"| pop   |

---

## API Endpoints

| Endpoint                                                                                  | Auth        | Tag         | Purpose                            |
|-------------------------------------------------------------------------------------------|-------------|-------------|------------------------------------|
| GET /obp/v5.0.0/banks/{bankId}/accounts/{accountId}/direct-debit/{directDebitId}          | DirectLogin | DirectDebits| Fetch full mandate data for display|
| DELETE /obp/v5.0.0/banks/{bankId}/accounts/{accountId}/direct-debit/{directDebitId}       | DirectLogin | DirectDebits| Cancel (delete) this mandate        |

---

## Design Tokens

| Token                          | Value   | Usage                                                              |
|--------------------------------|---------|--------------------------------------------------------------------|
| color.light.primary            | #4C662B | Merchant hero bg, section headers, collected status, retry btn    |
| color.light.primary_container  | #CDEDA3 | Mandate status badge bg (Active), frequency text                   |
| color.light.on_primary_container| #4C662B | Mandate status badge text                                         |
| color.light.secondary          | #386663 | Edit Mandate button bg, "View all" link                            |
| color.light.error              | #BA1A1A | Cancel Mandate border+text, Failed payment text, error state icon  |
| color.light.on_surface_variant | #44483D | Mandate detail row labels, payment history captions                |
| color.light.on_surface         | #1A1C16 | Mandate detail row values, payment history dates+amounts           |
| color.light.surface            | #FFFFFF | Mandate Details card, Payment History card                         |
| color.light.background         | #F9FAEF | Screen background, root container                                  |
| color.light.outline_variant    | #E1E4D5 | Card internal dividers                                             |
| typography.headline_small      | —       | Merchant name in hero                                              |
| typography.display_small       | —       | Mandate amount in hero                                             |
| typography.body_medium         | —       | Frequency, detail row labels+values, history items                 |
| typography.body_small          | —       | Payment status labels, masked account number                       |
| typography.title_medium        | —       | "Mandate Details" + "Recent Payments" section headers              |
| typography.label_small         | —       | Status badge text                                                  |
| typography.label_medium        | —       | "View all" link                                                    |
| radius.md                      | 12dp    | Mandate Details card, Payment History card, retry button           |
| radius.lg                      | 16dp    | (reserved for bottom sheet if mandate options expand)              |
| spacing.lg                     | 24dp    | Screen padding, hero padding                                       |

---

_Generated by /idea export | 2026-05-29_
