# Statement detail — API Contracts

> Generated from `screens/statement-detail/api.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Endpoints: 3 · DTOs: 2

Base path `/obie/open-banking/v4.0/aisp`.

## Endpoint summary

| # | ID | Method | Path | Permission | Response | Cache |
|---|---|---|---|---|---|---|
| 1 | `statement-detail` | GET | `/accounts/{AccountId}/statements/{StatementId}` | ReadStatementsDetail | `OBReadStatement2` | memory, composite key |
| 2 | `statement-txns` | GET | `…/{StatementId}/transactions` | ReadTransactions | `OBReadTransaction6` | memory, composite key |
| 3 | `statement-file` | GET | `…/{StatementId}/file` | ReadStatements | `ByteArray` (application/pdf) | **none** |

**Three different permissions.** A consent missing `ReadTransactions` still renders balances; a
consent missing `ReadStatements` still renders the statement but cannot download it. The
degradation is per-section, not all-or-nothing.

## Composite cache keys

Both cached stores key on the **pipe-joined pair**:

```
cacheKey = "$accountId|$statementId"
```

Keying on `statementId` alone would collide across accounts; keying on `accountId` alone would
serve the wrong statement. These are the only two composite-key stores in the app.

## 1 · Statement detail

`GET …/statements/{StatementId}` → `200` `OBReadStatement2` — the same envelope as the list
endpoint, filtered to one statement.

Rendered: `StartDateTime`/`EndDateTime` (period header), `StatementAmount[]` filtered by `Type`
for opening/closing balances, `StatementFee[]` (with `Rate` + `RateType`), and interest entries.

`StatementAmount[]` is a **typed array**, not flat fields — see
`exports/statements/API.md#1--statements-list`.

## 2 · Statement transactions

`GET …/{StatementId}/transactions` → `200` `OBReadTransaction6`

Same shape as the account transactions endpoint, scoped to the statement period. Reuses
`TransactionItem`, so rows navigate on to `transaction-detail`.

An **empty `Data.Transaction[]` is `Empty` with balances still shown** — a period with no
activity is information, not missing data.

The `Balance.CreditDebitIndicator` trap applies here too: it describes the transaction's
direction, not the balance's. Running balances unsigned.

## 3 · Statement file

`GET …/{StatementId}/file` → `200 application/pdf`, raw bytes.

Reuses `StatementFileRepository` and the `StatementFileHandler` seam from `feature/statements`
— **no second platform binding**. That reuse is the point of the seam.

## Parallel fetch

Statement metadata and transactions are independent and fetch concurrently; the ViewModel
merges them with `combineScreenStates`, whose priority is
**NoNetwork > Loading > Unauthenticated > Error > Empty > Content**, freshness worst-of, and
`transform` running only when both are `Content` (TC-STMTD-002).

## Error matrix

| HTTP | Endpoint | Kind | Retry? |
|---|---|---|:--:|
| 404 | detail | `StatementNotFound` | ✗ |
| 404 | file | `StatementFileNotFound` | ✗ — **snackbar**, the screen stays usable |
| 401 | any | `SessionExpired` | ✅ |
| 403 | any | `ConsentMissingReadStatements` | ✗ — names the missing permission |
| — | any | `NetworkError` | ✅ |
| — | txns | empty `Data.Transaction[]` | **Empty**, balances still rendered |

A file 404 is deliberately a snackbar rather than an error state: the statement itself loaded
fine, only the PDF is unavailable.

## Source binding

`core/network/api/Aisp.kt` `getStatementDetails` / `getStatementTransactions` /
`getStatementFile` · `BankingStores.statementDetailStore` + `statementTransactionsStore` (both
memory, composite-keyed) · `StatementDetailRepository` (two streams) · `StatementFileRepository`
(shared with `feature/statements`).
