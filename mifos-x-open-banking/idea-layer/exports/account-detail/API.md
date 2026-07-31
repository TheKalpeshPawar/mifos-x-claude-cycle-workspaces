# Account detail — API Contracts

> Generated from `screens/account-detail/api.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Source hash: `63022c4bdb68` · Endpoints: 2 · DTOs: 2

Base path `/obie/open-banking/v4.0/aisp`. Both AIS reads on the PSU bearer.

## Endpoint summary

| # | ID | Method | Path | Permission | Response DTO | Cache key |
|---|---|---|---|---|---|---|
| 1 | `account-detail` | GET | `/accounts/{AccountId}` | ReadAccountsDetail | `OBReadAccount6` | `DETAIL_CACHE_KEY:{id}` |
| 2 | `balances` | GET | `/accounts/{AccountId}/balances` | ReadBalances | `OBReadBalance1` | `BALANCES_CACHE_KEY:{id}` |

**Two streams, two cache keys.** One repository consumes two stores here, so the constants are
named `DETAIL_CACHE_KEY` / `BALANCES_CACHE_KEY` rather than colliding on `CACHE_KEY`. The
ViewModel merges them with `combineScreenStates`.

## 1 · Account detail

`GET /accounts/{AccountId}` → `200` `OBReadAccount6` — same envelope as the list, filtered to
one account.

Rendered: `Nickname`/`Name`, `Identification`, `Currency`, resolved subtype, `Servicer`, and
`Description` (verbatim, card omitted when blank).

## 2 · Balances

`GET /accounts/{AccountId}/balances` → `200` `OBReadBalance1`

Unlike the accounts list, which shows one preview balance, this screen renders **all** balance
types from `Data.Balance[]`: `Type` (`ITBD`, `ITAV`, `OPBD`, `CLBD`, …),
`Amount { Amount, Currency }`, `CreditDebitIndicator`, `DateTime`.

Balances are shown **unsigned** in `neutral` — see the `balanceIsCredit` trap in
`exports/home/API.md`.

## Merged-state contract

`combineScreenStates(detail, balances) { … }` — priority
**NoNetwork > Loading > Unauthenticated > Error > Empty > Content**; freshness is worst-of
(STALE > UPDATING > FRESH); `fetchedAt` is **null if any Content source has a null
`fetchedAt`**, else the oldest. `transform` runs only when both are `Content`.

The merged `NoNetwork` is always a bare `NoNetwork()` — **`isCaptivePortal` is dropped**. Read
it from the individual stream if the screen needs it.

## Capability gating — the `U000` correction layer

Not every HSBC product serves every endpoint. A savings account (`SVGS`) answers
`400 U000` "This action is not allowed on the account type" for standing orders and direct
debits.

The **store fetcher** records the refusal before rethrowing — one call site per gated endpoint
(`BankingStores.kt:210` DirectDebits, `:320` StandingOrders, `:353` ScheduledPayments):

```kotlin
is NetworkResult.Error -> {
    result.error.recordIfUnsupported(
        accountId = accountId,
        endpoint  = AccountEndpoint.DirectDebits,
        registry  = capabilityRegistry,
    )
    throw result.error.toThrowable()
}
```

`recordIfUnsupported` guards on `NetworkError.isUnsupportedForProduct()` — `BadRequest` **and**
`U000` in the body, falling back to a substring match when the body won't parse.

**Never record from a ViewModel.** The fetcher is the one point every call passes, including a
deep link that bypasses the chip entirely.

`partyStore` is the one memory store with **no** capability registry (there is no
`AccountEndpoint.Party`), so a `U000` on the party endpoint surfaces as an ordinary error
rather than hiding a chip.

> `AccountCapabilityRegistry.clear()` has **no production caller**, so runtime `U000` refusals
> survive logout for the process lifetime even though its KDoc says they must not.

## Error matrix

| HTTP | ErrorCode | Meaning | UI action |
|---|---|---|---|
| 401 | `UK.OBIE.Header.Invalid` | token expired | Error (`recoverable`) + Retry |
| 403 | `UK.OBIE.Resource.ConsentMismatch` | permission absent or consent revoked | Error, non-recoverable → consent-list |
| 404 | `U011` | unknown AccountId | Error, non-recoverable |
| 400 | `U000` | product does not serve this endpoint | **not surfaced here** — recorded by the fetcher, hides the chip |
| 429 | `UK.OBIE.Rules.TooManyRequests` | rate limited | Retry with back-off |
| — | — | empty `Data.Balance[]` | Empty — reuses `AccountDetailContent` with `balances = emptyList()` |

## Source binding

`core/network/api/Aisp.kt` `getAccountDetails` / `getBalances` ·
`core/data/.../banking/store/BankingStores.kt` `accountDetailStore` + `balanceLinesStore`
(both memory) · `AccountDetailRepositoryImpl` (two stores, one repository) ·
`core/data/.../banking/AccountCapabilityRegistry.kt` · `core/data/.../util/ObieErrorCodes.kt` —
all shipped and consumed.
