# SPEC — Forgot Password

| Field         | Value                      |
|---------------|----------------------------|
| Feature       | forgot-password            |
| Flavor        | shared                     |
| Status        | approved                   |
| Quality Score | 93                         |
| ViewModel     | ForgotPasswordViewModel    |
| Archetype     | form                       |

---

## Overview

The Forgot Password screen allows unauthenticated users to request a password reset email. The form collects a username and email address, then submits a reset request via the OBP API. On success, a confirmation message directs the user to check their inbox. The screen includes rate-limiting protection (429) and account-not-found handling (404). After submission, users can navigate back to the login screen.

---

## Screens

| ID               | Name            | Route             | Layout | Scroll   |
|------------------|-----------------|--------------------|--------|----------|
| forgot-password  | Forgot Password | /forgot-password   | Column | None     |

**Shell:** Top app bar with title "Forgot Password", back arrow navigation, no bottom nav.

---

## Components

| ID                        | Type    | Description                                                                |
|---------------------------|---------|----------------------------------------------------------------------------|
| fgpw_header_section       | stack   | Column with headline and instruction text                                  |
| fgpw_header_title         | text    | "Reset Your Password" — headline_small, #4C662B                           |
| fgpw_header_subtitle      | text    | Instruction copy for the reset flow — body_medium, #44483D                |
| fgpw_form_card            | card    | Filled card containing username and email inputs                           |
| fgpw_username_input       | input   | Username field — outlined, Outfit/body_medium                              |
| fgpw_email_input          | input   | Email field — outlined, keyboard type email                                |
| fgpw_error_banner         | banner  | Error feedback (account not found, rate limited) — #FFDAD6 bg, #BA1A1A    |
| fgpw_success_section      | stack   | Success confirmation with check icon and message                           |
| fgpw_submit_button        | button  | "Send Reset Link" — filled, #4C662B bg, #FFFFFF text                      |
| fgpw_back_to_login_link   | link    | "Back to Login" — inline link navigating to login screen                   |

---

## States

| ID         | Trigger                      | Description                                                            |
|------------|------------------------------|------------------------------------------------------------------------|
| idle       | Screen entry                 | Username and email inputs visible with submit button                   |
| content    | Screen entry (alias of idle) | Same as idle — form ready for input                                    |
| loading    | Screen entry                 | Brief skeleton while form initializes                                  |
| submitting | OnSubmitClicked              | Submit button shows loading spinner; form fields disabled              |
| success    | API 200 OK                   | Success section visible with confirmation message and back-to-login    |
| error      | API 404/429/500              | Error banner visible with retry option; form remains editable          |
| empty      | Unavailable                  | "Password reset unavailable" message with retry later suggestion       |

---

## State Model

```kotlin
data class ForgotPasswordUiState(
    val username: String = "",
    val email: String = "",
    val isSubmitting: Boolean = false,
    val errorMessage: String? = null,
    val isSuccess: Boolean = false
)
```

**Events:** OnUsernameChanged, OnEmailChanged, OnSubmitClicked, OnBackToLoginClicked

**Actions:**
- `onUsernameChanged(value: String)`
- `onEmailChanged(value: String)`
- `onSubmitClicked()`
- `onBackToLoginClicked()`

**DI:** AuthRepository

---

## Navigation

| ID                  | Target | Action                    |
|---------------------|--------|---------------------------|
| nav_back_to_login   | login  | Navigate back to login    |

---

## Dependencies

| Tier    | Features              |
|---------|-----------------------|
| feature | shared-core, obp-auth |

---

## Design Tokens

| Token      | Value                    |
|------------|--------------------------|
| Accent     | #4C662B (Earth Green)    |
| Typography | Outfit                   |
| Background | #F9FAEF                  |
| Surface    | #FFFFFF                  |
| On-Surface | #1A1C16                  |
| Error      | #BA1A1A                  |
| Success    | #4C662B                  |
