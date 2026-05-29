# API Reference — Agent Registration

| Field    | Value                                       |
|----------|---------------------------------------------|
| Feature  | agent-registration                          |
| Base URL | https://apisandbox.openbankproject.com      |

---

## POST /obp/v5.1.0/banks/{bankId}/agents

**Auth:** DirectLogin
**Tag:** Agent
**Trigger:** `submit_registration` action — fired when the field officer taps "Register as Agent" and client-side validation passes (`AgentRegistrationViewModel.onSubmitClicked()`)

Registers the currently authenticated field officer as an OBP bank agent for the given `bankId`. On success the response's `is_pending_agent` / `is_confirmed_agent` flags drive the state transition: `pending_approval` or `confirmed`. On 409 `AGENT_ALREADY_EXISTS`, `agent_number_error` is shown inline. All other 4xx/5xx errors transition to the `error` state with the global error banner.

### Path Parameters

| Name   | Type   | Value       | Description                                     |
|--------|--------|-------------|-------------------------------------------------|
| bankId | String | mifos-ke-001 | Mifos bank identifier — resolved from active session context |

### Request Body Fields

| Field               | Type            | Required | Example                                          | Notes                                                      |
|---------------------|-----------------|----------|--------------------------------------------------|------------------------------------------------------------|
| legal_name          | String          | Yes      | `"Priya Chakraborty"`                            | Full legal name as on government-issued ID or passport     |
| mobile_phone_number | String          | Yes      | `"+254712345678"`                                | `+254` prefix prepended to the 9-digit phone_number_input  |
| agent_number        | String          | Yes      | `"AGT-2026-00142"`                               | Unique identifier issued by Mifos admin; format AGT-YYYY-NNNNN |
| currency            | String (enum)   | Yes      | `"KES"`                                          | One of: `EUR`, `GBP`, `KES`, `USD`                        |
| supported_services  | List\<String\>  | Yes      | `["cash_deposit", "cash_withdrawal"]`            | At least one value required; see allowed values below      |
| commission_rate     | Number (Float)  | Yes      | `1.5`                                            | Range 0.5–5.0 inclusive; submitted as decimal float        |

**`supported_services` allowed values:** `cash_deposit`, `cash_withdrawal`, `account_opening`, `bill_payment`, `fund_transfer`

### Response Fields

| Field                | Type    | Description                                                              |
|----------------------|---------|--------------------------------------------------------------------------|
| agent_id             | String  | OBP-assigned unique agent identifier (e.g. `"agt-ke-2026-00142"`)        |
| is_pending_agent     | Boolean | `true` when registration submitted and awaiting bank approval            |
| is_confirmed_agent   | Boolean | `true` when agent is bank-confirmed and active                           |
| legal_name           | String  | Echo of submitted legal name                                             |
| mobile_phone_number  | String  | Echo of submitted mobile phone number (full E.164 format)                |

### State Transition on Response

| Response condition                  | ViewModel state transition       | UI outcome                                    |
|-------------------------------------|----------------------------------|-----------------------------------------------|
| `is_confirmed_agent = true`         | `uiState → Confirmed`            | Confirmed banner + "Go to Dashboard" CTA      |
| `is_pending_agent = true`           | `uiState → PendingApproval`      | Pending banner; form read-only                |
| HTTP 409 `AGENT_ALREADY_EXISTS`     | `validationErrors["agent_number"] = DUPLICATE_AGENT` | `agent_number_error` inline  |
| HTTP 400 `INVALID_PHONE_NUMBER`     | `validationErrors["phone_number"] = INVALID_FORMAT`  | `phone_error` inline         |
| HTTP 4xx / 5xx (other)              | `uiState → Error`                | Global error banner; form re-enabled          |

### Demo Data

**Request body (happy-path, KES agent):**

| Field               | Value                                               |
|---------------------|-----------------------------------------------------|
| legal_name          | `"Priya Chakraborty"`                               |
| mobile_phone_number | `"+254712345678"`                                   |
| agent_number        | `"AGT-2026-00142"`                                  |
| currency            | `"KES"`                                             |
| supported_services  | `["cash_deposit","cash_withdrawal","bill_payment","account_opening","fund_transfer"]` |
| commission_rate     | `1.5`                                               |

**Response body (pending approval):**

| Field               | Value                  |
|---------------------|------------------------|
| agent_id            | `"agt-ke-2026-00142"`  |
| is_pending_agent    | `true`                 |
| is_confirmed_agent  | `false`                |
| legal_name          | `"Priya Chakraborty"`  |
| mobile_phone_number | `"+254712345678"`      |

**Response body (already confirmed, second registration attempt):**

| Field               | Value                  |
|---------------------|------------------------|
| agent_id            | `"agt-ke-2026-00209"`  |
| is_pending_agent    | `false`                |
| is_confirmed_agent  | `true`                 |
| legal_name          | `"James Mwangi"`       |
| mobile_phone_number | `"+254734567890"`      |

### Error Codes

| Code | OBP Message               | UI Mapping                                                                     |
|------|---------------------------|--------------------------------------------------------------------------------|
| 400  | `INVALID_BANK_ID`         | Global error banner — "Registration failed. Please check your details and try again." |
| 400  | `INVALID_PHONE_NUMBER`    | `phone_error` inline — "Enter a valid 9-digit phone number"                    |
| 401  | `USER_NOT_LOGGED_IN`      | Global error banner; recommend redirecting to login screen                     |
| 403  | `INSUFFICIENT_AUTHORISATION` | Global error banner                                                         |
| 409  | `AGENT_ALREADY_EXISTS`    | `agent_number_error` inline — "An agent with this number already exists"       |
| 500  | OBP server error          | Global error banner — network/server error message                             |

---

_Generated by /idea export | 2026-05-30_
