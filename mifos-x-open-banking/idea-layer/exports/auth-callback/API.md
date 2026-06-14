# API Reference — Completing Connection (Auth Callback)

| Field    | Value                                                          |
|----------|----------------------------------------------------------------|
| Feature  | auth-callback                                                  |
| Base URL | https://secure.sandbox.ob.hsbc.co.uk/obie/open-banking        |

---

## POST /v1.1/oauth2/token

**Auth:** mTLS + PS256 `client_assertion` JWT (private_key_jwt)
**Tag:** Authentication
**Trigger:** `on_deep_link_received` — fires immediately when the deep-link `org.mifos.openbanking://oauth/callback` is received with a `code` parameter

Exchanges the short-lived authorization code returned by the HSBC authorise redirect for a PSU-bound access token and refresh token (grant_type=authorization_code). The request is form-encoded over mTLS; the client authenticates with a PS256-signed `client_assertion` JWT. The `code_verifier` from the PKCE challenge generated at `bank-authorize-handoff` is included to complete the S256 proof. The ViewModel first verifies the returned `state` parameter matches the stored CSRF value before dispatching this call — a mismatch immediately routes to the `error` state.

This endpoint is shared by both the AIS account-access-consent flow and the PISP payment-consent flow. The `scope` field in the response echoes the original consent scope (`accounts` for AIS, `payments` for PAYMENT), allowing the ViewModel to cross-check the `consentContext`.

### Request Fields (application/x-www-form-urlencoded)

| Field                 | Type   | Value / Source                                               |
|-----------------------|--------|--------------------------------------------------------------|
| grant_type            | String | `authorization_code`                                         |
| code                  | String | Authorization code from deep-link query parameter            |
| redirect_uri          | String | `org.mifos.openbanking://oauth/callback`                     |
| code_verifier         | String | PKCE code verifier stored by `ObpAuthRepository` at handoff  |
| client_assertion_type | String | `urn:ietf:params:oauth:client-assertion-type:jwt-bearer`     |
| client_assertion      | String | PS256-signed JWT (private_key_jwt method) per FAPI spec      |

### Response Fields

| Field         | Type   | Stored As        | Description                                                               |
|---------------|--------|------------------|---------------------------------------------------------------------------|
| access_token  | String | psu_access_token | PSU-bound Bearer token — used for all subsequent resource calls           |
| refresh_token | String | refresh_token    | Long-lived refresh token for silent renewal                               |
| id_token      | String | —                | JWT carrying PSU/consent binding + `refresh_token_expires_at` claim       |
| token_type    | String | —                | Always `Bearer`                                                           |
| expires_in    | Int    | —                | Access token lifetime in seconds (e.g. `3600`)                            |
| scope         | String | —                | Echoes consent scope: `accounts` (AIS) \| `payments` (PAYMENT)           |

### Demo Data

| Field         | Example Value                                        |
|---------------|------------------------------------------------------|
| access_token  | eyJhbGciOiJQUzI1NiIsImtpZCI6IjFMVGl5...             |
| token_type    | Bearer                                               |
| expires_in    | 3600                                                 |
| scope         | accounts                                             |
| id_token      | eyJhbGciOiJQUzI1NiIsImtpZCI6IkhTQkNT...             |

### Error Codes

| Code | Name              | UI Behaviour                                                                           |
|------|-------------------|----------------------------------------------------------------------------------------|
| 400  | INVALID_GRANT     | `error` state — "We couldn't complete your authorisation with HSBC. You can try again." |
| 401  | INVALID_CLIENT    | `error` state — "Your authorisation could not be verified. Please try again."           |
| 429  | TOO_MANY_REQUESTS | `error` state — "Too many attempts. Please wait a moment and try again."               |
| 500  | SERVER_ERROR      | `error` state — "Something went wrong on HSBC's end. Please try again in a moment."   |

---

## GET /v4.0/aisp/account-access-consents/{ConsentId}

**Auth:** Bearer (PSU access token)
**Tag:** Authentication
**Trigger:** `after_token_exchange_ais` — AIS context only, after the access token is obtained

Polls the account-access-consent until its `Status` field is `Authorised` (AUTH), confirming that the PSU's SCA at HSBC was accepted and the consent is now active. The ViewModel polls this endpoint with exponential back-off; on AUTH it emits `NavigateToHome` (replace). Not called in the PAYMENT context.

### Path Parameters

| Name      | Type   | Source      | Description                                     |
|-----------|--------|-------------|-------------------------------------------------|
| ConsentId | String | OidcCallbackBus | ConsentId bound into the original authorise request |

### Request Headers

| Header                | Value                     | Notes                          |
|-----------------------|---------------------------|--------------------------------|
| Authorization         | Bearer {psu_access_token} | Token obtained from /oauth2/token above |
| x-fapi-financial-id   | {hsbc_financial_id}       | HSBC ASPSP financial ID        |

### Response Fields

| Field     | Type   | Description                                                   |
|-----------|--------|---------------------------------------------------------------|
| ConsentId | String | Echo of the path ConsentId                                    |
| Status    | String | Consent status — polls until `Authorised`                     |

### Demo Data

| ConsentId                              | Status      |
|----------------------------------------|-------------|
| urn:alphabank:intent:a1b2c3d4-5678     | Authorised  |

### Error Codes

| Code | Name                  | UI Behaviour                                                                              |
|------|-----------------------|-------------------------------------------------------------------------------------------|
| 400  | CONSENT_NOT_AUTHORISED | `error` state — "We couldn't complete your authorisation with HSBC. You can try again."  |
| 401  | UNAUTHORIZED           | `error` state — "Your authorisation could not be verified. Please try again."            |

---

## POST /v4.0/pisp/domestic-payments

**Auth:** Bearer (PSU access token) + `x-jws-signature` (detached JWS) + `x-idempotency-key`
**Tag:** Authentication
**Trigger:** `after_token_exchange_payment` — PAYMENT context only, after the access token is obtained

Submits the authorised domestic-payment using the PSU-bound access token. The request body (ConsentId + Risk + Initiation block) must byte-match the authorised payment-consent; it is signed with a detached JWS (`x-jws-signature`). The returned `DomesticPaymentId` is polled to a terminal status (`AcceptedSettlementCompleted` or rejected) before the ViewModel emits `NavigateToPaymentResult`. Not called in the AIS context.

### Request Headers

| Header             | Value                     | Notes                                       |
|--------------------|---------------------------|---------------------------------------------|
| Authorization      | Bearer {psu_access_token} | PSU-bound token from /oauth2/token          |
| x-jws-signature    | {detached_jws}            | Detached JWS over the request body (PS256)  |
| x-idempotency-key  | {idempotency_key}         | Per-submission UUID for safe retry          |
| Content-Type       | application/json          |                                             |

### Response Fields

| Field             | Type   | Stored As          | Description                                              |
|-------------------|--------|--------------------|----------------------------------------------------------|
| DomesticPaymentId | String | domestic_payment_id | ID polled to confirm terminal payment status            |
| Status            | String | —                  | Initial: `AcceptedSettlementInProcess`; polls to terminal|

### Demo Data

| DomesticPaymentId                    | Status                         |
|--------------------------------------|--------------------------------|
| DP-2026-06-14-HSBC-00000123          | AcceptedSettlementInProcess    |

### Error Codes

| Code | Name             | UI Behaviour                                                                  |
|------|------------------|-------------------------------------------------------------------------------|
| 400  | OB_FIELD_INVALID | `error` state — "We couldn't submit your payment. Please try again."          |
| 403  | CONSENT_REJECTED | `error` state — "Your payment authorisation was declined. Please try again." |

---

_Generated by /idea export | 2026-06-14_
