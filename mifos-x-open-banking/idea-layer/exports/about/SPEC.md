# SPEC — About

| Field         | Value          |
|---------------|----------------|
| Feature       | about          |
| Flavor        | shared         |
| Status        | approved       |
| Quality Score | 95             |
| ViewModel     | AboutViewModel |

---

## Overview

The About screen provides users with app identity, version metadata, and legal navigation links. It is shared across both the Consumer and Field Officer flavors. The screen displays the Mifos X logo, the app name "Mifos X Open Banking", a tagline "Open Banking for Everyone", an App Information card showing the current version number (1.0.0) and build stamp (2026.05.001), a Legal card with tappable rows for Terms of Service, Privacy Policy, and Open Source Licenses — each opening an external WebView or browser — and an "Rate This App" outlined button that triggers the in-app review flow via the platform ReviewManager API.

---

## Screens

| ID    | Name  | Route  | Layout | Scroll   |
|-------|-------|--------|--------|----------|
| about | About | /about | Column | Vertical |

**Shell:** Top app bar, title "About", navigation icon `arrow_back`. No bottom navigation bar.

---

## Components

| ID                     | Type     | Description                                                                                           |
|------------------------|----------|-------------------------------------------------------------------------------------------------------|
| about_logo_image       | image    | Mifos X logo, 80×80dp, tinted `#4C662B`, centred; a11y label "Mifos X Open Banking logo"             |
| about_app_name_text    | text     | "Mifos X Open Banking" — headline_small (24sp/SemiBold), color `#4C662B`, centred                    |
| about_tagline_text     | text     | "Open Banking for Everyone" — body_medium (14sp/Regular), color `#44483D`, centred                   |
| about_app_info_card    | card     | Filled card, `#FFFFFF`, radius 12dp, padding 16dp — wraps version and build rows                     |
| about_version_label    | text     | "Version" — body_large (16sp/Regular), color `#1A1C16`                                               |
| about_version_value    | text     | "1.0.0" — body_medium (14sp/Regular), color `#44483D`; data-driven from BuildConfig.VERSION_NAME     |
| about_divider_1        | divider  | `#E1E4D5` (surface_variant) hairline separator between version and build rows                         |
| about_build_label      | text     | "Build" — body_large (16sp/Regular), color `#1A1C16`                                                 |
| about_build_value      | text     | "2026.05.001" — body_medium (14sp/Regular), color `#44483D`; data-driven from BuildConfig.VERSION_CODE |
| about_legal_card       | card     | Filled card, `#FFFFFF`, radius 12dp — wraps Legal section header and three link rows                  |
| about_legal_header     | text     | "Legal" — title_medium (16sp/Medium), color `#4C662B`; section heading                               |
| about_tos_link         | link     | "Terms of Service" — body_large, color `#1A1C16`; on_click opens terms-of-service                    |
| about_tos_chevron      | icon     | `open_in_new`, 18dp, color `#C5C8BA` (outline_variant) — trailing external-link affordance           |
| about_divider_2        | divider  | `#E1E4D5` separator between Terms of Service and Privacy Policy                                      |
| about_privacy_link     | link     | "Privacy Policy" — body_large, color `#1A1C16`; on_click opens privacy-policy                        |
| about_privacy_chevron  | icon     | `open_in_new`, 18dp, color `#C5C8BA` — trailing external-link affordance                             |
| about_divider_3        | divider  | `#E1E4D5` separator between Privacy Policy and Open Source Licenses                                  |
| about_licenses_link    | link     | "Open Source Licenses" — body_large, color `#1A1C16`; on_click opens licenses                        |
| about_licenses_chevron | icon     | `chevron_right`, 20dp, color `#C5C8BA` — trailing tap affordance                                     |
| about_rate_button      | button   | "Rate This App" — outlined, border `#4C662B`, text `#4C662B`, label_large; triggers ReviewManager API |
| about_loading_skeleton | skeleton | Settings-variant shimmer on `#F9FAEF` — shown while BuildConfig values resolve on cold start          |
| about_error_icon       | icon     | `info_outline`, 48dp, color `#BA1A1A` — error state centred icon                                     |
| about_error_message    | text     | "Unable to load app information. Please restart the app." — body_medium, color `#44483D`, centred    |

---

## States

| ID      | Trigger                                      | Description                                                                                        |
|---------|----------------------------------------------|----------------------------------------------------------------------------------------------------|
| content | Screen entry with BuildConfig resolved       | Logo, name, tagline, App Info card (version + build), Legal card, and Rate App button all visible  |
| loading | Cold start while BuildConfig values resolve  | Shimmer skeleton replaces logo/name block and both cards; no interactive elements                  |
| error   | BuildConfig retrieval fails                  | Error icon (`info_outline`) and message centred; cards hidden                                      |
| empty   | Version data unavailable, screen still loads | Logo section and Legal card visible; App Info card and Rate App button hidden                      |

---

## State Model

**ViewModel:** `AboutViewModel`
**Screen State Type:** `AboutUiState`

| Name        | Type   | Default         |
|-------------|--------|-----------------|
| appVersion  | String | `"1.0.0"`       |
| buildNumber | String | `"2026.05.001"` |

**Events:** `OnRateAppClicked`, `OnTermsClicked`, `OnPrivacyClicked`, `OnLicensesClicked`

**Actions:** `onRateAppClicked()`, `onTermsClicked()`, `onPrivacyClicked()`, `onLicensesClicked()`

**DI Dependencies:** `AppInfoProvider`, `ReviewManager`

**Errors:**
- _(No network errors — About is a static screen. BuildConfig read failures surface as the error state only.)_

---

## Navigation

| From  | To               | Trigger                         | Type     |
|-------|------------------|---------------------------------|----------|
| about | terms-of-service | about_tos_link tap              | external |
| about | privacy-policy   | about_privacy_link tap          | external |
| about | licenses         | about_licenses_link tap         | push     |
| about | (back)           | Top app bar back arrow          | pop      |

---

## API Endpoints

_No backend API dependencies — static/local screen._

---

## Design Tokens

| Token                           | Value     | Usage                                                        |
|---------------------------------|-----------|--------------------------------------------------------------|
| colors.light.primary            | `#4C662B` | App name text, Legal header, Rate App button text and border |
| colors.light.on_surface         | `#1A1C16` | Version/Build label text (body_large)                        |
| colors.light.on_surface_variant | `#44483D` | Tagline, version/build values, error message                 |
| colors.light.surface            | `#FFFFFF` | App Info card and Legal card background                      |
| colors.light.surface_variant    | `#E1E4D5` | Dividers between rows inside both cards                      |
| colors.light.outline_variant    | `#C5C8BA` | Chevron and external-link icons in Legal rows                |
| colors.light.background         | `#F9FAEF` | Screen background, skeleton shimmer base                     |
| colors.light.error              | `#BA1A1A` | Error state icon color                                       |
| typography.headline_small       | 24sp/SemiBold | App name                                               |
| typography.title_medium         | 16sp/Medium | Legal card section header                                  |
| typography.body_large           | 16sp/Regular | Version/Build label text, legal link text                 |
| typography.body_medium          | 14sp/Regular | Tagline, version/build values, error message              |
| typography.label_large          | 14sp/Medium | Rate App button label                                     |
| radius.md                       | 12dp      | App Info card and Legal card corner radius                   |
| spacing.xl                      | 32dp      | Logo section top/bottom padding                              |
| spacing.lg                      | 24dp      | Root column padding, Rate App button top margin              |
| spacing.md                      | 16dp      | Card internal padding                                        |

---

_Generated by /idea export | 2026-05-29_
