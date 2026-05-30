# mifos-x-open-banking — Requirements

> **Empty-slate state** — only scaffolding requirements are listed.
> Real product FRs will be added once feature scope is defined.

## Functional Requirements (scaffolding only)

### Home (FR-001)

| ID | Description |
|---|---|
| FR-001 | User lands on Home after Splash. Specific destinations TBD. |

### Profile (FR-002)

| ID | Description |
|---|---|
| FR-002 | User sees their profile placeholder on Profile screen. |

### Settings (FR-003 — FR-005)

| ID | Description |
|---|---|
| FR-003 | User can toggle application theme (light / dark / system) via SettingsDialog. |
| FR-004 | User can switch app language via LanguageDialog. |
| FR-005 | User sees Notification placeholder screen (preferences UI not yet implemented). |

---

## Non-Functional Requirements

These NFRs apply across all features regardless of product scope. They are determined by the architecture choice (Stream-First KMP) and must hold for any future feature added.

### Cross-platform

| ID | Description |
|---|---|
| NFR-001 | App MUST build and run on Android, iOS, Desktop (JVM), Web (Wasm + JS) from one Kotlin codebase. |
| NFR-002 | UI rendering MUST be Compose Multiplatform — no platform-specific UI fallbacks for shared screens. |
| NFR-003 | Platform-specific concerns (locale source, native splash, file paths) MUST use `expect`/`actual` via `Platform.kt`. |

### Architecture

| ID | Description |
|---|---|
| NFR-004 | All ViewModels MUST extend `BaseViewModel` and expose state via `ScreenDataStream` (Stream-First pattern). |
| NFR-005 | Network-backed repositories MUST use Store5 (`mobile.kotlin.store`) for cache-then-network behavior. |
| NFR-006 | DI MUST use Koin (`org.koin.koin-core`) with feature-scoped modules; no service-locators outside `koinInject`. |

### Observability

| ID | Description |
|---|---|
| NFR-007 | App MUST log uncaught crashes to Firebase Crashlytics (Android-only, no-op elsewhere). |
| NFR-008 | App MUST report cold-start + frame-time metrics to Firebase Performance (Android-only). |

### Performance

| ID | Description |
|---|---|
| NFR-009 | Cold start on mid-tier Android (Pixel 6a-class): < 1.5 s. |
| NFR-010 | Navigation between screens: transitions complete within 300 ms. |

### Accessibility

| ID | Description |
|---|---|
| NFR-011 | All interactive components MUST have minimum 48dp touch target (Material 3). |
| NFR-012 | Color contrast for text MUST meet WCAG AA (≥ 4.5:1 normal text). |
| NFR-013 | All images MUST have content descriptions; navigation actions MUST have accessibility labels. |

### Internationalization

| ID | Description |
|---|---|
| NFR-014 | All user-visible strings MUST live in `composeResources/values/strings.xml` and use string resources, no hard-coded literals. |
| NFR-015 | Date display MUST use locale-aware formatting. |
| NFR-016 | Currency display (when applicable) MUST use locale-aware formatting. |
