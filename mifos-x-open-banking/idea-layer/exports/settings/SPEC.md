# SPEC — Settings

| Field         | Value             |
|---------------|-------------------|
| Feature       | settings          |
| Flavor        | shared            |
| Status        | enriched          |
| Quality Score | 78                |
| ViewModel     | SettingsViewModel |

---

## Overview

The Settings screen exposes user-configurable preferences across four grouped sections: Appearance (dark mode + language), Notifications (push notifications + transaction alerts), Security (biometric login), and About (app version + About link). All preferences are persisted to DataStore and hydrated on screen entry. The Settings screen has no direct OBP API calls — it reads and writes local preferences only, delegating to platform managers (BiometricManager, NotificationManager, LocaleManager).

---

## Screens

| ID       | Name     | Route     | Layout | Scroll   |
|----------|----------|-----------|--------|----------|
| settings | Settings | /settings | Column | Vertical |

---

## Components

| ID                              | Type   | Description                                                                            |
|---------------------------------|--------|----------------------------------------------------------------------------------------|
| settings_root                   | stack  | Full-screen column, background #F5F5F5, padding spacing.lg                            |
| settings_appearance_group       | card   | White card, border-radius 12 dp; contains Appearance section header + dark mode + language rows |
| settings_appearance_header      | text   | "Appearance", title_medium, color #1800B1                                             |
| settings_dark_mode_row          | stack  | Row: label group (label + description) + dark mode switch                             |
| settings_dark_mode_label        | text   | "Dark Mode", body_large, color #212121                                                |
| settings_dark_mode_description  | text   | "Switch to a darker color scheme", body_small, color #757575                          |
| settings_dark_mode_toggle       | input  | Switch variant; active color #1800B1, inactive #BDBDBD; prefill=isDarkModeEnabled     |
| settings_language_row           | stack  | Row: label group + language select dropdown                                            |
| settings_language_label         | text   | "Language", body_large, color #212121                                                 |
| settings_language_description   | text   | "Choose your preferred display language", body_small, color #757575                   |
| settings_language_select        | input  | Select/combobox with options: English, Spanish, French, Hindi, Arabic                  |
| settings_notifications_group    | card   | White card; contains Notifications header + push notifications + transaction alerts    |
| settings_notifications_header   | text   | "Notifications", title_medium, color #1800B1                                          |
| settings_push_notifications_toggle| input| Switch; active #1800B1; prefill=isPushNotificationsEnabled; master toggle              |
| settings_transaction_alerts_toggle| input| Switch; active #008B8B; disabled when push notifications off; prefill=isTransactionAlertsEnabled |
| settings_security_group         | card   | White card; contains Security header + biometric row                                   |
| settings_security_header        | text   | "Security", title_medium, color #1800B1                                               |
| settings_biometric_toggle       | input  | Switch; active #1800B1; disabled when device has no biometric HW; prefill=isBiometricLoginEnabled |
| settings_about_group            | card   | White card; contains About header + About link row + divider + app version row        |
| settings_about_header           | text   | "About", title_medium, color #1800B1                                                  |
| settings_about_link             | link   | "About Mifos X Open Banking", body_large, color #212121; navigates to about screen    |
| settings_about_chevron          | icon   | chevron_right, 20 dp, color #BDBDBD; trailing affordance on About row                 |
| settings_app_version_label      | text   | "App Version", body_large, color #212121                                              |
| settings_app_version_value      | text   | "v1.0.0", body_small, color #757575; data from BuildConfig.VERSION_NAME              |

---

## States

| ID      | Trigger                    | Description                                                               |
|---------|----------------------------|---------------------------------------------------------------------------|
| loading | Screen entry               | Skeleton shimmer shown while preferences load from DataStore              |
| content | DataStore load complete    | All preference cards visible with current values pre-filled               |

---

## State Model

**ViewModel:** `SettingsViewModel`
**Screen State Type:** `SettingsUiState`

| Field                       | Type    | Default  |
|-----------------------------|---------|----------|
| isDarkModeEnabled           | Boolean | false    |
| selectedLanguage            | String  | "en"     |
| isPushNotificationsEnabled  | Boolean | true     |
| isTransactionAlertsEnabled  | Boolean | true     |
| isBiometricLoginEnabled     | Boolean | false    |
| isBiometricAvailableOnDevice| Boolean | false    |
| appVersion                  | String  | "v1.0.0" |
| isLoading                   | Boolean | true     |

**Events:** `LoadSettings`, `OnDarkModeToggled`, `OnLanguageSelected`, `OnPushNotificationsToggled`, `OnTransactionAlertsToggled`, `OnBiometricToggled`, `OnAboutClicked`

**Actions:** `onLoadSettings()`, `onDarkModeToggled()`, `onLanguageSelected(language: String)`, `onPushNotificationsToggled()`, `onTransactionAlertsToggled()`, `onBiometricToggled()`, `onAboutClicked()`

**DI Dependencies:** `SettingsRepository`, `BiometricManager`, `NotificationManager`, `LocaleManager`

**Errors:** `NETWORK_ERROR`

---

## Navigation

| ID           | From     | To    | Trigger               |
|--------------|----------|-------|-----------------------|
| nav_to_about | settings | about | About link row tapped |

---

## API Endpoints

No direct API calls — all data is read/written from/to local DataStore preferences via `SettingsRepository`. Network calls are not made from this screen.

---

## Design Tokens

| Token                       | Value     | Usage                                                    |
|-----------------------------|-----------|----------------------------------------------------------|
| color.light.primary         | #1800B1   | Section headers, active switch color (dark mode, push, biometric) |
| color.light.background      | #F5F5F5   | Root background                                          |
| color.surface.white         | #FFFFFF   | All four preference group card backgrounds               |
| color.accent.teal           | #008B8B   | Transaction alerts switch active color                   |
| color.neutral.dark          | #212121   | All preference row label texts                           |
| color.neutral.medium        | #757575   | All preference row description texts, app version value  |
| color.neutral.border        | #BDBDBD   | Switch inactive color, language select border, chevron icon |
| typography.title_medium     | Inter/title_medium  | All four section headers                       |
| typography.body_large       | Manrope/body_large  | All preference row labels                      |
| typography.body_small       | Manrope/body_small  | All preference row descriptions, app version   |
| typography.body_medium      | Manrope/body_medium | Language select dropdown text                  |
| spacing.lg                  | 24 dp     | Root padding, appearance header padding-top              |
| spacing.md                  | 16 dp     | Card padding                                             |
| spacing.sm                  | 8 dp      | Row padding-top/bottom, section header padding-bottom    |
| spacing.xs                  | 4 dp      | Divider margins                                          |

---

_Generated by /idea export | 2026-05-25_
