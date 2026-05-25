# SPEC — Login

| Field         | Value          |
|---------------|----------------|
| Feature       | login          |
| Flavor        | shared         |
| Status        | enriched       |
| Quality Score | 78             |
| ViewModel     | LoginViewModel |

---

## Overview

The Login screen handles dual authentication methods for both the Consumer and Field Officer personas: DirectLogin (form-based, OBP header credential submission) and OAuth/OIDC via the OBP OIDC provider (authorization_code + PKCE flow). On successful authentication the screen reads the returned role and navigates accordingly — Consumer users go to the Home Dashboard, Field Officers go to the FO Dashboard. A "Forgot Password?" link provides a secondary recovery path.

---

## Screens

| ID    | Name  | Route  | Layout | Scroll   |
|-------|-------|--------|--------|----------|
| login | Login | /login | Column | Vertical |

---

## Components

| ID                        | Type   | Description                                                                          |
|---------------------------|--------|--------------------------------------------------------------------------------------|
| login_root                | stack  | Full-screen column container, background #F5F5F5, padding spacing.lg                |
| login_header_logo         | image  | Mifos X logo 80×80 dp, tint #1800B1, centered                                       |
| login_header_title        | text   | "Welcome Back", headline_large, color #1800B1, centered                             |
| login_header_subtitle     | text   | "Sign in to your Mifos X account", body_medium, color #757575, centered             |
| login_username_input      | input  | Text field for username/customer ID; ime_action=next                                |
| login_password_input      | input  | Password field with visibility toggle icon; ime_action=done                         |
| login_remember_me_row     | stack  | Horizontal row containing checkbox + label                                           |
| login_remember_me_checkbox| input  | Checkbox variant, color #1800B1; persists session across restarts                   |
| login_remember_me_label   | text   | "Keep me signed in", body_medium, color #424242                                     |
| login_error_banner        | card   | Filled card, background #FFEBEE, border #FF5252; visible_when uiState==Error        |
| login_error_icon          | icon   | error_outline, 20 dp, color #FF5252                                                 |
| login_error_message       | text   | Dynamic error message, body_small, color #B71C1C                                    |
| login_cta_button          | button | "Sign In", filled, background #1800B1; submits DirectLogin; loading on Authenticating|
| login_or_divider_row      | stack  | Row with left divider + "OR" text + right divider                                   |
| login_oauth_button        | button | "Sign in with OBP Account", outlined, border/text #1800B1; opens system browser     |
| login_oauth_hint          | text   | "Redirects to Open Bank Project for secure authentication", body_small, #9E9E9E     |
| login_forgot_password_link| link   | "Forgot Password?", inline link, color #008B8B                                      |

---

## States

| ID               | Trigger                              | Description                                                                       |
|------------------|--------------------------------------|-----------------------------------------------------------------------------------|
| idle             | Screen open                          | All fields enabled; both auth method buttons active                              |
| authenticating   | Sign In button tapped                | CTA shows loading spinner; all inputs + OAuth button disabled                    |
| oauth_redirecting| OBP Account button tapped            | OAuth button shows loading; system browser opens to OBP OIDC auth endpoint       |
| oauth_exchanging | App returns from browser with code   | Full-screen loading overlay; code→token exchange in progress                     |
| error            | DirectLogin 400/401 or OAuth failure | Error banner visible above CTA; fields re-enabled for correction                 |

---

## State Model

**ViewModel:** `LoginViewModel`
**Screen State Type:** `LoginUiState`

| Field            | Type      | Default          | Notes                                        |
|------------------|-----------|------------------|----------------------------------------------|
| username         | String    | ""               |                                              |
| password         | String    | ""               |                                              |
| rememberMe       | Boolean   | false            |                                              |
| isPasswordVisible| Boolean   | false            |                                              |
| errorMessage     | String?   | null             |                                              |
| isLoading        | Boolean   | false            |                                              |
| authMethod       | AuthMethod| AuthMethod.NONE  | NONE / DIRECT_LOGIN / OAUTH_OIDC             |
| oauthState       | String?   | null             | CSRF state param for authorization_code flow |
| oauthCodeVerifier| String?   | null             | PKCE code_verifier                           |

**Events:** `OnUsernameChanged`, `OnPasswordChanged`, `OnRememberMeToggled`, `OnPasswordVisibilityToggled`, `OnDirectLoginClicked`, `OnOAuthLoginClicked`, `OnOAuthCallback`, `OnForgotPasswordClicked`, `OnLoginSuccess`, `OnLoginError`

**Actions:** `onUsernameChanged(value: String)`, `onPasswordChanged(value: String)`, `onRememberMeToggled()`, `onPasswordVisibilityToggled()`, `onDirectLoginClicked()`, `onOAuthLoginClicked()`, `onOAuthCallback(code: String, state: String)`, `onForgotPasswordClicked()`

**DI Dependencies:** `ObpAuthRepository`, `ObpOidcClient`, `SessionManager`, `CredentialStore`

**Errors:** `NETWORK_ERROR`, `INVALID_CREDENTIALS`, `UNAUTHORIZED`, `SERVER_ERROR`, `OAUTH_CANCELLED`, `OAUTH_TOKEN_EXCHANGE_FAILED`, `OAUTH_STATE_MISMATCH`

---

## Navigation

| ID                    | From  | To              | Trigger               | Condition              |
|-----------------------|-------|-----------------|-----------------------|------------------------|
| nav_to_consumer_home  | login | consumer-home   | on_login_success      | userRole == CONSUMER   |
| nav_to_home           | login | home            | on_login_success      | userRole == CONSUMER   |
| nav_to_fo_dashboard   | login | fo-dashboard    | on_login_success      | userRole == FIELD_OFFICER|
| nav_to_forgot_password| login | forgot-password | forgot_password_click | —                      |

---

## API Endpoints

| ID                  | Endpoint                                                                    | Auth         | Purpose                                         |
|---------------------|-----------------------------------------------------------------------------|--------------|--------------------------------------------------|
| obp_direct_login    | POST /my/logins/direct                                                      | DirectLogin  | Submit username+password; receive session token  |
| obp_oidc_discovery  | GET /obp/v5.1.0/well-known                                                  | None         | Discover OIDC provider configuration            |
| obp_oidc_authorize  | GET https://apisandbox-oidc.openbankproject.com/obp-oidc/auth               | None         | Browser auth_code + PKCE flow initiation         |
| obp_oidc_token      | POST https://apisandbox-oidc.openbankproject.com/obp-oidc/token             | None         | Exchange auth code for access_token + id_token  |
| obp_oidc_userinfo   | GET https://apisandbox-oidc.openbankproject.com/obp-oidc/userinfo           | Bearer token | Fetch user profile post-OAuth login             |
| obp_oidc_refresh    | POST https://apisandbox-oidc.openbankproject.com/obp-oidc/token             | None         | Refresh access_token using refresh_token        |
| obp_oidc_revoke     | POST https://apisandbox-oidc.openbankproject.com/obp-oidc/revoke            | None         | Revoke tokens on logout                         |

---

## Design Tokens

| Token                       | Value                | Usage                                            |
|-----------------------------|----------------------|--------------------------------------------------|
| color.light.primary         | #1800B1              | Logo, title, input focus border, CTA background, checkbox |
| color.light.background      | #F5F5F5              | Root background                                  |
| color.error.default         | #FF5252              | Error banner border, error icon                 |
| color.error.dark            | #B71C1C              | Error message text                              |
| color.error.surface         | #FFEBEE              | Error banner background                         |
| color.accent.teal           | #008B8B              | Forgot password link                            |
| color.neutral.medium        | #757575              | Subtitle, hint text                             |
| color.neutral.border        | #BDBDBD              | Input default border, dividers                  |
| typography.headline_large   | Inter/headline_large | "Welcome Back" title                            |
| typography.body_medium      | Manrope/body_medium  | Subtitle, remember-me label                     |
| typography.body_large       | Manrope/body_large   | Input field text                                |
| typography.label_large      | Inter/label_large    | CTA button, OAuth button                        |
| typography.body_small       | Manrope/body_small   | Error message, OAuth hint                       |

---

_Generated by /idea export | 2026-05-25_
