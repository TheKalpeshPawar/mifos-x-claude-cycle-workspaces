# API Reference — Redirecting to HSBC (Bank Authorize Handoff)

| Field    | Value                                                          |
|----------|----------------------------------------------------------------|
| Feature  | bank-authorize-handoff                                         |
| Base URL | https://secure.sandbox.ob.hsbc.co.uk/obie/open-banking        |

---

## POST /v1.1/oauth2/token (client_credentials)

**Auth:** mTLS + PS256 `client_assertion` JWT (private_key_jwt)
**Tag:** Authentication
**Trigger:** `before_consent_staging` — first call on screen entry, before staging the account-access-consent

Obtains a TPP-only client-credentials access token (grant_type=client_credentials) used to stage the consent at the HSBC ASPSP. This token is NOT a PSU-bound token — it authenticates the TPP app against the HSBC API, not the user. It is used exclusively to POST the account-access-consent object (or payment-consent object) which returns the ConsentId embedded in the authorise request object. Form-encoded; client authentication via PS256 private_key_jwt over mTLS.

### Request Fields (application/x-www-form-urlencoded)

| Field                 | Type   | Value / Source                                          |
|-----------------------|--------|---------------------------------------------------------|
| grant_type            | String | `client_credentials`                                    |
| scope                 | String | `accounts` (AIS) \| `payments` (PAYMENT)               |
| client_assertion_type | String | `urn:ietf:params:oauth:client-assertion-type:jwt-bearer`|
| client_assertion      | String | PS256-signed JWT (private_key_jwt method per FAPI spec) |

### Response Fields

| Field        | Type   | Stored As      | Description                                                  |
|--------------|--------|----------------|--------------------------------------------------------------|
| access_token | String | cc_access_token | Client-credentials token used to stage the consent          |
| token_type   | String | —              | Always `Bearer`                                              |
| expires_in   | Int    | —              | Token lifetime in seconds                                    |

### Demo Data

| Field        | Example Value                         |
|--------------|---------------------------------------|
| access_token | eyJhbGciOiJQUzI1NiIsImtpZCI6InRwcC...  |
| token_type   | Bearer                                |
| expires_in   | 3600                                  |

### Error Codes

| Code | Name            | UI Behaviour                                                                              |
|------|-----------------|-------------------------------------------------------------------------------------------|
| 400  | INVALID_REQUEST | `error` state — "Something went wrong preparing your secure sign-in. Please try again."   |
| 401  | INVALID_CLIENT  | `error` state — "Your session could not be verified. Please try again."                  |

---

## POST /v4.0/aisp/account-access-consents

**Auth:** Bearer (cc_access_token from client_credentials call above)
**Tag:** Authentication
**Trigger:** `on_handoff_entered_ais` — AIS context only, after obtaining the client-credentials token

Stages the AIS account-access-consent object at HSBC with Status `AwaitingAuthorisation`. The returned `ConsentId` becomes the `openbanking_intent_id` embedded in the signed authorise request object JWT. This call is AIS-specific — the PAYMENT flow uses a parallel domestic-payment-consent staging call (not listed here as it belongs to the payment-initiation feature boundary).

### Request Headers

| Header               | Value                   | Notes                              |
|----------------------|-------------------------|------------------------------------|
| Authorization        | Bearer {cc_access_token}| Client-credentials token           |
| x-fapi-financial-id  | {hsbc_financial_id}     | HSBC ASPSP financial ID            |
| Content-Type         | application/json        |                                    |

### Response Fields

| Field     | Type   | Stored As  | Description                                                    |
|-----------|--------|------------|----------------------------------------------------------------|
| ConsentId | String | consent_id | Becomes the `openbanking_intent_id` in the signed request JWT  |
| Status    | String | —          | `AwaitingAuthorisation` — expected for a freshly staged consent|

### Demo Data

| ConsentId                          | Status                  |
|------------------------------------|-------------------------|
| urn:alphabank:intent:a1b2c3d4-5678 | AwaitingAuthorisation   |

### Error Codes

| Code | Name           | UI Behaviour                                                                              |
|------|----------------|-------------------------------------------------------------------------------------------|
| 400  | OB_FIELD_INVALID | `error` state — "Something went wrong preparing your secure sign-in. Please try again." |
| 401  | UNAUTHORIZED   | `error` state — "Your session could not be verified. Please try again."                  |

---

## GET https://sandbox.ob.hsbc.co.uk/obie/open-banking/v1.1/oauth2/authorize

**Auth:** None (external browser request — PSU authenticates at HSBC)
**Tag:** Authentication
**Trigger:** `on_handoff_entered` — opened in system browser / Custom Tab after the authorise request object is built

This is not a REST call this screen consumes — it is the external HSBC authorise URL that the screen **constructs** and launches in the system browser or Custom Tab. The screen builds a signed request-object JWT embedding `openbanking_intent_id = ConsentId`, `response_type = code id_token`, and the PKCE `code_challenge + code_challenge_method S256`, using the per-brand authorize host (`sandbox.ob.hsbc.co.uk`, not `secure.sandbox.*`). The PSU enters their HSBC credentials and completes SCA entirely within the bank's pages. On completion HSBC redirects to `redirect_uri` with `code + id_token + state`; this deep-link is handled by `auth-callback`.

### Query Parameters Constructed by the App

| Parameter             | Type   | Value / Source                                                          |
|-----------------------|--------|-------------------------------------------------------------------------|
| response_type         | String | `code id_token`                                                         |
| client_id             | String | `{hsbc_client_id}` — registered HSBC client ID                         |
| redirect_uri          | String | `org.mifos.openbanking://oauth/callback`                                |
| scope                 | String | `openid accounts` (AIS)                                                 |
| state                 | String | `{csrf_state}` — random CSRF token stored in ObpAuthRepository          |
| nonce                 | String | `{oidc_nonce}` — random nonce for OIDC reply-protection                 |
| request               | String | Signed request-object JWT (PS256) embedding intent_id + PKCE challenge  |
| code_challenge        | String | PKCE S256 code challenge derived from code_verifier                     |
| code_challenge_method | String | `S256`                                                                  |

### Redirect Response Parameters (returned to deep-link)

| Name     | Type   | Description                                                                     |
|----------|--------|---------------------------------------------------------------------------------|
| code     | String | Authorization code (~30s lifetime) — exchanged at auth-callback POST /oauth2/token |
| id_token | String | Hybrid-flow ID token — carries PSU/consent binding + `refresh_token_expires_at`|
| state    | String | Echo of the request state — verified against csrf_state by auth-callback        |

### Error Codes

| Code | Name                 | UI Behaviour                                                                               |
|------|----------------------|--------------------------------------------------------------------------------------------|
| 302  | AUTHORIZATION_FAILED | App receives `error` param on redirect_uri → auth-callback routes to error / consent-declined |
| 400  | OB_FIELD_INVALID     | `error` state on this screen — "Something went wrong preparing your secure sign-in. Please try again." |
| 401  | UNAUTHORIZED         | `error` state — "Your session could not be verified. Please try again."                    |

---

_Generated by /idea export | 2026-06-14_
