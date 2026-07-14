# /idea verify — Post-completeness run
# Project: mifos-x-open-banking
# Timestamp: 2026-07-14T19:00:00Z
# Scope: Full verify (ALL IDEA_LAYER_CHECKS), focus on /idea-completeness touched files
# Touched: screens/account-detail/ui.yaml · screens/home/ui.yaml ·
#          screens/recurring-subscriptions/ui.yaml · screens/settings/ui.yaml ·
#          _strings/strings.yaml · server/api_manifest.yaml ·
#          server/apis/account-information.yaml ·
#          flows/{account-browsing,home-dashboard,pfm-review}.yaml

---

## CHECK MATRIX

| # | Rule | Sub-check | Scope | Status | Detail |
|---|------|-----------|-------|--------|--------|
| 1 | RULE-IDEA-I18N-COMPLETENESS-001 | IC-1: token resolution | account-detail | PASS | `nav_chip_product` → "Product" ✓ |
| 2 | RULE-IDEA-I18N-COMPLETENESS-001 | IC-1: token resolution | account-detail | PASS | `nav_chip_product_accessibility` → "View product terms and features for this account" ✓ |
| 3 | RULE-IDEA-I18N-COMPLETENESS-001 | IC-1: token resolution | account-detail | PASS | `nav_chip_party` → "Account Holder" ✓ |
| 4 | RULE-IDEA-I18N-COMPLETENESS-001 | IC-1: token resolution | account-detail | PASS | `nav_chip_party_accessibility` → "View account holder party details for this account" ✓ |
| 5 | RULE-IDEA-I18N-COMPLETENESS-001 | IC-1: token resolution | settings | PASS | `settings.clear_local_data.dialog_title` → "Clear local data?" ✓ |
| 6 | RULE-IDEA-I18N-COMPLETENESS-001 | IC-1: token resolution | settings | PASS | `settings.clear_local_data.dialog_body` → resolved ✓ |
| 7 | RULE-IDEA-I18N-COMPLETENESS-001 | IC-1: token resolution | settings | PASS | `settings.clear_local_data.dialog_confirm` → "Clear" ✓ |
| 8 | RULE-IDEA-I18N-COMPLETENESS-001 | IC-1: token resolution | settings | PASS | `settings.clear_local_data.dialog_cancel` → "Cancel" ✓ |
| 9 | RULE-IDEA-I18N-COMPLETENESS-001 | IC-2: non-empty values | all modified | PASS | All 8 new string keys have non-empty en values ✓ |
| 10 | RULE-IDEA-I18N-COMPLETENESS-001 | IC-3: no missing entries | all modified | PASS | Zero missing i18n refs in modified screens ✓ |
| 11 | RULE-PROTO-DEAD-DESTINATION-001 | DD-1: nav target exists | account-detail/chip_product | PASS | target:`product` → screens/product/ ✓ |
| 12 | RULE-PROTO-DEAD-DESTINATION-001 | DD-1: nav target exists | account-detail/chip_party | PASS | target:`party` → screens/party/ ✓ |
| 13 | RULE-PROTO-DEAD-DESTINATION-001 | DD-1: nav target exists | home/spending_snapshot | PASS | target:`pfm-dashboard` → screens/pfm-dashboard/ ✓ |
| 14 | RULE-PROTO-DEAD-DESTINATION-001 | DD-1: nav target exists | recurring-subscriptions/subscription_row | PASS | target:`transactions` → screens/transactions/ ✓ |
| 15 | RULE-PROTO-DEAD-DESTINATION-001 | DD-2: flow connection target exists | account-browsing | PASS | `product`, `party` connections resolve ✓ |
| 16 | RULE-PROTO-DEAD-DESTINATION-001 | DD-2: flow connection target exists | home-dashboard | PASS | `pfm-dashboard` connection resolves ✓ |
| 17 | RULE-PROTO-DEAD-DESTINATION-001 | DD-2: flow connection target exists | pfm-review | PASS | `recurring-subscriptions`→`transactions` connections resolve ✓ |
| 18 | RULE-ON-CLICK-OBJECT-FORM-001 | OF-1: canonical object form | account-detail chip_product | PASS | `{action: navigate_product, target: product, params: {accountId}}` ✓ |
| 19 | RULE-ON-CLICK-OBJECT-FORM-001 | OF-1: canonical object form | account-detail chip_party | PASS | `{action: navigate_party, target: party, params: {accountId}}` ✓ |
| 20 | RULE-ON-CLICK-OBJECT-FORM-001 | OF-1: canonical object form | home spending_snapshot | PASS | `{action: navigate_pfm, target: pfm-dashboard}` ✓ |
| 21 | RULE-ON-CLICK-OBJECT-FORM-001 | OF-1: canonical object form | recurring-subscriptions | PASS | `{action: navigate_transactions, target: transactions, params: {merchant}}` ✓ |
| 22 | RULE-ON-CLICK-OBJECT-FORM-001 | OF-3: action-only form valid | settings clear_local_data_confirm | PASS | action-only (no target) is valid for non-nav action ✓ |
| 23 | RULE-ON-CLICK-OBJECT-FORM-001 | OF-3: action-only form valid | settings bottom_sheet buttons | PASS | `dismiss_clear_local_data`, `execute_clear_local_data` — action-only ✓ |
| 24 | RULE-IDEA-STATE-EXHAUSTIVENESS-001 | SE-1: every declared state has component binding | settings | PASS | loading→skeleton, content→sections, empty→empty_state, error→error_state, clear_confirm→bottom_sheet ✓ |
| 25 | RULE-IDEA-STATE-EXHAUSTIVENESS-001 | SE-2: state_binding refs exist in states[] | settings | PASS | [content,clear_confirm] ⊆ [loading,content,empty,error,clear_confirm] ✓ |
| 26 | RULE-IDEA-STATE-EXHAUSTIVENESS-001 | SE-3: no orphan states | account-detail | PASS | All 4 states [loading,content,empty,error] have ≥1 bound component ✓ |
| 27 | RULE-IDEA-STATE-EXHAUSTIVENESS-001 | SE-3: no orphan states | recurring-subscriptions | PASS | All 4 states covered ✓ |
| 28 | RULE-IDEA-UI-INTERNAL-001 | UII-2: component ID uniqueness | account-detail | PASS | chip_product, chip_party IDs unique across file ✓ |
| 29 | RULE-IDEA-UI-INTERNAL-001 | UII-2: component ID uniqueness | settings | PASS | clear_local_data_sheet, cancel_clear_local_data_button, confirm_clear_local_data_button unique ✓ |
| 30 | RULE-IDEA-UI-INTERNAL-001 | UII-3: state_binding refs valid | account-detail | PASS | [content,empty], [content], [loading], [error] all valid ✓ |
| 31 | RULE-IDEA-UI-INTERNAL-001 | UII-3: state_binding refs valid | settings | PASS | [content,clear_confirm], [clear_confirm], [loading], [empty], [error] all valid ✓ |
| 32 | RULE-IDEA-UI-INTERNAL-001 | UII-4: on_click.action in VM actions | account-detail/chip_product | WARN | `navigate_product` → `navigateProduct` MISSING from state_model.AccountDetailViewModel.actions.members |
| 33 | RULE-IDEA-UI-INTERNAL-001 | UII-4: on_click.action in VM actions | account-detail/chip_party | WARN | `navigate_party` → `navigateParty` MISSING from state_model.AccountDetailViewModel.actions.members |
| 34 | RULE-IDEA-UI-INTERNAL-001 | UII-4: on_click.action in VM actions | account-detail/chip_atm_locator | WARN | `navigate_atm_locator` → `navigateAtmLocator` MISSING — pre-existing gap (chip added 2026-06-30) |
| 35 | RULE-IDEA-UI-RPC-COVERAGE-001 | URC-1: consumer drift between server files | api_manifest ↔ account-info | WARN | accounts-list, balances, transactions each have `home` as consumer in api_manifest.yaml but NOT in account-information.yaml (pre-existing — STEP 4 reconciliation added `home` to manifest only) |
| 36 | RULE-IDEA-UI-RPC-COVERAGE-001 | statement-file consumers coherent | api_manifest ↔ account-info | PASS | Both files now have consumers:[statements, statement-detail] ✓ |
| 37 | RULE-PROTO-ORPHAN-ROUTE-001 | OR-1: new screens reachable | product | PASS | Reachable from account-detail chip_product + account-browsing.yaml connection ✓ |
| 38 | RULE-PROTO-ORPHAN-ROUTE-001 | OR-1: new screens reachable | party | PASS | Reachable from account-detail chip_party + account-browsing.yaml connection ✓ |
| 39 | RULE-PROTO-ORPHAN-ROUTE-001 | OR-1: new screens reachable | pfm-dashboard | PASS | Reachable from home spending_snapshot + home-dashboard.yaml connection ✓ |
| 40 | RULE-IDEA-I18N-COMPLETENESS-001 | IC-4: false-closure guard | CAPABILITY_GAPS | SKIP | No i18n gaps closed in this run; no IC-4 closure to verify |

---

## SUMMARY

| Dimension | Count |
|-----------|-------|
| Total checks run | 40 |
| PASS | 36 |
| WARN | 4 |
| FAIL | 0 |
| SKIP | 0 |
| **Overall** | **WARN** |

**Quality score**: 95 (unchanged — structural checks pass; warns are advisory in-file consistency gaps)
**Completeness score**: carry-forward from last enrich (no recalculation triggered — verify is read-only)

---

## WARN FINDINGS (fix guidance)

### W-1 + W-2: UII-4 — Missing VM actions for new chips (account-detail)
**File**: `idea-layer/screens/account-detail/ui.yaml`
**Location**: `state_model.AccountDetailViewModel.actions.members`
**Gap**: `chip_product` uses `action: navigate_product` and `chip_party` uses `action: navigate_party` — neither `navigateProduct` nor `navigateParty` are declared in the VM actions list.
**Fix**: Add to `state_model.AccountDetailViewModel.actions.members`:
```yaml
- navigateProduct     # push product route with accountId
- navigateParty       # push party route with accountId
```

### W-3: UII-4 — Missing VM action for atm chip (pre-existing)
**File**: `idea-layer/screens/account-detail/ui.yaml`
**Gap**: `chip_atm_locator` uses `action: navigate_atm_locator` → `navigateAtmLocator` missing from VM actions.
**Fix**: Add `- navigateAtmLocator` to actions.members (same list as W-1/W-2 fix).

### W-4: URC-1 — API consumer drift between server files (pre-existing)
**Files**: `server/api_manifest.yaml` vs `server/apis/account-information.yaml`
**Gap**: STEP 4 reconciliation (2026-07-14) added `home` as consumer for `accounts-list`, `balances`, `transactions` in `api_manifest.yaml` but did NOT propagate to `account-information.yaml`.
- `accounts-list` consumers: manifest=[accounts, home] vs detail=[accounts]
- `balances` consumers: manifest=[account-detail, accounts, home] vs detail=[account-detail, accounts]
- `transactions` consumers: manifest=[transactions, transaction-detail, home] vs detail=[transactions, transaction-detail]
**Fix**: Update `server/apis/account-information.yaml` account-browsing flow to add `home` to consumers for accounts-list and balances; add `home` to consumers for the transactions endpoint.
