---
name: Mifos X Open Banking
version: "1.0.0"
generated_at: "2026-05-22"
token_source: design-tokens.yaml
design_system: material3
primary_color: "#1800B1"
platforms: [android, ios, desktop, web]
---

# Mifos X Open Banking — Design System

> Material Design 3 implementation tuned for fintech. Brand: Mifos deep-purple `#1800B1`.
> Token source-of-truth: `design-tokens.yaml`. Generated 2026-05-22.

## Principles

1. **Clarity over decoration** — finance UIs prioritize numerical legibility; spacing, hierarchy, and tabular alignment carry weight over visual flourish.
2. **Trust through consistency** — every monetary or rate value uses the same typographic treatment; never style the same value-type two ways.
3. **Cross-platform parity** — a screen rendered on Android, iOS, Desktop, and Web must look like the same product, not four ports.
4. **Offline-honest** — surface freshness clearly (timestamps, "cached" badges, error banners). Never lie about live-ness.
5. **WCAG AA minimum** — 4.5:1 contrast, 48dp touch targets, all icons paired with text where space allows.

## Color

**Primary**: `#1800B1` deep purple — Mifos brand, used for primary actions, app bar, key data emphasis.
**Secondary**: `#5C5D72` — supporting actions, secondary chrome.
**Tertiary**: `#785368` — accent in detail surfaces (e.g. rate-trend chart points).
**Error**: `#BA1A1A` (light) / `#FFB4AB` (dark) — destructive actions, validation errors, network failures.

Surface hierarchy (light): `background #FCF8FF` < `surface_container #F0EDF7` < `surface_container_high #EAE7F1`. Use container shades for elevated cards (watchlist items, rate rows, settings cards).

Dark mode mirrors with `background #13131B` and progressively lighter container shades.

## Typography

- **Display**: Space Grotesk — used for prices in detail screens (e.g. `$42,387.12`), large hero numbers.
- **Body**: Inter — all UI text, list items, form labels.
- **Monospace**: JetBrains Mono — amortization tables, rate columns (where digit alignment matters).

Type-scale clamping: never use `display_lg` (57sp) on phones; reserve for Desktop. Phone hero values use `headline_lg` (32sp).

## Spacing — 8dp grid

All padding, margins, gaps snap to the 8dp grid (`xs=4`, `sm=8`, `md=16`, `lg=24`, `xl=32`). Cards have `md` internal padding. Sections have `lg` vertical gaps. Screen edges use `md` horizontal padding (Android/iOS) or `xl` (Desktop/Web).

## Radius

Buttons: pill (fully rounded). Cards: `md` (12dp). Text fields: `xs` (4dp) — Material 3 default. Dialogs: `lg` (16dp).

## Elevation

Flat surfaces (level0) for screen background and app bar (Material 3 trend). Cards use level1. Dialogs use level3. Bottom sheets use level1 with scrim.

## Motion

Standard easing for most transitions. Use `emphasized` for screen-to-screen navigation. Avoid motion longer than 400ms (`medium4`) — finance apps prioritize speed.

## Iconography

Material Symbols Outlined at 24dp default. Common icons in current scaffolding:
- `home` — Home destination
- `account_circle` — Profile
- `settings` — Settings
- `dark_mode` / `light_mode` — theme picker
- `language` — language picker
- `notifications` — notification preferences
- `arrow_back`, `chevron_right` — navigation

Additional icons will be declared per feature once product scope is set. Icons never appear alone in primary actions — always paired with text (accessibility + clarity).

## Component principles (see COMPONENTS.md for full surface)

- **Buttons**: filled for primary action, tonal for secondary, outlined for tertiary; text-only for inline links.
- **Cards**: filled (no elevation) for in-list rows; elevated (level1) for standalone detail panels.
- **Text fields**: outlined (Material 3 default); never filled within forms.
- **Dialogs**: alert dialog for destructive confirmations; full-screen for multi-step pickers (theme, language).

## Accessibility checklist

- All touch targets ≥ 48dp (`component_tokens.touch_target_min`).
- All text-vs-background contrast ≥ 4.5:1 (verified against MD3 dynamic-color tuning).
- All non-text icons have `contentDescription` (i18n-aware).
- All interactive components have `Modifier.semantics { role = Role.Button }` or equivalent.
- Focus order on Desktop/Web follows visual reading order; Tab/Shift-Tab navigates predictably.

## i18n

All strings live in `composeResources/values/strings.xml` per feature module. Numeric formatting uses platform-native locale (`NumberFormat` on JVM/Android, `Intl.NumberFormat` on JS/Wasm, `NSNumberFormatter` on iOS — wrapped behind `expect/actual`).
