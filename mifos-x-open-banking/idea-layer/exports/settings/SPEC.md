# SPEC — Settings

| Field         | Value             |
|---------------|-------------------|
| Feature       | settings          |
| Flavor        | shared            |
| Status        | approved          |
| Quality Score | 93                |
| ViewModel     | SettingsViewModel |

---

## Overview

The Settings screen provides user-configurable preferences grouped into four card sections: Appearance (dark mode toggle + language selector), Notifications (push notifications master switch, transaction alerts sub-switch, and marketing updates opt-in), Security (biometric login toggle, Data & Consent link, and Change Password link), and About (About link, Terms of Service / Privacy Policy / Open-source Licences links, and app version display). All preferences are persisted to DataStore via `SettingsRepository` and hydrated on screen entry. The screen makes no OBP API calls. It is reachable via the "More" tab in the consumer bottom navigation and the equivalent tab in the field officer shell. On entry the screen shows a skeleton shimmer while DataStore reads complete.

---

## Screens

| ID       | Name     | Route     | Layout | Scroll   |
|----------|----------|-----------|--------|----------|
| settings | Settings | /settings | Column | Vertical |

**Shell:** Consumer — bottom navigation bar (More tab active). Field Officer — bottom navigation bar (More tab active). No top app bar on this screen (destination-level screen).

| Nav Item | ID        | Icon          | Target   |
|----------|-----------|---------------|----------|
| Home     | nav_home  | home          | home     |
| Accounts | nav_accts | account_balance| accounts|
| Pay      | nav_pay   | send          | send-money|
| Cards    | nav_cards | credit_card   | cards    |
| More     | nav_more  | more_horiz    | settings |

---

## Components

| ID                                   | Type  | Description                                                                                              |
|--------------------------------------|-------|----------------------------------------------------------------------------------------------------------|
| settings_root                        | stack | Full-screen column, background #F9FAEF, padding spacing.lg                                               |
| **Appearance Group**                 |       |                                                                                                          |
| settings_appearance_group            | card  | White card, radius 12dp, pad spacing.md, margin_bottom spacing.md; contains header + dark mode + language|
| settings_appearance_header           | text  | "Appearance" — Outfit/title_medium, color #4C662B; role=heading                                         |
| settings_dark_mode_row               | stack | Row: label group (label + description) + toggle switch                                                   |
| settings_dark_mode_label             | text  | "Dark Mode" — Outfit/body_large, color #1A1C16                                                          |
| settings_dark_mode_description       | text  | "Switch to a darker color scheme" — Outfit/body_small, color #44483D                                    |
| settings_dark_mode_toggle            | input | Switch; active #4C662B, inactive #C5C8BA; prefill=isDarkModeEnabled                                     |
| settings_divider_1                   | divider | #E1E4D5, separates dark mode row from language row                                                     |
| settings_language_row                | stack | Row: label group + language combobox                                                                     |
| settings_language_label              | text  | "Language" — Outfit/body_large, color #1A1C16                                                           |
| settings_language_description        | text  | "Choose your preferred display language" — Outfit/body_small, color #44483D                             |
| settings_language_select             | input | Select/combobox; options: English/Spanish/French/Hindi/Arabic; prefill=selectedLanguage                  |
| **Notifications Group**              |       |                                                                                                          |
| settings_notifications_group         | card  | White card, radius 12dp; contains header + push notifications + transaction alerts + marketing updates   |
| settings_notifications_header        | text  | "Notifications" — Outfit/title_medium, color #4C662B; role=heading                                     |
| settings_push_notifications_row      | stack | Row: label group + push switch                                                                           |
| settings_push_notifications_label    | text  | "Push Notifications" — Outfit/body_large, color #1A1C16                                                 |
| settings_push_notifications_description| text| "Receive alerts and updates from Mifos X" — Outfit/body_small, color #44483D                           |
| settings_push_notifications_toggle  | input | Switch; active #4C662B; prefill=isPushNotificationsEnabled; master toggle                               |
| settings_divider_2                   | divider | #E1E4D5                                                                                               |
| settings_transaction_alerts_row      | stack | Row: label group + alerts switch                                                                         |
| settings_transaction_alerts_label    | text  | "Transaction Alerts" — Outfit/body_large, color #1A1C16                                                 |
| settings_transaction_alerts_description| text| "Notify me for every debit and credit activity" — Outfit/body_small, color #44483D                    |
| settings_transaction_alerts_toggle  | input | Switch; active #386663; disabled when push notifications off; prefill=isTransactionAlertsEnabled        |
| settings_divider_notifications_2     | divider | #E1E4D5, separates transaction alerts from marketing updates                                          |
| settings_marketing_row               | stack | Row: label group (Marketing Updates + description) + marketing switch                                    |
| settings_marketing_label             | text  | "Marketing Updates" — Outfit/body_large, color #1A1C16                                                  |
| settings_marketing_description       | text  | "Product news and promotions" — Outfit/body_small, color #44483D                                       |
| settings_marketing_toggle            | input | Switch; active #4C662B, inactive #C5C8BA; prefill=isMarketingEnabled                                    |
| **Security Group**                   |       |                                                                                                          |
| settings_security_group              | card  | White card, radius 12dp; contains header + biometric + data & consent + change password                 |
| settings_security_header             | text  | "Security" — Outfit/title_medium, color #4C662B; role=heading                                          |
| settings_biometric_row               | stack | Row: label group + biometric switch                                                                      |
| settings_biometric_label             | text  | "Biometric Login" — Outfit/body_large, color #1A1C16                                                   |
| settings_biometric_description       | text  | "Use fingerprint or face ID to sign in faster" — Outfit/body_small, color #44483D                      |
| settings_biometric_toggle            | input | Switch; active #4C662B; disabled when !isBiometricAvailableOnDevice; prefill=isBiometricLoginEnabled    |
| settings_divider_security            | divider | #E1E4D5                                                                                              |
| settings_consent_manager_row         | stack | Row: label group (Data & Consent + description) + chevron_right icon                                    |
| settings_consent_manager_label       | text  | "Data & Consent" — Outfit/body_large, color #1A1C16                                                   |
| settings_consent_manager_description | text  | "Manage your data sharing consents" — Outfit/body_small, color #44483D                                 |
| settings_consent_manager_chevron     | icon  | chevron_right, 20dp, color #C5C8BA; on tap navigates to consent-manager                                 |
| settings_divider_security_2          | divider | #E1E4D5, separates data consent row from change password row                                          |
| settings_change_password_row         | stack | Row: label group (Change Password + description) + chevron_right icon                                   |
| settings_change_password_label       | text  | "Change Password" — Outfit/body_large, color #1A1C16                                                    |
| settings_change_password_description | text  | "Update your account login password" — Outfit/body_small, color #44483D                                |
| settings_change_password_chevron     | icon  | chevron_right, 20dp, color #C5C8BA; on tap navigates to change-password                                 |
| **About Group**                      |       |                                                                                                          |
| settings_about_group                 | card  | White card, radius 12dp; contains header + about link + Terms / Privacy / Licences links + version       |
| settings_about_header                | text  | "About" — Outfit/title_medium, color #4C662B; role=heading                                              |
| settings_about_link_row              | stack | Row: About link + chevron icon                                                                           |
| settings_about_link                  | link  | "About Mifos X Open Banking" — Outfit/body_large, color #1A1C16; navigates to about                    |
| settings_about_chevron               | icon  | chevron_right, 20dp, color #C5C8BA; trailing affordance (non-interactive)                               |
| settings_divider_about_1             | divider | #E1E4D5, separates About link from Terms of Service                                                   |
| settings_terms_row                   | stack | Row: Terms of Service link + chevron icon                                                                |
| settings_terms_link                  | link  | "Terms of Service" — Outfit/body_large, color #1A1C16; navigates to terms-of-service                   |
| settings_terms_chevron               | icon  | chevron_right, 20dp, color #C5C8BA; trailing affordance                                                 |
| settings_divider_about_2             | divider | #E1E4D5, separates Terms of Service from Privacy Policy                                                |
| settings_privacy_row                 | stack | Row: Privacy Policy link + chevron icon                                                                  |
| settings_privacy_link                | link  | "Privacy Policy" — Outfit/body_large, color #1A1C16; navigates to privacy-policy                       |
| settings_privacy_chevron             | icon  | chevron_right, 20dp, color #C5C8BA; trailing affordance                                                 |
| settings_divider_about_3             | divider | #E1E4D5, separates Privacy Policy from Open-source Licences                                            |
| settings_licenses_row                | stack | Row: Open-source Licences link + chevron icon                                                           |
| settings_licenses_link               | link  | "Open-source Licences" — Outfit/body_large, color #1A1C16; navigates to licenses                       |
| settings_licenses_chevron            | icon  | chevron_right, 20dp, color #C5C8BA; trailing affordance                                                 |
| settings_divider_3                   | divider | #E1E4D5                                                                                               |
| settings_app_version_row             | stack | Row: "App Version" label + "v1.0.0" value                                                               |
| settings_app_version_label           | text  | "App Version" — Outfit/body_large, color #1A1C16                                                       |
| settings_app_version_value           | text  | "v1.0.0" — Outfit/body_small, color #44483D; data from BuildConfig.VERSION_NAME                         |

---

## States

| ID      | Trigger                       | Description                                                                    |
|---------|-------------------------------|--------------------------------------------------------------------------------|
| loading | Screen entry                  | Skeleton shimmer on all four card groups while DataStore preferences load      |
| content | DataStore load complete       | All four card sections visible with current preference values pre-filled       |

---

## State Model

**ViewModel:** `SettingsViewModel`
**Screen State Type:** `SettingsUiState`

| Field                        | Type    | Default   |
|------------------------------|---------|-----------|
| isDarkModeEnabled            | Boolean | false     |
| selectedLanguage             | String  | "en"      |
| isPushNotificationsEnabled   | Boolean | true      |
| isTransactionAlertsEnabled   | Boolean | true      |
| isMarketingEnabled           | Boolean | false     |
| isBiometricLoginEnabled      | Boolean | false     |
| isBiometricAvailableOnDevice | Boolean | false     |
| appVersion                   | String  | "v1.0.0"  |
| isLoading                    | Boolean | true      |

**Events:** `LoadSettings`, `OnDarkModeToggled`, `OnLanguageSelected`, `OnPushNotificationsToggled`, `OnTransactionAlertsToggled`, `OnMarketingToggled`, `OnBiometricToggled`, `OnAboutClicked`

**Actions:** `onLoadSettings()`, `onDarkModeToggled()`, `onLanguageSelected(language: String)`, `onPushNotificationsToggled()`, `onTransactionAlertsToggled()`, `onMarketingToggled()`, `onBiometricToggled()`, `onAboutClicked()`

**DI Dependencies:** `SettingsRepository`, `BiometricManager`, `NotificationManager`, `LocaleManager`

**Errors:** `NETWORK_ERROR`

---

## Navigation

| ID                  | From     | To              | Trigger                               |
|---------------------|----------|-----------------|---------------------------------------|
| nav_to_about        | settings | about           | settings_about_link or chevron tapped |
| nav_to_consent_manager | settings | consent-manager | settings_consent_manager_chevron tapped |
| nav_to_change_password | settings | change-password | settings_change_password_chevron tapped |
| nav_to_terms_of_service | settings | terms-of-service | settings_terms_link tapped |
| nav_to_privacy_policy | settings | privacy-policy | settings_privacy_link tapped |
| nav_to_licenses | settings | licenses | settings_licenses_link tapped |

---

## API Endpoints

_No backend API dependencies — static/local screen._

All data is read/written via local `SettingsRepository` (Jetpack DataStore). No HTTP requests are issued from this screen.

---

## Design Tokens

| Token                           | Value     | Usage                                                                    |
|---------------------------------|-----------|--------------------------------------------------------------------------|
| colors.light.primary            | #4C662B   | All four section header texts; dark mode, push, biometric switch active  |
| colors.light.secondary          | #386663   | Transaction alerts switch active color                                   |
| colors.light.background         | #F9FAEF   | settings_root background                                                 |
| colors.light.surface            | #FFFFFF   | All four card group backgrounds                                           |
| colors.light.on_surface         | #1A1C16   | All preference row primary labels and link text                          |
| colors.light.on_surface_variant | #44483D   | All preference row description texts; app version value                  |
| colors.light.surface_variant    | #E1E4D5   | Divider colors between rows                                              |
| colors.light.outline_variant    | #C5C8BA   | Switch inactive color; chevron icon color; language select border        |
| typography.title_medium         | 16sp/500  | All four section headers                                                 |
| typography.body_large           | 16sp/400  | All preference row primary labels                                        |
| typography.body_small           | 12sp/400  | All preference row descriptions; app version value                       |
| typography.body_medium          | 14sp/400  | Language select dropdown text                                            |
| radius.md                       | 12dp      | All four card group corner radius                                        |
| spacing.lg                      | 24dp      | Root column padding; appearance header padding-top                       |
| spacing.md                      | 16dp      | Card internal padding                                                    |
| spacing.sm                      | 8dp       | Row padding-top/bottom; section header padding-bottom                    |
| spacing.xs                      | 4dp       | Divider vertical margins                                                 |

---

_Generated by /idea export | 2026-06-03_
