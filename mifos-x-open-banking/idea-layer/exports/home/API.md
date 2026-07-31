# Home — API Contracts

> Generated from `screens/home/api.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Source hash: `c48417190c81` · Endpoints: 3 · DTOs: 3

Base path `/obie/open-banking/v4.0/aisp`. All three are AIS reads on the PSU bearer — no JWS,
no idempotency key.

## Endpoint summary

| # | ID | Method | Path | Permission | Response DTO | Cache |
|---|---|---|---|---|---|---|
| 1 | `accounts-list` | GET | `/accounts` | ReadAccountsDetail | `OBReadAccount6` | memory 300s |
| 2 | `selected-account-balances` | GET | `/accounts/{AccountId}/balances` | ReadBalances | `OBReadBalance1` | via stream |
| 3 | `recent-transactions` | GET | `/accounts/{AccountId}/transactions` | ReadTransactionsDetail | `OBReadTransaction6` | via stream |

**Home adds no endpoint of its own** — it aggregates three AIS reads client-side.

## Parallel fan-out

Balances and transactions are independent, so they run concurrently:

```kotlin
coroutineScope {
    val balanceDef = async { apiService.getBalances(selectedAccountId) }
    val txDef      = async { apiService.getTransactions(selectedAccountId, limit = 5) }
    balanceDef.await() to txDef.await()
}
```

## Flow-keyed streams

`BalancesRepository.balanceStream` and `TransactionsRepository.transactionsStream` are the
**only two methods in the app** that take `Flow<String>` via the `keyFlow` + `cacheKeyFor`
overload, rather than a fixed `String` key. Home's selected account is the one key that changes
without navigating.

The reason is lifetime, not key semantics. On `CACHE_THEN_NETWORK` the fixed-key overload
launches two uncancelled coroutines per call on the passed scope; the `keyFlow` overload
launches one. Rebuilding a stream per key on the caller side would leak a network observer per
tap onto home's long-lived scope.

## 1 · Accounts list

`GET /accounts` → `200` `OBReadAccount6` — populates the account selector sheet.

`Data.Account[]` carries `AccountId`, `Currency`, `AccountCategory`, `AccountTypeCode`,
`Description`, `Servicer`, and an `Account[]` array of scheme identifiers
(`UK.OBIE.SortCodeAccountNumber`, `UK.OBIE.IBAN`).

> **HSBC UK Personal AIS v4.0 has no `AccountSubType` field.** v4.0 replaced the OBIE v3
> `AccountType`/`AccountSubType` pair with `AccountCategory` + `AccountTypeCode`, whose enum is
> `CHAR, CARD, CACC, LOAN, MORT, SVGS`. `AccountMapper` resolves
> `accountSubType = accountSubType ?: accountTypeCode ?: accountCategory ?: description ?: ""`.

## 2 · Balances

`GET /accounts/{AccountId}/balances` → `200` `OBReadBalance1`

`Data.Balance[]` — `CreditDebitIndicator`, `Type` (e.g. `ITBD`), `DateTime`,
`Amount { Amount, Currency }`. Home renders the `InterimAvailable` balance in the hero card.

## 3 · Recent transactions

`GET /accounts/{AccountId}/transactions` → `200` `OBReadTransaction6`, limited to 5.

> **Trap:** a per-transaction `Balance.CreditDebitIndicator` describes the **transaction's**
> direction, not the balance's. The sandbox returns `Balance {Debit, ITBD, 21530.92}` for an
> account whose `/balances` reports `{Credit, ITBD, 21530.92}`. Signing a running balance on it
> renders £21,530.92 as −£21,530.92 — running balances are shown **unsigned**.

## Error matrix

| HTTP | ErrorCode | Meaning | UI action |
|---|---|---|---|
| 401 | `UK.OBIE.Header.Invalid` | token expired | Error + Retry; recovery routes to login |
| 403 | `UK.OBIE.Resource.ConsentMismatch` | permission absent from the consent | Error, **non-recoverable**, directs to consent-list |
| 429 | `UK.OBIE.Rules.TooManyRequests` | rate limited | Error, recoverable, exponential back-off |
| 503 | `UK.OBIE.Unexpected.ServerError` | sandbox unavailable | Error, recoverable |
| — | — | empty `Data.Account[]` | Empty (`no_accounts`), not an error |

`Unauthenticated` falls through `ScreenContent`'s `error` slot with a **synthetic**
`IllegalStateException("Unauthenticated")` — never branch on that Throwable's type.

## Cache

| Resource | TTL | Source | Invalidated by |
|---|---|---|---|
| `allAccounts` | 300s | memory | account-switcher tap, app resume |
| `selectedAccountId` | ∞ | DataStore (`UserDataRepository`) | — |

`accountsStore` is one of only two Room-persisted stores (with `transactionsStore`). Its
fetcher must call `validator.markFresh()` or the TTL never starts, and its SoT reader emits
`null` for an empty table so cold start is Loading, not a premature Empty.

## Source binding

`core/network/api/Aisp.kt` `getAccounts` / `getBalances` / `getTransactions` ·
`core/data/.../banking/store/BankingStores.kt` `accountsStore` / `balancesStore` /
`transactionsStore` — all shipped and consumed.
