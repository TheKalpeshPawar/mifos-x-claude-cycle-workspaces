<!-- source: screens/settings/api.yaml -->
<!-- source_hash: regenerated-2026-07-14 -->
<!-- generated: 2026-07-14T21:00:00Z -->

# settings — API Reference

> **Client-only feature — no server API.**  
> Source: `idea-layer/screens/settings/api.yaml` (`endpoints: []`)  
> Generated: 2026-07-14T21:00:00Z

---

## Summary

The settings feature performs no network calls. All user preferences are persisted locally via
`androidx.datastore:datastore-preferences`. No OBIE endpoints are invoked.

| Aspect | Detail |
|---|---|
| Network calls | None |
| Persistence | DataStore (local key-value store) |
| Affected server state | None — Open Banking consent authorisations on the OBIE server are NOT modified |
| GDPR scope | `execute_clear_local_data` erases locally cached account/transaction rows (Room/SQLDelight) and resets DataStore cached-at timestamps only |

---

## Local DataStore Keys

Although no server API is called, the following DataStore keys are read and written by
`SettingsViewModel`:

| Key | Type | Values |
|---|---|---|
| `theme` | String | `Light` / `Dark` / `System` |
| `biometric_lock_enabled` | Boolean | `true` / `false` |
| `session_timeout` | String | `2 minutes` / `5 minutes` / `10 minutes` / `30 minutes` |
| `notify_consent_expiry` | Boolean | `true` / `false` |
| `notify_security_alerts` | Boolean | `true` / `false` |

All keys are read as a `Flow<Preferences>` and written via `DataStore.updateData { ... }` atomically.

---

## Clear Local Data Operation

`execute_clear_local_data` is a destructive local operation (not an API call):

1. Delete all cached account and transaction rows from Room/SQLDelight (transactional delete).
2. Reset DataStore `cached_at_*` timestamp keys to `null` — **only after** Room deletion succeeds.
3. Emit `LocalDataCleared` one-shot event; UI shows success snackbar.
4. On Room delete failure: show error snackbar with Retry; DataStore timestamps are NOT reset.
