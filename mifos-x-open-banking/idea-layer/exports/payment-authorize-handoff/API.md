# API Reference — Securing Payment (Payment Authorise Handoff)

| Field    | Value                                             |
|----------|---------------------------------------------------|
| Feature  | payment-authorize-handoff                         |
| Base URL | https://sandbox.ob.hsbc.co.uk/obie/open-banking   |

---

## POST /obie/open-banking/v4.0/pisp/domestic-payment-consents

**Auth:** Client Credentials (OAuth2 — not a user token)
**Tag:** PISP
**Trigger:** `on_handoff_mount` — called immediately when `PaymentAuthorizeHandoffViewModel` mounts; the result ConsentId becomes the `openbanking_intent_id` in the authorise request object

Stages the domestic-payment-consent ahead of the HSBC authorise redirect. The ASPSP creates the consent with Status AWAU (awaiting PSU authorisation) and returns the ConsentId. The Initiation block in this request MUST byte-match the later `POST /domestic-payments` submission (after the PSU authorises at HSBC). The CE HSBCnet equivalent is `POST /ce/obie/open-banking/v3.1/pisp/domestic-payment-consents`.

### Request Fields

| Field                                          | Type   | Required | Example                      | Description                                              |
|------------------------------------------------|--------|----------|------------------------------|----------------------------------------------------------|
| Data.Initiation.InstructionIdentification      | String | Yes      | —                            | Unique instruction reference (client-generated)          |
| Data.Initiation.InstructedAmount.Amount        | String | Yes      | `"250.00"`                   | Payment amount                                           |
| Data.Initiation.InstructedAmount.Currency      | String | Yes      | `"GBP"`                      | ISO 4217 currency code                                   |
| Data.Initiation.CreditorAccount.SchemeName     | String | Yes      | `"UK.OBIE.SortCodeAccountNumber"` | Creditor account scheme                             |
| Data.Initiation.CreditorAccount.Identification | String | Yes      | —                            | Creditor sort code + account number                      |
| Data.Initiation.CreditorAccount.Name          | String | Yes      | `"Jordan Avery"`             | Payee display name                                       |
| Data.Initiation.RemittanceInformation.Reference| String | No       | —                            | Payment reference visible on the payee's statement       |
| Risk.PaymentContextCode                        | String | Yes      | `"TransferToThirdParty"`     | OBIE payment risk context                                |

### Response Fields

| Field                  | Type   | Stored As           | Example                                  | Description                                |
|------------------------|--------|---------------------|------------------------------------------|--------------------------------------------|
| Data.ConsentId         | String | payment_consent_id  | `pdc-7a31f9c2-4b8e-4d1a-9f63-1c0ab2d4e5f6` | Unique consent ID — becomes the intent_id |
| Data.Status            | String | —                   | `AWAU`                                   | Initial status: Awaiting PSU Authorisation |
| Data.CreationDateTime  | String | —                   | `2026-06-14T10:30:00Z`                   | ISO 8601 UTC creation timestamp            |

### Demo Data

| Field         | Demo Value                                   |
|---------------|----------------------------------------------|
| Data.ConsentId| pdc-7a31f9c2-4b8e-4d1a-9f63-1c0ab2d4e5f6    |
| Data.Status   | AWAU                                         |
| Amount        | 250.00 GBP                                   |
| Payee         | Jordan Avery                                 |

### Error Codes

| Code | OBIE Error Name                    | UI Message                                                                                                               |
|------|------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| 400  | OB.Field.Invalid                   | We couldn't reach HSBC to authorise your payment. No money has left your account. Please check your connection and try again. |
| 401  | UNAUTHORIZED                       | We couldn't authorise this payment session. Please sign in again and retry.                                               |
| 403  | OB.Resource.InvalidConsentStatus   | This payment can't be authorised right now. Please go back and start the payment again.                                   |
| 429  | TOO_MANY_REQUESTS                  | HSBC is busy right now. Please wait a moment and try again.                                                              |
| 500  | OB.Unexpected.Error                | Something went wrong authorising your payment. No money has left your account. Please try again.                          |

---

## GET https://sandbox.ob.hsbc.co.uk/oauth2/authorize

**Auth:** PKCE Authorization Code with signed Request Object (PS256)
**Tag:** Authorization
**Trigger:** `on_consent_created` — built after Data.ConsentId is received; launched via system browser / Custom Tab (auto) or the "Continue to HSBC" button (manual fallback)

This is an **external redirect** — the app constructs the URL and launches it in the system browser or Android Custom Tab. The PSU authenticates and completes SCA at HSBC; no credentials or SCA codes are entered in the app. On success HSBC redirects to the registered deep-link with `code` + `id_token` + `state`. On PSU decline or consent RJCT it returns an `error` param. The deep-link `org.mifos.openbanking://oauth/callback` is handled by `auth-callback`, which exchanges the token and drives navigation to the payment result.

### Query Parameters

| Parameter             | Example / Value                  | Description                                                        |
|-----------------------|----------------------------------|--------------------------------------------------------------------|
| response_type         | `"code id_token"`                | Authorization code + identity token hybrid flow                    |
| client_id             | `{hsbc_client_id}`               | OBIE-registered client ID for the app                              |
| redirect_uri          | `org.mifos.openbanking://oauth/callback` | Registered deep-link redirect URI                          |
| scope                 | `"openid payments"`              | Consent scope — payments scope identifies PISP intent              |
| state                 | `{csrf_state}`                   | Opaque CSRF state value; validated on callback                     |
| nonce                 | `{oidc_nonce}`                   | OIDC nonce; validated in id_token                                  |
| request               | `{signed_request_object_jwt}`    | PS256-signed JWT carrying openbanking_intent_id = ConsentId        |
| code_challenge        | `{pkce_code_challenge}`          | S256 PKCE challenge                                                |
| code_challenge_method | `"S256"`                         | PKCE method                                                        |

### Callback (Redirect) Parameters — Success

| Parameter | Type   | Description                                                            |
|-----------|--------|------------------------------------------------------------------------|
| code      | String | Authorization code; exchanged for tokens in auth-callback              |
| id_token  | String | OIDC identity token; validated by auth-callback before token exchange  |
| state     | String | Must match the value sent in the request; CSRF validation              |

### Callback (Redirect) Parameters — Decline / Error

| Parameter | Type   | Description                                                                                     |
|-----------|--------|-------------------------------------------------------------------------------------------------|
| error     | String | Present when the PSU declines or the consent is RJCT at the bank. Drives navigation to payment-declined via auth-callback. |

### Error Codes

| Code | OBIE Error Name  | UI Message                                                                                 |
|------|------------------|--------------------------------------------------------------------------------------------|
| 302  | PSU_DECLINED     | You didn't approve this payment at HSBC. No money has left your account.                   |
| 400  | OB.Field.Invalid | Something went wrong preparing your payment authorisation. Please try again.               |

---

_Generated by /idea export | 2026-06-14_
