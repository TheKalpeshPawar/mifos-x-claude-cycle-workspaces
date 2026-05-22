# FEATURES — kmp-project-template

> 6 demo features shipped with the template, organized by complexity. Each demonstrates a distinct architectural pattern.
> Source links resolve via the `source/kmp-project-template/` symlink.

| # | Feature | Type | State | API | Screens | Requirements |
|---|---------|------|-------|-----|---------|--------------|
| 1 | [home](screens/home/ui.yaml) | navigation | stateless | — | `Home` | FR-001 |
| 2 | [profile](screens/profile/ui.yaml) | stub | stateless | — | `Profile` | FR-006 |
| 3 | [settings](screens/settings/ui.yaml) | preference | `UserEditableSettings` | DataStore | `Settings`, `SettingsDialog`, `LanguageDialog` | FR-002 |
| 4 | [crypto](screens/crypto/ui.yaml) | data-list (paging) | `PagingScreenStream<CoinMarket>` | CoinGecko | `CryptoWatchlist`, `CoinDetail` | FR-003, NFR-001 |
| 5 | [currency-rates](screens/currency-rates/ui.yaml) | data-list (search) | `RatesLocalState` + stream | Frankfurter | `CurrencyRates`, `RateHistory` | FR-004, NFR-001 |
| 6 | [emi-calculator](screens/emi-calculator/ui.yaml) | compute | `EmiState` | — (pure) | `EmiCalculator` | FR-005 |

---

## FR-001 — Hub navigation
**Feature:** `home`
User can navigate to any of the 6 demo features via card click on the Home hub. Home is a stateless `@Composable` — no `ViewModel`, no repository. Card click invokes the typed nav function from `cmp-navigation`.

## FR-002 — User preferences
**Feature:** `settings`
User can change theme brand, dark mode config, dynamic color, and language; choices persist to DataStore via `UserDataRepository` and apply immediately to the recomposing `MifosTheme`.

## FR-003 — Cryptocurrency watchlist (network + paging)
**Feature:** `crypto`
User can scroll an infinite list of cryptocurrencies sourced from CoinGecko `/api/v3/coins/markets`, pull-to-refresh, and tap a coin to view detail at `/api/v3/coins/{id}`. Demonstrates `PagingScreenStream<T>` with refresh + load-more + retry semantics.

## FR-004 — FX rates table (network + search)
**Feature:** `currency-rates`
User can view USD-based exchange rates sourced from Frankfurter `/v1/latest` and filter the table by currency code via a search field. Demonstrates `combineContent()` + `emptyIfContent()` operators for declarative state composition (Loading / Content / Empty).

## FR-005 — EMI calculator (pure local)
**Feature:** `emi-calculator`
User can input principal, annual interest rate, and tenure (months); results (monthly EMI, total payment, total interest) auto-compute and display. Demonstrates a `BaseViewModel<EmiState, Nothing, EmiAction>` with `Nothing` for events — pure-compute MVI pattern.

## FR-006 — Profile stub
**Feature:** `profile`
Profile tab renders a placeholder screen. Reserved as a stub slot for fork-specific identity / account flows. No ViewModel.

## NFR-001 — Consistent network state UX
**Feature:** all network-backed
All network-backed screens (`crypto`, `currency-rates`) render Loading / Content / Empty / Error states via the shared `ScreenContent` composable from `core-base:ui`.

## NFR-002 — MVI contract
**Feature:** all
All ViewModels with non-trivial state extend `BaseViewModel<LocalState, Event, Action>` (or use standard `ViewModel` for simple preference UI like `settings`). Navigation uses `kotlinx.serialization` route classes for type-safe destinations.

---

## Cross-Cutting Patterns

- **State framework** — `ScreenState<T>` (sealed Loading / Content / Error / Empty) and `PagingScreenStream<T>` (sealed Refresh / Append / Idle) live in `core-base:store`. Features compose them via `combineContent()`, `emptyIfContent()`, and `mapContent()` operators.
- **Scaffolding** — `KptScaffold` (top-bar + pull-to-refresh + snackbar host) wraps every primary screen.
- **Effects** — `EventsEffect` collects one-shot effects from `BaseViewModel.eventsFlow`; consumers usually wire `SnackbarHostState.showSnackbar()` or `navController.navigate()`.
- **DI** — Each feature module ships a `<Feature>Module.kt` Koin module wired via `koin-annotations`.
- **Navigation graph** — root is `AuthenticatedNavbarRoute` (bottom nav: Home / Profile / Crypto / Settings). Nested graphs: `CryptoGraphRoute` → `CryptoWatchlistRoute` → `CoinDetailRoute`. Currency Rates owns its own nested graph too. EMI Calculator + Settings are standalone destinations.

## API Surface (live external integrations)

| Service | Base URL | Endpoints | Auth |
|---------|----------|-----------|------|
| `CoinGeckoApi` | https://api.coingecko.com/ | `GET /api/v3/coins/markets`, `GET /api/v3/coins/{id}` | none |
| `FrankfurterApi` | https://api.frankfurter.app/ | `GET /v1/latest`, `GET /v1/{startDate}..{endDate}` | none |

Ktor engine: `OkHttp` (Android), `Darwin` (iOS), `CIO` (Desktop JVM), `Js` (Web). Timeout 60s. Loggable hosts whitelist; `Authorization` sanitized.

## Design Tokens

| Token | Value |
|-------|-------|
| Primary (light) | `#1800B1` |
| Primary (dark) | `#C1C1FF` |
| Secondary (light) | `#575899` |
| Tertiary (light) | `#5C0068` |
| Font | Outfit (9 weights) |
| Theme entry | `MifosTheme(darkTheme, androidTheme, useDynamicColor, content)` |
| Icons | Material Symbols (Filled / Outlined / Rounded) — no custom drawables |
| Dynamic color | Android 12+ opt-in via `useDynamicColor=true` |

Adaptive layouts available: `AdaptiveListDetailPaneScaffold`, `AdaptiveNavigableListDetailScaffold`, `AdaptiveNavigableSupportingPaneScaffold`, `AdaptiveNavigationSuiteScaffold`, `KptSidebarLayout`, `KptSplitPane`, `KptMasonryGrid`, `KptFlowRow`, `KptFlowColumn`, `KptGrid`, `KptResponsiveLayout`, `KptStack`.

## Release Pipeline (per release_plan)

- **Versioning**: Gradle Reckon (semantic via git tags) + monthly calendar (`YYYY.MM.0`).
- **Bot**: `openMF/mifos-x-actionhub@v1.0.8` (13+ custom Actions).
- **Workflows**: `pr-check`, `multi-platform-build-and-publish`, `promote-to-production`, `tag-weekly-release`, `monthly-version-tag`, `test-coverage`, `build-and-deploy-site`, `cache-cleanup`, `sync-dirs`.
- **Maturity grade**: **3.5 / 5** — production-ready Android + iOS (TestFlight); Desktop signing partial; Web untested in CI.
