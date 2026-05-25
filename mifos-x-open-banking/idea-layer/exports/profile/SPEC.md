# SPEC — User Profile

| Field         | Value            |
|---------------|------------------|
| Feature       | profile          |
| Flavor        | shared           |
| Status        | enriched         |
| Quality Score | 78               |
| ViewModel     | ProfileViewModel |

---

## Overview

The Profile screen allows authenticated users to view and edit their personal information (full name, email address, phone number) and manage their account avatar. It loads current profile data from `GET /obp/v4.0.0/users/current` on entry and persists changes via `PUT /obp/v4.0.0/users/current`. A danger-zone section provides quick access to logout. A success banner confirms saves; an error state surfaces API failures inline.

---

## Screens

| ID      | Name    | Route    | Layout | Scroll   |
|---------|---------|----------|--------|----------|
| profile | Profile | /profile | Column | Vertical |

---

## Components

| ID                          | Type   | Description                                                                          |
|-----------------------------|--------|--------------------------------------------------------------------------------------|
| profile_root                | stack  | Full-screen column, background #F5F5F5, padding spacing.lg                          |
| profile_avatar_section      | stack  | Centered column: avatar image + edit icon overlay + display name                    |
| profile_avatar_image        | image  | Circular avatar 96×96 dp, border #1800B1 2 dp, fallback to initials on #E8EAF6     |
| profile_avatar_edit_icon    | icon   | edit_photo, 28 dp, background #1800B1, color #FFFFFF; overlaid on avatar bottom-right|
| profile_display_name        | text   | "Maria Santos", headline_small, color #1800B1, centered; data-driven from state     |
| profile_form_section        | stack  | White card, border-radius 12 dp: section header + 3 input fields                   |
| profile_section_header      | text   | "Personal Information", title_medium, color #1800B1                                 |
| profile_full_name_input     | input  | Text field "Full Name"; prefill=fullName; ime_action=next                           |
| profile_email_input         | input  | Email field "Email Address"; prefill=email; validated RFC-5322; ime_action=next     |
| profile_phone_input         | input  | Tel field "Phone Number"; prefill=phoneNumber; E.164 format; ime_action=done        |
| profile_action_section      | stack  | Column: Save Changes button + Change Password button                                |
| profile_save_button         | button | "Save Changes", filled, #1800B1; disabled when no unsaved changes; loading on Saving|
| profile_change_password_button| button| "Change Password", outlined, border/text #1800B1; navigates to change-password     |
| profile_danger_section      | stack  | White card, border-radius 12 dp: Log Out button                                    |
| profile_logout_button       | button | "Log Out", text variant, color #FF5252; clears session + navigates to login         |
| profile_save_success_banner | card   | Green success banner; visible_when uiState==Saved; auto-hides after 2 s            |
| profile_success_icon        | icon   | check_circle, 20 dp, color #4CAF50                                                 |
| profile_success_message     | text   | "Your profile has been updated successfully.", body_small, color #1B5E20           |

---

## States

| ID      | Trigger                          | Description                                                                  |
|---------|----------------------------------|------------------------------------------------------------------------------|
| viewing | Screen load complete             | Fields read-only; Save button disabled; profile data populated               |
| editing | User modifies any input field    | Fields editable; Save button enabled; hasUnsavedChanges=true                 |
| saving  | Save Changes tapped              | Save button shows loading spinner; all inputs disabled                       |
| saved   | PUT API success                  | Success banner visible; auto-transitions to viewing after 2 s               |
| error   | API failure on load or save      | Error message shown (toast or inline); inputs remain editable for retry     |

---

## State Model

**ViewModel:** `ProfileViewModel`
**Screen State Type:** `ProfileUiState`

| Field             | Type    | Default |
|-------------------|---------|---------|
| fullName          | String  | ""      |
| email             | String  | ""      |
| phoneNumber       | String  | ""      |
| avatarUrl         | String? | null    |
| hasUnsavedChanges | Boolean | false   |
| isLoading         | Boolean | false   |
| errorMessage      | String? | null    |

**Events:** `LoadProfile`, `OnFullNameChanged`, `OnEmailChanged`, `OnPhoneChanged`, `OnSaveClicked`, `OnChangePasswordClicked`, `OnLogoutClicked`, `OnProfileSaved`, `OnProfileError`

**Actions:** `onLoadProfile()`, `onFullNameChanged(value: String)`, `onEmailChanged(value: String)`, `onPhoneChanged(value: String)`, `onSaveClicked()`, `onChangePasswordClicked()`, `onLogoutClicked()`

**DI Dependencies:** `ObpAuthRepository`, `UserProfileRepository`, `SessionManager`

**Errors:** `NETWORK_ERROR`, `VALIDATION_ERROR`, `AUTH_ERROR`

---

## Navigation

| ID                    | From    | To              | Trigger              |
|-----------------------|---------|-----------------|----------------------|
| nav_to_change_password| profile | change-password | Change Password tap  |
| nav_to_login_on_logout| profile | login           | on_logout_confirmed  |

---

## API Endpoints

| ID                    | Endpoint                           | Auth         | Purpose                               |
|-----------------------|------------------------------------|--------------|---------------------------------------|
| obp_get_user_profile  | GET /obp/v4.0.0/users/current      | DirectLogin  | Load current user profile on screen entry |
| obp_update_user_profile| PUT /obp/v4.0.0/users/current     | DirectLogin  | Persist edited profile fields         |

---

## Design Tokens

| Token                       | Value     | Usage                                            |
|-----------------------------|-----------|--------------------------------------------------|
| color.light.primary         | #1800B1   | Avatar border, display name, section headers, save button, focused borders |
| color.light.background      | #F5F5F5   | Root and input field backgrounds                |
| color.surface.white         | #FFFFFF   | Form card and danger section backgrounds         |
| color.error.default         | #FF5252   | Log Out button text                              |
| color.success.background    | #E8F5E9   | Success banner background                        |
| color.success.border        | #4CAF50   | Success banner border and icon                   |
| color.success.text          | #1B5E20   | Success message text                             |
| color.avatar.placeholder    | #E8EAF6   | Avatar placeholder background                    |
| typography.headline_small   | Inter/headline_small | Display name                         |
| typography.title_medium     | Inter/title_medium   | Section headers                      |
| typography.body_large       | Manrope/body_large   | Input field text                     |
| typography.label_large      | Inter/label_large    | Button labels                        |
| typography.body_small       | Manrope/body_small   | Success/error messages               |

---

_Generated by /idea export | 2026-05-25_
