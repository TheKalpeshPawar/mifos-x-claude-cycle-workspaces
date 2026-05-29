# SPEC — Login

| Field         | Value          |
|---------------|----------------|
| Feature       | login          |
| Flavor        | shared         |
| Status        | approved       |
| Quality Score | 95             |
| ViewModel     | LoginViewModel |

---

## Overview

The Login screen handles dual authentication for both Consumer and Field Officer personas: DirectLogin (form-based OBP header credential submission) and OAuth/OIDC via the OBP OIDC provider (authorization_code + PKCE flow). On successful authentication the screen reads the returned user role and navigates accordingly — Consumer users go to Home, Field Officers go to FO Dashboard. A "Forgot Password?" link provides a password recovery path. Six OAuth OIDC API calls cover the full auth lifecycle including token refresh and logout revocation.

---

## Screens

| ID    | Name  | Route  | Layout | Scroll   |
|-------|-------|--------|--------|----------|
| login | Login | /login | Column | Vertical |

**Shell:** No top app bar (first-launch screen). No bottom navigation bar.

---

## Components

| ID                        | Type   | Description                                                                                                  |
|---------------------------|--------|--------------------------------------------------------------------------------------------------------------|
| login_header_logo         | image  | Mifos X logo, 80×80dp, tint `#4C662B`, center-aligned, 16dp bottom padding                                  |
| login_header_title        | text   | "Welcome Back" — headline_small, `#4C662B`, centered, heading level 1                                       |
| login_header_subtitle     | text   | "Sign in to your Mifos X account" — body_medium, `#44483D`, centered, 32dp bottom padding                   |
| login_username_input      | input  | Outlined text field, label "Username", placeholder "Enter your username". White bg, `#C5C8BA` border, `#4C662B` focus border. ime_action=next |
| login_password_input      | input  | Outlined password field, label "Password", visibility_toggle trailing icon. Same border treatment as username. ime_action=done |
| login_remember_me_row     | stack  | Horizontal row: checkbox (color `#4C662B`) + "Keep me signed in" (body_medium, `#1A1C16`, 8dp start padding)|
| login_error_banner        | card   | Filled card, `#CDEDA3` bg, `#BA1A1A` 1dp border, 8dp radius, 16dp padding. Visible when uiState==Error. Contains error_outline icon (20dp, `#BA1A1A`) + error message text (body_small, `#BA1A1A`) |
| login_cta_button          | button | Filled, `#4C662B` bg, `#FFFFFF` text, label_large, 8dp radius, full-width. "Sign In". Shows loading spinner when Authenticating |
| login_or_divider_row      | stack  | Row: left divider (`#E1E4D5`, flex 1) + "OR" (label_medium, `#44483D`, 16dp horizontal padding) + right divider |
| login_oauth_button        | button | Outlined, `#4C662B` border/text, label_large, 8dp radius, full-width. "Sign in with OBP Account". Leading open_in_browser icon. Launches system browser to OBP OIDC auth endpoint |
| login_oauth_hint          | text   | "Redirects to Open Bank Project for secure authentication" — body_small, `#44483D`, centered, 4dp top padding|
| login_forgot_password_link| link   | "Forgot Password?" — body_medium, `#386663`, centered, 44dp min touch target. Navigates to forgot-password  |
| oauth_redirect_title      | text   | "Redirecting to Open Bank Project" — headline_small, `#1A1C16`, centered (oauth_redirecting state)          |
| oauth_redirect_msg        | text   | "Opening your browser for secure OAuth authentication…" — body_medium, `#44483D`, centered                  |
| oauth_redirect_spinner    | loading_indicator | Circular indeterminate, `#4C662B`, 32dp (oauth_redirecting state)                             |
| oauth_exchange_title      | text   | "Completing Sign In" — headline_small, `#1A1C16`, centered (oauth_exchanging state)                         |
| oauth_exchange_msg        | text   | "Exchanging authorization code for your session token…" — body_medium, `#44483D`, centered                  |
| oauth_exchange_spinner    | loading_indicator | Circular indeterminate, `#4C662B`, 32dp (oauth_exchanging state)                             |

---

## States

| ID               | Trigger                               | Description                                                                     |
|------------------|---------------------------------------|---------------------------------------------------------------------------------|
| idle             | Screen open                           | All form fields and both auth buttons enabled; no error banner                  |
| loading          | Alias for authenticating              | login_cta_button shows loading spinner; inputs and OAuth button disabled        |
| authenticating   | "Sign In" tapped                      | login_cta_button loading; inputs disabled; same layout as loading               |
| oauth_redirecting| "Sign in with OBP Account" tapped     | Full-screen takeover: logo + redirect title + message + spinner. System browser opens |
| oauth_exchanging | App returns from browser with code    | Full-screen takeover: logo + exchanging title + message + spinner                |
| error            | DirectLogin 400/401 or OAuth failure  | login_error_banner visible above login_cta_button; inputs re-enabled            |
| content          | Alias for idle                        | Same layout as idle; canonical loaded state                                     |
| empty            | No accounts found (account_circle_off)| Logo + title + subtitle + empty state: "No accounts found. Contact your bank." |

---

## State Model

**ViewModel:** `LoginViewModel`
**Screen State Type:** `LoginUiState`

| Field             | Type       | Default          | Notes                                           |
|-------------------|------------|------------------|-------------------------------------------------|
| username          | String     | ""               |                                                 |
| password          | String     | ""               |                                                 |
| rememberMe        | Boolean    | false            |                                                 |
| isPasswordVisible | Boolean    | false            |                                                 |
| errorMessage      | String?    | null             |                                                 |
| isLoading         | Boolean    | false            |                                                 |
| authMethod        | AuthMethod | AuthMethod.NONE  | NONE / DIRECT_LOGIN / OAUTH_OIDC                |
| oauthState        | String?    | null             | CSRF state parameter for authorization_code flow|
| oauthCodeVerifier | String?    | null             | PKCE code_verifier                              |

**Events:** `OnUsernameChanged`, `OnPasswordChanged`, `OnRememberMeToggled`, `OnPasswordVisibilityToggled`, `OnDirectLoginClicked`, `OnOAuthLoginClicked`, `OnOAuthCallback(code, state)`, `OnForgotPasswordClicked`, `OnLoginSuccess`, `OnLoginError`

**Actions:** `onUsernameChanged(String)`, `onPasswordChanged(String)`, `onRememberMeToggled()`, `onPasswordVisibilityToggled()`, `onDirectLoginClicked()`, `onOAuthLoginClicked()`, `onOAuthCallback(code: String, state: String)`, `onForgotPasswordClicked()`

**DI Dependencies:** `ObpAuthRepository`, `ObpOidcClient`, `SessionManager`, `CredentialStore`

**Errors:**
- `NETWORK_ERROR`: "Could not connect to banking services. Please try again."
- `INVALID_CREDENTIALS`: "Invalid username or password. Please check your credentials and try again."
- `UNAUTHORIZED`: "You are not authorized to access this account."
- `SERVER_ERROR`: "Something went wrong on our end. Please try again in a moment."
- `OAUTH_CANCELLED`: "Sign-in was cancelled. You can try again or use DirectLogin."
- `OAUTH_TOKEN_EXCHANGE_FAILED`: "Authentication failed. Please try signing in again."
- `OAUTH_STATE_MISMATCH`: "Security check failed. Please try signing in again."

---

## Navigation

| From  | To              | Trigger                     | Condition                  | Type |
|-------|-----------------|-----------------------------|----------------------------|------|
| login | home            | on_login_success            | userRole == CONSUMER       | replace |
| login | fo-dashboard    | on_login_success            | userRole == FIELD_OFFICER  | replace |
| login | forgot-password | forgot_password_link tap    | —                          | push |

---

## API Endpoints

| ID                 | Endpoint                                                                        | Auth        | Purpose                                          |
|--------------------|---------------------------------------------------------------------------------|-------------|--------------------------------------------------|
| obp_direct_login   | POST /my/logins/direct                                                          | DirectLogin | Submit username+password; receive session token  |
| obp_oidc_discovery | GET /obp/v5.1.0/well-known                                                      | None        | Discover OIDC provider configuration at startup  |
| obp_oidc_authorize | GET https://apisandbox-oidc.openbankproject.com/obp-oidc/auth                   | None        | Open browser for auth_code + PKCE flow           |
| obp_oidc_token     | POST https://apisandbox-oidc.openbankproject.com/obp-oidc/token                 | None        | Exchange auth code for access_token + id_token   |
| obp_oidc_userinfo  | GET https://apisandbox-oidc.openbankproject.com/obp-oidc/userinfo               | Bearer      | Fetch user profile after successful OAuth login  |
| obp_oidc_refresh   | POST https://apisandbox-oidc.openbankproject.com/obp-oidc/token (refresh)      | None        | Silent token refresh using refresh_token         |
| obp_oidc_revoke    | POST https://apisandbox-oidc.openbankproject.com/obp-oidc/revoke                | None        | Revoke tokens on logout                          |

---

## Design Tokens

| Token                         | Value     | Usage                                                                     |
|-------------------------------|-----------|---------------------------------------------------------------------------|
| color.light.primary           | #4C662B   | Logo tint, heading title, checkbox, CTA button bg, input focus border, OAuth button border/text |
| color.light.on_primary        | #FFFFFF   | CTA button text                                                           |
| color.light.secondary         | #386663   | Forgot password link color                                                |
| color.light.primary_container | #CDEDA3   | Error banner background                                                   |
| color.light.error             | #BA1A1A   | Error banner border, error icon, error message text                       |
| color.light.surface           | #FFFFFF   | Input field backgrounds                                                   |
| color.light.background        | #F9FAEF   | Screen background                                                         |
| color.light.on_surface        | #1A1C16   | Remember-me label text                                                    |
| color.light.on_surface_variant| #44483D   | Subtitle, OAuth hint, OR divider text, input placeholder                  |
| color.light.outline           | #75796C   | (reserved — input focus secondary)                                        |
| color.light.outline_variant   | #C5C8BA   | Input default border, OR divider lines                                    |
| typography.headline_small     | —         | "Welcome Back" title, OAuth state titles                                  |
| typography.body_medium        | —         | Subtitle, remember-me label, OAuth hint, forgot password link             |
| typography.body_large         | —         | Input field values                                                        |
| typography.body_small         | —         | Error message text                                                        |
| typography.label_large        | —         | CTA button, OAuth button                                                  |
| typography.label_medium       | —         | OR divider text                                                           |
| spacing.lg                    | 24dp      | Screen padding, section gap between form and buttons                      |
| spacing.md                    | 16dp      | Input field padding, error banner padding                                 |
| spacing.xl                    | 32dp      | Subtitle bottom padding                                                   |
| radius.xs                     | 4dp       | Input field border-radius                                                 |

---

_Generated by /idea export | 2026-05-29_
