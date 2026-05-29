# SPEC — User Profile

| Field         | Value              |
|---------------|--------------------|
| Feature       | profile            |
| Flavor        | shared             |
| Status        | approved           |
| Quality Score | 99                 |
| ViewModel     | ProfileViewModel   |

---

## Overview

The User Profile screen is a shared feature accessible from both Consumer and Field Officer personas via the top app bar profile icon or the Profile nav item. It allows the authenticated user to view and edit their personal information (full name, email address, phone number), upload or change their profile avatar, and navigate to the Change Password screen. A danger-zone card at the bottom provides a Log Out button that clears the session token and redirects to Login.

Profile data is pre-filled from `GET /obp/v4.0.0/users/current` on load. On save, `PUT /obp/v4.0.0/users/current` is called with the updated fields. The Save Changes button is enabled only when `hasUnsavedChanges` is true and the form state is Editing. After a successful save, a green success banner is displayed for 2 seconds before auto-transitioning back to the Viewing state.

---

## Screens

| ID      | Name    | Route | Layout | Scroll   |
|---------|---------|-------|--------|----------|
| profile | Profile | —     | Column | Vertical |

**Shell:** Top app bar ("Profile", back arrow). No bottom navigation bar.

---

## Components

| ID                          | Type   | Description                                                                                      |
|-----------------------------|--------|--------------------------------------------------------------------------------------------------|
| profile_root                | stack  | Column root, #F9FAEF bg, 24dp padding                                                           |
| profile_avatar_section      | stack  | Centred column — avatar image + edit icon overlay + display name                                |
| profile_avatar_image        | image  | Circle avatar, 96dp, #4C662B border 2dp, #CDEDA3 bg; data-driven from `obp_get_user_profile.avatar_url` |
| profile_avatar_edit_icon    | icon   | edit_photo icon — 28dp, bg #4C662B, color #FFFFFF; overlaid offset (x:32dp, y:-16dp); opens photo picker |
| profile_display_name        | text   | "Maria Santos" — Outfit/headline_small, #4C662B, centred; data-driven from `username`           |
| profile_form_section        | stack  | White card (radius 12, 24dp padding) — Personal Information section                             |
| profile_section_header      | text   | "Personal Information" — Outfit/title_medium, #4C662B, 16dp bottom padding                     |
| profile_full_name_input     | input  | "Full Name" — text variant, bg #F9FAEF, border #C5C8BA → focused #4C662B; pre-filled from `username`; placeholder "e.g. Maria Santos" |
| profile_email_input         | input  | "Email Address" — email variant, keyboard_type email; pre-filled from `email`; placeholder "e.g. maria.santos@example.com" |
| profile_phone_input         | input  | "Phone Number" — tel variant, keyboard_type tel; pre-filled from `phone_number`; placeholder "e.g. +63 917 123 4567" |
| profile_action_section      | stack  | Column with Save Changes + Change Password buttons                                               |
| profile_save_button         | button | "Save Changes" — filled, bg #4C662B, text #FFFFFF, radius 8, full width; enabled when hasUnsavedChanges=true AND state≠Viewing; shows spinner when Saving |
| profile_change_password_button | button | "Change Password" — outlined, border+text #4C662B, radius 8, full width; navigates to change-password |
| profile_danger_section      | stack  | White card (radius 12, 24dp padding, 16dp margin-top) — danger zone                            |
| profile_logout_button       | button | "Log Out" — text variant, color #BA1A1A, Outfit/label_large, full width; clears session → login |
| profile_save_success_banner | card   | #CDEDA3 bg, #4C662B border, radius 8 — visible when uiState==Saved; check_circle icon + success text |
| profile_success_icon        | icon   | check_circle, 20dp, color #4C662B                                                               |
| profile_success_message     | text   | "Your profile has been updated successfully." — Outfit/body_small, #4C662B                     |

---

## States

| ID      | Trigger                                  | Description                                                                       |
|---------|------------------------------------------|-----------------------------------------------------------------------------------|
| loading | Screen entry — profile data being fetched| Skeleton shimmer on avatar, display name, and all 3 input fields                  |
| viewing | Profile data loaded, no edits made       | All fields pre-filled; Save Changes button disabled                               |
| editing | User modifies any input field            | Fields editable; Save Changes button enabled; hasUnsavedChanges=true              |
| saving  | User taps Save Changes                   | Save button shows spinner; inputs disabled; PUT request in flight                 |
| saved   | PUT request succeeds                     | Success banner visible; auto-transitions to viewing after 2 seconds               |
| content | Alias for viewing (default loaded state) | Same layout as viewing                                                            |
| empty   | No profile data available                | Avatar + actions visible; form fields absent; "No profile data" note             |
| error   | GET /users/current fails                 | Fields may be blank; error state shown with retry option                          |

---

## State Model

**ViewModel:** `ProfileViewModel`
**Screen State Type:** `ProfileUiState`

| Name              | Type    | Default |
|-------------------|---------|---------|
| fullName          | String  | ""      |
| email             | String  | ""      |
| phoneNumber       | String  | ""      |
| avatarUrl         | String? | null    |
| hasUnsavedChanges | Boolean | false   |
| isLoading         | Boolean | false   |
| errorMessage      | String? | null    |

**Events:** `LoadProfile`, `OnFullNameChanged`, `OnEmailChanged`, `OnPhoneChanged`, `OnSaveClicked`, `OnChangePasswordClicked`, `OnLogoutClicked`, `OnProfileSaved`, `OnProfileError`

**DI Dependencies:** `ObpAuthRepository`, `UserProfileRepository`, `SessionManager`

**Errors:**
- `NETWORK_ERROR`: "Could not load your profile. Please check your connection."
- `VALIDATION_ERROR`: "Please correct the errors in the form before saving."
- `AUTH_ERROR`: "Session expired. Please sign in again."

---

## Navigation

| From    | To              | Trigger                          | Type  |
|---------|-----------------|----------------------------------|-------|
| profile | change-password | Change Password button tap       | push  |
| profile | login           | Log Out button tap (after confirm)| root |
| profile | (back)          | Back arrow tap                   | pop   |

---

## API Endpoints

| Endpoint                            | Auth        | Tag         | Purpose                                      |
|-------------------------------------|-------------|-------------|----------------------------------------------|
| GET /obp/v4.0.0/users/current       | DirectLogin | UserProfile | Fetch current user profile for pre-fill      |
| PUT /obp/v4.0.0/users/current       | DirectLogin | UserProfile | Save updated email and phone_number          |

---

## Design Tokens

| Token                           | Value   | Usage                                                           |
|---------------------------------|---------|-----------------------------------------------------------------|
| colors.light.primary            | #4C662B | Avatar border, display name, section headers, Save button bg, edit icon bg, success banner border/icon/text |
| colors.light.primary_container  | #CDEDA3 | Avatar placeholder background, success banner background       |
| colors.light.on_primary         | #FFFFFF | Save button text, edit icon color                              |
| colors.light.error              | #BA1A1A | Log Out button text                                            |
| colors.light.surface            | #FFFFFF | Form section card, danger section card                         |
| colors.light.background         | #F9FAEF | Screen root bg, input field backgrounds                        |
| colors.light.outline_variant    | #C5C8BA | Input field default border                                     |
| colors.light.outline            | #75796C | Change Password outlined button border                         |
| colors.light.on_surface_variant | #44483D | (secondary text)                                               |
| typography.headline_small       | —       | Display name below avatar (24sp, SemiBold)                     |
| typography.title_medium         | —       | "Personal Information" section header                          |
| typography.body_large           | —       | Input field values                                             |
| typography.body_small           | —       | Success banner message                                         |
| typography.label_large          | —       | Save Changes, Change Password, Log Out button text             |
| radius.md                       | 12dp    | Form section card, danger section card, success banner         |
| spacing.lg                      | 24dp    | Root padding, form card padding                                |
| spacing.md                      | 16dp    | Input bottom margin, section header bottom padding             |
| spacing.sm                      | 8dp     | Save button bottom margin                                      |

---

_Generated by /idea export | 2026-05-29_
