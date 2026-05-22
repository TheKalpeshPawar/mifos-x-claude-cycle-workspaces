# mifos-x-open-banking — Features

> **Empty-slate state** — product scope is not yet defined. Only architectural scaffolding (home / profile / settings) is in scope.
> Last updated: 2026-05-22

## Active Scaffolding

| Feature | Priority | Maturity | Screens | Requirements |
|---|---|---|---|---|
| [home](#home) | must | bootstrap | Home | FR-001 |
| [profile](#profile) | should | stub | Profile | FR-002 |
| [settings](#settings) | must | partial | Settings · Notification · LanguageDialog · SettingsDialog | FR-003…FR-005 |

## Pending Removal (template residue)

These source modules came from `kmp-project-template` and are **not** part of this product's scope. They remain in the source tree until removal:

| Source module | Reason in tree |
|---|---|
| `feature/crypto` | Template demo: Store5 + external HTTP — to be removed |
| `feature/currency-rates` | Template demo: streaming repository pattern — to be removed |
| `feature/emi-calculator` | Template demo: pure-derived state — to be removed |

> The idea-layer does NOT describe these as product features. When removed, also delete `idea-layer/screens/{crypto,currency-rates,emi-calculator}/` directories.

---

## home

> ⚪ **bootstrap** — entry hub. Will route to real features once product scope is defined.

App entry after Splash. Currently a minimal landing surface; final composition depends on product feature roster.

### Screens

#### `Home` (dashboard archetype — placeholder)
**Composition**: `KptScaffold` · top app bar · scaffolding-only body
**State**: `HomeViewModel` (Stream-First) — minimal until features added
**Data**: `UserDataRepository` (user identity if any)
**Source**: `feature/home/src/commonMain/kotlin/org/mifos/feature/home/HomeScreen.kt`

### Requirements

| ID | Description | Source |
|---|---|---|
| **FR-001** | User lands on Home after Splash. Specific tiles/destinations to be defined once feature scope is set. | `HomeScreen.kt`, `HomeDestination.kt` |

### Next steps

- [ ] Decide product feature roster (run `/idea add` for each)
- [ ] Add tiles or navigation entries from Home to real features

---

## profile

> ⚪ **stub** — placeholder. Currently a static Compose surface with no state.

User profile dashboard. Designed to integrate with user account / preferences when auth is added.

### Screens

#### `Profile` (profile archetype)
**Composition**: `KptScaffold` · avatar header · profile-card list
**State**: stateless
**Data**: none yet
**Source**: `feature/profile/src/commonMain/kotlin/org/mifos/feature/profile/ProfileScreen.kt`

### Requirements

| ID | Description | Source |
|---|---|---|
| **FR-002** | User sees their profile placeholder on Profile screen. | `ProfileScreen.kt`, `ProfileRoute.kt` |

### Next steps

- [ ] Define user-data model + auth provider
- [ ] Add `ProfileViewModel` once auth backend chosen
- [ ] Wire avatar + display-name + preferences

---

## settings

> 🟡 **partial** — theme + language toggles functional; notification is a stub.

App settings — theme (light/dark/system), language picker, notification preferences (placeholder).

### Screens

#### `Settings` (settings archetype)
Each setting category is an `OutlinedCard` with icon + label + chevron. Theme card opens `SettingsDialog`. Language card opens `LanguageDialog`. Notification card routes to `Notification` screen.

**State**: `SettingsViewmodel` (Stream-First) — theme + language state
**Data**: `UserDataRepository.{setThemeBrand, setDarkThemeConfig, setLanguage}`
**Source**: `feature/settings/src/commonMain/kotlin/org/mifos/feature/settings/SettingsScreen.kt`

#### `Notification` (settings sub-screen)
**Composition**: `KptScaffold` · `Column` · placeholder text
**State**: stateless — stub
**Source**: `feature/settings/src/commonMain/kotlin/org/mifos/feature/settings/NotificationScreen.kt`

#### `SettingsDialog` (dialog)
Theme picker (light / dark / system) + brand color selector.
**Source**: `feature/settings/src/commonMain/kotlin/org/mifos/feature/settings/SettingsDialog.kt`

#### `LanguageDialog` (dialog)
Locale picker — driven by `Platform.kt` expect/actual locale source.
**Source**: `feature/settings/src/commonMain/kotlin/org/mifos/feature/settings/LanguageDialog.kt`

### Requirements

| ID | Description | Source |
|---|---|---|
| **FR-003** | User can toggle application theme (light / dark / system) via SettingsDialog. | `SettingsDialog.kt` |
| **FR-004** | User can switch app language via LanguageDialog. | `LanguageDialog.kt`, `Platform.kt` |
| **FR-005** | User sees Notification placeholder screen (preferences UI not yet implemented). | `NotificationScreen.kt` |

### Flows

- **settings_theme_flow**: Settings → tap ThemeCard → SettingsDialog → pick theme → SettingsViewmodel updates
- **settings_language_flow**: Settings → tap LanguageCard → LanguageDialog → pick locale → SettingsViewmodel updates
- **settings_notification_flow**: Settings → tap NotificationCard → Notification screen (stub)

### Next steps

- [ ] Implement `NotificationViewModel` + `UserNotificationPreferences` once notification strategy is set
- [ ] Add settings rows once product scope is set: about, privacy, version, OSS licenses

---

## Cross-cutting (scaffolding)

### Splash (cmp-shared)
Bootstrap screen — `RootNavViewModel.bootstrap` loads theme + language prefs, then routes to `Home`.

### Repositories observed (source-derived)

| Repository | Purpose |
|---|---|
| `UserDataRepository` | User preferences (theme, language, brand color) — `core/data` |
| `NetworkMonitor` | Connectivity status via `Flow<Boolean>` — `core/data` |

> Template repositories (`CryptoRepository`, `CurrencyRatesRepository`) will be removed with their feature modules.

### Database (Room KMP)

| Entity | Module |
|---|---|
| `UserPreferencesEntity` | `core/datastore` |

> Template entities will be removed alongside template modules.
