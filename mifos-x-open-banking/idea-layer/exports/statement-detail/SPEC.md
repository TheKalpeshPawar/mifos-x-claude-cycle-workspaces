# Statement detail — Feature Specification

> Generated from `screens/statement-detail/ui.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Source hash: `329f9c2dc107`
> Endpoints: 3 · DTOs: 2 · Components: 15 · Test scenarios: 9

## Lossless Export Contract

Lossless per RULE-EXPORT-ROUNDTRIP-001 — State Defaults, Error Matrix, Test Mapping and
Nav Origins below let the generators consume this file alone.

## 1. Overview

Single statement: period header, opening/closing balances, fees, interest, and the transactions
within the statement period. Download PDF with inline progress and snackbar feedback.

| Attribute | Value |
|---|---|
| Feature ID | `statement-detail` · Cluster statements |
| Priority | should (FR-007) · Status approved · quality 95 |
| Archetype | detail_screen · Route `StatementDetailRoute(accountId, statementId)` |
| Source module | `feature/statement-detail` — **implemented** |

## 2. Composite two-stream merge + download-seam reuse

The **second exemplar of the two-stream shape** after `account-detail`, and the one that
demonstrates reuse of an existing platform seam rather than building a second.

Two streams merged in the ViewModel via `combineScreenStates`:

| Stream | Store | Key |
|---|---|---|
| statement metadata | `statementDetailStore` | `"$accountId\|$statementId"` |
| statement transactions | `statementTransactionsStore` | `"$accountId\|$statementId"` |

**Composite keys** — both stores are keyed on the pipe-joined pair, not on either id alone.

It **reuses `feature/statements`' `StatementFileHandler` seam and `StatementFileRepository`**
for Download PDF, so it holds two repositories but owns **no second platform binding**. That is
the reuse the seam was designed for.

Two route args: `ACCOUNT_ID_ARG` and `STATEMENT_ID_ARG`, both matching their route property
names.

## 3. Screen inventory

`progress_indicator` · `statement_header_card` · `balances_header`+`balances_list` ·
`fees_header`+`fees_list` · `interest_header`+`interest_list` ·
`transactions_header`+`statement_txns_list` · `empty_txns_state` · `download_pdf_button` ·
`download_progress` · `download_result_snackbar` · `error_state`.

Fifteen components — tied with `send-money` for the widest in the app.

## 4. State model — `StatementDetailViewModel`

**Fields:** `uiState` · `downloadState` · **Default:** `uiState = Loading`
**UiState:** `Loading` · `Content` · `Empty` · `Error`
**Error kinds:** `StatementNotFound` · `ConsentMissingReadStatements` · `SessionExpired` ·
`StatementFileNotFound` · `NetworkError`
**Actions:** `RetryLoad` · `DownloadPdf`
**Events:** `DownloadSucceeded` / `DownloadFailed` — non-`Nothing`, like `statements`
**DI:** `SavedStateHandle` · `StatementDetailRepository` · `StatementFileRepository` ·
`StatementFileHandler`

**An empty transaction list is `Empty`, balances still shown** — the period genuinely had no
activity, which is information, not an absence of data.

## 5. Navigation

| Origin | Trigger | Target |
|---|---|---|
| `statements` | tap a statement row | `statement-detail` (accountId, statementId) |
| transaction row | tap | **`transaction-detail`** |
| back | top-app-bar leading | `statements` |

It reuses `TransactionItem` for its transaction rows, so those taps navigate on to
`transaction-detail` via an `onNavigateToTransactionDetail` lambda — a third entry point to
that screen alongside `transactions` and `home`.

## 6. API dependencies

| ID | Method | Path | Permission | Response DTO |
|---|---|---|---|---|
| `statement-detail` | GET | `/accounts/{AccountId}/statements/{StatementId}` | ReadStatementsDetail | `OBReadStatement2` |
| `statement-txns` | GET | `…/{StatementId}/transactions` | ReadTransactions | `OBReadTransaction6` |
| `statement-file` | GET | `…/{StatementId}/file` | ReadStatements | `ByteArray` (application/pdf) |

Note the three declare **three different permissions** — `ReadStatementsDetail`,
`ReadTransactions` and `ReadStatements` — so a consent missing any one degrades a different
part of the screen.

## 7. Design tokens

`card`, `section_header` ×4, `list_item`, `amount` mono, `snackbar` for download feedback.
Canonical brand spec: `design-system/DESIGN.md` 1.1.0.

## 8. Test mapping

TC-STMTD-001 period + balances render · 002 **loading during the parallel fetch** · 003 404
statement not found · 004 **Download PDF triggers statement-file** · 005 back · 006 403
consent-specific message · **007 Empty when the statement has no transactions** · 008 download
error snackbar on file 404 · 009 session-expired message
→ `feature/statement-detail/src/commonTest/.../StatementDetailViewModelTest.kt` + Robolectric.
Ships Roborazzi goldens.

## 9. Notes

`docs.yaml` declares no `flow_ref` despite `flows/recurring-and-statements.yaml` existing.
