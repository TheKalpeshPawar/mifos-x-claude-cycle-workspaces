<!-- source: screens/spending-by-category/api.yaml -->
<!-- source_hash: regenerated-2026-07-16 -->
<!-- generated: 2026-07-16T00:00:00Z -->

# spending-by-category — API Reference

> **Client-only feature — no server API.**  
> Source: `idea-layer/screens/spending-by-category/api.yaml` (`endpoints: []`)  
> Generated: 2026-07-16T00:00:00Z

---

## Summary

The spending-by-category feature performs no network calls. Category aggregation runs entirely
in-app over locally cached AIS transaction data. No OBIE AIS endpoints are invoked by this screen.

| Aspect | Detail |
|---|---|
| Network calls | None |
| Data source | Local Room/SQLDelight `pfm_room_cache` — cached `OBTransaction6` debit rows |
| Local store | `PfmTransactionCache` (Room/SQLDelight, `pfm_room_cache`; shared with pfm-dashboard and budgets) |
| Access mode | Read-only — no writes to the transaction cache |
| Affected server state | None |

---

## Aggregation Algorithm (Client-Side)

All computation runs in `viewModelScope` via `selectPeriod(SpendingPeriod)` over cached
Room debit rows. Libraries: `kotlinx-datetime`, `kotlin-coroutines`.

| Step | Detail |
|---|---|
| Filter | `CreditDebitIndicator = Debit` AND `BookingDateTime` within `kotlinx-datetime` `LocalDate` range for the selected period |
| Group | By auto-assigned category tag (derived from `MerchantCategory` / `ProprietaryBankTransactionCode` MCC codes) |
| Aggregate per group | `totalAmount` (GBP), `transactionCount`, `percentageOfTotal` (rounded to 1dp), `fraction` (0.0–1.0) |
| Sort | By `totalAmount` descending |
| Period labels | `this_month` → current calendar month name; `last_month` → previous month name; `3_months` → `MMM–MMM YYYY` range |

Period chip changes trigger full re-aggregation in `viewModelScope`; no network call is made.

---

## Cache Lifecycle

| Property | Value |
|---|---|
| Cache name | `pfm_room_cache` |
| Path | `{platform.app_files_dir}/databases/pfm_cache` |
| Max size | ~50 MB (shared across pfm-dashboard, spending-by-category, budgets) |
| TTL | 24 hours |
| Clear triggers | (a) User action: Settings → Clear Local Data (`executeClearLocalData`) or Settings → Clear PFM Cache (`clearPfmCache`); (b) `consent_revoked` event from `ConsentRepository` wipes Room transactions table |
| On cache clear (screen active) | Next `selectPeriod` / `on_mount` produces 0 rows → `UiState.Empty`; period selector remains interactive; no background re-sync initiated by this screen |

---

## Navigation Output

Tapping a category row emits a navigation event — not a network call:

```
on_click:
  action: navigate_category_transactions
  target: transactions
  params:
    category: "{item.name}"   # URI-encoded category name
```
