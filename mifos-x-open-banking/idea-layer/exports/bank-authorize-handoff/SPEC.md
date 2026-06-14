# SPEC — Redirecting to HSBC (Bank Authorize Handoff)

| Field         | Value                            |
|---------------|----------------------------------|
| Feature       | bank-authorize-handoff           |
| Flavor        | consumer                         |
| Status        | enriched                         |
| Quality Score | 94                               |
| ViewModel     | BankAuthorizeHandoffViewModel    |

---

## Overview

The Redirecting to HSBC screen is a transitional full-screen takeover that manages the OBIE FAPI Hybrid Flow authorise redirect for both the AIS account-access-consent and PISP payment-consent journeys. It is entered from `consent-request` (AIS) or `send-money-confirm` (PAYMENT) after the user has reviewed the consent details and tapped Grant/Confirm. There is no Top App Bar, no bottom navigation bar, and no credential-entry UI — the PSU's username, password, and SCA codes are entered exclusively at HSBC, never in this app.

The screen operates in two sequential phases. In the `preparing` phase the `BankAuthorizeHandoffViewModel` asks `ObpAuthRepository` to stage the consent by calling the OBIE server-side staging endpoint (POST /aisp/account-access-consents for AIS, or the equivalent payment consent endpoint for PAYMENT, using a client-credentials Bearer token obtained from POST /oauth2/token). It then generates a PKCE code_verifier + S256 code_challenge, builds a signed authorise request-object JWT embedding the `openbanking_intent_id` (= ConsentId), and stores the CSRF `state` value. During this phase the screen shows the heading "Getting ready to connect securely" with an indeterminate 32dp spinner and the message body explaining that sign-in happens at HSBC, not in the app.

Once the authorise URL is ready the screen transitions to the `redirecting` phase. The ViewModel emits a `LaunchAuthorize(authorizeUrl)` one-shot event and the host opens the URL in the system browser or Custom Tab (auto-launch). The heading updates to "Taking you to HSBC to sign in and approve" and the spinner is replaced by the "Continue to HSBC" filled button — a manual-launch fallback for cases where the auto-launch is blocked or the Custom Tab was dismissed. Tapping "Continue to HSBC" re-opens the same external URL. The external redirect leaves the app; the PSU authenticates and completes SCA at HSBC, then HSBC redirects back via the deep-link `org.mifos.openbanking://oauth/callback` which is received by `auth-callback`.

If consent staging or signed-request building fails — network error, 400 OB.Field.Invalid, request-object signing error, or no available browser — the screen transitions to the `error` state. A `#FFDAD6` error card appears with the message "We couldn't start your secure sign-in with HSBC. Please check your connection and try again." A full-width "Try again" button returns the screen to `preparing`; a "Cancel" text link routes to `consent-declined` (the shared not-connected recovery screen).

The `consentId` and `consentContext` (AIS | PAYMENT) are received as route parameters from the originating flow and propagated through to `auth-callback` via `OidcCallbackBus` so the callback screen can correctly key its dual-routing logic.

---

## Screens

| ID                     | Name               | Route                      | Layout | Scroll |
|------------------------|--------------------|----------------------------|--------|--------|
| bank-authorize-handoff | Redirecting to HSBC | BankAuthorizeHandoffRoute  | Column | None   |

**Shell:** No Top App Bar. No bottom navigation bar. Full-screen `#F9FAEF` background. Column centred both axes.

**Route params:** `consentId: String` (required — ConsentId staged by the originating flow), `consentContext: String` (optional — AIS | PAYMENT, propagated to auth-callback).

---

## Components

| ID                     | Type              | Description                                                                                                                       |
|------------------------|-------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| handoff_root           | stack (column)    | Root container — `#F9FAEF` background, spacing.lg padding, align + justify center; a11y region "Securely connecting to HSBC"     |
| handoff_bank_icon      | icon              | `account_balance` (bank) icon — 80dp, `#4C662B`, centred; a11y contentDescription "HSBC bank"                                   |
| handoff_title          | text              | Phase-driven heading — preparing: "Getting ready to connect securely"; redirecting: "Taking you to HSBC to sign in and approve"; error: "We couldn't start your secure sign-in" — Outfit/headline_small, `#1A1C16`, centre, spacing.lg top |
| handoff_message        | text              | "You'll sign in directly with HSBC to approve access. Your username, password and security codes are never entered in this app — and you'll come straight back here once you've approved." — Outfit/body_medium, `#44483D`, centre, spacing.sm top; visible in preparing + redirecting |
| handoff_spinner        | loading_indicator | Circular indeterminate — 32dp, `#4C662B`, centre, spacing.lg top; visible in preparing state only                                |
| handoff_continue_button | button (filled)  | "Continue to HSBC" — `#4C662B` fill, `#FFFFFF` text, Outfit/label_large, 8dp radius, spacing.md padding, spacing.lg top margin, match_parent; visible in redirecting state (OPENING_BROWSER phase); launches external authorise URL |
| handoff_security_note  | text              | "Encrypted connection · You can return here anytime" — Outfit/body_small, `#74796D`, centre, spacing.md top; visible in preparing + redirecting |
| handoff_error_card     | card (filled)     | `#FFDAD6` fill, 8dp radius, spacing.md padding, spacing.lg top margin; a11y role=alert "Could not start authorisation"; visible in error state |
| handoff_error_icon     | icon              | `error` icon — 20dp, `#BA1A1A`; inside error card                                                                                |
| handoff_error_message  | text              | "We couldn't start your secure sign-in with HSBC. Please check your connection and try again." — Outfit/body_small, `#410002`, spacing.sm start; inside error card |
| handoff_retry_button   | button (filled)   | "Try again" — `#4C662B` fill, `#FFFFFF` text, Outfit/label_large, 8dp radius, spacing.md padding, spacing.lg top margin, match_parent; visible in error state; returns to preparing state |
| handoff_cancel_link    | button (text)     | "Cancel" — `#386663` text, Outfit/label_large, centre, min_height 44dp; visible in error state; navigates to consent-declined   |

---

## States

| ID          | Trigger                                                             | Description                                                                                                                     |
|-------------|---------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| preparing   | Screen entry — `HandoffPhase.STAGING / BUILDING_REQUEST`           | Stages consent (AWAU) + generates PKCE + builds signed request object. Heading "Getting ready to connect securely". Spinner + message + security note. No buttons. |
| redirecting | `AuthorizeRequestBuilt(authorizeUrl)` — `HandoffPhase.OPENING_BROWSER / REDIRECTED` | External URL ready; auto-launched in Custom Tab. Heading "Taking you to HSBC to sign in and approve". Spinner → "Continue to HSBC" manual fallback button. Leaves app on launch. |
| error       | `StagingFailed` — network / OB.Field.Invalid / signing failure / no browser | Error card `#FFDAD6` + "We couldn't start your secure sign-in…". "Try again" button (re-prepare) + "Cancel" link (consent-declined). |

---

## State Model

**ViewModel:** `BankAuthorizeHandoffViewModel`
**Screen State Type:** `BankAuthorizeHandoffUiState`

| Name           | Type           | Default                    |
|----------------|----------------|----------------------------|
| phase          | HandoffPhase   | HandoffPhase.STAGING       |
| consentContext | ConsentContext | ConsentContext.AIS         |
| authorizeUrl   | String?        | null                       |
| errorMessage   | String?        | null                       |
| isError        | Boolean        | false                      |

**Events:**
- `BankAuthorizeHandoffEvent.LaunchAuthorize(authorizeUrl: String)`
- `BankAuthorizeHandoffEvent.NavigateToConsentDeclined`

**Actions:**
- `BankAuthorizeHandoffAction.RetryClicked`
- `BankAuthorizeHandoffAction.CancelClicked`
- `BankAuthorizeHandoffAction.ContinueClicked`
- `BankAuthorizeHandoffAction.Internal.ConsentStaged(consentId: String)`
- `BankAuthorizeHandoffAction.Internal.AuthorizeRequestBuilt(authorizeUrl: String)`
- `BankAuthorizeHandoffAction.Internal.StagingFailed(error: BankAuthorizeHandoffError)`

**DI Dependencies:** `ObpAuthRepository`, `OidcCallbackBus`

**Errors:** `BadRequest`, `RequestTimeout`, `SigningFailed`, `BrowserUnavailable`, `Unknown` (all retry=true)

---

## Navigation

| From                   | Action                   | To                  | Type              | Description                                                                         |
|------------------------|--------------------------|---------------------|-------------------|-------------------------------------------------------------------------------------|
| bank-authorize-handoff | launch_authorize         | auth-callback       | external_redirect | PSU authenticates + completes SCA at HSBC → deep-link returns to auth-callback; not an imperative navigate |
| bank-authorize-handoff | cancel_click             | consent-declined    | replace           | Abort the handoff to the not-connected recovery screen                              |
| bank-authorize-handoff | retry_click              | (self / preparing)  | state             | Re-stage the consent and re-build the authorise redirect (returns to preparing)     |

---

## API Endpoints

| Endpoint                                                                                              | Auth                    | Tag            | Purpose                                                                              |
|-------------------------------------------------------------------------------------------------------|-------------------------|----------------|--------------------------------------------------------------------------------------|
| POST https://secure.sandbox.ob.hsbc.co.uk/obie/open-banking/v1.1/oauth2/token                        | mTLS + client_assertion | Authentication | Client-credentials token (grant_type=client_credentials) to stage the consent       |
| POST https://secure.sandbox.ob.hsbc.co.uk/obie/open-banking/v4.0/aisp/account-access-consents        | Bearer (cc_token)       | Authentication | AIS — stage the account-access-consent (Status AWAU); returns ConsentId             |
| GET https://sandbox.ob.hsbc.co.uk/obie/open-banking/v1.1/oauth2/authorize                            | None (external browser) | Authentication | FAPI Hybrid authorise redirect — opened in Custom Tab; PSU authenticates + SCA here |

---

## Design Tokens

| Token                           | Value           | Usage                                                                              |
|---------------------------------|-----------------|------------------------------------------------------------------------------------|
| colors.light.primary            | #4C662B         | `account_balance` icon; spinner; "Continue to HSBC" and "Try again" button fill   |
| colors.light.on_primary         | #FFFFFF         | "Continue to HSBC" and "Try again" button text                                     |
| colors.light.background         | #F9FAEF         | Full-screen background                                                             |
| colors.light.on_surface         | #1A1C16         | Phase-driven headline                                                              |
| colors.light.on_surface_variant | #44483D         | Security explainer body copy                                                       |
| colors.light.outline_variant    | #74796D         | "Encrypted connection · You can return here anytime" caption                       |
| colors.light.secondary          | #386663         | "Cancel" text button colour                                                        |
| colors.light.error              | #BA1A1A         | Error icon inside error card                                                       |
| colors.light.error_container    | #FFDAD6         | Error card fill                                                                    |
| colors.light.on_error_container | #410002         | Error message text                                                                 |
| typography.headline_small       | Outfit 24sp/400 | Phase-driven headline                                                              |
| typography.body_medium          | Outfit 14sp/400 | Security explainer body copy                                                       |
| typography.body_small           | Outfit 12sp/400 | Security note caption; error message inside card                                   |
| typography.label_large          | Outfit 14sp/500 | "Continue to HSBC", "Try again", "Cancel" button labels                            |
| radius.md                       | 8dp             | Error card corners; "Continue to HSBC" and "Try again" button corners              |

---

_Generated by /idea export | 2026-06-14_
