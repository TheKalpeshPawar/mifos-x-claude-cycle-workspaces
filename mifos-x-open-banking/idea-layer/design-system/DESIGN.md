---
name: Open Banking — Trust Blue
version: 1.0.0
description: >-
  Material 3 design system for a UK Open Banking AISP reference app. Calm,
  trustworthy, data-legible retail banking. Accessibility-first, regulated-industry
  restraint. Seeded from the Material Theme Builder export (primary #266489).
aesthetic_family: minimalist-ui
theme: auto
colors:
  primary: "#266489"
  on_primary: "#FFFFFF"
  primary_container: "#C9E6FF"
  secondary: "#50606E"
  tertiary: "#64597B"
  background: "#F7F9FF"
  surface: "#F7F9FF"
  surface_container: "#EBEEF3"
  on_surface: "#181C20"
  on_surface_variant: "#41474D"
  outline: "#72787E"
  error: "#BA1A1A"
  positive: "#266489"
  negative: "#BA1A1A"
typography:
  brand: Roboto
  body: Roboto
  mono: Roboto Mono
  scale: default
rounded:
  small: 8
  medium: 12
  large: 16
  extra_large: 28
spacing:
  base: 4
  screen_padding: 16
  density: comfortable
components:
  - card: { radius: "{rounded.medium}", container: "{colors.surface_container}", elevation: 1 }
  - button_filled: { container: "{colors.primary}", label: "{colors.on_primary}", radius: "{rounded.full}" }
  - list_item: { container: "{colors.surface}", supporting: "{colors.on_surface_variant}" }
  - amount: { font: "{typography.mono}", positive: "{colors.positive}", negative: "{colors.negative}" }
  - top_app_bar: { container: "{colors.surface}", title: "{colors.on_surface}" }
  - bottom_nav: { container: "{colors.surface_container}", active: "{colors.primary}" }
---

## Overview

Open Banking — Trust Blue is the design language for a UK Open Banking **AISP** (Account
Information) reference app. The product reads a customer's bank data — accounts, balances,
transactions, statements — strictly with their consent, and never moves money. The design's
job is therefore **trust and legibility**: the customer must always feel their data is handled
carefully, understand exactly what they are sharing, and read their finances at a glance.

The aesthetic is **minimalist Material 3** — restrained, grid-aligned, low-motion. It is a
regulated-industry, accessibility-first system: high contrast, generous touch targets, and no
decorative noise that could obscure financial data. The mood is a calm trust-blue: a
desaturated steel-blue primary (#266489) on near-white surfaces, with a quiet slate secondary
and a soft violet tertiary for occasional accent.

## Colors

The palette is the verbatim Material 3 role set from the theme export (29 light + 29 dark
roles in `design-tokens.yaml`). Key roles:

- **Primary `#266489`** (dark mode `#95CDF7`) — the brand trust-blue. Used for primary
  actions, the active bottom-nav tab, links, and selected states. Sparingly — it should mark
  intent, not fill the screen.
- **Secondary `#50606E`** — neutral slate for supporting controls and secondary emphasis.
- **Tertiary `#64597B`** — soft violet, reserved for category accents (e.g. PFM category chips).
- **Surface / Background `#F7F9FF`** with the tonal surface-container ladder
  (`#FFFFFF → #E0E3E8`) for cards, sheets, and elevation without shadows.
- **Error `#BA1A1A`** — also doubles as the **negative/debit** money colour; positive/credit
  uses the primary blue (never green-on-red, to stay calm and colour-blind-safe).

All foreground/background pairs meet **WCAG AA**. Theme is **auto** (follows the OS), with
dynamic colour enabled on Android 12+.

## Typography

**Roboto** throughout (Material 3 default), with **Roboto Mono** for monetary amounts and
account/sort-code numbers so figures align and scan cleanly. The full M3 type scale is in
`design-tokens.yaml`. Conventions:

- Screen titles: `headlineSmall` (24).
- Account balance / hero figures: `displaySmall`–`headlineMedium`, mono.
- List primary text: `bodyLarge` (16); supporting: `bodyMedium` (14) on `on_surface_variant`.
- Buttons / tabs: `labelLarge` (14, medium).

Avoid more than two type sizes per card. Let whitespace, not weight, create hierarchy.

## Layout

A single-column, **8dp grid**. Screen padding 16dp; comfortable density (`design_read`
density 5). Content is organised into M3 cards on the surface-container ladder. Lists are the
dominant pattern (accounts, transactions, beneficiaries) — full-width rows with a leading
glyph, primary + supporting text, and a trailing value or chevron. Detail screens use a
top-app-bar + scrollable content with grouped, labelled sections. The app shell is a
bottom-navigation scaffold (Accounts · Transactions · Consents · Settings).

## Elevation & Depth

Depth comes from **tonal surface containers**, not heavy shadows (M3 tonal elevation). Cards
sit on `surface_container` at elevation 1; sheets/dialogs at level 3. Keep elevation shallow —
a calm, flat banking surface reads as trustworthy. Reserve the highest containers for sticky
headers and the bottom-nav bar.

## Shapes

Soft, consistent rounding: small 8 / medium 12 / large 16 / extra-large 28dp. Cards use
`medium`; buttons are `full` (pill); bottom sheets use `extra_large` top corners. No sharp
0dp corners (that reads brutalist/cold for a consumer banking app).

## Components

- **Account / transaction list item** — leading category or bank glyph, primary label,
  supporting line (date / account type), trailing **mono amount** coloured positive (primary)
  or negative (error). 48dp min height.
- **Balance card** — hero mono figure, account label, available-vs-current sub-line.
- **Consent card** — clear "what you're sharing" permission list, expiry, and a revoke action;
  this is the trust-critical surface — always explicit, never truncated.
- **Filled button** (primary action), **outlined / text button** (secondary).
- **Category chip** (PFM) — tertiary-tinted, rounded-full.
- **Top app bar** + **bottom navigation** per the app shell.
- **State surfaces** — every data screen renders loading (skeleton), content, empty, and error
  (with retry) states.

## Do's and Don'ts

**Do**
- Keep primary blue for intent and the active tab only; let surfaces stay near-white/dark-grey.
- Show money in mono, credit in primary, debit in error.
- Make consent explicit: full permission list, expiry, easy revoke.
- Maintain WCAG AA contrast and 48dp touch targets everywhere.

**Don't**
- Don't use green/red money semantics or celebratory colour — this is calm, regulated finance.
- Don't add gradients/shadows for decoration (low-motion, low-variance system).
- Don't truncate or hide what data is being shared.
- Don't pin a `data-theme` — honour the OS (auto theme).
