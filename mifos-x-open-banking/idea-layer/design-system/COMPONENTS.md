---
name: Mifos X Open Banking — Components
version: "3.0.0"
generated_at: "2026-05-28"
figma_source: "tEEJwW4HkUR75fKhDq73Jz"
token_source: design-tokens.yaml
category: banking
---

# Mifos X Open Banking — Component Library

> M3 components extracted from Figma design system (schema v3.0). Each entry documents the Figma component spec, design token references, and Compose implementation target.
> Regenerated 2026-05-28 via /design-system --force.

## Buttons

### Button / Filled
- **Figma**: `colors.light.primary` (`#4C662B`) background, `colors.light.on_primary` (`#FFFFFF`) text, 40dp height, `radius.pill` (999dp) border-radius, 24dp horizontal padding
- **Typography**: `typography.scale.label_lg` — Outfit Medium 14sp / 20sp line-height
- **Min touch target**: 48dp (via `touchTargets.min_touch_target`)
- **Compose**: `Button(colors = ButtonDefaults.buttonColors(containerColor = Primary))`
- **Token refs**: `component_tokens.button.height_default`, `component_tokens.button.padding_horizontal`, `component_tokens.button.radius`
- **Usage**: Primary actions — Login, Send, Confirm, Save, Apply

### Button / Outlined
- **Figma**: 1dp `colors.light.outline` (`#75796C`) border, `colors.light.primary` (`#4C662B`) text, 40dp height, `radius.pill` (999dp) border-radius, 24dp horizontal padding
- **Typography**: `typography.scale.label_lg` — Outfit Medium 14sp
- **Compose**: `OutlinedButton(border = BorderStroke(1.dp, Outline))`
- **Usage**: Secondary actions — Continue with OBP-OIDC, Cancel, Skip

### Button / Text
- **Typography**: `typography.scale.label_lg` — Outfit Medium 14sp, `colors.light.primary` (`#4C662B`) color
- **Compose**: `TextButton(colors = ButtonDefaults.textButtonColors(contentColor = Primary))`
- **Usage**: Tertiary actions — Forgot password, See all, navigation links

## FAB

### FAB / Primary
- **Figma**: 56dp square, `component_tokens.fab.radius` = `radius.lg` (16dp) border-radius, `colors.light.primary` (`#4C662B`) background, white "+" icon 28dp
- **Min touch target**: naturally 56dp — satisfies 48dp requirement
- **Compose**: `FloatingActionButton(containerColor = Primary, shape = RoundedCornerShape(16.dp))`
- **Token refs**: `component_tokens.fab.size`, `component_tokens.fab.radius`, `component_tokens.fab.background`
- **Usage**: Primary creation — New payment, Add beneficiary, New account

## Badges

### Badge / Success
- **Figma**: `colors.light.primary` (`#4C662B`) background, `colors.light.on_primary` (`#FFFFFF`) text, 24dp height, `radius.sm` (8dp) border-radius, 10dp horizontal padding
- **Typography**: `typography.scale.label_md` — Outfit Medium 12sp
- **Token refs**: `component_tokens.badge.height`, `component_tokens.badge.radius`, `component_tokens.badge.variants.success`
- **Content**: "COMPLETED"

### Badge / Pending
- **Figma**: `colors.light.pending` (`#E8A317`) background, white text, same dimensions
- **Token refs**: `component_tokens.badge.variants.pending`
- **Content**: "INITIATED"

### Badge / Failed
- **Figma**: `colors.light.error` (`#BA1A1A`) background, white text, same dimensions
- **Token refs**: `component_tokens.badge.variants.failed`
- **Content**: "FAILED"

## Inputs

### TextField / Default
- **Figma**: `colors.light.surface` (white) background, 1dp `colors.light.outline` (`#75796C`) border, 56dp height (`component_tokens.text_field.height`), `radius.xs` (4dp) border-radius, 16dp horizontal padding, 8dp vertical padding
- **Label**: `typography.scale.label_sm` — Outfit Medium 11sp, `colors.light.outline` (`#75796C`)
- **Value**: `typography.scale.body_lg` — Outfit Regular 16sp, `colors.light.on_surface` (`#1A1C16`)
- **Min touch target**: 56dp height satisfies 48dp requirement; label area also has 48dp interactive zone
- **Compose**: `OutlinedTextField(shape = RoundedCornerShape(4.dp))`
- **Token refs**: `component_tokens.text_field.height`, `component_tokens.text_field.radius`, `component_tokens.text_field.border_color`

## Surfaces

### Card / Base
- **Figma**: `colors.light.surface` (white) background, 1dp `colors.light.outline_variant` (`#C5C8BA`) border, `radius.md` (12dp) border-radius, `spacing.md` (16dp) padding
- **Title**: `typography.scale.title_md` — Outfit Medium 16sp, `colors.light.on_surface` (`#1A1C16`)
- **Supporting text**: `typography.scale.body_md` — Outfit Regular 14sp, `colors.light.on_surface_variant` (`#44483D`)
- **Compose**: `Card(border = BorderStroke(1.dp, OutlineVariant), shape = RoundedCornerShape(12.dp))`
- **Token refs**: `component_tokens.card.radius`, `component_tokens.card.padding`, `component_tokens.card.border_color`, `component_tokens.card.elevation`

### Balance Card (Banking)
- **Figma**: `colors.light.primary_container` (`#CDEDA3`) background, `radius.lg` (16dp) border-radius, 20dp padding, no border, `elevation.level0`
- **Label**: `typography.scale.body_md` — Outfit Regular 14sp, `colors.light.on_surface_variant` (`#44483D`)
- **Amount**: `typography.scale.display_sm` — Outfit SemiBold 32sp / 40sp line-height, `colors.light.on_surface` (`#1A1C16`)
- **Subtitle**: `typography.scale.body_sm` — Outfit Regular 12sp, `colors.light.on_surface_variant` (`#44483D`)
- **Gradient overlay**: `mood_gradients.growth_dawn` (optional hero treatment)
- **Compose**: `Card(colors = CardDefaults.cardColors(containerColor = PrimaryContainer), shape = RoundedCornerShape(16.dp))`

### Transaction Item (Banking)
- **Container**: `colors.light.surface` (white) fill, `colors.light.outline_variant` border, `radius.md` (12dp) border-radius, `spacing.md` (16dp) padding
- **Icon**: 40dp circle with `colors.light.background` (`#F9FAEF`) fill
- **Merchant**: `typography.scale.title_md` — Outfit Medium 16sp, `colors.light.on_surface` (`#1A1C16`)
- **Category**: `typography.scale.body_sm` — Outfit Regular 12sp, `colors.light.on_surface_variant` (`#44483D`)
- **Amount (credit)**: `typography.scale.title_md` — Outfit Medium 16sp, `colors.light.primary` (`#4C662B`)
- **Amount (debit)**: `typography.scale.title_md` — Outfit Medium 16sp, `colors.light.error` (`#BA1A1A`)
- **Badge**: inline, right-aligned — see Badge section

## Navigation

### TopBar / Default
- **Figma**: `colors.light.background` (`#F9FAEF`) fill, `component_tokens.app_bar.height` (56dp) height, 16dp horizontal padding
- **Back arrow**: 24dp `colors.light.on_surface` (`#1A1C16`)
- **Title**: `typography.scale.title_lg` — Outfit Regular 22sp / 28sp line-height
- **Gap**: 16dp between arrow and title
- **Min touch target**: back arrow tappable area padded to 48dp
- **Compose**: `TopAppBar(colors = TopAppBarDefaults.topAppBarColors(containerColor = Background))`
- **Token refs**: `component_tokens.app_bar.height`, `component_tokens.app_bar.background`

### BottomNav / Home
- **Figma**: `colors.light.background` (`#F9FAEF`) fill, 1dp `colors.light.outline_variant` (`#C5C8BA`) border-top, `component_tokens.bottom_nav.height` (80dp) height
- **Layout**: 4 tabs evenly spaced — Home, Accounts, Payments, Profile
- **Active tab**: Icon inside 64×28dp pill with `colors.light.nav_active_indicator` (`#DCE7C8`) fill, 14dp pill radius. Label `typography.scale.label_sm` — Outfit Medium 11sp, `colors.light.on_surface` (`#1A1C16`)
- **Inactive tab**: No pill. Label `typography.scale.label_sm` — Outfit Medium 11sp, `colors.light.on_surface_variant` (`#44483D`)
- **Touch target per tab**: 80dp height satisfies 48dp; each tab is ≥80dp wide on a 390dp screen
- **Compose**: `NavigationBar(containerColor = Background)`
- **Token refs**: `component_tokens.bottom_nav.height`, `component_tokens.bottom_nav.background`, `component_tokens.bottom_nav.border_top`, `component_tokens.bottom_nav.active_indicator`, `component_tokens.bottom_nav.tabs`

## Search

### Search Bar / Default
- **Figma**: `colors.light.surface_container` (`#F0F1E6`) fill, `radius.pill` (999dp) border-radius, 56dp height, 16dp horizontal padding, search icon 24dp left, clear icon 24dp right (when active)
- **Placeholder**: `typography.scale.body_lg` — Outfit Regular 16sp, `colors.light.on_surface_variant` (`#44483D`)
- **Compose**: `SearchBar` or `DockedSearchBar` per M3 spec

## Feedback

### Loading States
- **Skeleton shimmer**: Gradient sweep `colors.light.surface_variant` (`#E1E4D5`) → `colors.light.background` (`#F9FAEF`); `motion.duration.long1` (450ms) linear infinite; `mood_gradients.trust_horizon` as base.
- **Circular spinner**: 3dp border, `colors.light.primary_container` (`#CDEDA3`) track, `colors.light.primary` (`#4C662B`) active arc; `motion.duration.long2` (500ms) linear
- **Pattern**: Chrome (TopBar, BottomNav) stays real during loading. Content surfaces replaced by skeletons matching the content layout geometry.

### Empty / Error States
- **Empty**: Centered icon (48dp, `colors.light.on_surface_variant` `#75796C`) + title `typography.scale.title_md` + description `typography.scale.body_md` (`#44483D`) + optional Button / Filled
- **Error**: Same layout, icon color `colors.light.error` (`#BA1A1A`), "Retry" Button / Filled

### Dialog / Bottom Sheet
- **Dialog**: `colors.light.surface` (white) fill, `elevation.level3` (6dp) shadow, `radius.xl` (24dp) top corners, `spacing.lg` (24dp) content padding
- **Bottom Sheet**: Same as dialog, anchors to screen bottom, scrim `colors.light.scrim` at 40% opacity

## Design Tokens Quick Reference

| Token | Light | Dark |
|-------|-------|------|
| primary | `#4C662B` | `#B2D188` |
| primary_container | `#CDEDA3` | `#354E16` |
| secondary | `#386663` | `#A0CFCB` |
| background | `#F9FAEF` | `#12140E` |
| surface | `#FFFFFF` | `#12140E` |
| error | `#BA1A1A` | `#FFB4AB` |
| pending | `#E8A317` | `#E8A317` |
| outline | `#75796C` | `#8F9285` |
| outline_variant | `#C5C8BA` | `#44483D` |
| on_surface (text primary) | `#1A1C16` | `#E3E3D8` |
| on_surface_variant (text secondary) | `#44483D` | `#C5C8BA` |
| nav_active_indicator | `#DCE7C8` | `#354E16` |

_Generated by /design-system --force · 2026-05-28 · schema v3.0 · Figma source: tEEJwW4HkUR75fKhDq73Jz_
