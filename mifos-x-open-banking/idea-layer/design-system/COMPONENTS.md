---
name: Mifos X Open Banking — Components
version: "1.0.0"
generated_at: "2026-05-22"
---

# Mifos X Open Banking — Component Library

> M3 components used across screens. Each entry: M3 component + project-specific usage notes + source location.
> Empty-slate scaffold: only universally-applicable + scaffolding-screen components are documented. Per-feature components will be added when product scope is defined.

## App-Shell Components

### TopAppBar
- **M3 variant**: small (single-line) for utility screens; medium (two-line) for detail screens.
- **Source**: `core/designsystem/component/MifosTopAppBar.kt`
- **Usage**: Home / Profile / Settings.

### BottomNavigation (Phone/Tablet)
- **M3 variant**: NavigationBar with destinations declared in `design-system/app-shell.yaml`.
- **Source**: `cmp-navigation/AppNavHost.kt`
- **Current scaffolding**: Home / Profile / Settings.

### NavigationRail (Desktop/Wide)
- **M3 variant**: NavigationRail on Desktop / Web ≥ 600dp width.
- **Source**: `cmp-navigation/AppNavHost.kt`

### Snackbar
- **M3 variant**: Snackbar for transient messages.
- **Source**: `core/designsystem/component/MifosSnackbar.kt`

### ErrorBanner
- **Custom**: persistent banner for network-down or error states.
- **Source**: `core/designsystem/component/MifosErrorBanner.kt`

## Form Components

### MifosOutlinedTextField
- **M3 variant**: OutlinedTextField with custom error treatment.
- **Source**: `core/designsystem/component/MifosOutlinedTextField.kt`

### MifosFilterChip
- **M3 variant**: FilterChip (selectable).
- **Source**: `core/designsystem/component/MifosFilterChip.kt`

### MifosButton (Primary)
- **M3 variant**: FilledButton (primary action).

### MifosTonalButton (Secondary)
- **M3 variant**: FilledTonalButton (secondary action).
- **Usage**: "Cancel" in dialogs.

### MifosOutlinedButton (Tertiary)
- **M3 variant**: OutlinedButton.

### MifosSlider
- **M3 variant**: Slider with discrete marks.

## Content Components

### MifosCard (in-list row)
- **M3 variant**: Card (no elevation) with `surface_container` background.
- **Source**: `core/designsystem/component/MifosCard.kt`
- **Usage**: Settings rows.

### MifosElevatedCard (standalone)
- **M3 variant**: ElevatedCard at level1.

### MifosListItem
- **M3 variant**: ListItem (M3 spec).
- **Usage**: Language picker rows.

## Feedback Components

### MifosLoadingIndicator (full-screen)
- **M3 variant**: CircularProgressIndicator centered.
- **Source**: `core/designsystem/component/MifosLoading.kt`

### MifosSkeleton (placeholder)
- **M3 variant**: shimmer placeholder.

### MifosEmptyState
- **Custom**: icon + headline + body + optional primary action.
- **Source**: `core/designsystem/component/MifosEmptyState.kt`

### MifosErrorBanner
- **Custom**: full-width banner with icon + message + "Retry" affordance.
- **Source**: `core/designsystem/component/MifosErrorBanner.kt`

## Dialog Components

### SettingsDialog
- **M3 variant**: AlertDialog with theme picker (radio group: light / dark / system + brand color).
- **Source**: `feature/settings/SettingsDialog.kt`
- **Usage**: Settings → tap Theme card.

### LanguageDialog
- **M3 variant**: AlertDialog with locale picker (radio group of platform-supported locales).
- **Source**: `feature/settings/LanguageDialog.kt`
- **Usage**: Settings → tap Language card.

## Cross-cutting

### MifosScaffold
- **Custom wrapper around M3 Scaffold** — applies safe-area insets, error banner host, snackbar host.
- **Source**: `core/designsystem/component/MifosScaffold.kt`
- **Usage**: every screen entry.
