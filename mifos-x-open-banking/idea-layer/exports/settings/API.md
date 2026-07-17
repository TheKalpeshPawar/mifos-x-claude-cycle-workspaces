<!-- source: screens/settings/api.yaml -->
<!-- source_hash: regenerated-2026-07-16 -->
<!-- generated: 2026-07-16T00:00:00Z -->

# settings — API Reference

> **Client-only feature — no server API.**  
> Source: `idea-layer/screens/settings/api.yaml` (`endpoints: []`)  
> Generated: 2026-07-16T00:00:00Z

---

## Summary

The settings feature performs no network calls. All preferences are persisted exclusively to
on-device local storage. No OBIE AIS endpoints are invoked.

| Aspect | Detail |
|---|---|
| Network calls | None |
| Local store — preferences | `androidx.datastore` (`SettingsDataStore`): theme, biometric_lock_enabled, session_timeout, notify_consent_expiry, notify_security_alerts |
| Local store — cache (clear target) | Room/SQLDelight `pfm_room_cache` — deleted by `executeClearLocalData` and `clearPfmCache` |
| Affected server state | None — Open Banking consent authorisations on the HSBC server are NOT modified by any settings action |

---

## Local Storage Details

### DataStore Preference Keys (written by `SettingsDataStore`)

| Key | Type | Default | Written by |
|---|---|---|---|
| `theme` | String | `System` | `updateTheme` |
| `biometric_lock_enabled` | Boolean | `false` | `toggleBiometricLock` |
| `session_timeout` | String | `5 minutes` | `updateSessionTimeout` |
| `notify_consent_expiry` | Boolean | `true` | `toggleConsentExpiryNotification` |
| `notify_security_alerts` | Boolean | `true` | `toggleSecurityAlertsNotification` |
| `cached_at` timestamps | Nullable Instant | null | Reset (set to null) by `executeClearLocalData` after Room deletion succeeds |

### Room/SQLDelight Cache (managed by `LocalCacheRepository`)

| Store | Path | Max size | Cleared by |
|---|---|---|---|
| `pfm_room_cache` | `{app_files_dir}/databases/pfm_cache` | ~50 MB (shared with pfm-dashboard and spending-by-category) | `executeClearLocalData` (full account + transaction cache wipe) · `clearPfmCache` (PFM aggregation rows only) |

Note: `executeClearLocalData` resets DataStore `cached_at` timestamps only after the Room
transactional delete succeeds. If the Room delete fails, DataStore timestamps are NOT reset
(`CacheDeleteError` — shows error snackbar with retry).

---

## Destructive Actions

Two destructive cache-erasure actions are gated by user confirmation before execution:

| Action | Scope | Library refs | Gate |
|---|---|---|---|
| `clearPfmCache` | Clears PFM Room aggregated spending/income/category rows (`pfm_room_cache`) only | `room` | Confirmation bottom-sheet |
| `executeClearLocalData` | Clears all locally cached account + transaction rows from Room/SQLDelight AND resets DataStore `cached_at` timestamps | `room`, `sqldelight`, `androidx.datastore` | `clear_local_data_sheet` bottom-sheet (reached via `clear_confirm` state) |

Neither action modifies Open Banking consent authorisations on the HSBC server.

---

## External URL Dispatch

The following rows dispatch URLs to the system browser via `platform-intent/openURL`
(Android intent / iOS `openURL`). These are not network calls within the app — they hand
off to the platform browser:

| Row | URL |
|---|---|
| `terms_row` | `https://www.openbanking.org.uk/customer-hub/terms-and-conditions/` |
| `privacy_row` | `https://www.openbanking.org.uk/privacy-policy/` |

If no browser is installed (`ActivityNotFoundException` / `NoBrowserError`), a snackbar is shown
and the app does not crash.
