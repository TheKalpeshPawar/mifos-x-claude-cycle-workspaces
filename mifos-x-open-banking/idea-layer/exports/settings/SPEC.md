<!-- source: screens/settings/ui.yaml -->
<!-- source_hash: regenerated-2026-07-16 -->
<!-- generated: 2026-07-16T00:00:00Z -->

# SPEC — settings

_Generated: 2026-07-16 · Source: idea-layer/screens/settings/ui.yaml_

---

## 1. Feature Overview

**Name:** Settings  
**Archetype:** settings  
**Cluster:** settings  
**Status:** enriched → designed → approved  
**Quality score:** 95  

**Description:**  
Settings hub persisting theme, biometric-lock, session-timeout and notifications to DataStore
(`kotlinx-serialization`). `SettingsViewModel` emits `Loading → Content`; no network calls.
`clear_confirm` state gates erasure via a bottom-sheet: `dismiss_clear_local_data` returns to
content; `execute_clear_local_data` wipes Room/SQLDelight cache + DataStore cached-at timestamps;
Open Banking consents are unaffected.

**Libraries:**

| Library | Purpose |
|---|---|
| `compose-settings` (`com.github.alorma:compose-settings-ui-m3`) | Pre-built Material 3 Compose settings UI components (list items, switches, dropdowns) |
| `kotlinx-serialization` (`org.jetbrains.kotlinx:kotlinx-serialization-json`) | Serialization for structured preference types stored in DataStore |
| `androidx.datastore` (`androidx.datastore:datastore-preferences`) | Async persistent key-value storage for all settings preferences |

---

## 2. Screen Inventory

| Screen | Archetype | Initial state | Shell |
|---|---|---|---|
| settings | settings | loading | Bottom nav visible · Top app bar `{strings.settings.title}` · No leading icon · No FAB |

**Entry point:** app_shell bottom nav → More tab (order 4)

---

## 3. States

| State | Trigger |
|---|---|
| `loading` | Screen mounts; DataStore `Flow<SettingsPreferences>` has not yet emitted |
| `content` | DataStore emits first `SettingsPreferences` object; all sections visible |
| `empty` | First cold start before DataStore writes defaults; transient (typically one frame) |
| `error` | DataStore read throws `IOException` (storage corruption / disk full) |
| `clear_confirm` | User taps `clear_local_data_row`; destructive bottom-sheet visible; underlying content rows remain rendered |

---

## 4. Components

### State: `loading`

| ID | Type | State binding | Purpose |
|---|---|---|---|
| `settings_loading_skeleton` | skeleton (variant=list, rows=8) | loading | Full-screen shimmer skeleton while DataStore initialises on first composition |

---

### Section: Appearance

| ID | Type | State binding | Purpose |
|---|---|---|---|
| `appearance_header` | section_header | content, clear_confirm | Section label separating appearance controls from other setting groups |
| `appearance_list` | list | content, clear_confirm | Container for appearance preference rows |
| `theme_row` | list_item — child of appearance_list | content, clear_confirm | Displays current theme from DataStore (`{settings.theme}`); hosts theme picker |
| `theme_dropdown` | select (trailing_content of theme_row) | content, clear_confirm | Picker for app colour theme (Light / Dark / System); persists to DataStore atomically; dynamic theme applies on next recomposition |

**theme_dropdown action contract:**

| Component | Action | Effect | Library refs | Description |
|---|---|---|---|---|
| `theme_dropdown` | `update_theme` | persist_db | `androidx.datastore` | Writes the selected theme key to DataStore atomically; `AppTheme` reacts via `collectAsStateWithLifecycle` on next recomposition. |

---

### Section: Security

| ID | Type | State binding | Purpose |
|---|---|---|---|
| `security_header` | section_header | content, clear_confirm | Section label separating security preference controls |
| `security_list` | list | content, clear_confirm | Container for security preference rows |
| `biometric_row` | list_item — child of security_list | content, clear_confirm | Hosts biometric lock toggle; shows informational dialog when no biometrics enrolled |
| `biometric_switch` | switch (trailing_content of biometric_row) | content, clear_confirm | Boolean toggle for biometric gate on app open; value: `{settings.biometric_lock_enabled}` |
| `session_timeout_row` | list_item — child of security_list | content, clear_confirm | Displays current session timeout from DataStore (`{settings.session_timeout}`); hosts picker |
| `session_dropdown` | select (trailing_content of session_timeout_row) | content, clear_confirm | Picker for inactivity session-timeout (2 / 5 / 10 / 30 minutes); only whitelisted options accepted |

**biometric_switch action contract:**

| Component | Action | Effect | Library refs | Description |
|---|---|---|---|---|
| `biometric_switch` | `toggle_biometric_lock` | persist_db | `androidx.datastore` | Flips `biometric_lock_enabled` boolean in DataStore; checks `BiometricManager` availability first — skips the write and emits `BiometricUnavailable` if no hardware or enrollment is present. |

**session_dropdown action contract:**

| Component | Action | Effect | Library refs | Description |
|---|---|---|---|---|
| `session_dropdown` | `update_session_timeout` | persist_db | `androidx.datastore` | Writes `session_timeout` key to DataStore; value must be one of `[2 minutes, 5 minutes, 10 minutes, 30 minutes]`. |

---

### Section: Permissions

| ID | Type | State binding | Purpose |
|---|---|---|---|
| `permissions_header` | section_header | content, clear_confirm | Section label for app runtime-permission visibility rows (GPS location for ATM distance sort) |
| `permissions_list` | list | content, clear_confirm | Container for runtime permission info rows |
| `location_permission_row` | info_row (icon=location_on, trailing=open_in_new) — child of permissions_list | content, clear_confirm | Displays GPS permission state (`granted` / `denied` / `not_asked`) from `{runtime.gps_permission_state}`; tapping opens OS app-settings deep-link |

**location_permission_row action contract:**

| Component | Action | Effect | Library refs | Description |
|---|---|---|---|---|
| `location_permission_row` | `open_app_system_settings` | share_external | platform-intent/openURL | Fires a platform intent to the OS app-settings screen so the user can grant or revoke GPS permission; no DataStore write occurs. |

---

### Section: Notifications

| ID | Type | State binding | Purpose |
|---|---|---|---|
| `notifications_header` | section_header | content, clear_confirm | Section label separating notification toggle controls |
| `notifications_list` | list | content, clear_confirm | Container for notification toggle rows |
| `consent_expiry_notif_row` | list_item — child of notifications_list | content, clear_confirm | Toggle for consent-expiry reminders; ensures PSU is alerted before Open Banking consent lapses |
| `consent_expiry_switch` | switch (trailing_content of consent_expiry_notif_row) | content, clear_confirm | Persists `notify_consent_expiry` flag to DataStore; value: `{settings.notify_consent_expiry}` |
| `security_alerts_notif_row` | list_item — child of notifications_list | content, clear_confirm | Toggle for security-alert notifications; regulated banking security-visibility requirement |
| `security_alerts_switch` | switch (trailing_content of security_alerts_notif_row) | content, clear_confirm | Persists `notify_security_alerts` flag to DataStore; value: `{settings.notify_security_alerts}` |

**consent_expiry_switch action contract:**

| Component | Action | Effect | Library refs | Description |
|---|---|---|---|---|
| `consent_expiry_switch` | `toggle_consent_expiry_notification` | persist_db | `androidx.datastore` | Flips `notify_consent_expiry` boolean in DataStore; the background notification scheduler reads this flag to decide whether to post consent-expiry alert notifications. |

**security_alerts_switch action contract:**

| Component | Action | Effect | Library refs | Description |
|---|---|---|---|---|
| `security_alerts_switch` | `toggle_security_alerts_notification` | persist_db | `androidx.datastore` | Flips `notify_security_alerts` boolean in DataStore; the FCM message handler reads this flag to decide whether to display security-event push notifications. |

---

### Section: Storage

| ID | Type | State binding | Purpose |
|---|---|---|---|
| `storage_header` | section_header | content, clear_confirm | Section label for on-device data storage visibility and PFM cache management |
| `storage_list` | list | content, clear_confirm | Container for PFM cache location info row and granular clear-cache action |
| `pfm_storage_location_row` | info_row (icon=storage) — child of storage_list | content, clear_confirm | Displays on-device file path of the PFM Room/SQLDelight cache (`{platform.app_files_dir}/databases/pfm_cache`); satisfies CC1 for pfm-dashboard and spending-by-category; read-only display row — no tap target |
| `clear_pfm_cache_row` | list_item (icon=cleaning_services, trailing=chevron_right) — child of storage_list | content, clear_confirm | Triggers clearing of the PFM Room/SQLDelight cache (pfm_room_cache); does NOT clear AIS consent, DataStore settings, or the budgets DataStore; confirmation bottom-sheet shown before execution |

**clear_pfm_cache_row action contract:**

| Component | Action | Effect | Library refs | Description |
|---|---|---|---|---|
| `clear_pfm_cache_row` | `clear_pfm_cache` | delete | `room` | Clears all PFM aggregated spending and category rows from the local PFM Room cache at `databases/pfm_cache` after user confirmation; DataStore settings and Open Banking AIS consents are unaffected. |

---

### Section: Account

| ID | Type | State binding | Purpose |
|---|---|---|---|
| `account_header` | section_header | content, clear_confirm | Section label for account management and data-control navigation rows |
| `account_links_list` | list | content, clear_confirm | Container for account-management navigation rows and destructive data-erasure action |
| `manage_consents_row` | list_item (icon=policy, trailing=chevron_right) — child of account_links_list | content, clear_confirm | Navigation entry to consent-list to view and revoke Open Banking account-access consents |
| `profile_row` | list_item (icon=account_circle, trailing=chevron_right) — child of account_links_list | content, clear_confirm | Navigation entry to profile screen |
| `clear_local_data_row` | list_item (icon=delete_sweep, trailing=chevron_right) — child of account_links_list | content, clear_confirm | Triggers destructive-action bottom-sheet before erasing locally cached account and transaction data; GDPR right-to-erasure for local cache; Open Banking consent authorisations NOT affected |

**manage_consents_row action contract:**

| Component | Action | Effect | Library refs | Description |
|---|---|---|---|---|
| `manage_consents_row` | `navigate_consent_list` | navigate | — | Navigates to the consent-list screen where the user can view and revoke active Open Banking account-access consents. |

**profile_row action contract:**

| Component | Action | Effect | Library refs | Description |
|---|---|---|---|---|
| `profile_row` | `navigate_profile` | navigate | — | Navigates to the profile screen displaying the account holder's identity details from the Open Banking party endpoint. |

**clear_local_data_row action contract:**

| Component | Action | Effect | Library refs | Description |
|---|---|---|---|---|
| `clear_local_data_row` | `clear_local_data_confirm` | transform_state | `kotlinx-coroutines` | Emits ShowClearDataConfirmation to transition the screen to `clear_confirm` state and open the destructive-action bottom-sheet; no database or DataStore writes occur at this stage. |

---

### Section: About & Legal

| ID | Type | State binding | Purpose |
|---|---|---|---|
| `about_header` | section_header | content, clear_confirm | Section label separating legal and informational rows |
| `about_list` | list | content, clear_confirm | Container for legal navigation rows and static version display |
| `terms_row` | list_item (icon=article, trailing=open_in_new) — child of about_list | content, clear_confirm | Opens OBIE ToS URL in system browser |
| `privacy_row` | list_item (icon=privacy_tip, trailing=open_in_new) — child of about_list | content, clear_confirm | Opens OBIE Privacy Policy URL in system browser |
| `licences_row` | list_item (icon=info_outline, trailing=chevron_right) — child of about_list | content, clear_confirm | Opens in-app OSS licences destination via AboutLibraries |
| `app_version_row` | list_item — child of about_list | content, clear_confirm | Displays build version string from `BuildConfig.VERSION_NAME` + `VERSION_CODE`; no tap target |

**terms_row action contract:**

| Component | Action | Effect | Library refs | URL |
|---|---|---|---|---|
| `terms_row` | `open_external_url` | share_external | `platform-intent/openURL` | `https://www.openbanking.org.uk/customer-hub/terms-and-conditions/` |

Note: Hands the URL to the platform browser launcher (Android intent / iOS `openURL`). Shows a snackbar when no browser app is installed (`NoBrowserError`).

**privacy_row action contract:**

| Component | Action | Effect | Library refs | URL |
|---|---|---|---|---|
| `privacy_row` | `open_external_url` | share_external | `platform-intent/openURL` | `https://www.openbanking.org.uk/privacy-policy/` |

**licences_row action contract:**

| Component | Action | Effect | Library refs | Description |
|---|---|---|---|---|
| `licences_row` | `open_oss_licences` | share_external | `AboutLibraries` | Launches the in-app Open Source licences screen via the AboutLibraries Compose destination; no DataStore or network interaction. |

---

### State: `clear_confirm` — bottom-sheet

| ID | Type | State binding | Purpose |
|---|---|---|---|
| `clear_local_data_sheet` | bottom_sheet (title + body) | clear_confirm | Destructive-action confirmation bottom-sheet; triggered by `clear_local_data_confirm`; all behind-sheet content rows remain rendered |
| `cancel_clear_local_data_button` | button (variant=text) — child of sheet | clear_confirm | Dismisses the confirmation sheet; returns to content state; no data erased |
| `confirm_clear_local_data_button` | button (variant=filled, color=error) — child of sheet | clear_confirm | Confirms erasure: clears cached account+transaction rows and resets DataStore cached-at timestamps; Open Banking consent authorisations NOT affected |

**cancel_clear_local_data_button action contract:**

| Component | Action | Effect | Library refs | Description |
|---|---|---|---|---|
| `cancel_clear_local_data_button` | `dismiss_clear_local_data` | transform_state | `kotlinx-coroutines` | Dismisses the clear-data confirmation bottom-sheet and transitions the screen back to content state without erasing any local data. |

**confirm_clear_local_data_button action contract:**

| Component | Action | Effect | Library refs | Description |
|---|---|---|---|---|
| `confirm_clear_local_data_button` | `execute_clear_local_data` | delete | `room`, `sqldelight`, `androidx.datastore` | Deletes all cached account and transaction rows from the Room/SQLDelight local database and resets DataStore cached-at timestamps to null so the next dashboard visit refetches; Open Banking consent authorisations are not affected. |

---

### State: `empty`

| ID | Type | State binding | Purpose |
|---|---|---|---|
| `settings_empty_state` | empty_state (variant=neutral, icon=settings) | empty | Shown on first cold start before DataStore emits default preferences; typically transitions to content within one frame |

### State: `error`

| ID | Type | State binding | Purpose |
|---|---|---|---|
| `settings_error_state` | empty_state (variant=error, icon=error_outline) | error | Shown when DataStore read throws an I/O exception (storage corruption, disk full) |
| `settings_error_retry_button` | button (variant=filled) — child of settings_error_state | error | Re-triggers the DataStore preferences Flow collection |

**settings_error_retry_button action contract:**

| Component | Action | Effect | Library refs | Description |
|---|---|---|---|---|
| `settings_error_retry_button` | `retry_load_settings` | transform_state | `kotlinx-coroutines` | Re-triggers the DataStore preferences Flow collection after an I/O failure, transitioning from Error to Loading state; returns to Content on success or back to Error on repeated IOException. |

---

## 5. ViewModel Contract

**ViewModel:** `SettingsViewModel`  
**State class:** `SettingsState`  
**Sealed class:** `SettingsUiState`

### State Fields

| Field | Type | Description |
|---|---|---|
| `uiState` | `SettingsUiState` | Sealed class governing which UI surface is active |
| `settings` | `SettingsPreferences` | Live preferences emitted by DataStore Flow |
| `gpsPermissionState` | `String` | Runtime GPS permission state: `granted` / `denied` / `not_asked` |

### Sealed Class Members

| Member | Description |
|---|---|
| `Loading` | DataStore flow has not yet emitted |
| `Content` | Preferences available; all sections visible |
| `Empty` | First cold start; DataStore default-write in progress (transient) |
| `Error` | DataStore `IOException`; retry available |
| `ClearConfirm` | Bottom-sheet gating destructive cache erasure; underlying content rows remain rendered |

### Error Types

| Type | Severity | Trigger |
|---|---|---|
| `DataStoreIOError` | error | `IOException` reading preferences Flow on mount — shows error state with retry |
| `CacheDeleteError` | error | Room/SQLDelight delete failure in `executeClearLocalData` — shows error snackbar with retry |
| `NoBrowserError` | warning | No browser app for `openExternalUrl` — shows snackbar; no crash |
| `BiometricUnavailableError` | info | No enrolled biometrics for `toggleBiometricLock` — shows informational dialog |

### Actions

| Action | Signature | Side Effects |
|---|---|---|
| `updateTheme` | `suspend fun updateTheme(theme: String)` | Writes `theme` key to DataStore atomically; dynamic theming reacts via `collectAsStateWithLifecycle` in `AppTheme` |
| `toggleBiometricLock` | `suspend fun toggleBiometricLock()` | Flips `biometric_lock_enabled` in DataStore atomically; if no enrolled biometrics detected, emits `BiometricUnavailable` event — no DataStore write |
| `updateSessionTimeout` | `suspend fun updateSessionTimeout(duration: String)` | Writes `session_timeout` key to DataStore; value must be one of `[2 minutes, 5 minutes, 10 minutes, 30 minutes]` |
| `toggleConsentExpiryNotification` | `suspend fun toggleConsentExpiryNotification()` | Persists `notify_consent_expiry` flag to DataStore atomically |
| `toggleSecurityAlertsNotification` | `suspend fun toggleSecurityAlertsNotification()` | Persists `notify_security_alerts` flag to DataStore atomically |
| `navigateConsentList` | `fun navigateConsentList()` | Emits navigation event to consent-list route |
| `navigateProfile` | `fun navigateProfile()` | Emits navigation event to profile route |
| `clearLocalDataConfirm` | `fun clearLocalDataConfirm()` | Emits `ShowClearDataConfirmation` event; transitions screen to `clear_confirm` state |
| `dismissClearLocalData` | `fun dismissClearLocalData()` | Dismisses `clear_local_data_sheet`; screen returns to `content` state; no data erased |
| `executeClearLocalData` | `suspend fun executeClearLocalData()` | Deletes all locally cached account and transaction rows from Room/SQLDelight (transactional delete); resets DataStore cached-at timestamp keys to null only after Room delete succeeds; emits `LocalDataCleared` event; UI shows success snackbar; Open Banking consent authorisations on the server are NOT affected |
| `openExternalUrl` | `fun openExternalUrl(url: String)` | Fires platform intent / `openURL` to system browser; on no browser: shows snackbar (`NoBrowserError`) |
| `openOssLicences` | `fun openOssLicences()` | Emits navigation event to AboutLibraries OSS licences destination |
| `openAppSystemSettings` | `fun openAppSystemSettings()` | Fires platform intent to OS app-settings screen |
| `clearPfmCache` | `suspend fun clearPfmCache()` | Deletes PFM Room cache rows (pfm_room_cache); prompts confirmation before execution |
| `retryLoadSettings` | `fun retryLoadSettings()` | Re-triggers DataStore preferences Flow collection; transitions error → loading |

### DI

- `SettingsDataStore` — `androidx.datastore`; persists all preference keys
- `LocalCacheRepository` — Room/SQLDelight; wipes `pfm_room_cache` on `executeClearLocalData`

---

## 6. Error Cases

| Trigger | Condition | Handling | Severity |
|---|---|---|---|
| `load_settings_on_mount` | DataStore preferences Flow throws `IOException` on initial collection (storage corruption, disk full) | Transition screen to Error state; display `error_outline` icon, title, body, and a Retry button; Retry re-triggers Flow collection (Loading → Content on recovery, or Error again on repeat failure) | error |
| `open_external_url` | No browser app installed on device (`ActivityNotFoundException` on Android) | Show snackbar — URL not opened silently; no crash | warning |
| `toggle_biometric_lock` | Device has no biometric hardware or no enrolled biometrics (`BiometricManager.BIOMETRIC_ERROR_NONE_ENROLLED` / `NO_HARDWARE`) | Emit `BiometricUnavailable` event; Settings screen shows informational AlertDialog; DataStore not written; switch remains Off | info |
| `clear_local_data` | Room/SQLDelight delete transaction fails (`IOException`, disk full) | Show error snackbar with Retry action; DataStore timestamps are NOT reset until Room deletion succeeds (transactional ordering preserved) | error |

---

## 7. Navigation

**Entry:** app_shell bottom nav → More tab (order 4)

| From | To | Trigger |
|---|---|---|
| settings | consent-list | Tap Manage Consents row |
| settings | profile | Tap Profile row |

---

## 8. Test Scenarios

21 scenarios (source: `screens/settings/tests.yaml`)

| ID | Description | State | Priority |
|---|---|---|---|
| TC-SET-001 | Loading skeleton renders before DataStore emits first value | loading | — |
| TC-SET-002 | Settings screen renders all sections with current preference values | content | — |
| TC-SET-003 | Tapping Manage Consents navigates to consent-list | content | — |
| TC-SET-004 | Tapping Profile navigates to profile | content | — |
| TC-SET-005 | Toggling Biometric App Lock persists new value | content | — |
| TC-SET-006 | Selecting Dark theme applies immediately | content | — |
| TC-SET-007 | Toggling Consent Expiry Reminders off persists and survives restart | content | — |
| TC-SET-008 | Clear Local Data shows confirmation bottom-sheet and clears cache on confirm | content | — |
| TC-SET-009 | Biometric toggle gracefully handles unavailable hardware | content | — |
| TC-SET-010 | Session timeout picker accepts only whitelisted durations | content | — |
| TC-SET-011 | Toggling Security Alerts notification off persists and survives restart | content | — |
| TC-SET-012 | Tapping an About & Legal external link opens the correct URL in system browser | content | — |
| TC-SET-013 | Error state renders with Retry button when DataStore throws IOException on mount | error | — |
| TC-SET-014 | Empty state renders transiently before DataStore writes first default preferences | empty | — |
| TC-SET-015 | Tapping Clear Local Data row triggers `clear_local_data_confirm` action and transitions to `clear_confirm` | clear_confirm | high |
| TC-SET-016 | Tapping Cancel in `clear_confirm` bottom-sheet dismisses sheet and returns to content; no data erased | clear_confirm | medium |
| TC-SET-017 | Tapping Confirm in `clear_confirm` bottom-sheet executes cache erasure; consent authorisations unaffected | clear_confirm | high |
| TC-SET-018 | Permissions section renders GPS permission state from runtime | content | medium |
| TC-SET-019 | Location permission row reflects denied state without blocking the screen | content | medium |
| TC-SET-020 | Tapping the location permission row deep-links to OS app settings | content | medium |
| TC-SET-021 | Storage section shows PFM cache location and clears only the PFM cache | content | medium |
