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

The Agent Registration screen allows a Field Officer to self-register as an authorized OBP bank agent. On entry, the screen performs a pre-flight status check against OBP — if the officer is already pending approval, a `status_banner_pending` informs them and the form is read-only; if confirmed, a `status_banner_confirmed` with a "Go to Dashboard" CTA is shown. Otherwise, the form collects: Legal Name, Mobile Phone Number (+254 Kenya prefix), Agent Number (AGT-YYYY-NNNNN format), Operating Currency (dropdown: EUR/GBP/KES/USD), a multi-select chip group for Supported Services (Cash Deposit, Cash Withdrawal, Account Opening, Bill Payment, Fund Transfer), and Commission Rate (0.5–5.0%). On submit, the form calls `POST /obp/v5.1.0/banks/{bankId}/agents`. Inline validation errors appear per-field; a global error banner covers API-level failures.

---

## Screens

| ID                 | Name               | Route               | Layout | Scroll   |
|--------------------|--------------------|---------------------|--------|----------|
| agent-registration | Agent Registration | /agent-registration | Column | Vertical |

**Shell:** Top app bar, title "Agent Registration", back arrow. No bottom navigation bar.

---

## Components

| ID                      | Type             | Description                                                                                            |
|-------------------------|------------------|--------------------------------------------------------------------------------------------------------|
| agent_reg_title         | text             | "Agent Registration" — headline_large (32sp/Bold), color `#4C662B`                                    |
| agent_reg_subtitle      | text             | "Register to become an authorised OBP field agent with your bank" — body_medium, color `#44483D`      |
| registration_loading_spinner | loading_indicator | Spinner 48dp `#4C662B`, centred — shown during pre-flight OBP status check                  |
| loading_label           | text             | "Checking registration status…" — body_medium, color `#44483D`, centred                               |
| status_banner_pending   | box              | `#CDEDA3` bg, `#E8A317` border, 14dp radius; contains pending icon + title + message                  |
| pending_icon            | icon             | `hourglass_empty`, 22dp, color `#44483D`; decorative                                                  |
| pending_banner_title    | text             | "Pending Approval" — body_medium/SemiBold, color `#44483D`                                            |
| pending_banner_message  | text             | "Your agent application is under review. You will be notified once your bank confirms your registration." — body_small, `#44483D` |
| status_banner_confirmed | box              | `#CDEDA3` bg, `#CDEDA3` border, 14dp radius; contains verified icon + title + message                 |
| confirmed_icon          | icon             | `verified_outlined`, 22dp, color `#4C662B`; decorative                                                |
| confirmed_banner_title  | text             | "Agent Confirmed" — body_medium/SemiBold, color `#4C662B`                                             |
| confirmed_banner_message| text             | "You are registered as an active Mifos field agent. You can now onboard customers and process transactions." — body_small, `#4C662B` |
| go_to_dashboard_button  | button           | "Go to Dashboard" — filled `#4C662B`/white, full-width, 14dp radius, label_large; navigates to fo-dashboard |
| legal_name_label        | text             | "Legal Name" — label_medium/SemiBold, color `#44483D`                                                 |
| legal_name_input        | input            | Outlined text field, placeholder "e.g. Priya Chakraborty"; maps to OBP `legal_name`                   |
| legal_name_error        | text             | "Legal name is required" — body_small, color `#BA1A1A`; alert role                                    |
| phone_label             | text             | "Mobile Phone Number" — label_medium/SemiBold, color `#44483D`                                        |
| phone_prefix_box        | box              | "+254" static badge — `#F9FAEF` bg, 12dp radius, body_medium/SemiBold `#1A1C16`                       |
| phone_number_input      | input            | Outlined tel field, placeholder "712 345 678"; combined with +254 prefix for OBP                       |
| phone_error             | text             | "Enter a valid 9-digit phone number" — body_small, color `#BA1A1A`; alert role                        |
| agent_number_label      | text             | "Agent Number" — label_medium/SemiBold, color `#44483D`                                               |
| agent_number_input      | input            | Outlined text field, placeholder "e.g. AGT-2026-00142"; maps to OBP `agent_number`                    |
| agent_number_error      | text             | "Agent number is required" — body_small, color `#BA1A1A`; reused for DUPLICATE_AGENT error            |
| currency_label          | text             | "Operating Currency" — label_medium/SemiBold, color `#44483D`                                         |
| currency_select         | input            | Dropdown combobox, trailing `expand_more` icon; options: EUR, GBP, KES, USD                           |
| currency_error          | text             | "Select an operating currency" — body_small, color `#BA1A1A`; alert role                              |
| services_section_label  | text             | "Supported Services" — label_medium/SemiBold, color `#44483D`                                         |
| services_chip_group     | stack            | Wrap chip group — Cash Deposit, Cash Withdrawal, Account Opening, Bill Payment, Fund Transfer. Selected: `#4C662B` bg/white; unselected: `#CDEDA3` bg/`#4C662B` text |
| commission_label        | text             | "Commission Rate (%)" — label_medium/SemiBold, color `#44483D`                                        |
| commission_rate_input   | input            | Decimal outlined field, placeholder "e.g. 1.5", trailing `percent` icon; range 0.5–5.0                |
| global_error_banner     | box              | `#CDEDA3` bg, `#BA1A1A` border, 12dp radius; contains `error_outline` icon + error message text       |
| register_agent_button   | button           | "Register as Agent" — filled `#4C662B`/white, full-width, 14dp radius, label_large; triggers OBP POST |
| terms_notice            | text             | "By registering, you agree to the Mifos Agent Terms and Conditions" — body_small, `#44483D`, centred  |

---

## States

| ID               | Trigger                                           | Description                                                                               |
|------------------|---------------------------------------------------|-------------------------------------------------------------------------------------------|
| loading          | Screen entry — OBP status pre-check in flight     | Spinner + "Checking registration status…" text; form hidden                               |
| idle             | Status check returned no existing agent record    | Full registration form ready; no errors shown                                             |
| submitting       | Register button tapped, OBP call in flight        | Form inputs disabled; register button shows loading indicator                             |
| validation_error | Submit attempted with invalid fields              | Inline error messages shown per-field; form inputs re-enabled                             |
| pending_approval | OBP returned `is_pending_agent=true`              | Pending banner shown; form fields read-only; Register button hidden                       |
| confirmed        | OBP returned `is_confirmed_agent=true`            | Confirmed banner + "Go to Dashboard" button; form hidden                                  |
| content          | Alias for idle — form ready state                 | Same as idle; used as the default loaded state                                            |
| empty            | OBP returns no valid bank context                 | Title only + empty message; form unavailable                                              |
| error            | OBP API returned 4xx/5xx on submit                | Global error banner above re-enabled form                                                 |

---

## State Model

**ViewModel:** `AgentRegistrationViewModel`
**Screen State Type:** `AgentRegistrationUiState`

| Name              | Type                  | Default        |
|-------------------|-----------------------|----------------|
| legalName         | `String`              | `""`           |
| phoneNumber       | `String`              | `""`           |
| agentNumber       | `String`              | `""`           |
| currency          | `String`              | `"KES"`        |
| selectedServices  | `List<String>`        | `emptyList()`  |
| commissionRate    | `String`              | `""`           |
| isSubmitting      | `Boolean`             | `false`        |
| isLoading         | `Boolean`             | `true`         |
| agentId           | `String?`             | `null`         |
| isPendingAgent    | `Boolean`             | `false`        |
| isConfirmedAgent  | `Boolean`             | `false`        |
| uiState           | `AgentRegistrationUiState` | `Loading` |
| validationErrors  | `Map<String, String>` | `emptyMap()`   |
| error             | `UiError?`            | `null`         |

**Events:** `LegalNameChanged(value)`, `PhoneNumberChanged(value)`, `AgentNumberChanged(value)`, `CurrencySelected(value)`, `ServiceToggled(service)`, `CommissionRateChanged(value)`, `SubmitClicked`, `RegistrationSuccess(agentId, isPending)`, `RegistrationFailed(error)`, `CurrencyPickerOpened`, `StatusCheckSuccess(isPending, isConfirmed)`, `StatusCheckFailed`

**Actions:** `focus_legal_name`, `focus_phone`, `focus_agent_number`, `open_currency_picker`, `toggle_service`, `focus_commission_rate`, `submit_registration`, `navigate_to_dashboard`

**DI Dependencies:** `AgentRepository`, `BankRepository`, `ValidationService`

**Errors:**
- `legal_name / REQUIRED`: "Legal name is required"
- `phone_number / INVALID_FORMAT`: "Enter a valid 9-digit phone number"
- `agent_number / REQUIRED`: "Agent number is required"
- `agent_number / DUPLICATE_AGENT`: "An agent with this number already exists"
- `currency / REQUIRED`: "Select an operating currency"
- `services / REQUIRED`: "Select at least one supported service"
- `global / SUBMIT_FAILED`: "Registration failed. Please check your details and try again."
- `global / NETWORK_ERROR`: "No internet connection. Please check your network and retry."

---

## Navigation

| From               | To           | Trigger                                  | Type     |
|--------------------|--------------|------------------------------------------|----------|
| agent-registration | fo-dashboard | go_to_dashboard_button tap (confirmed)   | replace  |
| agent-registration | fo-dashboard | Top app bar back arrow                   | pop      |

---

## API Endpoints

| Endpoint                                        | Auth        | Tag   | Purpose                                               |
|-------------------------------------------------|-------------|-------|-------------------------------------------------------|
| POST /obp/v5.1.0/banks/{bankId}/agents           | DirectLogin | Agent | Register field officer as an OBP bank agent           |

---

## Design Tokens

| Token                           | Value     | Usage                                                              |
|---------------------------------|-----------|--------------------------------------------------------------------|
| colors.light.primary            | `#4C662B` | Page title, confirmed banner text, chip selected state, submit btn |
| colors.light.on_primary         | `#FFFFFF` | Submit button text, selected service chip text                     |
| colors.light.primary_container  | `#CDEDA3` | Pending + confirmed banner bg, unselected service chip bg          |
| colors.light.on_surface         | `#1A1C16` | Phone prefix badge text                                            |
| colors.light.on_surface_variant | `#44483D` | Subtitle, field labels, pending banner text (a11y-corrected)       |
| colors.light.error              | `#BA1A1A` | Inline validation error text, global error banner border + icon    |
| colors.light.pending            | `#E8A317` | Pending banner border                                              |
| colors.light.surface_variant    | `#E1E4D5` | Input field border color                                           |
| colors.light.background         | `#F9FAEF` | Screen background, phone prefix box background                     |
| typography.headline_large       | 32sp/Bold | Page title                                                        |
| typography.body_medium          | 14sp/Regular | Subtitle, banner messages, loading label, input values          |
| typography.label_medium         | 12sp/Medium  | Field labels, service chip labels                               |
| typography.label_large          | 14sp/Medium  | Submit and Go to Dashboard button labels                        |
| typography.body_small           | 12sp/Regular | Inline validation errors, terms notice                         |
| radius.lg                       | 16dp      | Submit + Go to Dashboard button radius (14dp specified)             |
| radius.md                       | 12dp      | Input fields, global error banner                                  |
| spacing.md                      | 16dp      | Standard horizontal margin for inputs and banners                  |

---

_Generated by /idea export | 2026-05-29_
