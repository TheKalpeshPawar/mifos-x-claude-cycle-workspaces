# Accounts — Feature Specification

> Generated from `screens/accounts/ui.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Source hash: `96e7b1f02bf2`
> Endpoints: 2 · DTOs: 2 · Components: 5 · Test scenarios: 10

## Lossless Export Contract

Lossless per RULE-EXPORT-ROUNDTRIP-001 — State Defaults, Error Matrix, Test Mapping and
Nav Origins below let the generators consume this file alone.

## 1. Overview

Authorised accounts list with a balance preview per account. Accounts tab, **bottom-nav order
1** (Home is 0). Entry point to account-detail.

| Attribute | Value |
|---|---|
| Feature ID | `accounts` |
| Cluster | account |
| Priority | must (FR-003, FR-004) |
| Status | approved · quality 95 |
| Archetype | index_list |
| Source module | `feature/accounts` — **implemented** |
| Graph | `accountsGraph(onNavigateToAccountDetail)` |

## 2. Screen inventory

| Component | Type | Bound states |
|---|---|---|
| `loading_skeleton` | stack | loading |
| `account_type_filter` | chip_group | content |
| `accounts_list` | list | content |
| `empty_accounts` · `error_accounts` | empty_state, error_state | empty, error |

### Four filter chips — and deliberately no Global

**All · Current · Savings · Credit.** A Global Money wallet reports `CACC`, indistinguishable
here from a current account, so it already sits under Current. A chip matching the
`GlobalMoney`/`GlobalWallet` subtypes could never match and would render a permanently empty
list. The only runtime signal is the free-text `Description` (`"GLOBAL MONEY ACCOUNT"`), which
`HsbcProductType.resolve` matches and account-detail displays.

`canonicalSubtype()` normalises for every screen, accepting the OBIE enum names **and** the ISO
codes (`cacc`/`svgs`/`ccrd`) — because v4.0 dropped `AccountSubType` entirely, not out of
defensiveness.

## 3. State model — `AccountsViewModel`

**State fields:** `uiState: ScreenState<AccountsData>`
**State defaults:** `uiState = ScreenState.Loading`

`ScreenState` members: `Loading` · `Content` · `Empty` · `Error` · `NoNetwork` · `Unauthenticated`

**Actions:** `FilterAccounts` · `RetryLoad`
**Events:** none (`E = Nothing`)
**DI:** `AccountsOverviewRepository`

### The one repository that is not stateless — do not copy

`AccountsOverviewRepository` is the sole exception to the stream-ownership rule. It does not
return `ScreenDataStream`: it exposes `overviewState(scope): Flow<ScreenState<List<AccountWithBalance>>>`
plus an interface-level `refresh()`, and the impl holds **two mutable fields** —
`private var accountsStream` (memoised) and `private var refreshBalances` (a one-shot flag
consumed by the next balance fan-out, because the balances store is memory-only and a cached
read would keep returning the first figure).

So this feature calls `repository.refresh()`, **not** `stream.refresh()`. Its own KDoc still
justifies the unsynchronised `var` as "matching the plain `var stream` pattern in the sibling
repositories" — no sibling does that any more; disregard it.

## 4. Navigation

| Origin | Trigger | Target |
|---|---|---|
| `app_shell_bottom_nav` | Accounts tab (order 1) | `accounts` |
| `consent-callback` | successful OAuth callback | `accounts` |
| `back_stack_pop` | back from account-detail | `accounts` |
| account card | tap | `account-detail` (accountId) |
| — | 401 token expired | `login` |
| "Reconfirm access" | consent expiry banner | `consent-detail` |
| — | 403 consent revoked mid-session | `consent-list` |

## 5. API dependencies

| ID | Method | Path | Permission | Response DTO |
|---|---|---|---|---|
| `accounts-list` | GET | `/accounts` | ReadAccountsDetail | `OBReadAccount6` |
| `balances` | GET | `/accounts/{AccountId}/balances` | ReadBalances | `OBReadBalance1` |

Balances fan out per account via `getOnce`. Full contracts in `API.md`.

### Error matrix

| HTTP | UI | Recovery |
|---|---|---|
| 401 | Error + Retry | routes to `login` |
| 403 | Error | routes to `consent-list` |
| 429 | Error, recoverable | back-off |
| — | Empty | no accounts returned |
| partial balance failure | **card still shown, without the balance** | not an error state |

That last row matters — one account's balance failing must not blank the whole list.

## 6. Design tokens

`design-tokens.yaml` 2.1.0 — `list_item` (48dp min), `amount` (mono; credit `primary`, debit
`error`), `chip` for the filter row, `accountDisplayName` from `core/ui` for the label.
Canonical brand spec: `design-system/DESIGN.md` 1.1.0.

### Shared account-name label

`core/ui/.../account/AccountDisplayName.kt` is the one place Home, Accounts and Account-detail
resolve a display name: the bank-provided `Nickname`/`Name` if present, else a localised
account-type + last-4 label ("Current account ·· 3349") — except a **credit card**, whose
account-number field is a mid-PAN slice, so it shows the real masked last-4 via
`maskCardNumber` ("Credit card •••• 7654").

## 7. Test mapping

| TC | Assertion | Expected path |
|---|---|---|
| TC-ACCTS-001 | list renders with balance preview | `feature/accounts/src/commonTest/.../AccountsViewModelTest.kt` |
| TC-ACCTS-002 | shimmer skeleton cards | ↑ |
| TC-ACCTS-003 | 401 → error with Retry | ↑ |
| TC-ACCTS-004 | empty when no accounts | ↑ |
| TC-ACCTS-005 | card tap → account-detail | ↑ |
| TC-ACCTS-006 | GlobalMoney / GlobalWallet cards render | ↑ |
| TC-ACCTS-007 | consent expiry banner under 30 days | ↑ |
| TC-ACCTS-008 | credit card shows "Balance owed" badge | `AccountsScreenRobolectricTest.kt` |
| TC-ACCTS-009 | filter chip narrows visible cards | ↑ |
| TC-ACCTS-010 | **partial balance failure — card shown without balance** | ↑ |

## 8. Stale-artifact fix applied 2026-07-30

`docs.yaml#description` claimed "Primary bottom-nav anchor (tab order 0)" — Home is order 0,
Accounts is 1 — and implied a dedicated multi-currency surface. Corrected to describe list
rendering under the Current filter, with the reason no Global chip exists.

`docs.yaml` declares no `flow_ref` despite `flows/account-browsing.yaml` existing.
