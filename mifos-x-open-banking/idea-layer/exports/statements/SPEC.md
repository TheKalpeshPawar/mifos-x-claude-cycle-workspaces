# Statements — Feature Specification

> Generated from `screens/statements/ui.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Source hash: `cdfae01bc3af`
> Endpoints: 2 · DTOs: 1 · Components: 5 · Test scenarios: 9

## Lossless Export Contract

Lossless per RULE-EXPORT-ROUNDTRIP-001 — State Defaults, Error Matrix, Test Mapping and
Nav Origins below let the generators consume this file alone.

## 1. Overview

Chronological statement list for an account. Each row shows a ViewModel-derived period label
("May 2026"), closing balance, formatted date range and a download icon.

| Attribute | Value |
|---|---|
| Feature ID | `statements` · Cluster statements |
| Priority | should (FR-007) · Status approved · **quality 97 — the highest in the corpus** |
| Archetype | index_list · Route `StatementsRoute(accountId: String)` |
| Source module | `feature/statements` — **implemented** |

## 2. The download side-effect and platform seam — reuse this

**The first feature with a non-`Nothing` event type**, and the origin of the file-delivery
pattern.

The list is an ordinary memory-cached `ScreenDataStream` the ViewModel owns. The **download**
is separate: a one-shot `StatementFileRepository.downloadStatementFile(...)` returning
`NetworkResult<ByteArray, …>` with **no store at all** — the bytes go straight to the
platform's save/share sheet, never cached, never rendered as screen state.

Those bytes are handed to an injected **`StatementFileHandler`** — a delivery-seam *interface
the feature declares but does not implement*, keeping the ViewModel testable against a fake.

The platform binding is an **app-layer `expect`/`actual`** in cmp-navigation:
`StatementFileHandlerProvider.kt` (`expect`) + `.nonJs.kt` (FileKit `openFileSaver` +
`PlatformFile.write`) + `.js.kt` (documented no-op — FileKit's saver is non-web-only), via the
`nonJsCommonMain`/`jsCommonMain` split, bound as
`single<StatementFileHandler> { platformStatementFileHandler() }`.

**Reuse this whole shape** for any feature producing a file the platform must save or share.
`statement-detail` already does, injecting the same repository and handler without owning a
second platform binding.

## 3. Screen inventory

`statements_skeleton` · `statements_list` · `statement_row_divider` · `empty_statements` ·
`error_state`.

## 4. State model — `StatementsViewModel`

**Fields:** `uiState` · **`downloadState`** · **Default:** `uiState = Loading`
**UiState:** `Loading` · `Content` · `Empty` · `Error`
**Error kinds:** `TokenExpiredError` · `ConsentScopeError` · `RateLimitedError` ·
`StatementDownloadUnsupportedError` · `NetworkError` — **all five retriable**, unlike
`direct-debits`: a consent-scope 403 offers Retry because re-authorising in Consents is a path back
**Actions:** `RetryLoad` · `DownloadStatement`
**Events:** two, both download-failure snackbars — `ShowDownloadUnavailable` (501) and
`ShowDownloadError`. A *successful* download needs no event: the platform's own save/share
sheet is the feedback.
**DI:** `SavedStateHandle` · `StatementsRepository` · `StatementFileRepository` · `StatementFileHandler`

`DownloadStatement(statementId)` flips that row into `DownloadState.InProgress` in a **per-id
`Map<String, DownloadState>`** on state — absent means `Idle`, so the map stays empty in the
common case — then returns the row to `Idle`.

## 5. Navigation

| Origin | Trigger | Target |
|---|---|---|
| `account-detail` | Statements Explore option | `statements` (accountId) |
| statement row | tap | `statement-detail` (accountId, statementId) |
| back | top-app-bar leading | `account-detail` |

**Gated chip — credit-card-only.** `Statements` = {CreditCard}; every non-credit-card product
hides it. It is the mirror of ScheduledPayments and Beneficiaries.

## 6. API dependencies

| ID | Method | Path | Permission | Response DTO |
|---|---|---|---|---|
| `statements` | GET | `/accounts/{AccountId}/statements` | ReadStatementsDetail | `OBReadStatement2` |
| `statement_file` | GET | `/accounts/{AccountId}/statements/{StatementId}/file` | ReadStatementsDetail | `ByteArray` (application/pdf) |

Full contracts in `API.md`.

## 7. Design tokens

`list_item` + `divider`, `amount` mono for closing balance. Dates and money formatted in the
ViewModel — composables receive finished `*Formatted` strings.
Canonical brand spec: `design-system/DESIGN.md` 1.1.0.

## 8. Test mapping

TC-STMTS-001 six rows render · 002 skeleton · 003 401 + Retry · 004 empty · 005 row →
statement-detail · 006 closing balance · **007 download icon triggers the file request** ·
008 429 rate-limit message · 009 403 consent-scope message
→ `feature/statements/src/commonTest/.../StatementsViewModelTest.kt` +
`StatementsActionTest.kt` (commonTest, `runComposeUiTest`-shaped) + Robolectric.

### First feature to apply Roborazzi

`StatementsScreenScreenshotTest` (androidUnitTest, `@GraphicsMode(NATIVE)`) captures each state
through `createComposeRule().onRoot().captureRoboImage(...)` — **not** the standalone
`captureRoboImage { }` overload, which silently skipped alternate captures when several ran in
one class. Goldens committed under `src/androidUnitTest/screenshots/`.

Its `*UnitTest` exclusion filter covers `*ActionTest` **as well as** `*ScreenUiTest`.

## 9. Notes

`docs.yaml` declares no `flow_ref` despite `flows/recurring-and-statements.yaml` existing.
