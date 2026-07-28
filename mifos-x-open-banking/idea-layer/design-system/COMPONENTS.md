# COMPONENTS.md — Open Banking — Trust Blue

> Component catalog for the AISP app. Tokens resolve against `design-tokens.yaml`.
> Material 3, minimalist-ui, accessibility-first (WCAG AA, 48dp touch targets).

## Core components

| Component | Role | Key tokens |
|---|---|---|
| `top_app_bar` | Screen title + back/actions | container `surface`, title `on_surface` |
| `bottom_nav` | App shell (Accounts · Transactions · Consents · Settings) | container `surfaceContainer`, active `primary` |
| `card` | Grouping surface (balances, sections) | container `surfaceContainer`, radius `medium`, elevation 1 |
| `list_item` | Account / transaction / beneficiary row | primary `on_surface`, supporting `on_surface_variant`, 48dp min |
| `amount` | Monetary value | mono font; credit `primary`, debit `error` |
| `balance_hero` | Account balance figure | `displaySmall` mono, available/current sub-line |
| `consent_card` | What's being shared + expiry + revoke (trust-critical) | permission list, `error` revoke action |
| `permission_row` | One permission in a consent | label + on/off state, never truncated |
| `button_filled` | Primary action | container `primary`, label `on_primary`, radius `full` |
| `button_outlined` / `button_text` | Secondary action | outline `outline` |
| `category_chip` | PFM category tag | tertiary-tinted, radius `full` |
| `text_field` | Search inputs (transactions, beneficiaries) | outline `outline`, focus `primary` |
| `segmented_filter` | Transaction filters (all/credit/debit, period) | selected `secondaryContainer` |
| `state_loading` | Skeleton shimmer | `surfaceContainer` placeholders |
| `state_empty` | No data | glyph + message + optional CTA |
| `state_error` | Failure | message + **retry** action |
| `chart_donut` | UNUSED — declared for the PFM breakdown; that screen was never built (removed 2026-07-28) | tertiary/secondary tints per category |
| `progress_budget` | Budget tracker bar | `primary` fill, over-budget `error` |

## States contract

Every data-backed screen renders **loading → content → empty → error(+retry)**. Forms add
`submitting`. Auth-gated surfaces add `unauthenticated`.

## Money semantics

Credit/incoming = `primary`. Debit/outgoing = `error`. No green/red. Amounts always mono,
right-aligned in lists.
