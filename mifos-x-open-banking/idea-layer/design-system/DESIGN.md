---
name: Mifos X Open Banking
version: "3.0.0"
generated_at: "2026-05-28"
token_source: design-tokens.yaml
design_system: material3
figma_source: "figma.com/design/tEEJwW4HkUR75fKhDq73Jz"
aesthetic_family: taste-default
colors:
  primary: "#4C662B"
  secondary: "#386663"
  accent: "#CDEDA3"
  error: "#BA1A1A"
  background: "#F9FAEF"
  surface: "#FFFFFF"
typography:
  body:
    family: "Outfit"
  heading:
    family: "Outfit"
rounded:
  small: 4
  medium: 12
  large: 16
spacing:
  gap: 16
  padding: 16
  unit: 8
platforms: [android, ios, desktop, web]
---

# Mifos X Open Banking — Design System

> Material Design 3 · Outfit typeface · Green primary `#4C662B` · 390px mobile baseline
> Figma source: `tEEJwW4HkUR75fKhDq73Jz`. Token source-of-truth: `design-tokens.yaml` (schema v3.0).
> Regenerated 2026-05-28 via /design-system --force.

## Overview

Professional open banking super-app for Mifos X — earth-green M3 palette, card-based layouts, trust-first density with measured motion. Serves two user personas: Consumer (account management, payments, cards) and Field Officer (customer onboarding, KYC, loan applications). The palette conveys financial stability and responsible growth. A single typeface (Outfit) and a warm off-white background create a clean, modern, trustworthy surface across all screens.

Aesthetic family: `taste-default` — variance dial 4 (measured expressiveness, not loud). Motion is intentional and brief; elevation is flat-card style (border-based depth) except for FAB and dialogs.

## Colors

**Primary palette** — earth green signals reliability and growth:
- `primary` `#4C662B` — buttons, selected nav items, credit amounts, FAB
- `primary_container` `#CDEDA3` — balance card backgrounds, highlighted rows
- `on_primary` `#FFFFFF` — text/icons on primary surfaces
- `on_primary_container` `#102000` — text on primary_container

**Secondary palette** — teal accent for field-officer surfaces and supporting emphasis:
- `secondary` `#386663`
- `secondary_container` `#BCEBE7`

**Semantic colors**:
- `error` `#BA1A1A` — debit amounts, failed badges, destructive actions
- `pending` `#E8A317` — initiated/in-flight transaction status badges

**Surfaces (light scheme)**:
- `background` `#F9FAEF` — warm off-white, screen base
- `surface` `#FFFFFF` — pure white cards floating on background
- `surface_variant` `#E1E4D5` — dividers, disabled states, shimmer base
- `surface_container` `#F0F1E6` — grouped content containers
- `surface_container_high` `#EAECE1` — elevated inner containers

**Text**:
- `on_background` / `on_surface` `#1A1C16` — near-black, primary body and titles
- `on_surface_variant` `#44483D` — captions, supporting text, inactive nav labels

**Borders**:
- `outline` `#75796C` — input field borders, active focus rings
- `outline_variant` `#C5C8BA` — card borders, dividers, bottom nav border-top

**Navigation**:
- `nav_active_indicator` `#DCE7C8` — active tab pill background

Dark scheme: full 29-role M3 tonal inversion — see `design-tokens.yaml#colors.dark`.

## Typography

Single typeface: **Outfit** — geometric sans-serif, clean and modern. All weights from Regular (400) through SemiBold (600). Chosen for legibility at small sizes on financial data and for warm geometric character that avoids the cold precision of pure neutrals.

| Style | Size (sp) | Weight | Line Height | Tracking | Usage |
|-------|-----------|--------|-------------|---------|-------|
| Display Large | 57 | Regular | 64 | -0.25 | (reserved — not used in current screen set) |
| Display Medium | 45 | Regular | 52 | 0 | (reserved) |
| Display Small | 32 | SemiBold | 40 | 0 | Hero balances, welcome headers |
| Headline Large | 32 | Regular | 40 | 0 | (reserved) |
| Headline Medium | 28 | Regular | 36 | 0 | (reserved) |
| Headline Small | 24 | SemiBold | 32 | 0 | Section titles, screen headers |
| Title Large | 22 | Regular | 28 | 0 | Top app bar title |
| Title Medium | 16 | Medium | 24 | 0.15 | List primary text, card titles |
| Title Small | 14 | Medium | 20 | 0.1 | Subsection labels |
| Body Large | 16 | Regular | 24 | 0.5 | Body text, form field values |
| Body Medium | 14 | Regular | 20 | 0.25 | Secondary descriptions |
| Body Small | 12 | Regular | 16 | 0.4 | Timestamps, captions |
| Label Large | 14 | Medium | 20 | 0.1 | Button text, tab labels |
| Label Medium | 12 | Medium | 16 | 0.5 | Chips, badges, tags |
| Label Small | 11 | Medium | 16 | 0.5 | Metadata, timestamps |

Minimum body text size: 14sp (enforced via `touchTargets.min_text_size`).

## Layout

- **Mobile baseline**: 390px width (iPhone 14 / Pixel 7)
- **Grid**: 8dp baseline grid (`spacing.unit = 8`)
- **Content padding**: 16dp horizontal (`spacing.md`)
- **Card gap**: 16dp vertical between cards (`spacing.md`)
- **Section spacing**: 24dp between groups (`spacing.lg`)
- **Touch targets**: 48dp minimum (`touchTargets.min_touch_target`)
- **Touch target gap**: 8dp between adjacent interactive elements

Cards occupy full content width (390 - 32 = 358dp usable) with 12dp radius and a single-pixel `outline_variant` border. No horizontal scroll surfaces on primary flows.

## Elevation & Depth

Cards use border-based depth (`outline_variant` border, `radius.md` = 12dp) rather than shadow elevation — matching the Figma flat card aesthetic and improving legibility on the warm `#F9FAEF` background. Only FAB and dialogs use material elevation.

| Surface | Level | Treatment |
|---------|-------|-----------|
| Screen background | level0 | Flat `#F9FAEF` |
| Card / Base | level0 | White + 1dp `#C5C8BA` border + 12dp radius |
| Surface container | level0 | `#F0F1E6` grouped container |
| Bottom nav | level0 | Border-top `#C5C8BA` |
| FAB | level3 (6dp shadow) | Primary fill `#4C662B` + 16dp radius |
| Dialog / Bottom sheet | level3 (6dp shadow) | White + scrim |

## Shapes

| Token | Value | Usage |
|-------|-------|-------|
| `radius.none` | 0dp | Sharp corners — rare |
| `radius.xs` | 4dp | Text fields |
| `radius.sm` | 8dp | Badges, chips |
| `radius.md` | 12dp | Cards, balance containers |
| `radius.lg` | 16dp | FAB, bottom sheet top corners |
| `radius.xl` | 24dp | Modal bottom sheets |
| `radius.pill` | 999dp | Buttons (filled + outlined) |

## Components

**Button / Filled**: `#4C662B` background, white text (Label Large 14sp/Medium), 40dp height, pill radius (999dp), 24dp horizontal padding. Used for primary actions — Login, Send, Confirm.

**Button / Outlined**: `#75796C` 1dp border, `#4C662B` text, same height/radius. Used for secondary actions — Continue with OBP-OIDC, Cancel.

**Button / Text**: `#4C662B` text, 14sp Medium. Tertiary actions — Forgot password, See all.

**FAB / Primary**: 56dp square, `#4C662B` fill, 16dp radius, white "+" icon 28dp. New payment, Add beneficiary.

**Badge / Success**: `#4C662B` fill, white text, 24dp height, 8dp radius, 10dp padding. "COMPLETED".
**Badge / Pending**: `#E8A317` fill, white text. "INITIATED".
**Badge / Failed**: `#BA1A1A` fill, white text. "FAILED".

**TextField / Default**: White fill, `#75796C` border, 56dp height, 4dp radius. Label in Label Small (11sp/Medium), value in Body Large (16sp/Regular).

**Card / Base**: White fill, `#C5C8BA` border, 12dp radius, 16dp padding.

**Balance Card**: `#CDEDA3` fill, 16dp radius, no border. Amount in Display Small (32sp/SemiBold).

**TopBar / Default**: `#F9FAEF` background, 56dp height, Title Large (22sp/Regular).

**BottomNav**: `#F9FAEF` background, `#C5C8BA` border-top, 80dp height. 4 tabs: Home, Accounts, Payments, Profile. Active: `#DCE7C8` pill indicator.

See `COMPONENTS.md` for full component spec with Compose implementation targets.

## Do's and Don'ts

**Do**: Use primary green (`#4C662B`) only for interactive elements — buttons, selected states, credit amounts, FAB. Its high contrast on white (5.8:1) makes it ideal for actionable elements.

**Don't**: Use primary green for large background areas. Use `primary_container` (`#CDEDA3`) for highlighted cards — it's much lighter and avoids overwhelming the user.

**Do**: Use `pending` (`#E8A317`) exclusively for in-progress transaction states. Use `error` (`#BA1A1A`) exclusively for failed/debit states. These two semantic colors must never appear together on the same badge or label.

**Don't**: Mix pending and error colors on the same surface. Each status badge uses exactly one semantic color.

**Do**: Maintain the single-typeface discipline — Outfit for every surface, every weight, every size. Weight and size alone create hierarchy.

**Don't**: Introduce additional typefaces for display or marketing copy. The Figma system is Outfit-only; adding a second face breaks the clean, unified feel.

**Do**: Keep touch targets at 48dp minimum for all interactive elements, even when the visual affordance appears smaller (e.g., icon-only buttons — wrap with a 48dp invisible tap zone).

**Don't**: Place interactive elements within 8dp of each other. The `touchTargets.spacing_between_targets = 8dp` rule prevents mis-taps on financial actions like "Send" and "Cancel."
