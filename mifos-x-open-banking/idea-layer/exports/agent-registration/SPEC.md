# Feature Specification: Agent Registration

| Field | Value |
|---|---|
| Feature | agent-registration |
| Flavor | fieldOfficer |
| Status | designed |
| Quality Score | 88 |
| Contract Version | 1.1.0 |

---

## Feature Overview

The Agent Registration screen enables a logged-in Mifos field officer (FO) to self-register as an authorised OBP agent for a specific bank. The officer supplies their legal business name, mobile phone number (Kenya +254 prefix), their Mifos-assigned agent number, operating currency, a multi-select list of supported agent banking services, and their preferred commission rate (0.5–5%).

On submission the app calls `POST /obp/v5.1.0/banks/{bankId}/agents`. The screen transitions inline — no navigation — to either:
- **pending_approval** when the bank requires manual review (`is_pending_agent: true`)
- **confirmed** when instant approval is granted (`is_confirmed_agent: true`)

A pre-flight OBP status check runs on screen entry (loading state) to detect if the officer already has a pending or confirmed record, preventing duplicate submissions.

The screen is anchored by a top app bar with a back arrow returning to `fo-dashboard`. No bottom navigation bar is shown on this screen.

---

## Screen Inventory

| Screen ID | Name | Route | Archetype | Scroll |
|---|---|---|---|---|
| agent-registration | Agent Registration | /agent-registration | form | vertical |

---

## Components

### Page Header

| ID | Type | Content | Style |
|---|---|---|---|
| agent_reg_title | text | "Agent Registration" | headline_large, #1800B1, bold, px 20, pt 16 |
| agent_reg_subtitle | text | "Register to become an authorised OBP field agent with your bank" | body_medium, #666666, px 20, pb 24 |

### Loading State

| ID | Type | Content | Style |
|---|---|---|---|
| registration_loading_spinner | loading_indicator | "Checking existing agent status…" | size 48, #1800B1, centered, mt 80 |
| loading_label | text | "Checking registration status…" | body_medium, #888888, centered, px 40 |

### Pending Approval Banner

| ID | Type | Content | Style |
|---|---|---|---|
| status_banner_pending | box | Pending Approval container | bg #FFF8E1, radius 14, border #FFD54F 1px, mx 20, mb 20 |
| pending_banner_row | stack | Horizontal icon + text row | horizontal, spacing 10, align center |
| pending_icon | icon | hourglass_empty | size 22, #F57F17, decorative |
| pending_text_col | stack | Vertical text group | vertical, flex 1 |
| pending_banner_title | text | "Pending Approval" | body_medium, #F57F17, semibold |
| pending_banner_message | text | "Your agent application is under review. You will be notified once your bank confirms your registration." | body_small, #795548 |

### Confirmed Banner

| ID | Type | Content | Style |
|---|---|---|---|
| status_banner_confirmed | box | Confirmed status container | bg #E8F5E9, radius 14, border #A5D6A7 1px, mx 20, mb 20 |
| confirmed_banner_row | stack | Horizontal icon + text row | horizontal, spacing 10, align center |
| confirmed_icon | icon | verified_outlined | size 22, #4CAF50, decorative |
| confirmed_banner_title | text | "Agent Confirmed" | body_medium, #2E7D32, semibold |
| confirmed_banner_message | text | "You are registered as an active Mifos field agent. You can now onboard customers and process transactions." | body_small, #388E3C |
| go_to_dashboard_button | button | "Go to Dashboard" | filled, bg #1800B1, white text, radius 14, full width, elevation 2 |

### Registration Form

| ID | Type | Content | Style |
|---|---|---|---|
| legal_name_label | text | "Legal Name" | label_medium, #444444, semibold, px 20 |
| legal_name_input | input | placeholder "e.g. Priya Chakraborty" | outlined, border #CCCCCC, radius 12, mx 20 |
| legal_name_error | text | "Legal name is required" | body_small, #B00020, alert role, assertive live |
| phone_label | text | "Mobile Phone Number" | label_medium, #444444, semibold, px 20 |
| phone_input_row | stack | Country code + number row | horizontal, spacing 8, mx 20 |
| phone_prefix_box | box | "+254" | bg #F5F5F5, radius 12, border #CCCCCC, body_medium semibold |
| phone_number_input | input | placeholder "712 345 678" | outlined, keyboard_type phone, flex 1 |
| phone_error | text | "Enter a valid 9-digit phone number" | body_small, #B00020, alert role, assertive live |
| agent_number_label | text | "Agent Number" | label_medium, #444444, semibold, px 20 |
| agent_number_input | input | placeholder "e.g. AGT-2026-00142" | outlined, border #CCCCCC, radius 12, mx 20; hint "Format: AGT-YYYY-NNNNN" |
| agent_number_error | text | "Agent number is required" | body_small, #B00020, alert role, assertive live |
| currency_label | text | "Operating Currency" | label_medium, #444444, semibold, px 20 |
| currency_select | input | placeholder "Select currency" | outlined, input_type select, trailing expand_more icon, combobox role |
| currency_error | text | "Select an operating currency" | body_small, #B00020, alert role, assertive live |
| services_section_label | text | "Supported Services" | label_medium, #444444, semibold, px 20, heading role |
| services_chip_group | chip_group | Cash Deposit / Cash Withdrawal / Account Opening / Bill Payment / Fund Transfer | wrap orientation, selected bg #1800B1 white text, unselected bg #EEF0FF #1800B1 text, radius 20 |
| commission_label | text | "Commission Rate (%)" | label_medium, #444444, semibold, px 20 |
| commission_rate_input | input | placeholder "e.g. 1.5" | outlined, keyboard_type decimal, trailing percent icon, mx 20; hint "Enter value between 0.5 and 5.0 percent" |

### Error & Submit

| ID | Type | Content | Style |
|---|---|---|---|
| global_error_banner | box | "Registration failed. Please check your details and try again." | bg #FFEBEE, radius 12, border #EF9A9A 1px, mx 20, alert role, assertive live |
| global_error_row | stack | Horizontal error icon + message | horizontal, spacing 10, align center |
| error_icon | icon | error_outline | size 20, #B00020, decorative |
| global_error_message | text | Dynamic error.message from OBP response | body_small, #B00020 |
| register_agent_button | button | "Register as Agent" | filled, bg #1800B1, white text, radius 14, full width, elevation 2 |
| terms_notice | text | "By registering, you agree to the Mifos Agent Terms and Conditions" | body_small, #888888, centered, px 20, pb 24 |

---

## States

| State | Trigger | Description |
|---|---|---|
| loading | Screen entry | Pre-flight OBP status check in progress. Shows spinner + "Checking registration status…" label. Form is not rendered. |
| idle | Status check completes — no existing record | Empty registration form. All inputs enabled. Register button visible. No status banner. |
| submitting | Register button tapped | Form still visible. All inputs disabled. Register button shows loading indicator. OBP call in flight. |
| validation_error | Submit with invalid/missing fields | Form re-enabled. Inline error messages appear beneath each invalid field. Global error banner hidden. |
| pending_approval | OBP returns is_pending_agent=true | Amber pending banner shown above read-only form. Register button hidden. |
| confirmed | OBP returns is_confirmed_agent=true | Green confirmed banner + "Go to Dashboard" button shown. Form inputs hidden. |
| error | OBP API returns 4xx/5xx | Global red error banner shown above re-enabled form. Register button visible for retry. |

### State-to-Component Visibility Matrix

| Component | loading | idle | submitting | validation_error | pending_approval | confirmed | error |
|---|---|---|---|---|---|---|---|
| agent_reg_title | Y | Y | Y | Y | Y | Y | Y |
| agent_reg_subtitle | — | Y | Y | Y | — | — | Y |
| registration_loading_spinner | Y | — | — | — | — | — | — |
| loading_label | Y | — | — | — | — | — | — |
| status_banner_pending | — | — | — | — | Y | — | — |
| status_banner_confirmed | — | — | — | — | — | Y | — |
| go_to_dashboard_button | — | — | — | — | — | Y | — |
| global_error_banner | — | — | — | — | — | — | Y |
| registration form (all fields) | — | Y | Y | Y | Y (read-only) | — | Y |
| legal_name_error | — | — | — | Y | — | — | — |
| phone_error | — | — | — | Y | — | — | — |
| agent_number_error | — | — | — | Y | — | — | — |
| currency_error | — | — | — | Y | — | — | — |
| register_agent_button | — | Y | Y (loading) | Y | — | — | Y |
| terms_notice | — | Y | Y | Y | — | — | Y |

---

## State Model

**ViewModel:** `AgentRegistrationViewModel`

### State Fields

| Field | Type | Default | Description |
|---|---|---|---|
| legalName | String | "" | Legal business name input value |
| phoneNumber | String | "" | 9-digit phone number (without +254 prefix) |
| agentNumber | String | "" | Mifos-assigned unique agent identifier |
| currency | String | "KES" | Selected operating currency; defaults to Kenyan Shilling |
| selectedServices | List\<String\> | emptyList() | Multi-select list of OBP service codes |
| commissionRate | String | "" | Commission percentage string; validated 0.5–5.0 |
| isSubmitting | Boolean | false | True while OBP POST call is in flight |
| isLoading | Boolean | true | True during pre-flight OBP status check |
| agentId | String? | null | OBP-assigned agent_id received on success |
| isPendingAgent | Boolean | false | True when OBP returns is_pending_agent=true |
| isConfirmedAgent | Boolean | false | True when OBP returns is_confirmed_agent=true |
| uiState | AgentRegistrationUiState | Loading | Active display state enum |
| validationErrors | Map\<String, String\> | emptyMap() | Field code → error message pairs |
| error | UiError? | null | Global error for banner display |

### Validation Error Codes

| Field | Code | User-Facing Message |
|---|---|---|
| legal_name | REQUIRED | "Legal name is required" |
| phone_number | INVALID_FORMAT | "Enter a valid 9-digit phone number" |
| agent_number | REQUIRED | "Agent number is required" |
| agent_number | DUPLICATE_AGENT | "An agent with this number already exists" |
| currency | REQUIRED | "Select an operating currency" |
| services | REQUIRED | "Select at least one supported service" |
| global | SUBMIT_FAILED | "Registration failed. Please check your details and try again." |
| global | NETWORK_ERROR | "No internet connection. Please check your network and retry." |

### Events

| Event | Payload | Effect |
|---|---|---|
| LegalNameChanged | value: String | Updates legalName; clears legal_name validation error |
| PhoneNumberChanged | value: String | Updates phoneNumber; clears phone_number validation error |
| AgentNumberChanged | value: String | Updates agentNumber; clears agent_number validation error |
| CurrencySelected | value: String | Updates currency; clears currency validation error |
| ServiceToggled | service: String | Toggles item in selectedServices; clears services validation error |
| CommissionRateChanged | value: String | Updates commissionRate |
| CurrencyPickerOpened | — | Opens currency bottom sheet picker |
| SubmitClicked | — | Runs client-side validation → OBP POST if valid |
| RegistrationSuccess | agentId: String, isPending: Boolean | Updates agentId, isPendingAgent / isConfirmedAgent; transitions uiState |
| RegistrationFailed | error: UiError | Populates error field; transitions uiState to Error |
| StatusCheckSuccess | isPending: Boolean, isConfirmed: Boolean | Determines initial state (idle / pending_approval / confirmed) |
| StatusCheckFailed | — | Logs failure silently; renders idle form |

### Actions (UI → ViewModel)

`focus_legal_name` · `focus_phone` · `focus_agent_number` · `open_currency_picker` · `toggle_service` · `focus_commission_rate` · `submit_registration` · `navigate_to_dashboard`

### DI Dependencies

`AgentRepository` · `BankRepository` · `ValidationService`

---

## Navigation

| Trigger | From | To | Type |
|---|---|---|---|
| navigate_back (top app bar arrow) | agent-registration | fo-dashboard | pop |
| navigate_to_dashboard (confirmed state CTA) | agent-registration | fo-dashboard | navigate |
| submit_registration success | agent-registration | (inline state transition) | no navigation |

---

## Supported Services (chip_group values)

| OBP Code | Display Label |
|---|---|
| cash_deposit | Cash Deposit |
| cash_withdrawal | Cash Withdrawal |
| account_opening | Account Opening |
| bill_payment | Bill Payment |
| fund_transfer | Fund Transfer |

At least one service must be selected before submission.

---

## API Dependencies

| Endpoint | Auth | Purpose |
|---|---|---|
| POST /obp/v5.1.0/banks/{bankId}/agents | DirectLogin token | Register the FO as an OBP agent |

Full request/response contract: see `API.md`.

---

## Design Tokens

| Token | Value | Usage |
|---|---|---|
| primary | #1800B1 | Title text, register button bg, chip selected bg, spinner |
| on_primary | #FFFFFF | Button label, chip selected text |
| input_border | #CCCCCC | All form field borders (idle state) |
| input_radius | 12dp | border_radius for all input fields |
| label_color | #444444 | All field labels |
| subtitle_color | #666666 | Subtitle, hint text |
| error_color | #B00020 | Inline validation errors, error icon |
| pending_bg | #FFF8E1 | Pending approval banner background |
| pending_border | #FFD54F | Pending banner border color |
| pending_text | #F57F17 | Pending icon + title color |
| pending_message | #795548 | Pending banner body text |
| confirmed_bg | #E8F5E9 | Confirmed banner background |
| confirmed_border | #A5D6A7 | Confirmed banner border color |
| confirmed_text | #2E7D32 | Confirmed banner title color |
| confirmed_message | #388E3C | Confirmed banner body text |
| confirmed_icon | #4CAF50 | Verified badge icon color |
| error_banner_bg | #FFEBEE | Global error banner background |
| error_banner_border | #EF9A9A | Global error banner border |
| prefix_bg | #F5F5F5 | Phone prefix box background |
| chip_unselected_bg | #EEF0FF | Unselected service chip background |
| chip_button_radius | 14dp | Corner radius for primary action buttons |

### Typography Scale

| Token | Usage |
|---|---|
| headline_large | Screen title (agent_reg_title) |
| label_large | Button labels (register_agent_button, go_to_dashboard_button) |
| label_medium | Field labels, section headings |
| body_medium | Input text, subtitle, loading label |
| body_small | Validation errors, terms notice, banner body text |

---

_Generated by /idea export | 2026-05-25_
