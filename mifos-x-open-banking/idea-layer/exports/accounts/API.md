# Accounts — API Contracts

> Generated from `screens/accounts/api.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Source hash: `e9536984d3c5` · Endpoints: 2 · DTOs: 2

Base path `/obie/open-banking/v4.0/aisp`. Both are AIS reads on the PSU bearer.

## Endpoint summary

| # | ID | Method | Path | Permission | Response DTO |
|---|---|---|---|---|---|
| 1 | `accounts-list` | GET | `/accounts` | ReadAccountsDetail | `OBReadAccount6` |
| 2 | `balances` | GET | `/accounts/{AccountId}/balances` | ReadBalances | `OBReadBalance1` |

## 1 · Accounts list

`GET /accounts` → `200` `OBReadAccount6`

```json
{
  "Data": { "Account": [
    { "AccountId": "1123456841", "Currency": "GBP", "AccountCategory": "Personal",
      "AccountTypeCode": "SVGS", "Description": "BMM ACCOUNT",
      "Servicer": { "SchemeName": "UK.OBIE.BICFI", "Identification": "HSBC0236" },
      "Account": [
        { "SchemeName": "UK.OBIE.SortCodeAccountNumber", "Identification": "80122590953695", "Name": "ACCNT SHORT" },
        { "SchemeName": "UK.OBIE.IBAN", "Identification": "GB12HSBC80122590953695", "Name": "ACCNT SHORT" }
      ] }
  ] },
  "Links": { "Self": "…/accounts" },
  "Meta": { "TotalPages": 1 }
}
```

### No `AccountSubType` in v4.0

HSBC UK Personal AIS v4.0 replaced the OBIE v3 `AccountType`/`AccountSubType` pair with
`AccountCategory` + `AccountTypeCode`, whose enum is `CHAR, CARD, CACC, LOAN, MORT, SVGS` —
**no wallet code** (only the business and HSBCnet specs carry `WALT`).

`AccountMapper` therefore resolves:

```
accountSubType = accountSubType ?: accountTypeCode ?: accountCategory ?: description ?: ""
```

and every screen normalises through `canonicalSubtype()`, which accepts the OBIE enum names
*and* the ISO codes (`cacc`/`svgs`/`ccrd`).

**Consequence for filtering:** a Global Money wallet reports `CACC` — indistinguishable from an
ordinary current account. That is why the filter row is All · Current · Savings · Credit with
no Global chip: such a chip could never match. The only runtime signal is the free-text
`Description` (`"GLOBAL MONEY ACCOUNT"`).

Note the sandbox is uneven: two test accounts return the literal filler
`"Description of the account"`, one `BMM ACCOUNT`, one `GLOBAL MONEY ACCOUNT`.

## 2 · Balances

`GET /accounts/{AccountId}/balances` → `200` `OBReadBalance1`

`Data.Balance[]` — `AccountId`, `CreditDebitIndicator`, `Type`, `DateTime`,
`Amount { Amount, Currency }`. Priority for the list preview: `InterimAvailable` →
`InterimBooked` → `OpeningBooked`.

### Fan-out and partial failure

Balances are fetched per account via `getOnce`, each wrapped so one failure does not blank the
list:

```kotlin
accounts.map { a ->
    async { AccountWithBalance(a, runCatching { balancesStore.getOnce(a.accountId, refresh) }.getOrNull()) }
}.awaitAll()
```

A `null` balance renders the card **without** a balance line — not an error state (TC-ACCTS-010).

## Error matrix

| HTTP | ErrorCode | Meaning | UI action |
|---|---|---|---|
| 401 | `UK.OBIE.Header.Invalid` | token expired | Error + Retry; recovery routes to `login` |
| 403 | `UK.OBIE.Resource.ConsentMismatch` | ReadAccountsDetail/ReadBalances absent, or consent revoked mid-session | Error; routes to `consent-list` |
| 429 | `UK.OBIE.Rules.TooManyRequests` | rate limited | Retry with back-off |
| 500 | `UK.OBIE.Unexpected.ServerError` | HSBC-side failure | Error + Retry |
| — | — | empty `Data.Account[]` | Empty state, not an error |

## Repository shape — the documented exception

`AccountsOverviewRepository` does **not** return `ScreenDataStream`. It exposes
`overviewState(scope): Flow<ScreenState<List<AccountWithBalance>>>` plus `refresh()`, and its
impl holds `private var accountsStream` (memoised) and `private var refreshBalances` (a
one-shot flag — the balances store is memory-only, so a cached read would keep returning the
first figure).

This is the one repository in the app that holds state. Every other one is a stateless gateway
whose stream is owned by the ViewModel. Do not copy this shape.

## Source binding

`core/network/api/Aisp.kt` `getAccounts` / `getBalances` ·
`core/data/.../banking/store/BankingStores.kt` `accountsStore` (Room-persisted) /
`balancesStore` (memory) · `AccountsOverviewRepository` — all shipped and consumed.
