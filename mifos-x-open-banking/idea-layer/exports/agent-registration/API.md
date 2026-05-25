# API Reference: Agent Registration

| Field | Value |
|---|---|
| Feature | agent-registration |
| Base URL | https://apisandbox.openbankproject.com |
| Auth | DirectLogin — `DirectLogin token="<token>"` header |
| OBP API Version | v5.1.0 |

---

## POST /obp/v5.1.0/banks/{bankId}/agents

Registers the authenticated user as a field agent for the specified bank. Called when the officer taps "Register as Agent" and all client-side validation passes.

On success, the response body determines which inline state the screen transitions to:
- `is_pending_agent: true` → transitions to `pending_approval` state
- `is_confirmed_agent: true` → transitions to `confirmed` state

### Path Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| bankId | String | Yes | OBP bank identifier (e.g. `mifos-nairobi`, `gh.29.uk`) |

### Headers

| Header | Value |
|---|---|
| Authorization | `DirectLogin token="<token>"` |
| Content-Type | `application/json` |

### Request Body

```json
{
  "legal_name": "Priya Chakraborty",
  "mobile_phone_number": "+254712345678",
  "agent_number": "AGT-2026-00142",
  "currency": "KES",
  "supported_services": ["cash_deposit", "cash_withdrawal", "account_opening"],
  "commission_rate": 1.5
}
```

| Field | Type | Required | Constraints | Example |
|---|---|---|---|---|
| legal_name | String | Yes | Non-empty; maps to ViewModel `legalName` | "Priya Chakraborty" |
| mobile_phone_number | String | Yes | Format: `+254XXXXXXXXX` (9-digit number with Kenya prefix) | "+254712345678" |
| agent_number | String | Yes | Format: `AGT-YYYY-NNNNN`; must be unique across OBP | "AGT-2026-00142" |
| currency | String | Yes | Enum: `EUR`, `GBP`, `KES`, `USD`; default UI selection: KES | "KES" |
| supported_services | List\<String\> | Yes | One or more of: `cash_deposit`, `cash_withdrawal`, `account_opening`, `bill_payment`, `fund_transfer` | ["cash_deposit", "fund_transfer"] |
| commission_rate | Number | Yes | Decimal; range 0.5–5.0 (inclusive) | 1.5 |

### Response Body (200 OK)

```json
{
  "agent_id": "obp-agent-42a8f3e2",
  "is_pending_agent": true,
  "is_confirmed_agent": false,
  "legal_name": "Priya Chakraborty",
  "mobile_phone_number": "+254712345678"
}
```

| Field | Type | Description |
|---|---|---|
| agent_id | String | Unique agent identifier assigned by OBP; stored in ViewModel `agentId` |
| is_pending_agent | Boolean | `true` when the bank requires manual approval; triggers `pending_approval` UI state |
| is_confirmed_agent | Boolean | `true` when the bank instantly approves; triggers `confirmed` UI state |
| legal_name | String | Echo of the submitted legal name |
| mobile_phone_number | String | Echo of the submitted mobile phone number |

### ViewModel Mapping (Response → State Fields)

| Response Field | ViewModel Field | Action |
|---|---|---|
| agent_id | agentId | Store on RegistrationSuccess |
| is_pending_agent | isPendingAgent | If true → uiState = PendingApproval |
| is_confirmed_agent | isConfirmedAgent | If true → uiState = Confirmed |

### Error Codes

| HTTP Status | OBP Error Code | Description | UI Handling |
|---|---|---|---|
| 400 | INVALID_BANK_ID | The `bankId` path parameter is not recognised by OBP | Show global error banner: "Invalid bank configuration. Contact support." |
| 400 | INVALID_PHONE_NUMBER | `mobile_phone_number` does not match expected E.164 format | Set `validationErrors["phone_number"] = INVALID_FORMAT`; show inline phone_error |
| 401 | USER_NOT_LOGGED_IN | DirectLogin token missing or expired | Redirect to login screen |
| 403 | INSUFFICIENT_AUTHORISATION | Authenticated user lacks OBP CanCreateAgent entitlement | Show global error banner: "You are not authorised to register as an agent." |
| 409 | AGENT_ALREADY_EXISTS | An agent record with this `agent_number` already exists in OBP | Set `validationErrors["agent_number"] = DUPLICATE_AGENT`; show inline agent_number_error |
| 500 | OBP_CONNECTOR_CANNOT_SAVE | OBP backend storage failure | Emit RegistrationFailed; show global error banner: "Registration failed. Please try again." |

### Client-Side Validation (Pre-Request)

Run before the OBP call; populates `validationErrors` map to trigger `validation_error` UI state.

| Field | Rule | Error Code |
|---|---|---|
| legal_name | Non-empty string | REQUIRED |
| mobile_phone_number | Matches regex `^\d{9}$` (9 digits) | INVALID_FORMAT |
| agent_number | Non-empty string | REQUIRED |
| currency | Must be one of: EUR, GBP, KES, USD | REQUIRED |
| supported_services | List must have ≥ 1 item | REQUIRED |
| commission_rate | Parseable decimal; value ∈ [0.5, 5.0] | REQUIRED / INVALID_FORMAT |

---

## GET /obp/v5.1.0/banks/{bankId}/agents/me _(Pre-flight status check)_

Called automatically on screen entry (loading state) to detect an existing agent record for the authenticated user before rendering the registration form.

### Path Parameters

| Parameter | Type | Description |
|---|---|---|
| bankId | String | OBP bank identifier bound from session |

### Response (200 OK — agent record exists)

```json
{
  "agent_id": "obp-agent-42a8f3e2",
  "is_pending_agent": true,
  "is_confirmed_agent": false
}
```

### ViewModel Mapping

| is_pending_agent | is_confirmed_agent | uiState transition |
|---|---|---|
| true | false | PendingApproval (shows read-only form + amber banner) |
| false | true | Confirmed (shows confirmed banner + Go to Dashboard CTA) |
| false | false | Idle (shows empty registration form) |

### Pre-flight Error Handling

| Error | Behaviour |
|---|---|
| 404 (no existing record) | Emit StatusCheckSuccess(isPending=false, isConfirmed=false) → render Idle state |
| 401 USER_NOT_LOGGED_IN | Redirect to login |
| Any 5xx | Emit StatusCheckFailed; log silently; render Idle state (fail-open to allow registration attempt) |

---

_Generated by /idea export | 2026-05-25_
