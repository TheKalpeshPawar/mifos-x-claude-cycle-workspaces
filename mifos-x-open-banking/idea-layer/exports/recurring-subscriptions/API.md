<!-- source: screens/recurring-subscriptions/api.yaml -->
<!-- source_hash: regenerated-2026-07-14 -->
<!-- generated: 2026-07-14T21:00:00Z -->

# recurring-subscriptions — API Reference

> **Client-only feature — no server API.**  
> Source: `idea-layer/screens/recurring-subscriptions/api.yaml` (`endpoints: []`)  
> Generated: 2026-07-14T21:00:00Z

---

## Summary

The recurring-subscriptions feature performs no network calls. Recurring payment patterns are
detected entirely in-app from the local DataStore transaction cache populated by the
transactions feature. No OBIE AIS endpoints are invoked.

| Aspect | Detail |
|---|---|
| Network calls | None |
| Data source | Local DataStore transaction cache (written by `transactions` feature) |
| Access mode | Read-only — no writes to the shared cache |
| Affected server state | None |

---

## Algorithm (Client-Side)

All computation runs on `List<TransactionInformation>` read from local DataStore:

| Step | Detail |
|---|---|
| Normalise merchant | Lower-case, strip legal suffixes, collapse whitespace |
| Filter | Groups with ≥ 2 occurrences |
| Infer cadence | `kotlinx-datetime` DatePeriod comparisons; ± 5 day tolerance for Weekly / Fortnightly / Monthly / Annual |
| Project next date | Last transaction date + detected DatePeriod |
| Normalise to monthly | Monthly → same; Annual ÷ 12; Weekly × 52/12; Fortnightly × 26/12 |
| Sort | By `monthly_equivalent` descending |

---

## Navigation Output

Tapping a subscription row emits a navigation event to the **transactions** screen with a
merchant filter parameter — this is an in-app navigation, not a network call:

```
on_click:
  action: navigate_transactions
  target: transactions
  params:
    merchant: "{item.merchant}"   # normalised merchant name
```
