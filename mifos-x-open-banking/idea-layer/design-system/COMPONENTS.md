# COMPONENTS.md — Open Banking — Trust Blue

> Component catalog for the AISP + PISP app. Tokens resolve against `design-tokens.yaml`.
> Material 3, minimalist-ui, accessibility-first (WCAG AA, 48dp touch targets).
> v1.1.0 (2026-07-30) — payment components added; PFM components removed.

## Core components

| Component | Role | Key tokens |
|---|---|---|
| `top_app_bar` | Screen title + back/actions | container `surface`, title `on_surface` |
| `bottom_nav` | App shell (**Home · Accounts · Pay · More**) | container `surfaceContainer`, active `primary` |
| `card` | Grouping surface (balances, sections) | container `surfaceContainer`, radius `medium`, elevation 1 |
| `list_item` | Account / transaction / beneficiary row | primary `on_surface`, supporting `on_surface_variant`, 48dp min |
| `amount` | Monetary value | mono; credit `primary`, debit `error`, unsigned balance `neutral` |
| `balance_hero` | Account balance figure | `displaySmall` mono, available/current sub-line |
| `consent_card` | What's being shared + expiry + revoke (trust-critical) | permission list, `error` revoke action |
| `permission_row` | One permission in a consent | label + on/off state, never truncated |
| `button_filled` | Primary action | container `primary`, label `on_primary`, radius `full` |
| `button_outlined` / `button_text` | Secondary action | outline `outline` |
| `chip` | Generic assist chip | radius `full` |
| `text_field` | Text input — search **and** form entry | radius `small`, outline `outline`, focus `primary`, error `error` |
| `segmented_filter` | Transaction filters (all/credit/debit, period) | selected `secondaryContainer` |
| `state_loading` | Skeleton shimmer | `surfaceContainer` placeholders |
| `state_empty` | No data | glyph + message + optional CTA |
| `state_error` | Failure | message + **retry** action |

## Payment components (added 1.1.0)

| Component | Role | Key tokens |
|---|---|---|
| `amount_field` | Money entry | mono `headlineSmall`, radius `small`, currency prefix non-editable |
| `field_error` | Field-level validation message | `error` text, `bodySmall`, below field, 2dp `error` outline on the field |
| `status_chip` | Payment disposition | in-progress `secondaryContainer` · settled `primaryContainer` · rejected `errorContainer`; **icon + label always** |
| `review_card` | Final surface before money moves | container `surfaceContainer`, radius `medium`; every committed value listed in full |
| `step_indicator` | Multi-step form position | textual ("Step 2 of 3"), `labelMedium` `on_surface_variant` — not a progress bar |
| `payment_summary_row` | One label/value pair inside `review_card` | label `on_surface_variant`, value `on_surface`, amounts mono |

## Removed 1.1.0

`category_chip`, `chart_donut`, `progress_budget` — declared for the PFM dashboard,
spending-by-category and budgets screens, none of which were built. The screens were deleted
in the 2026-07-28 reverse sync. Struck from the catalog so a generator does not try to satisfy
an aspirational entry.

## States contract

Every data-backed screen renders **loading → content → empty → error(+retry)**. Forms add
`submitting`. Payment screens add `success`. Auth-gated surfaces add `unauthenticated`.

## Money semantics

Credit/incoming = `primary`. Debit/outgoing = `error`. Running balances = `neutral`, unsigned.
No green/red. Amounts always mono, right-aligned in lists.

**A payment is not a boolean.** In progress = `secondary` (slate), settled = `primary`,
rejected = `error`. In progress is deliberately not primary — primary is the credit colour, so
a primary chip would read as "money arrived". Colour is never the only signal: each state
carries its icon and its text label.

## Irreversible actions

`send_money_confirm` and `consent_revoke` require: a review surface listing every committed
value; a CTA naming the action and amount ("Send £850.00"); a same-weight escape beside it; and
a CTA that locks with progress on tap. The send-money confirm stays `primary` — red would frame
an intended payment as a danger, and red is reserved for genuine failure.
