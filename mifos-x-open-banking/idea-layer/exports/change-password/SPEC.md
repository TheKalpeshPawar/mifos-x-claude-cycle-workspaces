# SPEC — Change Password

| Field         | Value                    |
|---------------|--------------------------|
| Feature       | change-password          |
| Flavor        | shared                   |
| Status        | approved                 |
| Quality Score | 95                       |
| ViewModel     | ChangePasswordViewModel  |

---

## Overview

The Change Password screen allows both Consumer and Field Officer users to update their account password from within the app. It presents a single-page form (no bottom navigation, top app bar with back arrow) containing three password fields — Current Password, New Password, and Confirm New Password — a real-time password strength indicator, contextual feedback banners, and a primary "Update Password" action button. Validation occurs on submit: the current password must match the server-side value, the new password must reach a minimum strength threshold, and both new password fields must match. On success, a green banner is shown and the user is auto-navigated back to the Profile screen after 2 seconds. On API error, a red banner describes the failure without clearing the form.

---

## Screens

| ID              | Name              | Route            | Layout | Scroll   |
|-----------------|-------------------|------------------|--------|----------|
| change-password | Change Password   | /change-password | Column | Vertical |

**Shell:** Top app bar ("Change Password", back arrow → Profile). No bottom navigation bar.

---

## Components

| ID                          | Type         | Description                                                                                          |
|-----------------------------|--------------|------------------------------------------------------------------------------------------------------|
| chpw_root                   | stack        | Root column; background `#F9FAEF`; padding `spacing.lg` (24dp)                                      |
| chpw_header_section         | stack        | Column; padding-bottom `spacing.xl` (32dp)                                                          |
| chpw_header_title           | text         | "Update Your Password" — `headline_small` (24sp/SemiBold), color `#4C662B`                          |
| chpw_header_subtitle        | text         | "Choose a strong password that you don't use elsewhere." — `body_medium` (14sp), color `#44483D`    |
| chpw_form_card              | card         | White card (`#FFFFFF`); border-radius 12dp; padding `spacing.md` (16dp); margin-bottom `spacing.md` |
| chpw_current_password_input | input        | Label "Current Password"; placeholder "Enter your current password"; password variant; border `#C5C8BA`; focused `#4C662B`; error `#BA1A1A` |
| chpw_divider_1              | divider      | Color `#E1E4D5`; separates current and new password fields                                           |
| chpw_new_password_input     | input        | Label "New Password"; placeholder "At least 8 characters"; password variant; triggers strength update on each keystroke |
| chpw_strength_indicator     | stack        | Column container for strength bar + label                                                            |
| chpw_strength_bar           | progress_bar | Linear bar 4dp height; color_low `#BA1A1A` / color_medium `#F4B400` / color_high `#4C662B`; driven by `passwordStrengthProgress` (0–1) |
| chpw_strength_label         | text         | "Password strength: Good" — `body_small` (12sp), color `#44483D`; driven by `passwordStrengthLabel` (Weak / Fair / Good / Strong) |
| chpw_divider_2              | divider      | Color `#E1E4D5`; separates new and confirm fields                                                    |
| chpw_confirm_password_input | input        | Label "Confirm New Password"; placeholder "Re-enter your new password"; password variant; IME action: done |
| chpw_error_banner           | banner       | "Password change failed. Please check your current password and try again." — background `#FFDAD6`; text `#BA1A1A`; 8dp radius; visible in `error` state |
| chpw_success_banner         | banner       | "Your password has been changed successfully." — background `#D8EED0`; text `#4C662B`; 8dp radius; visible in `success` state |
| chpw_submit_button          | button       | "Update Password" — filled; background `#4C662B`; white text; `label_large`; 12dp radius; loading spinner in `submitting` state |

---

## States

| ID         | Trigger                                     | Description                                                                |
|------------|---------------------------------------------|----------------------------------------------------------------------------|
| loading    | Screen entry — auth session validation      | Header visible; brief skeleton while local auth resolves; transitions immediately to `idle` |
| idle       | Default after load                          | Header + form card + submit button visible; all fields empty               |
| submitting | `OnSubmitClicked` while form is valid       | Submit button shows loading spinner; all fields disabled                   |
| success    | API returns 200 OK                          | Success banner visible; form card hidden; auto-navigate to profile after 2s |
| error      | API returns 400/401 or network failure      | Error banner + form card + submit button visible; user can correct and retry |
| content    | Alias for `idle`                            | Header + form card + submit button                                         |
| empty      | Session invalid / endpoint unavailable      | Header only; empty state with `lock_reset` icon and "Password change unavailable. Please try again later." |

---

## State Model

**ViewModel:** `ChangePasswordViewModel`
**Screen State Type:** `ChangePasswordUiState`

| Name                     | Type    | Default              |
|--------------------------|---------|----------------------|
| currentPassword          | String  | `""`                 |
| newPassword              | String  | `""`                 |
| confirmPassword          | String  | `""`                 |
| passwordStrengthProgress | Float   | `0f`                 |
| passwordStrengthLabel    | String  | `"Enter a password"` |
| isSubmitting             | Boolean | `false`              |
| errorMessage             | String? | `null`               |
| isSuccess                | Boolean | `false`              |

**Events:** `OnCurrentPasswordChanged`, `OnNewPasswordChanged`, `OnConfirmPasswordChanged`, `OnSubmitClicked`

**Actions:**
- `onCurrentPasswordChanged(value: String)` — updates `currentPassword`
- `onNewPasswordChanged(value: String)` — updates `newPassword`; triggers `PasswordStrengthEvaluator`
- `onConfirmPasswordChanged(value: String)` — updates `confirmPassword`
- `onSubmitClicked()` — validates then calls `PUT /obp/v5.0.0/users/{userId}/password`

**DI Dependencies:** `AuthRepository`, `PasswordStrengthEvaluator`

**Errors:**
- `WRONG_CURRENT_PASSWORD`: "Password change failed. Please check your current password and try again."
- `PASSWORDS_DO_NOT_MATCH`: "New passwords do not match. Please re-enter."
- `WEAK_PASSWORD`: "Your new password is too weak. Please choose a stronger one."
- `NETWORK_ERROR`: "Could not connect. Please check your connection and try again."

---

## Navigation

| From            | To       | Trigger                                | Type       |
|-----------------|----------|----------------------------------------|------------|
| change-password | profile  | Back arrow in top app bar              | pop        |
| change-password | profile  | `success` state — auto after 2 seconds | pop (auto) |

---

## API Endpoints

| Endpoint                                | Auth        | Tag   | Purpose                                     |
|-----------------------------------------|-------------|-------|---------------------------------------------|
| PUT /obp/v5.0.0/users/{userId}/password | DirectLogin | Users | Update authenticated user's account password |

---

## Design Tokens

| Token                          | Value   | Usage                                                                     |
|--------------------------------|---------|---------------------------------------------------------------------------|
| color.light.primary            | #4C662B | Header title, focused field border, strength bar high, submit button bg, success banner text |
| color.light.background         | #F9FAEF | Screen background                                                         |
| color.light.surface            | #FFFFFF | Form card background                                                      |
| color.light.on_surface_variant | #44483D | Header subtitle text, strength label text                                 |
| color.light.outline_variant    | #C5C8BA | Default input border, dividers                                            |
| color.light.error              | #BA1A1A | Error banner text, error field border, strength bar low fill              |
| color.light.error_container    | #FFDAD6 | Error banner background                                                   |
| color.semantic.success_bg      | #D8EED0 | Success banner background                                                 |
| color.semantic.strength_medium | #F4B400 | Strength bar medium fill                                                  |
| color.light.surface_variant    | #E1E4D5 | Divider color, strength bar track background                              |
| typography.headline_small      | —       | "Update Your Password" header title (24sp/SemiBold)                       |
| typography.body_medium         | —       | Header subtitle, input values (14sp)                                      |
| typography.body_small          | —       | Password strength label (12sp)                                            |
| typography.label_large         | —       | Submit button text (14sp/Medium)                                          |
| spacing.lg                     | 24dp    | Root column padding                                                       |
| spacing.xl                     | 32dp    | Header section bottom padding                                             |
| spacing.md                     | 16dp    | Card padding, margin-bottom                                               |
| radius.md                      | 12dp    | Form card and submit button border-radius                                 |
| radius.sm                      | 8dp     | Banner border-radius                                                      |

---

_Generated by /idea export | 2026-05-29_
