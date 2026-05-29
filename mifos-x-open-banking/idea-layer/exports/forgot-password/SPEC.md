# SPEC — Forgot Password

| Field         | Value                      |
|---------------|----------------------------|
| Feature       | forgot-password            |
| Flavor        | shared                     |
| Status        | approved                   |
| Quality Score | 95                         |
| ViewModel     | ForgotPasswordViewModel    |

---

## Overview

The Forgot Password screen allows both Consumer and Field Officer users to request a password reset link. It presents a centered lock-reset illustration, a headline ("Forgot your password?"), instructional copy, and a single text field accepting either a username or email address. Submitting triggers a POST to the OBP password-reset endpoint. On success, the form section is replaced by a success confirmation (mark_email_read icon + "Check your inbox" message) that deliberately avoids confirming whether the account exists — preventing account enumeration. On error, a red banner appears above the submit button. A "Back to Login" text link is always visible for escape. No bottom navigation bar (shared flavor).

---

## Screens

| ID              | Name             | Route             | Layout | Scroll   |
|-----------------|------------------|-------------------|--------|----------|
| forgot-password | Forgot Password  | /forgot-password  | Column | Vertical |

**Shell:** Top app bar ("Reset Password") with back arrow. No bottom navigation bar.

| Shell Element     | Type | Value                              |
|-------------------|------|------------------------------------|
| Top app bar title | text | "Reset Password"                   |
| Navigation icon   | icon | arrow_back → navigate_back (login) |

---

## Components

| ID                   | Type    | Description                                                                                                      |
|----------------------|---------|------------------------------------------------------------------------------------------------------------------|
| fpw_root             | stack   | Column root — #F9FAEF background, lg spacing (24dp) padding                                                     |
| fpw_illustration     | image   | ic_lock_reset icon — 72×72dp, #4C662B tint, centered                                                            |
| fpw_header_title     | text    | "Forgot your password?" — Outfit/headline_small, #4C662B, centered                                             |
| fpw_header_subtitle  | text    | "Enter your username or email address and we'll send you a link to reset your password." — Outfit/body_medium, #44483D, centered |
| fpw_form_section     | stack   | Column container for input field — hidden when uiState == success                                               |
| fpw_identifier_input | input   | "Username or Email" — placeholder "e.g. john.doe or john@example.com", border #C5C8BA, focus border #4C662B, error border #BA1A1A, 56dp height, Outfit/body_medium |
| fpw_error_banner     | banner  | "We couldn't find an account with that username or email. Please try again." — #FFDAD6 fill, #BA1A1A text, 8dp radius — visible when uiState == error |
| fpw_success_section  | stack   | Column — centered vertically, xl padding — visible when uiState == success                                      |
| fpw_success_icon     | icon    | mark_email_read — 48dp, #4C662B, centered                                                                       |
| fpw_success_title    | text    | "Check your inbox" — Outfit/title_large, #4C662B, centered                                                     |
| fpw_success_body     | text    | "If an account exists for that email, you'll receive a password reset link within a few minutes." — Outfit/body_medium, #44483D, centered |
| fpw_submit_button    | button  | "Send Reset Link" — filled, #4C662B fill, #FFFFFF text, Outfit/label_large, 12dp radius — shows loading spinner when uiState == submitting — hidden when uiState == success |
| fpw_back_to_login_link | link  | "Back to Login" — Outfit/body_medium, #386663, centered — always visible                                        |

---

## States

| ID      | Trigger                               | Description                                                                              |
|---------|---------------------------------------|------------------------------------------------------------------------------------------|
| idle    | Screen entry                          | Illustration + title + subtitle + form input + submit button + back link visible        |
| loading | Submit button tapped, request in flight | Same as idle + submit button shows loading spinner + input disabled                    |
| success | API returns 200                       | Form section hidden; success icon + "Check your inbox" + body copy + back link visible  |
| error   | API returns 404 / 400 / 429           | Same as idle + error banner (red) appears above submit button                           |
| content | (alias for idle — same layout)        | Illustration + form + submit + back link                                                 |
| empty   | Reset service unavailable             | Illustration + title + back link only; empty state copy: "Password reset unavailable. Contact your bank." |

---

## State Model

**ViewModel:** `ForgotPasswordViewModel`
**Screen State:** `ForgotPasswordUiState`

| Name           | Type    | Default |
|----------------|---------|---------|
| identifier     | String  | ""      |
| isSubmitting   | Boolean | false   |
| isSuccess      | Boolean | false   |
| errorMessage   | String? | null    |

**Errors:** `ACCOUNT_NOT_FOUND`, `NETWORK_ERROR`, `RATE_LIMITED`

**Events:** `OnIdentifierChanged`, `OnSubmitClicked`, `OnBackToLoginClicked`

**Actions:** `onIdentifierChanged(value: String)`, `onSubmitClicked()`, `onBackToLoginClicked()`

**DI Dependencies:** `AuthRepository`

---

## Navigation

| From            | To    | Trigger                        | Type |
|-----------------|-------|--------------------------------|------|
| forgot-password | login | fpw_back_to_login_link tap     | pop  |
| forgot-password | login | navigate_back (top bar arrow)  | pop  |

---

## API Endpoints

| Endpoint                            | Auth | Tag  | Purpose                               |
|-------------------------------------|------|------|---------------------------------------|
| POST /obp/v5.0.0/users/password-reset | None | Auth | Request password reset link via email |

---

## Design Tokens

| Token                           | Value     | Usage                                                    |
|---------------------------------|-----------|----------------------------------------------------------|
| colors.light.primary            | #4C662B   | Illustration tint, title color, submit button fill, success icon + title |
| colors.light.secondary          | #386663   | "Back to Login" link color                               |
| colors.light.background         | #F9FAEF   | Screen background                                        |
| colors.light.on_surface_variant | #44483D   | Subtitle text, success body text                         |
| colors.light.on_surface         | #1A1C16   | Input field value text                                   |
| colors.light.outline_variant    | #C5C8BA   | Input default border                                     |
| colors.light.outline            | #75796C   | Input focus border (maps to #4C662B in spec override)    |
| colors.light.error              | #BA1A1A   | Input error border, error banner text                    |
| colors.light.error_container    | #FFDAD6   | Error banner background                                  |
| typography.headline_small       | Outfit 24sp/600 | Screen headline title                              |
| typography.title_large          | Outfit 22sp     | Success state "Check your inbox" heading           |
| typography.body_medium          | Outfit 14sp/400 | Subtitle, success body, back-to-login link         |
| typography.label_large          | Outfit 14sp/500 | Submit button text                                 |
| spacing.lg                      | 24dp      | Root container padding                                   |
| spacing.xl                      | 32dp      | Submit button horizontal padding, success section padding|
| radius.md                       | 12dp      | Submit button border radius                              |
| radius.sm                       | 8dp       | Error banner border radius                               |

---

_Generated by /idea export | 2026-05-29_
