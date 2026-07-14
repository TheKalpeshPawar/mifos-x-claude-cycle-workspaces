# /idea completeness — mifos-x-open-banking — 2026-07-14

**Args:** `ignore server and stitch mockups`
**Scope (clarified):** nav graph + **API coverage** (third-party HSBC/OBIE surface). Excluded: server-layer plans / self-owned-backend "apis absence" (this app is a third-party API consumer — no backend to build); stitch/mockups/preview.
**Entry screen:** `user-onboarding` · bottom-nav roots: home, accounts, transactions, settings.
**Inventory:** 25 screens (all `status: enriched`, q94–98; each with ui/flow/api/docs.yaml), 18 features, 20 documented third-party endpoints.

## Gap matrix (before → after)

| Source | Before | After |
|---|---|---|
| A — missing screens | 0 | 0 |
| A — broken wiring | 1 | **0** |
| A — unreachable (orphans) | 5 | **0** |
| B — modal gaps | 1 | **0** |
| C — FR coverage | 0 | 0 |
| D — declared-but-absent | 0 | 0 |
| E1 — unbound endpoints | 0 (+1 adjacent) | **0** |
| E2 — undocumented calls | 0 | 0 |
| E3 — data-need | 4 (sanctioned client_only) | 4 (sanctioned — no action) |
| F — untyped click intents | 0 | 0 |

**Remaining gaps: 0.** E3 (pfm-dashboard, spending-by-category, budgets, recurring-subscriptions) are FR-011 `gap_strategy: client_only` — derived from cached AIS data, no endpoint required; not real gaps.

## Fixes applied

1. **`product` + `party` unreachable** → added Product chip (`chip_product` → product) + Account-Holder chip (`chip_party` → party) to `account-detail/ui.yaml` `action_chips` (realizes edges asserted in `APP_FLOW.mmd:62-63`). New strings: `nav_chip_product(_accessibility)`, `nav_chip_party(_accessibility)`.
2. **`pfm-dashboard` unreachable (cluster root)** → repointed `home/ui.yaml` `spending_snapshot_card` from `spending-by-category` → `pfm-dashboard` (hub). Transitively rescues `budgets` + `recurring-subscriptions` (both linked from the hub). spending-by-category stays reachable via the hub.
3. **`recurring-subscriptions` broken row** → `subscription_row` fired `show_merchant_transaction_history` with no target; now `navigate_transactions` → `transactions` (params.merchant preserved), per `APP_FLOW.mmd:133`.
4. **`settings` modal gap** → defined `clear_local_data_sheet` (`type: bottom_sheet`, state `clear_confirm`) with cancel/confirm buttons (`dismiss_clear_local_data` / `execute_clear_local_data`); strings already existed. Content components now bind `[content, clear_confirm]` so the list renders behind the overlay.
5. **Manifest** → added `statements` to `statement-file` `consumers[]` in both `server/api_manifest.yaml` and `server/apis/account-information.yaml` (statements screen also calls `GET .../statements/{StatementId}/file`).

## Flow sync

- `flows/account-browsing.yaml` — added forward edges account-detail → product, party, atm-locator.
- `flows/home-dashboard.yaml` — retargeted home spending-card edge → pfm-dashboard (+ description).
- `flows/pfm-review.yaml` — added recurring-subscriptions → transactions drill-through.

## Files touched
screens/account-detail/ui.yaml, screens/home/ui.yaml, screens/recurring-subscriptions/ui.yaml, screens/settings/ui.yaml, _strings/strings.yaml, server/api_manifest.yaml, server/apis/account-information.yaml, flows/{account-browsing,home-dashboard,pfm-review}.yaml.

**Not touched (out of scope):** any server-layer scaffolding, stitch prompts, mockups, preview HTML.
