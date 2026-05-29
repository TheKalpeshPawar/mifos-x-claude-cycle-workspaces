# SPEC — Open Source Licenses

| Field         | Value              |
|---------------|--------------------|
| Feature       | licenses           |
| Flavor        | shared             |
| Status        | approved           |
| Quality Score | 90                 |
| ViewModel     | LicensesViewModel  |

---

## Overview

The Open Source Licenses screen is a shared legal information screen accessible from the About screen. It presents a static, bundled list of 8 open-source libraries used in Mifos X Open Banking — each with library name, version, author, and SPDX license identifier badge. Tapping any library row opens its license URL in the system browser (Apache 2.0 for all bundled libraries). The screen has three states: content (all 8 rows visible), loading (shimmer while the bundled asset parses), and error (if asset is unreadable — should never occur in production). No backend API is required; all data comes from the bundled `licenses.json` asset.

---

## Screens

| ID       | Name                 | Route           | Layout | Scroll   |
|----------|----------------------|-----------------|--------|----------|
| licenses | Open Source Licenses | /legal/licenses | Column | Vertical |

**Shell:** Top app bar ("Open Source Licenses") with back arrow. No bottom navigation bar.

---

## Components

| ID                         | Type      | Description                                                                                             |
|----------------------------|-----------|---------------------------------------------------------------------------------------------------------|
| licenses_subtitle_text     | text      | "Mifos X Open Banking is built on these outstanding open-source libraries." — body_medium, `#44483D`, 24dp bottom padding |
| licenses_list              | stack     | White card container (`#FFFFFF`, 12dp radius) wrapping all 8 library rows with dividers                 |
| license_item_compose       | list_item | Two-line row: "Compose Multiplatform" (body_large, `#1A1C16`, weight 500) + "v1.8.2 · JetBrains" (body_small, `#44483D`) + "Apache 2.0" badge (`#CDEDA3` bg, `#4C662B` text). Taps open Apache 2.0 URL |
| license_item_ktor          | list_item | "Ktor" (v3.2.0 · JetBrains) + Apache 2.0 badge. Taps open Apache 2.0 URL                              |
| license_item_koin          | list_item | "Koin" (v4.1.0 · insert-koin.io) + Apache 2.0 badge. Taps open Apache 2.0 URL                         |
| license_item_store5        | list_item | "Store5" (v5.1.0 · Mobile Kotlin) + Apache 2.0 badge. Taps open Apache 2.0 URL                        |
| license_item_room          | list_item | "Room KMP" (v2.7.0 · Google / AndroidX) + Apache 2.0 badge. Taps open Apache 2.0 URL                  |
| license_item_serialization | list_item | "kotlinx.serialization" (v1.8.1 · JetBrains) + Apache 2.0 badge. Taps open Apache 2.0 URL             |
| license_item_coroutines    | list_item | "kotlinx.coroutines" (v1.10.1 · JetBrains) + Apache 2.0 badge. Taps open Apache 2.0 URL               |
| license_item_material3     | list_item | "Material3" (v1.3.2 · Google / Compose) + Apache 2.0 badge. Taps open Apache 2.0 URL                  |
| license_divider_1..7       | divider   | Intra-list dividers: `#E1E4D5`, 16dp horizontal margin                                                  |
| licenses_loading_skeleton  | skeleton  | Shimmer list placeholder (variant: list), `#F9FAEF` bg, 24dp padding                                   |
| licenses_error_icon        | icon      | `code_off`, 48dp, `#BA1A1A`, center-aligned                                                             |
| licenses_error_message     | text      | "Unable to load license information. Please restart the app." — body_medium, `#44483D`, center-aligned  |

---

## States

| ID      | Trigger                                    | Description                                                              |
|---------|--------------------------------------------|--------------------------------------------------------------------------|
| content | Bundled license asset parsed successfully  | Subtitle + all 8 library rows with dividers and Apache 2.0 badges        |
| loading | Asset parse in progress                    | Shimmer skeleton list; no interactive elements                           |
| error   | Bundled asset unreadable (production-rare) | code_off icon (48dp, #BA1A1A) + error message, centered                 |
| empty   | Asset parsed but returned 0 entries        | Subtitle + empty_state (code_off icon + "No licenses found" + message)  |

---

## State Model

**ViewModel:** `LicensesViewModel`
**Screen State Type:** `LicensesUiState`

| Name      | Type                    | Default      |
|-----------|-------------------------|--------------|
| licenses  | List\<LibraryLicense\>  | emptyList()  |
| isLoading | Boolean                 | true         |

**Events:** `OnBack`, `OnLicenseClicked(licenseUrl: String)`

**Actions:** `onLicenseClicked(licenseUrl: String)` — opens URL via `ExternalLinkLauncher`

**DI Dependencies:** `LicenseRepository`, `ExternalLinkLauncher`

**Errors:**
- `load_failed`: "Failed to load open source license data."

---

## Navigation

| From     | To    | Trigger         | Type |
|----------|-------|-----------------|------|
| licenses | about | Back arrow / OnBack | pop  |

---

## API Endpoints

_No backend API dependencies — static/local screen._

All license data is bundled in `composeResources/files/licenses.json` and loaded by `LicenseRepository` at startup. No network calls are made.

---

## Design Tokens

| Token                         | Value     | Usage                                                         |
|-------------------------------|-----------|---------------------------------------------------------------|
| color.light.primary           | #4C662B   | Library name badge text                                       |
| color.light.primary_container | #CDEDA3   | Library name badge background                                 |
| color.light.error             | #BA1A1A   | Error state icon color                                        |
| color.light.surface           | #FFFFFF   | License list card background                                  |
| color.light.background        | #F9FAEF   | Screen background, loading skeleton background                |
| color.light.on_surface        | #1A1C16   | Library name text (body_large, weight 500)                    |
| color.light.on_surface_variant| #44483D   | Version/author metadata text, subtitle text, error message    |
| color.light.outline_variant   | #E1E4D5   | Dividers between library rows                                 |
| typography.body_large         | —         | Library name in each row                                      |
| typography.body_medium        | —         | Screen subtitle                                               |
| typography.body_small         | —         | Version and author metadata                                   |
| typography.label_small        | —         | License badge text ("Apache 2.0")                            |
| spacing.lg                    | 24dp      | Screen padding, subtitle bottom padding                       |
| spacing.md                    | 16dp      | Row padding horizontal, divider margin                        |
| radius.md                     | 12dp      | License list card border-radius                               |
| radius.sm                     | 6dp       | License badge border-radius                                   |

---

_Generated by /idea export | 2026-05-29_
