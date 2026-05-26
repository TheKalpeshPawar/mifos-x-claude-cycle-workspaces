---
name: Mifos X Open Banking
version: "2.0.0"
generated_at: "2026-05-25"
token_source: design-tokens.yaml
design_system: material3
figma_source: "figma.com/design/tEEJwW4HkUR75fKhDq73Jz"
colors:
  primary: "#4C662B"
  secondary: "#386663"
  error: "#BA1A1A"
  background: "#F9FAEF"
  surface: "#FFFFFF"
typography:
  body:
    family: "Outfit"
rounded:
  small: 4
  medium: 12
  large: 16
spacing:
  unit: 8
platforms: [android, ios, desktop, web]
---

# Mifos X Open Banking — Design System

> Material Design 3 · Outfit typeface · Green primary `#4C662B` · 390px mobile baseline
> Extracted from Figma design system (file `tEEJwW4HkUR75fKhDq73Jz`).
> Token source-of-truth: `design-tokens.yaml`. Regenerated 2026-05-25.

## Overview

Open banking app for Mifos X — Consumer (account management, payments, cards) + Field Officer (customer onboarding, KYC, applications). Material 3 with an earth-green primary palette conveying financial stability and growth. Single typeface (Outfit) across all surfaces for a clean, modern feel.

## Colors

**Primary**: `#4C662B` — buttons, selected nav, credit indicators, FAB.
**Primary container**: `#CDEDA3` — balance card backgrounds, highlighted sections.
**Error / Debit**: `#BA1A1A` — debit amounts, failed badges, destructive actions.
**Pending**: `#E8A317` — initiated/pending transaction status badges.
**Tertiary accent**: `#386663` — accent text, secondary emphasis.

**Surfaces (light)**:
- Background: `#F9FAEF` (warm off-white, screen base)
- Surface (card): `#FFFFFF` (pure white cards on tinted background)
- Surface variant: `#E1E4D5` (dividers, disabled states)

**Text**:
- Primary text: `#1A1C16` (near-black, body + titles)
- Secondary text: `#44483D` (captions, supporting text)

**Borders**:
- Outline: `#75796C` (input field borders)
- Outline variant: `#C5C8BA` (card borders, dividers)

**Navigation**:
- Active indicator: `#DCE7C8` (tab pill background for selected nav item)
- On primary: `#FFFFFF` (text/icons on primary-colored surfaces)

Dark mode derives from the same seed using M3 tonal palette inversion — see `design-tokens.yaml` for full dark scheme.

## Typography

**Single typeface: Outfit** — geometric sans-serif, clean and modern. All weights from Regular (400) through SemiBold (600).

| Style | Size | Weight | Line Height | Usage |
|-------|------|--------|-------------|-------|
| Display Small | 32 | SemiBold | 40 | Hero balances, welcome headers |
| Headline Small | 24 | SemiBold | 32 | Section titles, screen headers |
| Title Large | 22 | Regular | 28 | Top app bar title |
| Title Medium | 16 | Medium | 24 | List primary text, card titles |
| Body Large | 16 | Regular | 24 | Body text, descriptions |
| Body Medium | 14 | Regular | 20 | Secondary content |
| Label Large | 14 | Medium | 20 | Button text |
| Label Medium | 12 | Medium | 16 | Chips, tabs |
| Label Small | 11 | Medium | 16 | Timestamps, metadata |

## Layout

- **Mobile baseline**: 390px width (iPhone 14 / Pixel 7)
- **Grid**: 8dp baseline grid
- **Content padding**: 16dp horizontal
- **Card gap**: 16dp vertical
- **Section spacing**: 24dp between groups
- **Touch targets**: 48dp minimum

## Elevation & Depth

Cards use border-based depth (`outline_variant` border, `md` radius) rather than shadow elevation — matching the Figma flat card style. Only FAB and dialogs use elevation.

| Surface | Elevation | Treatment |
|---------|-----------|-----------|
| Screen background | level0 | Flat `#F9FAEF` |
| Card | level0 | White + 1dp `#C5C8BA` border + 12dp radius |
| FAB | level3 | Primary fill + 16dp radius |
| Dialog | level3 | White + shadow |
| Bottom nav | level0 | Border-top `#C5C8BA` |

## Shapes

| Token | Value | Usage |
|-------|-------|-------|
| `radius.xs` | 4dp | Text fields |
| `radius.sm` | 8dp | Badges |
| `radius.md` | 12dp | Cards |
| `radius.lg` | 16dp | FAB |
| `radius.pill` | 999dp | Buttons (filled + outlined) |
| `radius.xl` | 24dp | Bottom sheets |

## Components

**Button / Filled**: `#4C662B` background, white text, 40dp height, pill radius, 24dp horizontal padding. Used for primary actions (Login, Send, Confirm).

**Button / Outlined**: `#75796C` border, `#4C662B` text, 40dp height, pill radius. Used for secondary actions (Continue with OBP-OIDC, Cancel).

**FAB / Primary**: 56dp square, `#4C662B` fill, 16dp radius. Used for primary creation actions (new payment, new beneficiary).

**Badge / Success**: `#4C662B` fill, white text, 24dp height, 8dp radius. Shows "COMPLETED".
**Badge / Pending**: `#E8A317` fill, white text. Shows "INITIATED".
**Badge / Failed**: `#BA1A1A` fill, white text. Shows "FAILED".

**TextField**: White fill, `#75796C` border, 56dp height, 4dp radius. Label in `Label Small` (11/Medium), value in `Body Large` (16/Regular).

**Card / Base**: White fill, `#C5C8BA` border, 12dp radius, 16dp padding. Title in `Title Medium`, supporting text in `Body Medium` `#44483D`.

**TopBar / Default**: `#F9FAEF` background, 56dp height, back arrow + `Title Large` title.

**BottomNav**: `#F9FAEF` background, `#C5C8BA` border-top, 80dp height. 4 tabs: Home, Accounts, Payments, Profile. Active tab: `#DCE7C8` pill indicator + `#1A1C16` text. Inactive: `#44483D` text.

## Do's and Don'ts

**Do**: Use primary green (`#4C662B`) only for interactive elements — buttons, selected states, credit amounts. Keep backgrounds warm off-white (`#F9FAEF`).

**Don't**: Use primary green for large background areas — it becomes overwhelming. Use `primary_container` (`#CDEDA3`) for highlighted cards instead.

**Do**: Use the pending color (`#E8A317`) exclusively for in-progress states. Use error (`#BA1A1A`) for failed/debit.

**Don't**: Mix pending and error colors on the same surface. Each status badge should use exactly one semantic color.

**Do**: Maintain the single-typeface discipline — Outfit for everything. Weight and size create hierarchy, not font switching.

**Don't**: Add additional typefaces for "variety." The Figma system uses Outfit exclusively.
