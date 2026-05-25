# Feature Specification: Agent Registration

| Field | Value |
|---|---|
| Feature | agent-registration |
| Flavor | fieldOfficer |
| Status | enriched |
| Quality Score | 78 |

## Overview

The Agent Registration screen enables a logged-in Mifos user to apply to become an authorised field agent for a specific bank branch. The officer fills in their legal name, mobile phone number (with +254 Kenya prefix), their assigned agent number, and their operating currency. On submission the OBP API creates the agent record and transitions the screen inline to either a Pending Approval state (most common) or a Confirmed state if instant approval is granted. A top app bar with back navigation anchors the screen to the Field Officer Dashboard.

## Screens

| Screen ID | Name | Route | Layout | Scroll |
|---|---|---|---|---|
| agent-registration | Agent Registration | /agent-registration | form | vertical |

## Components

| ID | Type | Description |
|---|---|---|
| agent_reg_title | text | "Agent Registration" — headline_large #1800B1 bold |
| agent_reg_subtitle | text | "Register to become an authorised Mifos field agent" — body_medium #666666 |
| status_banner_pending | box | Amber banner with hourglass icon: "Pending Approval" — shown in pending_approval state |
| status_banner_confirmed | box | Green banner with verified icon: "Agent Confirmed" — shown in confirmed state |
| legal_name_input | input | Outlined text field — "Enter your full legal name" |
| phone_prefix_box | box | Static "+254" country code box in #F5F5F5 |
| phone_number_input | input | Phone number field — keyboard type: phone; placeholder "712 345 678" |
| agent_number_input | input | Outlined text field — "e.g. AGT-2026-00142" |
| currency_select | input | Dropdown selector — options: EUR, GBP, KES, USD; trailing expand_more icon |
| register_agent_button | button | "Register as Agent" — filled #1800B1 full-width; loading state during submission |
| terms_notice | text | "By registering, you agree to the Mifos Agent Terms and Conditions" — body_small centered |

## States

| ID | Trigger | Description |
|---|---|---|
| idle | Screen mount | All form fields and Register button visible; no status banner |
| submitting | Register button tapped | Button shows loading indicator; all inputs disabled; form still visible |
| pending_approval | API returns is_pending_agent: true | Amber banner shown; form fields shown read-only; Register button hidden |
| confirmed | API returns is_confirmed_agent: true | Green banner shown; form fields hidden; Register button hidden |
| error | API returns error | Snackbar shown with "Registration failed. Please check your details and try again." |

## State Model

**ViewModel:** `AgentRegistrationViewModel`

| Field | Type | Default |
|---|---|---|
| legalName | String | "" |
| phoneNumber | String | "" |
| agentNumber | String | "" |
| currency | String | "KES" |
| isSubmitting | Boolean | false |
| agentId | String? | null |
| isPendingAgent | Boolean | false |
| isConfirmedAgent | Boolean | false |
| uiState | AgentRegistrationUiState | Idle |
| validationErrors | Map\<String, String\> | emptyMap() |
| error | UiError? | null |

**Validation Errors:**

| Field | Code | Message |
|---|---|---|
| legal_name | REQUIRED | Legal name is required |
| phone_number | INVALID_FORMAT | Enter a valid 9-digit phone number |
| agent_number | REQUIRED | Agent number is required |
| currency | REQUIRED | Select an operating currency |
| global | SUBMIT_FAILED | Registration failed. Please check your details and try again. |
| global | DUPLICATE_AGENT | An agent with this number already exists. |

**Events:** `LegalNameChanged`, `PhoneNumberChanged`, `AgentNumberChanged`, `CurrencySelected`, `SubmitClicked`, `RegistrationSuccess`, `RegistrationFailed`, `CurrencyPickerOpened`

**Actions:** `focus_legal_name`, `focus_phone`, `focus_agent_number`, `open_currency_picker`, `submit_registration`

**DI Dependencies:** `AgentRepository`, `BankRepository`, `ValidationService`

## Navigation

| From | To | Trigger | Type |
|---|---|---|---|
| agent-registration | fo-dashboard | navigate_back (top app bar) | pop |
| agent-registration | (inline) | submit_registration success | state transition (no nav) |

## API Endpoints

| Endpoint | Auth | Purpose |
|---|---|---|
| POST /obp/v5.1.0/banks/{bankId}/agents | DirectLogin token | Submit agent registration; returns agent_id, is_pending_agent, is_confirmed_agent |

## Design Tokens

| Token | Value | Usage |
|---|---|---|
| primary | #1800B1 | Title, register button background |
| input_border | #CCCCCC | All form field borders (idle state) |
| input_radius | 12dp | border_radius for all input fields |
| pending_bg | #FFF8E1 | Pending approval banner background |
| pending_border | #FFD54F | Pending banner border color |
| pending_text | #F57F17 | "Pending Approval" text color |
| confirmed_bg | #E8F5E9 | Confirmed banner background |
| confirmed_border | #A5D6A7 | Confirmed banner border color |
| confirmed_text | #2E7D32 | "Agent Confirmed" text color |
| prefix_bg | #F5F5F5 | Phone prefix box background |

---
_Generated by /idea export | 2026-05-25_
