---
name: Open Banking — Trust Blue
version: 1.1.0
description: >-
  Material 3 design system for a UK Open Banking AISP + PISP reference app. Calm,
  trustworthy, data-legible retail banking that now also moves money. Accessibility-first,
  regulated-industry restraint. Seeded from the Material Theme Builder export (primary #266489).
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
  - text_field: { radius: "{rounded.small}", outline: "{colors.outline}", focus: "{colors.primary}", error: "{colors.error}" }
  - amount_field: { font: "{typography.mono}", scale: headlineSmall, radius: "{rounded.small}" }
  - status_chip: { in_progress: "{colors.secondary}", success: "{colors.primary}", failure: "{colors.error}" }
  - review_card: { radius: "{rounded.medium}", container: "{colors.surface_container}", elevation: 1 }
---

## Overview

Open Banking — Trust Blue is the design language for a UK Open Banking **AISP + PISP**
reference app. The product reads a customer's bank data — accounts, balances, transactions,
statements — strictly with their consent, and **initiates domestic payments on their
instruction**. The design's job is therefore **trust and legibility**: the customer must
always feel their data is handled carefully, understand exactly what they are sharing, read
their finances at a glance, and — before any money moves — see precisely what they are about
to commit to.

> **Changed in 1.1.0.** Through 1.0.0 this app never moved money, and the system was written
> for a read-only product: no forms beyond search, no field validation, no irreversible
> actions, and a two-way money palette (credit / debit). Payment initiation breaks all four
> assumptions. The additions are confined to three areas — **form input and validation**,
> **payment disposition**, and the **irreversible-action contract** — plus a correction to
> the documented bottom-nav rail, which had been wrong since the 2026-07-28 reverse sync.
> No colour role, type scale, radius or spacing value changed.

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
- **Tertiary `#64597B`** — soft violet. Currently **unused in production**: it was reserved
  for PFM category accents, and the PFM screens were removed in the 2026-07-28 reverse sync.
  Kept in the palette as the third M3 role, but do not reach for it to differentiate payment
  states — those use the secondary/primary/error triad below, which carries meaning.
- **Surface / Background `#F7F9FF`** with the tonal surface-container ladder
  (`#FFFFFF → #E0E3E8`) for cards, sheets, and elevation without shadows.
- **Error `#BA1A1A`** — also doubles as the **negative/debit** money colour; positive/credit
  uses the primary blue (never green-on-red, to stay calm and colour-blind-safe).

### Payment disposition — a submitted payment is not a boolean

A successful submit returns `AcceptedSettlementInProcess`: accepted, **not settled**. Showing
that as success is a false statement about someone's money, so the system gives it its own
identity rather than folding it into a success/failure pair.

| Disposition | Role | Container / on-container | Icon | Contrast |
|---|---|---|---|---|
| **In progress** | `secondary` | `#D3E5F5` / `#384956` | `schedule` | 7.22:1 |
| **Settled** | `primary` | `#C9E6FF` / `#004B6F` | `check_circle` | 7.27:1 |
| **Rejected** | `error` | `#FFDAD6` / `#93000A` | `error` | 7.24:1 |

In progress is deliberately **not** primary. Primary is already the credit colour here, so a
primary chip would read as *money arrived*. Neutral slate reads as *working*.

**Colour is never the only signal.** Every disposition carries its icon **and** its text
label. That is WCAG 1.4.1, and it is also what makes the rule auditable — a reviewer can read
the label and see whether a screen is claiming a settlement it does not have. An OBIE status
outside the mapped vocabulary renders as **in progress**, never as success or failure.

All foreground/background pairs meet **WCAG AA** — 15 pairs measured for 1.1.0, ratios
recorded in `state/DESIGN_SYSTEM_STATE.yaml`. Theme is **auto** (follows the OS), with dynamic
colour enabled on Android 12+.

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
top-app-bar + scrollable content with grouped, labelled sections.

The app shell is a bottom-navigation scaffold: **Home · Accounts · Pay · More**. (Corrected in
1.1.0 — this section previously documented "Accounts · Transactions · Consents · Settings",
which stopped being true at the 2026-07-28 reverse sync. Transactions is reached from account
detail and from Home's "View all", never from a tab; consents live under More → Settings.)

**Multi-step forms** — new in 1.1.0, and so far only send-money — advance one step per screenful
rather than scrolling one long form: choose the funding account and payee, then the amount, then
review. Each step ends in a single primary action; the step indicator is textual, not a
decorative progress bar, in keeping with the low-motion dial.

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
- **Top app bar** + **bottom navigation** per the app shell.
- **State surfaces** — every data screen renders loading (skeleton), content, empty, and error
  (with retry) states. Forms add **submitting**; payment screens add **success**.

Added in 1.1.0 for payments:

- **Text field** — 8dp radius (tighter than a card's 12dp), 56dp min height, label above,
  helper or error text below. Validation runs **on change after the first blur**: flagging a
  half-typed amount as wrong reads as hostile, but waiting until submit makes correction slow.
- **Amount field** — mono `headlineSmall`, currency symbol as a non-editable prefix. Mono so
  digits don't reflow while typing. Held and validated as minor units; displayed formatted.
- **Status chip** — the disposition triad above; icon + label always, colour never alone.
- **Review card** — the last surface before money moves. Lists every value that will be
  committed: funding account, payee, amount, reference. Nothing summarised, nothing truncated.
  It is to payments what the consent card is to data sharing, and it is trust-critical in the
  same way.

**Removed in 1.1.0** — `category_chip`, `chart_donut` and `progress_budget` were declared for
PFM screens that were never built and were deleted on 2026-07-28. They are struck from the
catalog rather than left as aspirational entries a generator might try to satisfy.

## Do's and Don'ts

**Do**
- Keep primary blue for intent and the active tab only; let surfaces stay near-white/dark-grey.
- Show money in mono, credit in primary, debit in error.
- Make consent explicit: full permission list, expiry, easy revoke.
- Maintain WCAG AA contrast and 48dp touch targets everywhere.
- Show a review surface listing every committed value before money moves, with a same-weight
  escape beside the confirm.
- Label the confirm CTA with the action **and the amount** — "Send £850.00", not "Confirm".
- Lock the CTA and show progress on tap, so double-submission is impossible from the UI.
- Show running balances **unsigned**, in neutral.

**Don't**
- Don't use green/red money semantics or celebratory colour — this is calm, regulated finance.
  This applies with full force to a completed payment: a settled payment gets the trust-blue
  chip, not a green tick and not a celebration.
- Don't render an in-progress payment as sent, complete, or successful — see Payment disposition.
- Don't colour the send-money confirm CTA `error`. Red frames a payment the customer intends as
  a danger; red is reserved for genuine failure. Weight comes from the review surface and the
  amount in the label.
- Don't sign a running balance off a per-transaction credit/debit indicator — that indicator
  describes the transaction, not the balance, and signing on it renders a healthy account
  negative.
- Don't add gradients/shadows for decoration (low-motion, low-variance system).
- Don't truncate or hide what data is being shared, or what a payment will commit.
- Don't pin a `data-theme` — honour the OS (auto theme).
