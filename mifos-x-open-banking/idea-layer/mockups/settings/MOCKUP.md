# MOCKUP — Settings

| Field   | Value    |
|---------|----------|
| Feature | settings |
| Flavor  | shared   |

---

## Screen Layout

The settings screen is a scrollable column on a light grey background (#F5F5F5), padded spacing.lg (24 dp) on all sides. It is organized into four white cards stacked vertically:

1. **Appearance card** — Dark Mode toggle row + Language select row
2. **Notifications card** — Push Notifications toggle + Transaction Alerts toggle
3. **Security card** — Biometric Login toggle
4. **About card** — About Mifos X link + App Version display row

Each card uses border-radius 12 dp, padding spacing.md (16 dp), and margin-bottom spacing.md, separated by the grey background gap between cards.

---

## Components

### Appearance Card

**settings_appearance_group**
- White card (#FFFFFF), border-radius 12 dp, padding 16 dp, margin-bottom 16 dp

**settings_appearance_header**
- Content: "Appearance"
- Style: Inter/title_medium (16 sp, 500 weight), color #1800B1, padding-bottom spacing.sm (8 dp), padding-top spacing.lg from outside context

**settings_dark_mode_row**
- Horizontal row: label group (left, flex) + switch (right)
- Label: "Dark Mode" (Manrope/body_large, #212121)
- Description: "Switch to a darker color scheme" (Manrope/body_small, #757575)
- Switch: active track #1800B1 / inactive track #BDBDBD; prefilled from `isDarkModeEnabled`

**settings_divider_1**
- Thin horizontal rule, color #E0E0E0, margin-top and margin-bottom spacing.xs (4 dp)

**settings_language_row**
- Horizontal row: label group (left, flex) + combobox select (right)
- Label: "Language" (Manrope/body_large, #212121)
- Description: "Choose your preferred display language" (Manrope/body_small, #757575)
- Select: min-width 140 dp, options: English / Spanish / French / Hindi / Arabic; prefilled from `selectedLanguage` (default="en")

---

### Notifications Card

**settings_notifications_group**
- White card (#FFFFFF), border-radius 12 dp, padding 16 dp, margin-bottom 16 dp

**settings_notifications_header**
- Content: "Notifications"
- Style: Inter/title_medium, color #1800B1

**settings_push_notifications_row**
- Label: "Push Notifications" (Manrope/body_large, #212121)
- Description: "Receive alerts and updates from Mifos X" (Manrope/body_small, #757575)
- Switch: active #1800B1; prefilled from `isPushNotificationsEnabled` (default=true)

**settings_divider_2**
- Thin horizontal rule, color #E0E0E0

**settings_transaction_alerts_row**
- Label: "Transaction Alerts" (Manrope/body_large, #212121)
- Description: "Notify me for every debit and credit activity" (Manrope/body_small, #757575)
- Switch: active #008B8B (teal accent, differentiates from push notifications toggle); disabled when `!isPushNotificationsEnabled`

---

### Security Card

**settings_security_group**
- White card (#FFFFFF), border-radius 12 dp, padding 16 dp, margin-bottom 16 dp

**settings_security_header**
- Content: "Security"
- Style: Inter/title_medium, color #1800B1

**settings_biometric_row**
- Label: "Biometric Login" (Manrope/body_large, #212121)
- Description: "Use fingerprint or face ID to sign in faster" (Manrope/body_small, #757575)
- Switch: active #1800B1; disabled when `!isBiometricAvailableOnDevice` (device capability check)

---

### About Card

**settings_about_group**
- White card (#FFFFFF), border-radius 12 dp, padding 16 dp, margin-bottom 16 dp

**settings_about_header**
- Content: "About"
- Style: Inter/title_medium, color #1800B1

**settings_about_link_row**
- Horizontal row: "About Mifos X Open Banking" link (Manrope/body_large, #212121, flex) + chevron_right icon (20 dp, #BDBDBD)
- Full row is tappable; navigates to `about` screen

**settings_divider_3**
- Thin horizontal rule, color #E0E0E0

**settings_app_version_row**
- Horizontal row: "App Version" label (Manrope/body_large, #212121) + "v1.0.0" value (Manrope/body_small, #757575)
- Not tappable (display only)

---

## Interaction Patterns

| Element                         | Gesture | Outcome                                                                         |
|---------------------------------|---------|---------------------------------------------------------------------------------|
| settings_dark_mode_toggle       | Toggle  | `onDarkModeToggled()` → DataStore write → app-wide theme recomposition          |
| settings_language_select        | Tap     | Opens dropdown with 5 language options; `onLanguageSelected(language)` → LocaleManager update |
| settings_push_notifications_toggle| Toggle| `onPushNotificationsToggled()` → DataStore; if false, disables transaction alerts switch |
| settings_transaction_alerts_toggle| Toggle| `onTransactionAlertsToggled()` → DataStore; only active when push is enabled   |
| settings_biometric_toggle       | Toggle  | `onBiometricToggled()` → BiometricManager enrollment flow if enabling for first time |
| settings_about_link_row         | Tap     | Navigates to `about` screen                                                     |
| settings_app_version_row        | None    | Display only — no interaction                                                   |

**Cascade behavior:**
- Disabling Push Notifications immediately greys out and disables the Transaction Alerts switch. Re-enabling Push Notifications restores the Transaction Alerts switch to its last persisted state.

**Loading state:**
- On screen entry, skeleton shimmer cards replace all four preference cards while DataStore values are read. Once loaded, the shimmer dissolves (crossfade) and actual preference values are shown.

---

## Content Data

| Component                          | Content Value                                      |
|------------------------------------|----------------------------------------------------|
| settings_appearance_header         | "Appearance"                                       |
| settings_dark_mode_label           | "Dark Mode"                                        |
| settings_dark_mode_description     | "Switch to a darker color scheme"                  |
| settings_language_label            | "Language"                                         |
| settings_language_description      | "Choose your preferred display language"           |
| settings_language_select options   | English (en), Spanish (es), French (fr), Hindi (hi), Arabic (ar) |
| settings_notifications_header      | "Notifications"                                    |
| settings_push_notifications_label  | "Push Notifications"                               |
| settings_push_notifications_desc   | "Receive alerts and updates from Mifos X"          |
| settings_transaction_alerts_label  | "Transaction Alerts"                               |
| settings_transaction_alerts_desc   | "Notify me for every debit and credit activity"    |
| settings_security_header           | "Security"                                         |
| settings_biometric_label           | "Biometric Login"                                  |
| settings_biometric_description     | "Use fingerprint or face ID to sign in faster"     |
| settings_about_header              | "About"                                            |
| settings_about_link                | "About Mifos X Open Banking"                       |
| settings_app_version_label         | "App Version"                                      |
| settings_app_version_value         | "v1.0.0"                                           |

---

## Design Notes

**Color usage:**
- All section headers use #1800B1 — creates consistent visual grouping anchors throughout the scroll.
- Dark mode and biometric switches share the primary #1800B1 active color — both are "primary" security/display preferences.
- Transaction Alerts switch uses #008B8B (accent teal) to visually signal it is a subordinate/conditional toggle, distinct from the master push notifications switch above it.
- #BDBDBD on all inactive switch tracks and the chevron icon provides a uniform "passive/available" visual tone.

**Typography:**
- Consistent Inter/title_medium for all section headers — the 500 weight distinguishes it from row labels without requiring color change.
- Manrope/body_large for row labels provides good legibility in list contexts.
- Manrope/body_small for descriptions creates a clear two-level text hierarchy within each row.

**Spacing:**
- Cards use 12 dp border-radius aligned with the MD3 medium-component shape spec.
- Row padding-top/bottom spacing.sm (8 dp) creates comfortable touch targets while keeping the list dense enough to show multiple settings without excessive scrolling.
- Dividers use spacing.xs (4 dp) top and bottom margins to create minimal visual weight while still providing clear row separation.

**Accessibility:**
- All switch components have role=switch with explicit label strings.
- Transaction alerts switch conveys disabled state through both opacity and `disabled_when` property — screen readers will announce "dimmed" or "unavailable" to communicate the conditional state.
- Language select has role=combobox, allowing screen readers to announce the current selected language and available options.
- Chevron icon on About row has empty label (decorative) — the link label "Navigate to About Mifos X Open Banking" carries the full accessible meaning.
- All row labels in the About section use meaningful non-generic text.

---

_Generated by /idea export | 2026-05-25_
