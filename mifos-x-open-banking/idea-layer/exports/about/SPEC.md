# SPEC — About

| Field | Value |
|---|---|
| Feature | about |
| Flavor | shared |
| Status | approved |
| Quality | 95 |
| ViewModel | AboutViewModel |
| Archetype | settings |
| Dependencies | shared-core |

## Overview

The About screen is a static utility screen that surfaces build-time constants (app version, build number) and legal navigation links. It provides users with a transparent view of the app identity, current release information, and direct access to Terms of Service, Privacy Policy, and Open Source Licenses via external web links. A rate-app affordance surfaces in-app store review intent. No network requests are made; all content is resolved from build-time constants.

## Screens

| Screen ID | Display Name | Shell |
|---|---|---|
| about/content | About — Content | Top app bar "About" + back arrow, no bottom nav |
| about/loading | About — Loading | Top app bar "About" + back arrow, no bottom nav |
| about/error | About — Error | Top app bar "About" + back arrow, no bottom nav |
| about/empty | About — Empty | Top app bar "About" + back arrow, no bottom nav |

## Components

| Component | Type | States Present | Notes |
|---|---|---|---|
| Logo section | image + text | content, empty | App logo image + app name text |
| App info card | card | content | Version 1.0.0, Build 2026.05.001 |
| Legal card | card | content, empty | Rows: Terms of Service, Privacy Policy, Open Source Licenses |
| Rate app button | button | content | Triggers in-app review / store link |
| Skeleton overlay | loading_skeleton | loading | Full-screen placeholder |
| Error icon + message | error_state | error | Icon + descriptive error message |

## States

| State | Description | Components Visible |
|---|---|---|
| content | Fully loaded; all data resolved from build constants | Logo section, App info card, Legal card, Rate app button |
| loading | Data resolving (build constants look-up / initial composition) | Skeleton overlay |
| error | Failed to resolve build constants or compose screen | Error icon + message |
| empty | Screen composed but version info unavailable | Logo section, Legal card |

## State Model

```kotlin
data class AboutUiState(
    val appVersion: String,
    val buildNumber: String,
)
```

### Events

| Event | Trigger |
|---|---|
| OnRateAppClicked | User taps Rate App button |
| OnTermsClicked | User taps Terms of Service row |
| OnPrivacyClicked | User taps Privacy Policy row |
| OnLicensesClicked | User taps Open Source Licenses row |

## Navigation

| Action | Destination | Type |
|---|---|---|
| Terms of Service | External URL (terms) | External browser |
| Privacy Policy | External URL (privacy) | External browser |
| Open Source Licenses | External URL (licenses) | External browser |
| Back arrow | Previous screen | Back stack pop |

## Dependencies

| Dependency | Purpose |
|---|---|
| shared-core | Build config constants (version, build number), navigation utilities |

## Design Tokens

| Token | Value |
|---|---|
| Accent color | #4C662B (Earth-green) |
| Typography | Outfit |
| Design system | Material 3 (M3) |
