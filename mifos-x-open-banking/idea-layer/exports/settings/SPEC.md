# Settings — Feature Specification

> Generated from `screens/settings/ui.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Source hash: `fa85e05ffcdf`
> Endpoints: **0** · DTOs: 0 · Components: 10 · Test scenarios: 9

## Export gate exception

Fails gate **E3** (api[] has ≥1 entry). This is a **client-only** feature: it reads and writes
`UserDataRepository` and calls no external API. `API.md` records the absence explicitly rather
than being omitted. E1 passes — it has a real ViewModel.
Recorded in `PIPELINE_STATE#capabilities.idea-feature-export.metrics.e1_e3_exceptions`.

## 1. Overview

App settings hub — appearance (theme dropdown), a Manage Consents shortcut, and About & Legal.

| Attribute | Value |
|---|---|
| Feature ID | `settings` · Cluster settings |
| Priority | should · Status approved · quality 95 |
| Archetype | settings · Route `SettingsRoute` (flat `data object`) |
| Source module | `feature/settings` — **implemented** |

**It *is* the More tab.** `MoreTab` points `graphRoute` and `startDestinationRoute` at
`SettingsRoute`; the former `MoreRoute` placeholder and its `bankingPlaceholderDestinations()`
line were deleted in the same commit. Because it stays a **flat route** (not a
`navigation<Graph>`) and `shouldShowNavigation` tests `startDestinationRoute`, the bottom bar
stays visible on it.

## 2. The client-only template

No store, no `core/data` banking layer, no `core/network`. Its `build.gradle.kts` **drops**
`projects.core.network` and adds `libs.multiplatform.settings.test` to `commonTest`.

The ViewModel injects **`UserDataRepository`** (`core/data`, **not** `core/datastore` — no
feature depends on `:core:datastore`) and is the **first production caller of
`setDarkThemeConfig`**; the read path (`UserDataRepository → AppViewModel → ComposeApp →
MifosXOpenBankingTheme`) was already wired end to end, so the dropdown works with no extra
plumbing.

## 3. Screen inventory

`appearance_header`+`theme_row` (select) · `account_header`+`consents_row` ·
`about_header`+`privacy_row`+`licences_row`+`app_version_row` · `settings_empty` ·
`settings_error`.

## 4. State model — `SettingsViewModel`

**Fields:** `uiState` · **Default:** `Content` (`initial_state: content`)
**UiState:** `Content` · `Empty` · `Error` — **no `Loading`**
**Error kinds:** `PreferencesUnavailable` · `Unknown`
**Actions:** `SelectTheme` · `ToggleThemeMenu` · `DismissThemeMenu` · `RetryLoad`
**DI:** `UserDataRepository` · `SettingsAppVersion`

**There is no `Loading` state because DataStore reads do not fail.** `Empty` and `Error` are
renderable only from synthetic state in tests — so design `FakeUserDataRepository` with a
failure hook **from the start**, or TC-SET-008 and TC-SET-009 cannot be written at all.

## 5. Navigation

| Origin | Trigger | Target |
|---|---|---|
| `app_shell_bottom_nav` | More tab (order 3) | `settings` |
| `consents_row` | tap (Account section) | `consent-list` |
| `licences_row` | tap (About section) | `licences` |
| `privacy_row` | tap | **leaves the app** — `https://mifos.org/privacy-policy/` via `LocalUriHandler` |
| `app_version_row` | — | inert |

The host reads `LocalUriHandler.current` above the `NavHost` and passes an `onOpenUrl` lambda
into `settingsScreen`. There is **no Terms page** — the project publishes none.

## 6. API dependencies

**None.** See `API.md`.

## 7. Design tokens

`section_header` ×3, `list_item` rows, `select` for the theme dropdown.
Canonical brand spec: `design-system/DESIGN.md` 1.1.0.

## 8. Test mapping

TC-SET-001 three sections render · **002 theme dropdown persists** · 003 dismiss leaves the
selection unchanged · 004 Consents → consent-list · 005 Licences → licences · **006 Privacy
leaves the app for a browser** · 007 app-version row is inert · 008 preferences failure →
retriable error · 009 empty when no preferences resolve
→ `feature/settings/src/commonTest/.../SettingsViewModelTest.kt` + `SettingsScreenUiTest.kt`.

Carries a `commonTest` `*ScreenUiTest`, which needs `compose.uiTest` +
`desktop.uiTestJUnit4`/`currentOs` **plus** the `tasks.withType<Test> { … excludeTestsMatching("*ScreenUiTest") }`
guard — without it every case NPEs in the Android unit-test task, where there is no Robolectric
runner. `feature/settings/build.gradle.kts` is the reference for that block.

## 9. Stale-artifact fix applied 2026-07-30

`docs.yaml#description` listed **security (biometric lock + session timeout), notifications, a
Profile row and Clear Local Data**. None ships — the components are appearance, consents and
about/legal only. `idea-plan.yaml` already carried the reverse-sync note that biometric
app-lock, session timeout and notification preferences "were specified but never built"; this
prose was never updated to match. The Profile row was deleted when `profile` became
`account-holder`.

`docs.yaml` declares **no `acceptance_refs`** — the only feature besides `licences` with none.
