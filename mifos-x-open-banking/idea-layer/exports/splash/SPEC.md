# SPEC — Splash Screen

| Field         | Value           |
|---------------|-----------------|
| Feature       | splash          |
| Flavor        | shared          |
| Status        | approved        |
| Quality Score | 92              |
| ViewModel     | SplashViewModel |

---

## Overview

The Splash screen is the application entry point on every cold start. It is shared across Consumer and Field Officer flavors. The screen displays the Mifos X logo, app name, and tagline while `SplashViewModel` runs a background session check via `ObpAuthRepository` and `SessionManager`. Navigation fires automatically: unauthenticated users are sent to Login after a 2 000 ms delay; users with a valid token are navigated immediately — Consumer users to Home, Field Officer users to the FO Dashboard. There are no user-interactive elements. The screen uses a vertical centered column layout, full-screen white surface, with a circular indeterminate progress indicator at the bottom of the composition.

---

## Screens

| ID     | Name   | Route   | Layout | Scroll |
|--------|--------|---------|--------|--------|
| splash | Splash | /splash | Column | None   |

**Shell:** No top app bar. No bottom navigation bar. Full-screen surface only.

---

## Components

| ID                       | Type              | Description                                                                                             |
|--------------------------|-------------------|---------------------------------------------------------------------------------------------------------|
| splash_root              | stack             | Full-screen centered column; background surface (#FFFFFF); horizontal+vertical alignment center         |
| splash_logo              | image             | `mifos_logo` asset, 120×120 dp, tint #4C662B; role=image, a11y label "Mifos X application logo"       |
| splash_app_name          | text              | "Mifos X Open Banking" — Outfit/display_small (32sp/600), color #4C662B; padding_top 24dp; role=heading|
| splash_tagline           | text              | "Banking for Everyone" — Outfit/body_large (16sp/400), color #386663; padding_top 8dp                  |
| splash_loading_indicator | loading_indicator | Circular indeterminate, color #4C662B, size 40dp, padding_top 32dp; role=progressbar                   |

---

## States

| ID         | Trigger                       | Description                                                                              |
|------------|-------------------------------|------------------------------------------------------------------------------------------|
| loading    | App cold start                | All four components visible; circular progress spinning; session check runs in background|
| navigating | Session check completes       | Same visual layout; auto-navigation fires based on `hasValidToken` and `userRole`        |

---

## State Model

**ViewModel:** `SplashViewModel`
**Screen State Type:** `SplashUiState`

| Field                | Type    | Default |
|----------------------|---------|---------|
| sessionCheckComplete | Boolean | false   |
| hasValidToken        | Boolean | false   |
| isNavigating         | Boolean | false   |

**Events:** `CheckSession`, `NavigateToLogin`, `NavigateToHome`

**Actions:** `onCheckSession()`, `onNavigateToLogin()`, `onNavigateToHome()`

**DI Dependencies:** `ObpAuthRepository`, `SessionManager`

**Errors:** `NETWORK_ERROR`

---

## Navigation

| ID                        | From   | To           | Trigger     | Condition                                               | Delay   |
|---------------------------|--------|--------------|-------------|----------------------------------------------------------|---------|
| nav_to_login              | splash | login        | auto        | `hasValidToken == false`                                | 2 000 ms|
| nav_to_consumer_home      | splash | home         | auto        | `hasValidToken == true && userRole == CONSUMER`         | 0 ms    |
| nav_to_home_authenticated | splash | home         | token_exists| `isAuthenticated == true && userRole == CONSUMER`       | —       |
| nav_to_fo_dashboard       | splash | fo-dashboard | auto        | `hasValidToken == true && userRole == FIELD_OFFICER`    | 0 ms    |

---

## API Endpoints

_No backend API dependencies — static/local screen._

Session validation is performed entirely via local `SessionManager` reading the persisted DirectLogin token from `CredentialStore`. No HTTP requests are issued from this screen. Token refresh, if needed, is delegated to `ObpAuthRepository` without surfacing any loading state on this screen.

---

## Design Tokens

| Token                        | Value     | Usage                                                            |
|------------------------------|-----------|------------------------------------------------------------------|
| colors.light.primary         | #4C662B   | splash_logo tint; splash_app_name color; loading indicator color|
| colors.light.secondary       | #386663   | splash_tagline color                                             |
| colors.light.surface         | #FFFFFF   | splash_root background                                           |
| typography.display_small     | 32sp/600  | splash_app_name                                                  |
| typography.body_large        | 16sp/400  | splash_tagline                                                   |
| spacing.lg                   | 24dp      | splash_app_name padding_top                                      |
| spacing.sm                   | 8dp       | splash_tagline padding_top                                       |
| spacing.xl                   | 32dp      | splash_loading_indicator padding_top                             |
| iconography.default_size     | 24dp base | splash_logo uses 120dp (oversized hero usage)                    |

---

_Generated by /idea export | 2026-05-29_
