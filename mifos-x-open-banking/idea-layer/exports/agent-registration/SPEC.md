# SPEC — Agent Registration

| Field         | Value                          |
|---------------|--------------------------------|
| Feature       | agent-registration             |
| Flavor        | fieldOfficer                   |
| Status        | approved                       |
| Quality Score | 97                             |
| ViewModel     | AgentRegistrationViewModel     |

---

## Overview

The Agent Registration screen enables a Field Officer to self-register as an authorised OBP bank agent. On entry the screen performs a pre-flight OBP status check (`isLoading=true`): if the officer is already pending, a `status_banner_pending` (#CDEDA3 bg / #E8A317 border, `hourglass_empty` icon, `#44483D` text) informs them and the form is fully read-only with the Register button hidden; if already confirmed, a `status_banner_confirmed` (#CDEDA3 bg / #CDEDA3 border, `verified_outlined` icon, #4C662B text) is shown alongside the "Go to Dashboard" CTA that navigates to `fo-dashboard`. When no prior agent record exists the idle form renders: Legal Name (text input, placeholder "e.g. Priya Chakraborty"), Mobile Phone Number (horizontal row — static +254 Kenya prefix box + 9-digit phone input), Agent Number (text input, placeholder "e.g. AGT-2026-00142", format AGT-YYYY-NNNNN), Operating Currency (combobox: EUR / GBP / KES / USD, trailing `expand_more`), Supported Services (multi-select wrap chip group: Cash Deposit / Cash Withdrawal / Account Opening / Bill Payment / Fund Transfer), and Commission Rate (decimal input 0.5–5.0, trailing `percent` icon). Submitting calls `POST /obp/v5.1.0/banks/{bankId}/agents`; inline per-field errors cover client-side validation failures; a global error banner covers OBP 4xx/5xx responses. There is no bottom navigation bar — only a top app bar with back arrow navigating to `fo-dashboard`.

---

## Screens

| ID                 | Name               | Route               | Layout | Scroll   |
|--------------------|--------------------|---------------------|--------|----------|
| agent-registration | Agent Registration | /agent-registration | Column | Vertical |

**Shell:** Top app bar — title "Agent Registration", `arrow_back` navigation icon → `navigate_back` → `fo-dashboard`. No bottom navigation bar.

---

## Components

| ID                          | Type              | Description                                                                                                                                |
|-----------------------------|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| agent_reg_title             | text              | "Agent Registration" — Outfit/headline_large (32sp/Bold), color `#4C662B`, 20dp H padding, 16dp top / 4dp bottom padding                  |
| agent_reg_subtitle          | text              | "Register to become an authorised OBP field agent with your bank" — body_medium, `#44483D`, 20dp H / 24dp bottom padding                  |
| registration_loading_spinner| loading_indicator | 48dp circular indicator, `#4C662B`; centred with 80dp top margin; shown during pre-flight OBP status check                                 |
| loading_label               | text              | "Checking registration status…" — body_medium, `#44483D`, centred; 16dp bottom margin; shown below spinner                                |
| status_banner_pending       | box               | `#CDEDA3` bg, `#E8A317` border (1dp), 14dp radius, 16dp H / 14dp V padding, 20dp H / 20dp bottom margin                                   |
| pending_banner_row          | stack             | Horizontal row, 10dp spacing, aligned centre — holds `pending_icon` + `pending_text_col`                                                   |
| pending_icon                | icon              | `hourglass_empty`, 22dp, `#44483D`; decorative (role: none)                                                                                |
| pending_text_col            | stack             | Vertical column (flex 1) — holds `pending_banner_title` + `pending_banner_message`                                                         |
| pending_banner_title        | text              | "Pending Approval" — body_medium/SemiBold, `#44483D`                                                                                       |
| pending_banner_message      | text              | "Your agent application is under review. You will be notified once your bank confirms your registration." — body_small, `#44483D`          |
| status_banner_confirmed     | box               | `#CDEDA3` bg, `#CDEDA3` border (1dp), 14dp radius, 16dp H / 14dp V padding, 20dp H / 20dp bottom margin                                   |
| confirmed_banner_row        | stack             | Horizontal row, 10dp spacing, aligned centre — holds `confirmed_icon` + confirmed text nodes                                               |
| confirmed_icon              | icon              | `verified_outlined`, 22dp, `#4C662B`; decorative (role: none)                                                                              |
| confirmed_banner_title      | text              | "Agent Confirmed" — body_medium/SemiBold, `#4C662B`                                                                                        |
| confirmed_banner_message    | text              | "You are registered as an active Mifos field agent. You can now onboard customers and process transactions." — body_small, `#4C662B`       |
| go_to_dashboard_button      | button            | "Go to Dashboard" — filled, `#4C662B` bg / `#FFFFFF` text, full-width, 14dp radius, label_large, 24dp H / 16dp V padding, 2dp elevation; `on_click: navigate_to_dashboard → fo-dashboard` |
| legal_name_label            | text              | "Legal Name" — label_medium/SemiBold, `#44483D`, 20dp H padding, 6dp bottom                                                                |
| legal_name_input            | input             | Outlined text field; placeholder "e.g. Priya Chakraborty"; 12dp radius; `#E1E4D5` border; maps to OBP `legal_name`                         |
| legal_name_error            | text              | "Legal name is required" — body_small, `#BA1A1A`; `role: alert`; `live: assertive`                                                         |
| phone_label                 | text              | "Mobile Phone Number" — label_medium/SemiBold, `#44483D`, 20dp H padding, 6dp bottom                                                       |
| phone_input_row             | stack             | Horizontal, 8dp gap, 20dp H margin — contains `phone_prefix_box` + `phone_number_input`                                                    |
| phone_prefix_box            | box               | "+254" — static Kenya dialling code; `#F9FAEF` bg, 12dp radius, 14dp H/V padding, `#E1E4D5` border (1dp), `#1A1C16` body_medium/SemiBold  |
| phone_number_input          | input             | Outlined tel input (flex 1); placeholder "712 345 678"; keyboard: phone; combined with +254 prefix → `+254XXXXXXXXX` sent to OBP           |
| phone_error                 | text              | "Enter a valid 9-digit phone number" — body_small, `#BA1A1A`; `role: alert`; `live: assertive`                                             |
| agent_number_label          | text              | "Agent Number" — label_medium/SemiBold, `#44483D`, 20dp H padding, 6dp bottom                                                              |
| agent_number_input          | input             | Outlined text field; placeholder "e.g. AGT-2026-00142"; 12dp radius; format AGT-YYYY-NNNNN; maps to OBP `agent_number`                     |
| agent_number_error          | text              | "Agent number is required" — body_small, `#BA1A1A`; also shown for `DUPLICATE_AGENT` error from OBP                                        |
| currency_label              | text              | "Operating Currency" — label_medium/SemiBold, `#44483D`, 20dp H padding, 6dp bottom                                                        |
| currency_select             | input             | Combobox (dropdown), `expand_more` trailing icon; options: EUR — Euro, GBP — British Pound, KES — Kenyan Shilling, USD — US Dollar         |
| currency_error              | text              | "Select an operating currency" — body_small, `#BA1A1A`; `role: alert`; `live: assertive`                                                   |
| services_section_label      | text              | "Supported Services" — label_medium/SemiBold, `#44483D`, 20dp H padding, 8dp top / 10dp bottom; `role: heading`                            |
| services_chip_group         | stack             | Wrap chip group, 8dp gap, 20dp H margin; chips: Cash Deposit / Cash Withdrawal / Account Opening / Bill Payment / Fund Transfer. Selected: `#4C662B` bg / `#FFFFFF` text; unselected: `#CDEDA3` bg / `#4C662B` text / `#4C662B` border (1dp) / 20dp radius |
| commission_label            | text              | "Commission Rate (%)" — label_medium/SemiBold, `#44483D`, 20dp H padding, 6dp bottom                                                       |
| commission_rate_input       | input             | Decimal outlined field; placeholder "e.g. 1.5"; trailing `percent` icon; keyboard: decimal; range 0.5–5.0; 28dp bottom margin              |
| global_error_banner         | box               | `#CDEDA3` bg, `#BA1A1A` border (1dp), 12dp radius, 16dp H / 12dp V padding, 20dp H / 16dp bottom margin; holds `error_icon` + `global_error_message` |
| global_error_row            | stack             | Horizontal, 10dp spacing, centre-aligned — icon + message                                                                                  |
| error_icon                  | icon              | `error_outline`, 20dp, `#BA1A1A`; decorative (role: none)                                                                                  |
| global_error_message        | text              | "Registration failed. Please check your details and try again." — body_small, `#BA1A1A`; driven by `error.message`                         |
| register_agent_button       | button            | "Register as Agent" — filled, `#4C662B` bg / `#FFFFFF` text, full-width, 14dp radius, label_large, 2dp elevation; disabled + loading during `submitting` state |
| terms_notice                | text              | "By registering, you agree to the Mifos Agent Terms and Conditions" — body_small, `#44483D`, centred, 20dp H / 24dp bottom padding         |

---

## States

| ID               | Trigger                                              | Description                                                                                               |
|------------------|------------------------------------------------------|-----------------------------------------------------------------------------------------------------------|
| loading          | Screen entry — OBP status pre-check in flight        | Spinner (48dp `#4C662B`) + "Checking registration status…" centred; form hidden; `isLoading=true`         |
| idle             | Status check returned no existing agent record       | Full registration form ready; no error messages shown; `isLoading=false`                                  |
| content          | Alias for idle — default loaded state                | Same layout as idle; used by dashboard/pipeline as the canonical "loaded" state                           |
| submitting       | Register button tapped, OBP POST in flight           | Form inputs disabled (`inputs_enabled=false`); register button shows loading indicator                    |
| validation_error | Submit attempted with invalid field values           | Inline error messages per-field (`legal_name_error`, `phone_error`, `agent_number_error`, `currency_error`); form re-enabled |
| pending_approval | OBP pre-check or POST returned `is_pending_agent=true` | Pending banner shown; all form inputs read-only; Register button hidden; terms notice hidden              |
| confirmed        | OBP pre-check or POST returned `is_confirmed_agent=true` | Confirmed banner + "Go to Dashboard" button; form hidden                                             |
| error            | OBP API returned 4xx/5xx on registration POST        | Global error banner above re-enabled form; `show_error_snackbar=false`                                    |
| empty            | OBP returns no valid bank context for current user   | Page title only + empty message "Registration form not available"; form unavailable                       |

---

## State Model

**ViewModel:** `AgentRegistrationViewModel`
**Screen State Type:** `AgentRegistrationUiState`

| Name              | Type                       | Default        |
|-------------------|----------------------------|----------------|
| legalName         | `String`                   | `""`           |
| phoneNumber       | `String`                   | `""`           |
| agentNumber       | `String`                   | `""`           |
| currency          | `String`                   | `"KES"`        |
| selectedServices  | `List<String>`             | `emptyList()`  |
| commissionRate    | `String`                   | `""`           |
| isSubmitting      | `Boolean`                  | `false`        |
| isLoading         | `Boolean`                  | `true`         |
| agentId           | `String?`                  | `null`         |
| isPendingAgent    | `Boolean`                  | `false`        |
| isConfirmedAgent  | `Boolean`                  | `false`        |
| uiState           | `AgentRegistrationUiState` | `Loading`      |
| validationErrors  | `Map<String, String>`      | `emptyMap()`   |
| error             | `UiError?`                 | `null`         |

**Events:** `LegalNameChanged(value: String)`, `PhoneNumberChanged(value: String)`, `AgentNumberChanged(value: String)`, `CurrencySelected(value: String)`, `ServiceToggled(service: String)`, `CommissionRateChanged(value: String)`, `SubmitClicked`, `RegistrationSuccess(agentId: String, isPending: Boolean)`, `RegistrationFailed(error: UiError)`, `CurrencyPickerOpened`, `StatusCheckSuccess(isPending: Boolean, isConfirmed: Boolean)`, `StatusCheckFailed`

**Actions:** `focus_legal_name`, `focus_phone`, `focus_agent_number`, `open_currency_picker`, `toggle_service`, `focus_commission_rate`, `submit_registration`, `navigate_to_dashboard`

**DI Dependencies:** `AgentRepository`, `BankRepository`, `ValidationService`

**Errors:**

| Field        | Code              | Message                                                             |
|--------------|-------------------|---------------------------------------------------------------------|
| legal_name   | REQUIRED          | "Legal name is required"                                            |
| phone_number | INVALID_FORMAT    | "Enter a valid 9-digit phone number"                                |
| agent_number | REQUIRED          | "Agent number is required"                                          |
| agent_number | DUPLICATE_AGENT   | "An agent with this number already exists"                          |
| currency     | REQUIRED          | "Select an operating currency"                                      |
| services     | REQUIRED          | "Select at least one supported service"                             |
| global       | SUBMIT_FAILED     | "Registration failed. Please check your details and try again."     |
| global       | NETWORK_ERROR     | "No internet connection. Please check your network and retry."      |

---

## Navigation

| From               | To           | Trigger                                              | Type    |
|--------------------|--------------|------------------------------------------------------|---------|
| agent-registration | fo-dashboard | `go_to_dashboard_button` tap (confirmed state)       | replace |
| agent-registration | fo-dashboard | Top app bar `arrow_back` → `navigate_back` action    | pop     |
| agent-registration | —            | `submit_registration` success: transitions to `pending_approval` or `confirmed` inline (no navigation) | inline |

---

## API Endpoints

| Endpoint                                            | Auth        | Tag   | Purpose                                            |
|-----------------------------------------------------|-------------|-------|----------------------------------------------------|
| POST /obp/v5.1.0/banks/{bankId}/agents              | DirectLogin | Agent | Register field officer as an OBP bank agent        |

---

## Design Tokens

| Token                           | Value     | Usage                                                                                           |
|---------------------------------|-----------|-------------------------------------------------------------------------------------------------|
| colors.light.primary            | `#4C662B` | Page title, confirmed banner text+icon, selected chip bg, Register + Go to Dashboard button fill |
| colors.light.on_primary         | `#FFFFFF` | Button text, selected chip text                                                                 |
| colors.light.primary_container  | `#CDEDA3` | Pending + confirmed banner bg, unselected chip bg, global error banner bg                       |
| colors.light.on_surface         | `#1A1C16` | Phone prefix badge text (`body_medium/SemiBold`)                                                |
| colors.light.on_surface_variant | `#44483D` | Subtitle text, all field labels, pending banner text (a11y-corrected from `#E8A317`)            |
| colors.light.error              | `#BA1A1A` | Inline validation error text, global error banner border, `error_outline` icon                  |
| colors.light.pending            | `#E8A317` | Pending banner border only                                                                      |
| colors.light.surface_variant    | `#E1E4D5` | Input field outline border                                                                      |
| colors.light.background         | `#F9FAEF` | Screen base, phone prefix box background                                                        |
| typography.headline_large       | Outfit 32sp / Bold    | Page title `agent_reg_title`                                                   |
| typography.body_medium          | Outfit 14sp / Regular | Subtitle, banner messages, loading label, input placeholder text               |
| typography.label_medium         | Outfit 12sp / Medium  | Field labels, chip labels                                                      |
| typography.label_large          | Outfit 14sp / Medium  | Register + Go to Dashboard button labels                                       |
| typography.body_small           | Outfit 12sp / Regular | Inline validation errors, terms notice, banner body text                       |
| radius.md                       | 12dp      | Input fields, phone prefix box, global error banner                                             |
| radius.lg                       | 16dp      | Button radius (14dp specified in source — nearest token)                                        |
| spacing.md                      | 16dp      | Standard horizontal padding and banner padding                                                  |
| spacing.lg                      | 24dp      | Button horizontal padding, bottom-of-form breathing room                                        |
| elevation.level2                | 3dp       | Register + Go to Dashboard button elevation (2dp specified)                                     |
| touchTargets.min_touch_target   | 48dp      | All inputs and buttons minimum touch target                                                     |

---

_Generated by /idea export | 2026-05-30_
