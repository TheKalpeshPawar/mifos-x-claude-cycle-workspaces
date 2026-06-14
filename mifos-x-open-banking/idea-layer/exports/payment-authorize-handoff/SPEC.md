# SPEC — Securing Payment (Payment Authorise Handoff)

| Field         | Value                               |
|---------------|-------------------------------------|
| Feature       | payment-authorize-handoff           |
| Flavor        | consumer                            |
| Status        | enriched                            |
| Quality Score | 94                                  |
| ViewModel     | PaymentAuthorizeHandoffViewModel    |

---

## Overview

The Securing Payment screen is a full-screen transitional takeover that bridges the gap between a confirmed payment on `send-money-confirm` and the PSU's authorisation session at HSBC. The screen owns two sequential operations: staging the domestic-payment-consent (POST `/obie/open-banking/v4.0/pisp/domestic-payment-consents` → ConsentId, Status AWAU), and constructing + launching the signed OAuth2 authorise redirect (openbanking_intent_id = ConsentId, scope=payments, PKCE S256). This is a handoff screen, not a form — the PSU never enters credentials or SCA codes in-app.

A payment-summary card restates the amount (£250.00) and payee (Jordan Avery) being authorised throughout the transition so the user always knows what they are approving. In the `preparing` state an indeterminate spinner runs while the consent is staged and the PKCE code_verifier, S256 code_challenge, and signed request-object JWT are assembled. When the authorise URL is ready the screen transitions to `redirecting`, auto-launches the HSBC authorise URL in the system browser or a Custom Tab, and surfaces a "Continue to HSBC" manual-launch fallback in case the auto-launch is blocked. SCA is performed entirely at HSBC during the external redirect; on completion HSBC redirects to the registered deep-link `org.mifos.openbanking://oauth/callback`, which is handled by `auth-callback` — not by this screen. Consent staging or signing failures produce the `error` state, which reassures the PSU that no money has left their account and offers retry or cancel to `payment-declined`.

The screen is visually consistent with its AIS sibling `bank-authorize-handoff`: earth-green accent (#4C662B), #F9FAEF background, Outfit typeface, no top app bar, no bottom navigation. The obsolete in-app `sca-challenge` one-time-code screen is removed under OBIE — this screen is its replacement.

---

## Screens

| ID                        | Name             | Route                          | Layout | Scroll |
|---------------------------|------------------|--------------------------------|--------|--------|
| payment-authorize-handoff | Securing Payment | PaymentAuthorizeHandoffRoute   | Column | None   |

**Shell:** No top app bar. No bottom navigation bar. Full-screen takeover.

**Route Parameters:**

| Param     | Type    | Required | Description                                                                                     |
|-----------|---------|----------|-------------------------------------------------------------------------------------------------|
| consentId | String? | No       | Pre-existing payment ConsentId (re-entry after partial failure). Usually null — staged on mount. |
| amount    | String  | Yes      | Display amount carried from the confirmed PaymentDraft (e.g. £250.00).                         |
| payeeName | String  | Yes      | Payee display name carried from the confirmed PaymentDraft (e.g. Jordan Avery).                |

---

## Components

| ID                      | Type              | Description                                                                                                                 |
|-------------------------|-------------------|-----------------------------------------------------------------------------------------------------------------------------|
| handoff_root            | stack (column)    | Full-screen root; #F9FAEF bg; spacing.lg padding; center-aligned both axes                                                  |
| handoff_bank_icon       | icon              | `account_balance` — 80dp, #4C662B; role image; a11y "HSBC bank"                                                            |
| handoff_title           | text              | Outfit/headline_small, #1A1C16, center; content overridden per state (see States)                                           |
| handoff_message         | text              | Outfit/body_medium, #44483D, center; "You'll authorise this payment directly with HSBC…" security explainer                 |
| handoff_summary_card    | card (filled)     | #FFFFFF fill; 16dp radius; 1dp #CDEDA3 border; spacing.md padding; groups amount + payee + securing label                   |
| handoff_amount_value    | text              | "£250.00" — Outfit/display_small, #4C662B, bold 700, center                                                                |
| handoff_payee_value     | text              | "To Jordan Avery" — Outfit/body_large, #1A1C16, center                                                                     |
| handoff_securing_label  | text              | "Authorising securely with HSBC Open Banking" — Outfit/body_small, #44483D, center                                         |
| handoff_spinner         | loading_indicator | Circular indeterminate; 32dp, #4C662B; visible in `preparing` state                                                        |
| handoff_continue_button | button (filled)   | "Continue to HSBC"; #4C662B bg, #FFFFFF text; Outfit/label_large; 8dp radius; match_parent; visible in `redirecting` state |
| handoff_security_note   | text              | "Encrypted connection · You can return here anytime" — Outfit/body_small, #74796D, center                                  |
| handoff_error_card      | card (filled)     | #FFDAD6 bg; 8dp radius; groups error icon + error message; visible in `error` state                                        |
| handoff_error_icon      | icon              | `error` — 20dp, #BA1A1A                                                                                                    |
| handoff_error_message   | text              | "We couldn't reach HSBC to authorise your payment…" — Outfit/body_small, #410002; role alert                               |
| handoff_retry_button    | button (filled)   | "Try again"; #4C662B bg, #FFFFFF text; Outfit/label_large; 8dp radius; match_parent; visible in `error` state              |
| handoff_cancel_link     | button (text)     | "Cancel"; #386663 text; Outfit/label_large; min_height 44dp; visible in `error` state → navigates to payment-declined      |

---

## States

| ID          | Trigger                                                              | Description                                                                                                                |
|-------------|----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| preparing   | Screen mount — consent staging + PKCE + signed request building      | Full-screen takeover: bank icon, title, security message, summary card, spinner, security note. No user action required.   |
| redirecting | ConsentId returned (AWAU) + signed authorise URL built               | Same layout; spinner replaced by "Continue to HSBC" button (manual fallback). Auto-launches HSBC URL in system browser.    |
| error       | Consent staging or authorise-request build / launch fails            | Bank icon, error title, error card with icon + message, retry button, cancel link. Reassures no charge was made.           |

---

## State Model

**ViewModel:** `PaymentAuthorizeHandoffViewModel`
**Screen State Type:** `PaymentAuthorizeHandoffUiState`

| Field          | Type                   | Default               | Notes                                                                             |
|----------------|------------------------|-----------------------|-----------------------------------------------------------------------------------|
| phase          | HandoffPhase (enum)    | HandoffPhase.STAGING  | STAGING/BUILDING_REQUEST → `preparing`; OPENING_BROWSER/REDIRECTED → `redirecting`; ERROR → `error` |
| amount         | String                 | ""                    | Display amount from confirmed PaymentDraft (e.g. £250.00)                         |
| payeeName      | String                 | ""                    | Payee display name from confirmed PaymentDraft (e.g. Jordan Avery)                |
| consentId      | String?                | null                  | Data.ConsentId from create_domestic_payment_consent; becomes the intent_id         |
| authorizeUrl   | String?                | null                  | Fully-built HSBC authorise URL; set when BUILDING_REQUEST completes                |
| errorMessage   | String?                | null                  | Human-readable error copy; null when not in error state                            |
| isError        | Boolean                | false                 | Shortcut field; true when phase == ERROR                                           |

**Derived:** `isReadyToRedirect: Boolean` = `authorizeUrl != null && phase == HandoffPhase.OPENING_BROWSER`

**Events:** `LaunchAuthorize(authorizeUrl: String)`, `NavigateToCallback`, `NavigateToPaymentDeclined`

**Actions:**

| Action                               | Trigger                                          |
|--------------------------------------|--------------------------------------------------|
| `RetryClicked`                       | Tap "Try again" in error state                   |
| `CancelClicked`                      | Tap "Cancel" in error state                      |
| `ContinueClicked`                    | Tap "Continue to HSBC" manual-launch fallback    |
| `Internal.ConsentStaged(consentId)`  | Payment consent reached AWAU                     |
| `Internal.AuthorizeRequestBuilt(url)`| Signed request object built; authorizeUrl set    |
| `Internal.StagingFailed(error)`      | Consent staging or signing failed                |

**Error Types:**

| Type                  | Retry | Message Key                      |
|-----------------------|-------|----------------------------------|
| BadRequest            | Yes   | error_authorize_bad_request      |
| RequestTimeout        | Yes   | error_network                    |
| SigningFailed          | Yes   | error_authorize_signing          |
| InvalidConsentStatus  | Yes   | error_invalid_consent_status     |
| BrowserUnavailable    | Yes   | error_browser_unavailable        |
| Unknown               | Yes   | error_unknown                    |

**DI:** `ObpAuthRepository`, `PaymentsRepository`, `OidcCallbackBus`

---

## Navigation

| ID                      | From                      | To               | Trigger                            | Type              | Notes                                                                                              |
|-------------------------|---------------------------|------------------|------------------------------------|-------------------|----------------------------------------------------------------------------------------------------|
| nav_to_auth_callback    | payment-authorize-handoff | auth-callback    | external_redirect_return           | deep-link return  | HSBC redirects to org.mifos.openbanking://oauth/callback after the PSU authorises. Handled by auth-callback, not this screen. |
| nav_to_payment_declined | payment-authorize-handoff | payment-declined | cancel_click (error state)         | navigate          | Cancel in the error state aborts the handoff; routes to the shared payment-not-completed recovery screen. No charge was made. |

---

## API Endpoints

| Endpoint                                                          | Method | Auth               | Tag           | Trigger              |
|-------------------------------------------------------------------|--------|--------------------|---------------|----------------------|
| POST /obie/open-banking/v4.0/pisp/domestic-payment-consents       | POST   | Client Credentials | PISP          | on_handoff_mount     |
| GET https://sandbox.ob.hsbc.co.uk/oauth2/authorize               | GET    | PKCE + request JWT | Authorization | on_consent_created   |

---

## Design Tokens

| Token                            | Value                 | Usage                                                                    |
|----------------------------------|-----------------------|--------------------------------------------------------------------------|
| colors.light.primary             | #4C662B               | Bank icon; net/amount text; spinner; filled button bg; securing label    |
| colors.light.primary_container   | #CDEDA3               | Summary card border                                                      |
| colors.light.error               | #BA1A1A               | Error icon colour                                                        |
| colors.light.error_container     | #FFDAD6               | Error card background                                                    |
| colors.light.on_error_container  | #410002               | Error message text                                                       |
| colors.light.background          | #F9FAEF               | Screen root background                                                   |
| colors.light.surface             | #FFFFFF               | Summary card fill                                                        |
| colors.light.on_surface          | #1A1C16               | Title text; payee text                                                   |
| colors.light.on_surface_variant  | #44483D               | Security explainer body; securing label; retry note                      |
| colors.light.secondary           | #386663               | Cancel link text colour                                                  |
| colors.light.outline_variant     | #74796D               | Security note caption text                                               |
| typography.headline_small        | Outfit 24sp/400       | Screen title (state-overridden)                                          |
| typography.display_small         | Outfit 36sp/400       | Amount value in summary card                                             |
| typography.body_large            | Outfit 16sp/400       | Payee line in summary card                                               |
| typography.body_medium           | Outfit 14sp/400       | Security explainer body                                                  |
| typography.body_small            | Outfit 12sp/400       | Securing label; security note; error message                             |
| typography.label_large           | Outfit 14sp/500       | Button labels (Continue to HSBC; Try again; Cancel)                      |
| radius.md                        | 8dp                   | Filled button + retry button corner radius; error card radius            |
| radius.lg                        | 16dp                  | Summary card corner radius                                               |
| spacing.lg                       | 24dp                  | Root padding; top/bottom spacing between major sections                  |
| spacing.md                       | 16dp                  | Summary card padding; button padding                                     |
| spacing.sm                       | 8dp                   | Securing label top padding; cancel link vertical padding                 |
| icon.size.xl                     | 80dp                  | Bank icon (`account_balance`)                                            |
| icon.size.sm                     | 20dp                  | Error icon within error card                                             |
| spinner.size.md                  | 32dp                  | Indeterminate circular progress indicator                                |

---

_Generated by /idea export | 2026-06-14_
