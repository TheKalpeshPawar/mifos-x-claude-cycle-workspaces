# Targeted Verify Re-check — UII-4 + URC-1
**Run:** 2026-07-14T19:30:00Z
**Scope:** RULE-IDEA-UI-INTERNAL-001 (sub-check UII-4) + RULE-IDEA-UI-RPC-COVERAGE-001 (sub-check URC-1)
**Purpose:** Confirm the 4 WARNs from T19:00 run are resolved by the prior fixes.

---

## UII-4 — AccountDetailViewModel.actions.members vs on_click actions

**File:** `idea-layer/screens/account-detail/ui.yaml`

### on_click → VM action mapping (all components)

| Component ID | on_click.action | VM action (camelCase) | Status |
|---|---|---|---|
| back_button | navigate_back | navigateBack | PASS |
| chip_transactions | navigate_transactions | navigateTransactions | PASS |
| chip_statements | navigate_statements | navigateStatements | PASS |
| chip_standing_orders | navigate_standing_orders | navigateStandingOrders | PASS |
| chip_direct_debits | navigate_direct_debits | navigateDirectDebits | PASS |
| chip_scheduled_payments | navigate_scheduled_payments | navigateScheduledPayments | PASS |
| chip_beneficiaries | navigate_beneficiaries | navigateBeneficiaries | PASS |
| chip_atm_locator | navigate_atm_locator | **navigateAtmLocator** | **PASS (was WARN)** |
| chip_product | navigate_product | **navigateProduct** | **PASS (was WARN)** |
| chip_party | navigate_party | **navigateParty** | **PASS (was WARN)** |
| retry_button | retry_load | retryLoad | PASS |

**VM actions declared** (state_model.AccountDetailViewModel.actions.members):
loadAccountDetail, retryLoad, navigateBack, navigateTransactions, navigateStatements,
navigateStandingOrders, navigateDirectDebits, navigateScheduledPayments, navigateBeneficiaries,
navigateAtmLocator, navigateProduct, navigateParty

**UII-4 result: PASS** — all 11 on_click actions resolve to declared VM actions. 3 previously-missing
entries (navigateAtmLocator, navigateProduct, navigateParty) are now present at lines 66-68 of ui.yaml.

---

## URC-1 — Consumer consistency: account-information.yaml vs api_manifest.yaml

**Files compared:**
- `idea-layer/server/apis/account-information.yaml`
- `idea-layer/server/api_manifest.yaml`

### Full consumer cross-check

| Endpoint ID | account-information.yaml consumers | api_manifest.yaml consumers | Match |
|---|---|---|---|
| consent-create | [login, consent-callback] | [login, consent-callback] | PASS |
| consent-status | [consent-callback, consent-detail] | [consent-callback, consent-detail] | PASS |
| consent-revoke | [consent-detail] | [consent-detail] | PASS |
| accounts-list | [accounts, home] | [accounts, home] | **PASS (was WARN)** |
| account-detail | [account-detail] | [account-detail] | PASS |
| balances | [account-detail, accounts, home] | [account-detail, accounts, home] | **PASS (was WARN)** |
| product | [product] | [product] | PASS |
| party | [party, profile] | [party, profile] | PASS |
| parties | [party] | [party] | PASS |
| transactions | [transactions, transaction-detail, home] | [transactions, transaction-detail, home] | **PASS (was WARN)** |
| beneficiaries | [beneficiaries] | [beneficiaries] | PASS |
| standing-orders | [standing-orders] | [standing-orders] | PASS |
| direct-debits | [direct-debits] | [direct-debits] | PASS |
| scheduled-payments | [scheduled-payments] | [scheduled-payments] | PASS |
| statements | [statements] | [statements] | PASS |
| statement-detail | [statement-detail] | [statement-detail] | PASS |
| statement-txns | [statement-detail] | [statement-detail] | PASS |
| statement-file | [statements, statement-detail] | [statements, statement-detail] | PASS |

Note: `atms` endpoint is in api_manifest.yaml (API-002 open-data group) but NOT in
account-information.yaml — this is correct; it belongs to server/apis/open-data.yaml (API-002),
not the AIS account-information API group. No drift.

**URC-1 result: PASS** — zero consumer drift across all 18 AIS endpoints.

---

## Summary

| Warning (T19:00 run) | Prior status | Current status |
|---|---|---|
| UII-4: navigateProduct missing from account-detail VM actions | WARN | PASS |
| UII-4: navigateParty missing from account-detail VM actions | WARN | PASS |
| UII-4: navigateAtmLocator missing from account-detail VM actions | WARN | PASS |
| URC-1: home consumer drift api_manifest vs account-information.yaml | WARN | PASS |

**Overall: PASS — all 4 prior warnings resolved.**
