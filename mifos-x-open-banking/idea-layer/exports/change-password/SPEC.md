# SPEC — Change Password

| Field | Value |
|---|---|
| Feature | change-password |
| Flavor | shared |
| Status | approved |
| Quality | 95 |
| ViewModel | ChangePasswordViewModel |
| Archetype | form |
| Dependencies | shared-core, obp-auth |

## Overview

The Change Password screen allows authenticated users to update their account password through a secure three-field form: current password verification, new password entry with real-time strength evaluation, and confirmation. A live strength indicator (progress bar + label) provides immediate feedback as the user types the new password. On successful submission the screen presents a success banner; on failure an inline error banner surfaces the API error reason. The screen is guarded against unauthenticated access and handles the full error surface of the OBP v7.0.0 password change endpoint.

## Screens

| Screen ID | Display Name | Shell |
|---|---|---|
| change-password/idle | Change Password — Idle | Top app bar "Change Password" + back arrow, no bottom nav |
| change-password/loading | Change Password — Loading | Top app bar "Change Password" + back arrow, no bottom nav |
| change-password/submitting | Change Password — Submitting | Top app bar "Change Password" + back arrow, no bottom nav |
| change-password/success | Change Password — Success | Top app bar "Change Password" + back arrow, no bottom nav |
| change-password/error | Change Password — Error | Top app bar "Change Password" + back arrow, no bottom nav |
| change-password/content | Change Password — Content | Top app bar "Change Password" + back arrow, no bottom nav |
| change-password/empty | Change Password — Empty | Top app bar "Change Password" + back arrow, no bottom nav |

## Components

| Component | Type | States Present | Notes |
|---|---|---|---|
| Header section | text_header | all | Title "Update Your Password", subtitle |
| Form card | card | idle, submitting, error, content | Contains all three password fields |
| Current password field | text_field_password | idle, submitting, error, content | Masked input, show/hide toggle |
| New password field | text_field_password | idle, submitting, error, content | Masked input, show/hide toggle |
| Password strength indicator | progress_indicator + label | idle, submitting, error, content | Float progress (0.0–1.0) + strength label |
| Confirm password field | text_field_password | idle, submitting, error, content | Masked input, show/hide toggle |
| Error banner | banner_error | error | Inline; surfaces API error message |
| Success banner | banner_success | success | Confirms password updated |
| Submit button | button_primary | idle, error, content | Label "Update Password"; disabled during submitting |
| Loading spinner | loading_indicator | loading, submitting | Full-screen on loading; inline on submitting |

## States

| State | Description | Components Visible |
|---|---|---|
| loading | Screen initialising / auth check in progress | Header section, Loading spinner |
| idle | Form ready for input | Header section, Form card, Submit button |
| submitting | API request in-flight; form locked | Header section, Form card (disabled), Loading spinner |
| success | Password updated successfully | Header section, Success banner |
| error | API returned an error | Header section, Error banner, Form card, Submit button |
| content | Alias for idle with pre-populated state context | Header section, Form card, Submit button |
| empty | Password change unavailable (feature flag off / unsupported account type) | Header section (title + "Password change unavailable" message) |

## State Model

```kotlin
data class ChangePasswordUiState(
    val currentPassword: String,
    val newPassword: String,
    val confirmPassword: String,
    val passwordStrengthProgress: Float,       // 0.0 – 1.0
    val passwordStrengthLabel: String,          // e.g. "Weak", "Fair", "Strong"
    val isSubmitting: Boolean,
    val errorMessage: String?,
    val isSuccess: Boolean,
)
```

### Events

| Event | Trigger |
|---|---|
| OnCurrentPasswordChanged | User edits current password field |
| OnNewPasswordChanged | User edits new password field (also triggers strength re-evaluation) |
| OnConfirmPasswordChanged | User edits confirm password field |
| OnSubmitClicked | User taps "Update Password" button |

### Dependency Injection

| Dependency | Role |
|---|---|
| AuthRepository | Calls OBP v7.0.0 password change endpoint |
| PasswordStrengthEvaluator | Computes `passwordStrengthProgress` + `passwordStrengthLabel` on each keystroke |

## Navigation

| Action | Destination | Type |
|---|---|---|
| nav_back_to_profile | profile | Back stack pop to profile screen |
| Back arrow | Previous screen | Back stack pop |

## Dependencies

| Dependency | Purpose |
|---|---|
| shared-core | Common UI primitives, navigation utilities, design tokens |
| obp-auth | AuthRepository wrapping OBP v7.0.0 `/users/current/password` endpoint |

## Design Tokens

| Token | Value |
|---|---|
| Accent color | #4C662B (Earth-green) |
| Typography | Outfit |
| Design system | Material 3 (M3) |
