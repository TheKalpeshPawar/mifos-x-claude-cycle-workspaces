# Gap Analysis: Dynamic DataTable Steps in Loan Account Creation

**Feature**: Loan DataTable Entity Check — Dynamic Steps Driven by Product Selection
**Gap ID**: GAP-LOAN-DATATABLE-001
**Type**: Enhancement (existing infrastructure wired but navigation callback commented out)
**Affected module**: `feature:loan` + `feature:data-table` + `cmp-navigation`
**Date**: 2026-05-22
**Analyst**: claude (sonnet-router, idea-gap tier)

---

## 1. What the User Wants

When a field officer creates a loan, the selected loan product may require one or more custom data tables (e.g. "DATOS_RAZON_SOCIAL" with fields NOMBRE_RAZON_SOCIAL, NO_MATRICULA, NO_PERMISO, NOMBRE_EMBARCACION, MONTO_SOLICITADO). The backend already returns these in the loan template response under `dataTables`. The Android app must:

1. When a product is selected, fetch its template (`/loans/template?clientId=X&productId=Y`).
2. Read `dataTables` from the response.
3. If dataTables is non-empty: navigate to the `DataTableListScreen` (feature:data-table) — one form page per datatable — before final loan creation.
4. If dataTables is empty: submit the loan directly (current behaviour).
5. On DataTableListScreen "Save", merge the filled datatable payloads into the `LoansPayload.dataTables` field and create the loan.

The Mifos WebApp (Angular) already implements this exactly: `CreateLoansAccountComponent` calls `setDatatables()` after product selection, reads `loansAccountProductTemplate.datatables`, creates one `MatStepper` step per datatable via `*ngFor` on `LoansAccountDatatableStepComponent`, then on submit collects each step's `payload` and merges into the loan creation payload.

---

## 2. Current State in Android Client

### What Exists (Infrastructure Ready)

| Layer | File | Status |
|-------|------|--------|
| API service | `core/network/.../DataTableService.kt` | Full CRUD: GET tables, GET data, POST entry, DELETE entry |
| Network API | `core/network/.../DataTablesApi.kt` | Wired to Ktorfit |
| Mapper | `core/network/.../GetDataTablesResponseMapper.kt` | Maps `GetDataTablesResponse` → `DataTableEntity` (missing `dataTableColumnName` — maps `columnName` but not populating the `dataTableColumnName` field on `ColumnHeader`) |
| Repository impl | `core/data/.../DataTableListRepositoryImp.kt` | Has `createLoansAccount(loansPayload)` |
| Repository impl | `core/data/.../DataTableDataRepositoryImp.kt` | Has `getDataTableInfo`, `deleteDataTableEntry` |
| Entity | `core/database/.../DataTableEntity.kt` | `applicationTableName`, `registeredTableName`, `columnHeaderData: List<ColumnHeader>` |
| Entity | `core/database/.../ColumnHeader.kt` | `columnDisplayType`, `columnPrimaryKey`, `dataTableColumnName`, `columnValues`, etc. |
| LoanTemplate model | `core/database/.../LoanTemplate.kt` | Has `dataTables: ArrayList<DataTableEntity>` — field exists and is serializable |
| LoansPayload | `core/network/.../LoansPayload.kt` | Has `dataTables: ArrayList<DataTablePayload>?` |
| DataTableListScreen | `feature/data-table/.../DataTableListScreen.kt` | Full UI: shows table name + `TableColumnHeader` form widgets per column type (STRING, INT, DECIMAL, CODELOOKUP, DATE, BOOL) |
| DataTableListViewModel | `feature/data-table/.../DataTableListViewModel.kt` | `initArgs()` + `processDataTable()` + `createLoanAccount()` — full logic exists |
| LoanAccountScreen | `feature/loan/.../LoanAccountScreen.kt` | `dataTable: (List<DataTableEntity>, LoansPayload) -> Unit` callback at lines 103, 143, 624 |
| Navigation | `feature/loan/.../LoanAccountScreenRoute.kt` | `addLoanAccountScreen(onBackPressed, dataTable)` — callback declared |
| Navigation graph | `cmp-navigation/.../AuthenticatedNavigation.kt` | `dataTableNavGraph(...)` already in NavGraph |

### The Gap (Single Root Cause)

**The `dataTable` callback in `AuthenticatedNavigation.kt` is commented out / empty (lines 164–170):**

```kotlin
addLoanAccountScreen(
    onBackPressed = navController::popBackStack,
    dataTable = { _, _ ->
//                navController.navigateDataTableList(dataTable, payload, Constants.CLIENT_LOAN)
//                TODO()
    },
)
```

The call to `navigateDataTableList` is commented out. This is the one wire that, when connected, activates the entire pre-built pipeline.

### Secondary Gaps Discovered During Analysis

| ID | Gap | Severity | File |
|----|-----|----------|------|
| GAP-DT-001 | Navigation callback is a no-op (commented out) | Critical | `cmp-navigation/AuthenticatedNavigation.kt:166` |
| GAP-DT-002 | `navigateDataTableList` signature requires `formWidget: MutableList<List<FormWidgetDTO>>` but `LoanAccountScreen` only passes `List<DataTableEntity>` — the `FormWidgetDTO` list must be built from `columnHeaderData` before navigation | Critical | `feature/loan/.../LoanAccountScreen.kt:624` |
| GAP-DT-003 | `GetDataTablesResponseMapper` does not populate `ColumnHeader.dataTableColumnName` — column names appear as null in `TableColumnHeader` composable (line 209: `label = columnHeader.dataTableColumnName ?: ""` shows blank labels) | High | `core/network/.../GetDataTablesResponseMapper.kt:29-36` |
| GAP-DT-004 | `TableColumnHeader` filter: `table.columnHeaderData.filter { it.columnPrimaryKey != null }` — this keeps all rows where `columnPrimaryKey` is non-null, including the primary key column itself (loan_id). Should filter to `it.columnPrimaryKey == false` to skip system columns (loan_id, created_at, updated_at) | High | `feature/data-table/.../DataTableListScreen.kt:203` |
| GAP-DT-005 | `DataTableListViewModel.addDataTableInput` uses `FormWidgetModel` class (references obsolete class, not `FormWidgetDTO`) — the widget list passed through `navigateDataTableList` isn't being built anywhere in the new KMP codebase | Medium | `feature/data-table/.../DataTableListViewModel.kt:202` |
| GAP-DT-006 | `TableColumnHeader` fields are stateless — form inputs are `value = ""` with `onValueChange = {}`, so user input is never captured. State must be lifted to a `ViewModel`-owned `Map<String, String>` keyed by `columnHeader.dataTableColumnName` | High | `feature/data-table/.../DataTableListScreen.kt:205-340` |
| GAP-DT-007 | `LoanAccountScreen` fetches template with first product on load (`state.productLoans[0].id?.let { fetchTemplate(it) }`) but only updates template when a product is explicitly selected via `onLoanProductSelected`. There is no reactive link between template refresh and dataTables population | Low | `feature/loan/.../LoanAccountScreen.kt:169` |

---

## 3. API Contract

**Endpoint**: `GET /fineract-provider/api/v1/loans/template?templateType=individual&clientId={X}&productId={Y}`

**Response** (relevant excerpt from `loan_product_1.json`):
```json
{
  "datatables": [
    {
      "applicationTableName": "m_loan",
      "registeredTableName": "DATOS_RAZON_SOCIAL",
      "columnHeaderData": [
        { "columnName": "loan_id",             "columnDisplayType": "INTEGER", "isColumnPrimaryKey": true  },
        { "columnName": "NOMBRE_RAZON_SOCIAL",  "columnDisplayType": "STRING",  "isColumnPrimaryKey": false },
        { "columnName": "NO_MATRICULA",         "columnDisplayType": "STRING",  "isColumnPrimaryKey": false },
        { "columnName": "NO_PERMISO",           "columnDisplayType": "STRING",  "isColumnPrimaryKey": false },
        { "columnName": "NOMBRE_EMBARCACION",   "columnDisplayType": "STRING",  "isColumnPrimaryKey": false },
        { "columnName": "MONTO_SOLICITADO",     "columnDisplayType": "DECIMAL", "isColumnPrimaryKey": false },
        { "columnName": "created_at",           "columnDisplayType": "DATETIME","isColumnPrimaryKey": false }
      ]
    }
  ]
}
```

The `datatables` array is NOT in the `/loans/template` response — it comes in the **loan product template** response. The `LoanTemplate` entity already has `dataTables: ArrayList<DataTableEntity>` and the Fineract API does populate it when queried per-product.

**Loan Products 2+ have no datatables** (loan_product_2.json has 0 occurrences of `datatables`) — confirmed: each product independently declares its own set of required datatables. This is the "product-driven dynamic step" behaviour the user is asking for.

---

## 4. Web App Reference Implementation

The Angular web app implements this in `create-loans-account.component.ts`:

```typescript
setDatatables(): void {
  this.datatables = [];
  if (this.loansAccountProductTemplate.datatables) {
    this.loansAccountProductTemplate.datatables.forEach((datatable: any) => {
      this.datatables.push(datatable);
    });
  }
}
```

On submit, it iterates each `LoansAccountDatatableStepComponent` and collects `.payload`, then merges into `payload['datatables']`. The Android app has equivalent structures but the wiring is missing.

---

## 5. Requirements Gap

| FR ID | Requirement | Status |
|-------|-------------|--------|
| FR-LOAN-DT-001 | When a loan product is selected, load and display only the datatables attached to that product (0 to N tables) | Missing |
| FR-LOAN-DT-002 | Each datatable is rendered as a form with fields derived from `columnHeaderData`, skipping system columns (loan_id, created_at, updated_at) | Missing (UI exists but stateless + filter bug) |
| FR-LOAN-DT-003 | Datatable form fields must support: STRING (text input), DECIMAL/INTEGER (numeric input), DATE (date picker), CODELOOKUP/CODEVALUE (dropdown), BOOLEAN (toggle) | Partially present (TableColumnHeader has cases) |
| FR-LOAN-DT-004 | On submit, merge datatable form data into `LoansPayload.dataTables` as `DataTablePayload` objects before API call | Infrastructure present in DataTableListViewModel but not wired for loan flow |
| FR-LOAN-DT-005 | If the selected product has no datatables, submit the loan directly (no extra step) | Already works — line 624 of LoanAccountScreen: `if (loanTemplate.dataTables.isNotEmpty()) { dataTable(...) } else { createLoanAccount(...) }` |
| FR-LOAN-DT-006 | Datatable form values must be captured into ViewModel state (not stateless composable locals) | Missing — inputs are `value = ""` with no state |

---

## 6. Affected Screens / Idea-Layer Sections

### Screens to Update / Add

| Screen | Change Type | Description |
|--------|-------------|-------------|
| `LoanAccountScreen` (existing) | Update | Add `FormWidgetDTO` builder logic before calling the `dataTable` callback; remove `LoanAccountViewModel` dependency on pre-built formWidgets |
| `DataTableListScreen` (existing) | Update | Lift `TableColumnHeader` field state to ViewModel (`Map<String, String>` per table); fix column filter; fix `dataTableColumnName` rendering |
| `DataTableListViewModel` (existing) | Update | Fix `addDataTableInput` to use `FormWidgetDTO`-compatible input collection from stateful ViewModel; add `processLoanDataTableDirect` path that doesn't require pre-built `FormWidgetDTO` list |

### Alternative Approach (Simpler, No FormWidget dependency)

Instead of building a `FormWidgetDTO` list in `LoanAccountScreen` and passing it through navigation (which is brittle and requires serialisation), the simpler approach — matching what the web app does — is:

1. Pass only `List<DataTableEntity>` to the datatable screen (already present in the callback signature).
2. In `DataTableListViewModel`, derive the form state directly from `DataTableEntity.columnHeaderData` (which is already deserialized by `LoanTemplate.dataTables`).
3. Eliminate the `formWidget: MutableList<List<FormWidgetDTO>>` parameter from `navigateDataTableList` for the loan creation path (or keep it as empty list and ignore it).

This avoids the entire `FormWidgetDTO` serialization problem (GAP-DT-005).

---

## 7. Flows Gap

### Current Flow
```
LoanAccountScreen → [select product] → loadLoanAccountTemplate()
    → [submit form] → if dataTables empty → createLoanAccount()
                    → if dataTables non-empty → dataTable() callback = NO-OP
```

### Target Flow
```
LoanAccountScreen → [select product] → loadLoanAccountTemplate()
    → [submit form] → if dataTables empty → createLoanAccount() [unchanged]
                    → if dataTables non-empty →
                        navigateDataTableList(dataTables, loansPayload, CLIENT_LOAN)
                            → DataTableListScreen [one form per datatable]
                                → [fill fields] → [Save]
                                    → processDataTable()
                                        → merge into LoansPayload.dataTables
                                        → createLoanAccount(mergedPayload)
                                            → success → pop to client detail
```

---

## 8. Implementation Path

**Classification**: Direct Fix + Enhancement (infrastructure exists, needs wiring + 3 bug fixes)

**Recommended path**: `/implement` (not `/idea-plan`, not `/idea-enrich` — code is the deliverable)

**Reason**: The idea-layer is a stub (`_overall_quality: 0`). This is a well-understood backend-driven enhancement with a clear web app reference. All infrastructure exists. The work is:

1. Fix the navigation callback wire (1 line change in `AuthenticatedNavigation.kt`)
2. Fix `GetDataTablesResponseMapper` to populate `dataTableColumnName` from `columnName`
3. Fix `TableColumnHeader` column filter: `columnPrimaryKey == false` (not `!= null`)
4. Lift `TableColumnHeader` input state to `DataTableListViewModel`
5. Fix `addDataTableInput` in `DataTableListViewModel` to use stateful input from step 4
6. (Optional) simplify `navigateDataTableList` to not require pre-built `FormWidgetDTO` for loan path

**Estimated scope**: 4–6 files, ~200 lines of changes. No new modules required.

---

## 9. Gap Summary

```
━━━ /idea gap — android-client feature:loan DataTable Steps ━━━

  Requirements → Features:
    ❌ FR-LOAN-DT-001 — dynamic datatable steps per product: no feature assigned
    ❌ FR-LOAN-DT-002 — stateful datatable form rendering: missing state lift
    ❌ FR-LOAN-DT-003 — field type coverage: partial (stateless UI only)
    ❌ FR-LOAN-DT-004 — datatable payload merge on submit: not wired for loan flow
    ✅ FR-LOAN-DT-005 — skip datatables when empty: already works
    ❌ FR-LOAN-DT-006 — form field state capture: missing

  Features → Implementation:
    ❌ GAP-DT-001 (Critical)  — navigation callback no-op in AuthenticatedNavigation.kt:166
    ❌ GAP-DT-002 (Critical)  — FormWidgetDTO list not built before navigateDataTableList
    ❌ GAP-DT-003 (High)      — GetDataTablesResponseMapper missing dataTableColumnName mapping
    ❌ GAP-DT-004 (High)      — TableColumnHeader filter keeps primary key columns
    ❌ GAP-DT-005 (Medium)    — addDataTableInput references non-existent FormWidgetModel class
    ❌ GAP-DT-006 (High)      — TableColumnHeader inputs are stateless (value="", onValueChange={})
    ℹ  GAP-DT-007 (Low)       — template reload on product change: minor UX issue, not blocking

  Implementation → Tests:
    ❌ Zero unit/UI tests for DataTable loan flow

  Total gaps: 7 (2 Critical, 3 High, 1 Medium, 1 Low)

  Next step: Run `/implement` to fix all gaps in feature:loan + feature:data-table + cmp-navigation.
```

---

## 10. Files to Touch

| File | Change |
|------|--------|
| `cmp-navigation/authenticated/AuthenticatedNavigation.kt` | Uncomment + fix `navigateDataTableList` call; pass formWidgets or use simplified path |
| `core/network/mappers/dataTable/GetDataTablesResponseMapper.kt` | Add `dataTableColumnName = it.columnName` to `ColumnHeader` mapping |
| `feature/data-table/dataTableList/DataTableListScreen.kt` | Fix column filter: `columnPrimaryKey == false`; add stateful value holders per column |
| `feature/data-table/dataTableList/DataTableListViewModel.kt` | Add `MutableStateFlow<Map<Int, Map<String, String>>>` for form state; fix `addDataTableInput` |
| `feature/loan/loanAccount/LoanAccountScreen.kt` | Build formWidget list from `loanTemplate.dataTables` before calling `dataTable()` callback (or simplify to pass dataTables only) |
| `feature/data-table/navigation/DataTableNavigation.kt` | (Optional) overload `navigateDataTableList` without formWidget param for loan path |

---

_Gap analysis produced by: claude (sonnet-router) on 2026-05-22_
_Source inspected: feature:loan, feature:data-table, cmp-navigation, core/network, core/database, web-app/loans_
_Loan product samples: loan_product_1.json (has datatables), loan_product_2.json (no datatables)_
