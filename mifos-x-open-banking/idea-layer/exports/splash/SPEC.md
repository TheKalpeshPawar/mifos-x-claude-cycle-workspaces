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

The Splash screen is the application entry point on every cold start. It is shared across Consumer and Field Officer flavors. The screen displays the Mifos X logo, app name, and tagline with a circular indeterminate progress indicator while the app resolves its initial route. There are no user-interactive elements. The screen uses a vertical centered column layout, full-screen surface, with the progress indicator at the bottom of the composition.

**Routing ownership (reconciled 2026-05-30):** session check and post-splash routing are **owned by `RootNavViewModel`** (`cmp.navigation.rootnav`), not by `SplashViewModel`. `RootNavViewModel` reads the persisted auth/user state and maps it to a `RootNavState` (`Splash` → `Auth` / `ShowOnboarding` / `UserLocked` / `UserUnlocked`); `RootNavScreen` performs the navigation. `SplashViewModel` is therefore a **thin visual host only** — it drives the branded loading visual and the reduced-motion fallback and holds no repositories. This matches the kmp-project-template root-nav architecture; the splash visual lives in `cmp-navigation`, not in a feature module.

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

**ViewModel:** `SplashViewModel` (thin visual host — no routing, no repositories)
**Screen State Type:** `SplashUiState`

| Field         | Type    | Default | Purpose                          |
|---------------|---------|---------|----------------------------------|
| reducedMotion | Boolean | false   | Static-logo fallback for the loading indicator |

**Events:** _none_

**Actions:** _none_

**DI Dependencies:** _none_

**Errors:** _none_

> Session check + auth routing are owned by `RootNavViewModel` (`cmp.navigation.rootnav`), which consumes the persisted user/auth state and emits `RootNavState`. `SplashViewModel` does not read auth state or decide navigation.

---

## Navigation

Navigation away from the splash visual is **driven by `RootNavViewModel` / `RootNavScreen`**, not by `SplashViewModel`. The targets below document the intended transitions for the app-flow graph and journey linkage; the resolving owner is `RootNavViewModel` mapping `RootNavState`.

| ID                        | From   | To           | Trigger      | Owner            | Maps from                                  |
|---------------------------|--------|--------------|--------------|------------------|---------------------------------------------|
| nav_to_login              | splash | login        | auto         | RootNavViewModel | `RootNavState.Auth` (unauthenticated)       |
| nav_to_consumer_home      | splash | home         | auto         | RootNavViewModel | `RootNavState.UserUnlocked` (Consumer)      |
| nav_to_home_authenticated | splash | home         | token_exists | RootNavViewModel | persisted token → `UserUnlocked` (Consumer) |
| nav_to_fo_dashboard       | splash | fo-dashboard | auto         | RootNavViewModel | `RootNavState.UserUnlocked` (Field Officer) |

---

## API Endpoints

_No backend API dependencies — static/local screen._

The splash visual issues no HTTP requests and holds no repositories. Any session validation (local token read, refresh) happens in `RootNavViewModel` upstream of routing and never surfaces loading state on this screen.

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

_Generated by /idea export | 2026-05-30 (reconciled: routing owned by RootNavViewModel)_
