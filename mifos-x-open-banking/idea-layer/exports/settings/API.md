# Settings — API Contracts

> Generated from `screens/settings/api.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Endpoints: 0 · DTOs: 0

## No external API surface

**This feature makes no network calls.** It is the app's client-only template.

This file exists deliberately rather than being omitted, so a reader can tell **"this feature
has no API"** apart from **"this feature has not been exported yet"**.

| | |
|---|---|
| Endpoints | 0 |
| DTOs | 0 |
| Auth requirement | none |
| Cache strategy | n/a — DataStore is the store |

## What it reads and writes instead

`UserDataRepository` (`core/data`, **not** `core/datastore` — no feature depends on
`:core:datastore` directly; preferences are reached through `core/data`).

| Operation | Signature | Note |
|---|---|---|
| read theme | `observeDarkThemeConfig: Flow<DarkThemeConfig>` | already wired end to end before this feature existed |
| write theme | `setDarkThemeConfig(config)` | **`SettingsViewModel` is its first production caller** |
| app version | `SettingsAppVersion` | static, injected |

The read path — `UserDataRepository → AppViewModel → ComposeApp → MifosXOpenBankingTheme` — was
already complete, so the dropdown worked end to end with no extra plumbing. Only the setter was
new.

`setDarkThemeConfig` is the feature's **only** persisted setting.

## Why there is no `Loading` state

DataStore reads do not fail and do not meaningfully block, so the screen's initial state is
`Content`, not `Loading`. `Empty` and `Error` exist in the state machine but have **no
production trigger** — they are renderable only from synthetic state.

**Consequence for testing:** `FakeUserDataRepository` must be designed with a failure hook from
the start. Without one, TC-SET-008 (preferences failure → retriable error) and TC-SET-009
(empty state) cannot be written at all.

## Build-config consequence

Because there is no network layer, `feature/settings/build.gradle.kts` **drops**
`projects.core.network` from `commonTest` — unlike every store-backed feature, where a fake
typed on `NetworkResult`/`NetworkError` will not compile without it — and adds
`libs.multiplatform.settings.test`.

Copying a store-backed feature's build file here would pull in a dependency this feature has no
use for; copying this one into a store-backed feature would fail to compile its fakes.

## Gate E3

Export gate **E3** requires `api[] has ≥1 entry with a response section`. This feature fails it
by design; E1 passes. Two other features share the shape:

| Feature | Gates failed | Why |
|---|---|---|
| `settings` | E3 only | client-only — reads `UserDataRepository` |
| `licences` | E1 + E3 | bundled `composeResources` text asset; no ViewModel |
| `user-onboarding` | E1 + E3 | static IntroScreen; no ViewModel, no I/O |

## Outbound link

`privacy_row` leaves the app for `https://mifos.org/privacy-policy/` via `LocalUriHandler` —
not an API call, but the one place this feature reaches the network at all, and it does so by
handing off to the platform browser. There is no Terms page.
