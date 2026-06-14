# SPEC — Completing Connection (Auth Callback)

| Field         | Value                      |
|---------------|----------------------------|
| Feature       | auth-callback              |
| Flavor        | consumer                   |
| Status        | enriched                   |
| Quality Score | 96                         |
| ViewModel     | AuthCallbackViewModel      |

---

## Overview

The Completing Connection screen is a headless full-screen takeover that handles the OBIE OAuth2 deep-link return for both the AIS account-access-consent flow and the PISP payment-initiation flow. It is entered automatically when HSBC redirects back to the app via `org.mifos.openbanking://oauth/callback` after the PSU has authenticated and completed SCA. There is no Top App Bar, no bottom navigation bar, and no credential-entry UI — all authentication happened at HSBC.

The screen operates in two sequential processing phases driven by a `CallbackPhase` enum. In the `exchanging` phase the ViewModel verifies the CSRF `state` parameter against the stored value, then POSTs to the HSBC token endpoint (`POST /oauth2/token`) using the PKCE `code_verifier` and a PS256 `client_assertion` JWT over mTLS to exchange the short-lived authorization code for a PSU-bound access token and refresh token. The screen shows the headline "Finishing secure connection…" with a 32dp spinner and the reassurance caption "Verifying your authorisation · Encrypted connection".

Once the token exchange succeeds the screen transitions to the `verifying` phase, where behaviour branches on the `consentContext` enum carried from `bank-authorize-handoff` via `OidcCallbackBus`. For the AIS context the ViewModel polls `GET /aisp/account-access-consents/{ConsentId}` until the consent reaches Status `AUTH`, then navigates to `home` (replace). For the PAYMENT context the ViewModel submits `POST /pisp/domestic-payments` using the PSU Bearer token and polls the returned `DomesticPaymentId` to a terminal status, then navigates to `payment-result` (replace). The heading updates to "Confirming your approval…" (AIS) or "Finalising your payment…" (PAYMENT) while verifying.

If any step fails — callback carries an `error` param, CSRF state mismatches, PSU declined SCA, token exchange returns `invalid_grant`, or the consent never reaches AUTH — the screen transitions to the `error` state. A `#FFDAD6` error card appears with a brief message, a full-width "Try again" filled button (restarts at `bank-authorize-handoff`), and a "Cancel" text link (routes to `consent-declined` for AIS or `payment-declined` for PAYMENT, resolved by `consentContext`).

---

## Screens

| ID             | Name                  | Route              | Layout | Scroll |
|----------------|-----------------------|--------------------|--------|--------|
| auth-callback  | Completing Connection | (deep-link target) | Column | None   |

**Shell:** No Top App Bar. No bottom navigation bar. Full-screen `#F9FAEF` background. Column layout centred horizontally and vertically.

---

## Components

| ID                     | Type              | Description                                                                                                                          |
|------------------------|-------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| callback_root          | stack (column)    | Root container — `#F9FAEF` background, spacing.lg padding, align + justify center; a11y region "Completing your secure connection with HSBC" |
| callback_bank_icon     | icon              | `verified_user` (shield) icon — 80dp, `#4C662B`, centre-aligned; a11y role=image "Secure connection with HSBC"                     |
| callback_title         | text              | Phase-driven headline — exchanging: "Finishing secure connection…"; verifying (AIS): "Confirming your approval…"; verifying (PAYMENT): "Finalising your payment…"; error: same as most-recent phase — Outfit/headline_small, `#1A1C16`, centre, spacing.lg top padding |
| callback_message       | text              | Phase-driven supporting copy — exchanging: "Securely finishing your authorisation with HSBC. This only takes a moment."; verifying (AIS): "Checking your account-sharing approval went through."; verifying (PAYMENT): "Submitting your payment to HSBC and confirming it was accepted." — Outfit/body_medium, `#44483D`, centre, spacing.sm top |
| callback_spinner       | loading_indicator | Circular indeterminate — 32dp, `#4C662B`, centre; visible in exchanging + verifying states; spacing.lg top padding               |
| callback_security_note | text              | "Verifying your authorisation · Encrypted connection" — Outfit/body_small, `#74796D`, centre, spacing.md top; visible in exchanging + verifying |
| callback_error_card    | card (filled)     | `#FFDAD6` fill, 8dp radius, spacing.md padding, spacing.lg top margin; a11y role=alert "Authorisation could not be completed"; visible in error state |
| callback_error_icon    | icon              | `error` icon — 20dp, `#BA1A1A`; inside error card                                                                                  |
| callback_error_message | text              | Context-keyed error copy — AIS: "We couldn't complete your authorisation with HSBC. You can try again."; PAYMENT: "Your payment authorisation was declined. You can try again." — Outfit/body_small, `#410002`, spacing.sm start; inside error card |
| callback_retry_button  | button (filled)   | "Try again" — `#4C662B` fill, `#FFFFFF` text, Outfit/label_large, 8dp radius, spacing.md padding, spacing.lg top margin, match_parent; visible in error state; navigates to bank-authorize-handoff |
| callback_cancel_link   | button (text)     | "Cancel" — `#386663` text, Outfit/label_large, centre, min_height 44dp; visible in error state; routes to consent-declined (AIS) or payment-declined (PAYMENT) via consentContext |

---

## States

| ID         | Trigger                                                             | Description                                                                                                                      |
|------------|---------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------|
| exchanging | Deep-link received — `DeepLinkReceived(code, state, error?)`       | Phase 1: CSRF verify + POST /oauth2/token. Heading "Finishing secure connection…". Spinner + security note. No buttons. On success → verifying. On error → error. |
| loading    | Canonical alias for exchanging                                      | Identical composition to exchanging — satisfies the loading/content/error contract; runtime drives exchanging → verifying         |
| verifying  | `TokenExchanged(accessToken)` — post-exchange phase                 | Phase 2 branched on consentContext: AIS polls consent AUTH → home; PAYMENT submits domestic-payment → payment-result. Heading updates per branch. Same spinner + security note. |
| error      | Callback error param / CSRF mismatch / invalid_grant / AUTH timeout | Error card `#FFDAD6` + error icon + context-keyed copy. "Try again" button (restarts handoff) + "Cancel" link (consent-declined / payment-declined). Spinner hidden. |

---

## State Model

**ViewModel:** `AuthCallbackViewModel`
**Screen State Type:** `AuthCallbackUiState`

| Name           | Type            | Default                    |
|----------------|-----------------|----------------------------|
| phase          | CallbackPhase   | CallbackPhase.EXCHANGING   |
| consentContext | ConsentContext  | ConsentContext.AIS         |
| consentId      | String?         | null                       |
| errorMessage   | String?         | null                       |
| isError        | Boolean         | false                      |

**Events:**
- `AuthCallbackEvent.NavigateToHome`
- `AuthCallbackEvent.NavigateToPaymentResult(domesticPaymentId: String)`
- `AuthCallbackEvent.NavigateToConsentDeclined`
- `AuthCallbackEvent.NavigateToPaymentDeclined`
- `AuthCallbackEvent.RestartHandoff`

**Actions:**
- `AuthCallbackAction.DeepLinkReceived(code: String, state: String, error: String?)`
- `AuthCallbackAction.RetryClicked`
- `AuthCallbackAction.CancelClicked`
- `AuthCallbackAction.Internal.TokenExchanged(accessToken: String)`
- `AuthCallbackAction.Internal.ConsentAuthorised(consentId: String)`
- `AuthCallbackAction.Internal.PaymentSubmitted(domesticPaymentId: String)`
- `AuthCallbackAction.Internal.ExchangeFailed(error)`

**DI Dependencies:** `ObpAuthRepository`, `OidcCallbackBus`

**Errors:** `INVALID_GRANT`, `INVALID_CLIENT`, `STATE_MISMATCH`, `CONSENT_NOT_AUTHORISED`, `CONSENT_REJECTED`, `REQUEST_TIMEOUT`, `TOO_MANY_REQUESTS`, `UNKNOWN`

---

## Navigation

| From           | Action                     | To                | Type    | Description                                                                         |
|----------------|----------------------------|-------------------|---------|-------------------------------------------------------------------------------------|
| auth-callback  | ais_consent_authorised     | home              | replace | AIS success — consent reached AUTH; replace back-stack entry, enter app              |
| auth-callback  | payment_submitted          | payment-result    | replace | PAYMENT success — domestic-payment polled to terminal; navigate to result screen     |
| auth-callback  | ais_callback_error         | consent-declined  | replace | AIS failure — auto-routed when unrecoverable; also destination for Cancel (AIS)     |
| auth-callback  | payment_callback_error     | payment-declined  | replace | PAYMENT failure — auto-routed; also destination for Cancel (PAYMENT)                |
| auth-callback  | retry_clicked              | bank-authorize-handoff | push | Error-state retry — restarts handoff preserving consentContext                    |

---

## API Endpoints

| Endpoint                                                                                         | Auth                    | Tag            | Purpose                                                            |
|--------------------------------------------------------------------------------------------------|-------------------------|----------------|--------------------------------------------------------------------|
| POST https://secure.sandbox.ob.hsbc.co.uk/obie/open-banking/v1.1/oauth2/token                   | mTLS + client_assertion | Authentication | Exchange authorization code for PSU-bound access + refresh tokens |
| GET https://secure.sandbox.ob.hsbc.co.uk/obie/open-banking/v4.0/aisp/account-access-consents/{ConsentId} | Bearer (PSU)    | Authentication | AIS only — poll consent until Status AUTH before entering app      |
| POST https://secure.sandbox.ob.hsbc.co.uk/obie/open-banking/v4.0/pisp/domestic-payments         | Bearer (PSU) + JWS      | Authentication | PAYMENT only — submit authorised domestic-payment, poll terminal   |

---

## Design Tokens

| Token                           | Value           | Usage                                                                                  |
|---------------------------------|-----------------|----------------------------------------------------------------------------------------|
| colors.light.primary            | #4C662B         | `verified_user` icon tint; spinner colour; "Try again" filled button fill              |
| colors.light.on_primary         | #FFFFFF         | "Try again" button text                                                                |
| colors.light.background         | #F9FAEF         | Full-screen background                                                                 |
| colors.light.on_surface         | #1A1C16         | Phase-driven headline text                                                             |
| colors.light.on_surface_variant | #44483D         | Phase-driven supporting copy                                                           |
| colors.light.outline_variant    | #74796D         | Security note caption ("Verifying your authorisation · Encrypted connection")          |
| colors.light.secondary          | #386663         | "Cancel" text button colour                                                            |
| colors.light.error              | #BA1A1A         | Error icon tint inside error card                                                      |
| colors.light.error_container    | #FFDAD6         | Error card background                                                                  |
| colors.light.on_error_container | #410002         | Error message text inside error card                                                   |
| typography.headline_small       | Outfit 24sp/400 | Phase-driven headline                                                                  |
| typography.body_medium          | Outfit 14sp/400 | Phase-driven supporting copy                                                           |
| typography.body_small           | Outfit 12sp/400 | Security note; error message inside card                                               |
| typography.label_large          | Outfit 14sp/500 | "Try again" and "Cancel" button labels                                                 |
| radius.md                       | 8dp             | Error card corners; "Try again" button corners                                         |

---

_Generated by /idea export | 2026-06-14_
