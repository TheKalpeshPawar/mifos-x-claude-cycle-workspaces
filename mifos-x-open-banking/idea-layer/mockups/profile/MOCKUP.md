# MOCKUP — User Profile

| Field   | Value   |
|---------|---------|
| Feature | profile |
| Flavor  | shared  |

---

## Screen Layout

The profile screen is a scrollable column on a light grey background (#F5F5F5), padded spacing.lg (24 dp) on all sides. It is divided into four distinct visual sections from top to bottom:

1. **Avatar section** — centered column with circular avatar, overlaid edit icon, and display name
2. **Personal Information card** — white card with three editable input fields
3. **Action section** — Save Changes (filled) + Change Password (outlined) buttons
4. **Danger section** — white card containing the Log Out text button

---

## Components

### profile_avatar_section
- **Description:** Centered column containing the user's avatar, an edit badge, and their display name
- **Position:** Top of screen, below top app bar
- **Style tokens:** alignment=center, padding-bottom spacing.xl (32 dp)

### profile_avatar_image
- **Description:** Circular portrait image `user_avatar_placeholder`; falls back to initials on placeholder background when no `avatarUrl` is set
- **Position:** Center-aligned in avatar section
- **Style tokens:** width/height 96 dp, border-color #1800B1, border-width 2 dp, background #E8EAF6 (placeholder)
- **Accessibility:** role=image, label="Your profile photo"

### profile_avatar_edit_icon
- **Description:** Circular badge icon `edit_photo` overlaid at the bottom-right of the avatar; tapping opens the photo picker
- **Position:** Offset { x: 32 dp, y: -16 dp } relative to avatar bottom-right corner
- **Style tokens:** background #1800B1, icon color #FFFFFF, size 28 dp
- **Accessibility:** role=button, label="Change profile photo"

### profile_display_name
- **Description:** Current user's full name rendered from `ProfileUiState.fullName`; sample value "Maria Santos"
- **Position:** Below avatar image; padding-top spacing.sm (8 dp)
- **Style tokens:** Inter/headline_small (24 sp), color #1800B1, alignment=center

### profile_form_section
- **Description:** White card with rounded corners containing Personal Information section header and three input fields
- **Style tokens:** background #FFFFFF, border-radius 12 dp, padding spacing.lg, margin-bottom spacing.md

### profile_section_header
- **Content:** "Personal Information"
- **Style tokens:** Inter/title_medium (16 sp, weight 500), color #1800B1, padding-bottom spacing.md

### profile_full_name_input
- **Description:** Outlined text field, label "Full Name", placeholder "e.g. Maria Santos"; pre-filled from `ProfileUiState.fullName`
- **Style tokens:** background #F5F5F5, Manrope/body_large, border #BDBDBD (rest) / #1800B1 (focused), margin-bottom spacing.md
- **Behavior:** keyboard_type=text, ime_action=next

### profile_email_input
- **Description:** Email-type field, label "Email Address", placeholder "e.g. maria.santos@example.com"; pre-filled from `ProfileUiState.email`
- **Style tokens:** Same as full name input
- **Behavior:** keyboard_type=email, ime_action=next; validated against RFC-5322 on save

### profile_phone_input
- **Description:** Tel-type field, label "Phone Number", placeholder "e.g. +63 917 123 4567"; pre-filled from `ProfileUiState.phoneNumber`
- **Style tokens:** Same as other inputs (no margin-bottom — last field in card)
- **Behavior:** keyboard_type=tel, ime_action=done; validated for E.164 format on save

### profile_save_button
- **Description:** Full-width filled button "Save Changes"
- **Style tokens:** background #1800B1, text #FFFFFF, Inter/label_large, border-radius 8 dp, margin-bottom spacing.sm
- **Behavior:** Disabled when `uiState==Viewing` or `!hasUnsavedChanges`; shows loading spinner when `uiState==Saving`

### profile_change_password_button
- **Description:** Full-width outlined button "Change Password"
- **Style tokens:** border #1800B1, text #1800B1, Inter/label_large, border-radius 8 dp

### profile_save_success_banner
- **Description:** Green confirmation card visible only in `saved` state
- **Position:** Top of scroll content, above avatar section, when visible
- **Style tokens:** background #E8F5E9, border #4CAF50, border-radius 8 dp, padding spacing.md
- **Content:** check_circle icon (#4CAF50, 20 dp) + "Your profile has been updated successfully." (Manrope/body_small, #1B5E20)
- **Behavior:** Auto-transitions to `viewing` state after 2 seconds

### profile_danger_section
- **Description:** White card at the bottom of the form, visually isolated from the action section by margin-top
- **Style tokens:** background #FFFFFF, border-radius 12 dp, padding spacing.lg, margin-top spacing.md
- **Contents:** `profile_logout_button` only

### profile_logout_button
- **Description:** Full-width text-variant button "Log Out"
- **Style tokens:** Inter/label_large, color #FF5252 (danger red), padding spacing.md
- **Behavior:** Clears session token via `SessionManager`, navigates to login

---

## Interaction Patterns

| Element                      | Gesture | Outcome                                                              |
|------------------------------|---------|----------------------------------------------------------------------|
| profile_avatar_edit_icon     | Tap     | Opens system photo picker (ACTION_PICK intent)                       |
| profile_full_name_input      | Focus   | Border turns #1800B1; sets `hasUnsavedChanges=true` on text change  |
| profile_email_input          | Focus   | Border turns #1800B1; sets `hasUnsavedChanges=true` on text change  |
| profile_phone_input          | Focus   | Border turns #1800B1; sets `hasUnsavedChanges=true` on text change  |
| profile_save_button          | Tap     | Fires `onSaveClicked()`; transitions to `saving` state              |
| profile_change_password_button| Tap    | Navigates to `change-password` screen                               |
| profile_logout_button        | Tap     | Shows confirmation dialog → `onLogoutClicked()` → navigate to login |
| profile_save_success_banner  | Auto   | Auto-dismisses after 2 s; screen transitions to `viewing`           |

**State transitions:**
- `viewing` → `editing` when any input value changes
- `editing` → `saving` on Save tapped
- `saving` → `saved` on API success
- `saving` → `error` on API failure
- `saved` → `viewing` after 2 s auto-timeout

---

## Content Data

| Component              | Sample Content Value                                   |
|------------------------|--------------------------------------------------------|
| profile_display_name   | "Maria Santos"                                         |
| profile_full_name_input| prefill: "Maria Santos" (from ProfileUiState.fullName) |
| profile_email_input    | prefill: "maria.santos@example.com" (from state)      |
| profile_phone_input    | prefill: "+63 917 123 4567" (from state)              |
| profile_success_message| "Your profile has been updated successfully."          |
| profile_section_header | "Personal Information"                                 |
| profile_save_button    | "Save Changes"                                         |
| profile_change_password| "Change Password"                                      |
| profile_logout_button  | "Log Out"                                              |

---

## Design Notes

**Color usage:**
- Primary #1800B1 applied to avatar border, display name, section headers, focused input borders, and Save button — the entire "identity and action" layer uses brand purple.
- #FF5252 (error/danger red) exclusively for Log Out — creates an unmistakable visual signal for a destructive action without requiring a dialog prompt for recognition.
- Success triad: #E8F5E9 (background) / #4CAF50 (border + icon) / #1B5E20 (text) — green spectrum, unambiguous confirmation.
- Placeholder avatar background #E8EAF6 (light indigo) is a tinted variant of primary that gives initials-based fallbacks brand coherence.

**Typography:**
- headline_small (Inter, 24 sp) for the display name — prominent but subordinate to the avatar image in visual weight.
- title_medium (Inter, 16 sp, 500 weight) for section headers — clear structural wayfinding without competing with the form content.
- body_large (Manrope, 16 sp) in inputs for maximum legibility of personal data at default font sizes.
- label_large (Inter, 14 sp, 500 weight) for button labels — uniform with the design system button spec.

**Spacing:**
- Avatar section padding-bottom spacing.xl (32 dp) creates a clear visual break between avatar identity block and the form card.
- White cards use border-radius 12 dp, consistent with the MD3 large-component shape spec.
- margin-top spacing.md (16 dp) above the danger section creates spatial isolation from the main action buttons.

**Accessibility:**
- Edit icon on avatar carries `role=button` with explicit label "Change profile photo" — the small 28 dp visual size is compensated by a touch-target expansion to 48 dp.
- Success banner message carries `role=alert` so TalkBack announces the confirmation automatically.
- All three inputs carry role=textbox with descriptive labels including the field name.
- Log Out button color #FF5252 meets 4.5:1 contrast ratio against the white card background.

---

_Generated by /idea export | 2026-05-25_
