# Statements — API Contracts

> Generated from `screens/statements/api.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Endpoints: 2 · DTOs: 1

Base path `/obie/open-banking/v4.0/aisp`.

## Endpoint summary

| # | ID | Method | Path | Permission | Response | Cache |
|---|---|---|---|---|---|---|
| 1 | `statements` | GET | `/accounts/{AccountId}/statements` | ReadStatementsDetail | `OBReadStatement2` | memory LRU |
| 2 | `statement_file` | GET | `/accounts/{AccountId}/statements/{StatementId}/file` | ReadStatementsDetail | `ByteArray` (application/pdf) | **none** |

Two very different shapes: a cached list read, and an uncached binary fetch.

## 1 · Statements list

```json
{
  "Data": { "Statement": [
    { "AccountId": "1123456842", "StatementId": "960808",
      "StatementReference": "Reference 654", "Type": "Annual",
      "StartDateTime": "2023-06-06T12:41:00+00:00",
      "EndDateTime": "2023-07-06T12:40:00+00:00",
      "CreationDateTime": "2023-07-06T12:41:00+00:00",
      "StatementAmount": [
        { "CreditDebitIndicator": "Credit",
          "Type": "UK.OBIE.AverageBalanceWhenInCredit",
          "Amount": { "Amount": "5678.88", "Currency": "GBP" } } ],
      "StatementBenefit": [ … ], "StatementFee": [ … ],
      "StatementDateTime": [ … ], "StatementValue": [ … ] }
  ] },
  "Links": { "Self": "…/statements" },
  "Meta": { "TotalPages": 1 }
}
```

`StatementAmount[]` is a **typed array**, not a flat closing balance. The row's closing balance
is the entry whose `Type` is the closing-balance variant — reaching for
`Statement.ClosingBalance` returns nothing.

`StatementFee[]` entries carry `Rate` + `RateType` (`UK.OBIE.AER`) — the source of the `%%`
rendering trap documented in `exports/product/API.md`.

The period label ("May 2026") is **derived in the ViewModel** from `StartDateTime`/`EndDateTime`;
the bank sends no label.

## 2 · Statement file

`GET /accounts/{AccountId}/statements/{StatementId}/file` → `200 application/pdf`, raw bytes.

**No store, no cache, no screen state.** `StatementFileRepository.downloadStatementFile(...)`
returns `NetworkResult<ByteArray, NetworkError>` and the bytes go straight to the injected
`StatementFileHandler` — a delivery seam the feature *declares* but does not implement.

Platform binding is an app-layer `expect`/`actual` in cmp-navigation
(`nonJsCommonMain` FileKit `openFileSaver` + `PlatformFile.write`; `jsCommonMain` a documented
no-op). A **501** means the bank does not offer a file for that statement — surfaced as
`ShowDownloadUnavailable`, distinct from a genuine failure.

## Error matrix

| HTTP | Endpoint | Kind | Retry? |
|---|---|---|:--:|
| 401 | either | `TokenExpiredError` | ✅ |
| 403 | either | `ConsentScopeError` | ✅ — re-authorising in Consents is a path back |
| 429 | list | `RateLimitedError` | ✅ back-off |
| **501** | file | `StatementDownloadUnsupportedError` | ✗ — the bank offers no file |
| — | either | `NetworkError` | ✅ |
| — | list | empty `Data.Statement[]` | Empty state |

All five kinds are retriable, unlike `direct-debits` where `ConsentRevoked` is terminal.

A **successful download raises no event** — the platform's save/share sheet is the feedback.
Only the two failure paths produce snackbars.

## Product gating

`Statements` = **{CreditCard} only** — per HSBC's spec, "Supported product types (Credit
Cards)". Every non-credit-card product hides the Explore option. It is the mirror of
ScheduledPayments and Beneficiaries, which are offered on everything *except* a credit card.

## Cache

`statementsStore` — `createMemoryStore(fetcher)`. Statement metadata is consent-scoped: a
cached copy could outlive the consent that permitted it. The **file** is never cached at all.

## Source binding

`core/network/api/Aisp.kt` `getStatements` / `getStatementFile` ·
`BankingStores.statementsStore` (memory) · `StatementsRepository` (stateless stream) ·
`StatementFileRepository` (storeless one-shot) · `feature/statements/.../StatementFileHandler.kt`
(interface) + `cmp-navigation/.../statements/StatementFileHandlerProvider.kt` (binding).
