<!-- source: screens/settings/ui.yaml -->
<!-- source_hash: regenerated-2026-07-14 -->
<!-- generated: 2026-07-14T21:00:00Z -->

# SPEC — settings

_Generated: 2026-07-14 · Source: idea-layer/screens/settings/ui.yaml_

---

## 1. Feature Overview

**Name:** Settings  
**Archetype:** settings  
**Cluster:** settings  
**Status:** enriched → designed  
**Quality score:** 95  

**Description:**  
App settings hub — appearance (theme), security (biometric lock + session timeout), notifications
(consent-expiry reminders, security alerts), account links (Manage Consents, Profile, Clear Local
Data), and About & Legal. Client-only; no external API. `SettingsViewModel` drives a
Loading → Content state machine over a DataStore preferences Flow. The `clear_confirm` state
gates irreversible local-data erasure behind a bottom-sheet (`clear_local_data_sheet`):
`dismiss_clear_local_data` returns to content; `execute_clear_local_data` wipes
Room/SQLDelight cache + DataStore cached-at timestamps. Open Banking consent authorisations
on the server are NOT affected.

**Libraries:**

| Library | Purpose |
|---|---|
| `androidx.datastore:datastore-preferences` | Async persistent key-value store for all settings |
| `com.github.alorma:compose-settings-ui-m3` | Material 3 Compose settings UI components |
| `org.jetbrains.kotlinx:kotlinx-serialization-json` | Serialisation for structured preference types |

---

## 2. Screen Inventory

| Screen | Archetype | Initial state | Shell |
|---|---|---|---|
| settings | settings | loading | Bottom nav visible · Top app bar "Settings" · No FAB |

### 2.1 Component Layout by State

**State: `loading`**

| Component | Type | Description |
|---|---|---|
| `settings_loading_skeleton` | skeleton (variant=list, rows=8) | Full-screen shimmer while DataStore initialises |

**States: `content` / `clear_confirm`** (same layout; sheet overlaid in `clear_confirm`)

_Appearance_

| Component | Type | Description |
|---|---|---|
| `appearance_header` | section_header | "Appearance" section label |
| `theme_row` | list_item | Label + live theme value from StateFlow |
| `theme_dropdown` | dropdown | Light / Dark / System; `on_click: update_theme` |

_Security_

| Component | Type | Description |
|---|---|---|
| `security_header` | section_header | "Security" section label |
| `biometric_row` | list_item | "Biometric Lock" preference |
| `biometric_switch` | switch | Bound to `settings.biometric_lock_enabled`; `on_click: toggle_biometric_lock` |
| `session_timeout_row` | list_item | Live session timeout value from StateFlow |
| `session_dropdown` | dropdown | 2 min / 5 min / 10 min / 30 min; `on_click: update_session_timeout` |

_Notifications_

| Component | Type | Description |
|---|---|---|
| `notifications_header` | section_header | "Notifications" section label |
| `consent_expiry_notif_row` | list_item | OBIE-mandated consent-expiry awareness toggle |
| `consent_expiry_switch` | switch | Bound to `settings.notify_consent_expiry`; `on_click: toggle_consent_expiry_notification` |
| `security_alerts_notif_row` | list_item | Security-alert notification toggle |
| `security_alerts_switch` | switch | Bound to `settings.notify_security_alerts`; `on_click: toggle_security_alerts_notification` |

_Account_

| Component | Type | Description |
|---|---|---|
| `account_header` | section_header | "Account" section label |
| `manage_consents_row` | list_item (icon=policy, trailing=chevron_right) | `on_click: navigate_consent_list → consent-list` |
| `profile_row` | list_item (icon=account_circle, trailing=chevron_right) | `on_click: navigate_profile → profile` |
| `clear_local_data_row` | list_item (icon=delete_sweep, trailing=chevron_right) | GDPR right-to-erasure; `on_click: clear_local_data_confirm` |

_About & Legal_

| Component | Type | Description |
|---|---|---|
| `about_header` | section_header | "About & Legal" section label |
| `terms_row` | list_item (icon=article, trailing=open_in_new) | Opens OBIE ToS in system browser |
| `privacy_row` | list_item (icon=privacy_tip, trailing=open_in_new) | Opens OBIE Privacy Policy in system browser |
| `licences_row` | list_item (icon=info_outline, trailing=chevron_right) | Opens AboutLibraries OSS licences |
| `app_version_row` | list_item | `settings.app_version` from BuildConfig; no tap target |

**State: `clear_confirm`** — overlay on top of content layout

| Component | Type | Description |
|---|---|---|
| `clear_local_data_sheet` | bottom_sheet | Destructive-action confirmation |
| `cancel_clear_local_data_button` | button (variant=text) | `on_click: dismiss_clear_local_data` → back to `content` |
| `confirm_clear_local_data_button` | button (variant=filled, color=error) | `on_click: execute_clear_local_data` → wipes cache |

**State: `empty`**

| Component | Type | Description |
|---|---|---|
| `settings_empty_state` | empty_state (variant=neutral, icon=settings) | First cold start before DataStore emits defaults |

**State: `error`**

| Component | Type | Description |
|---|---|---|
| `settings_error_state` | empty_state (variant=error, icon=error_outline) | DataStore IOException (disk full / corruption) |
| `settings_error_retry_button` | button (variant=filled) | `on_click: retry_load_settings` |

---

## 3. State Model

**ViewModel:** `SettingsViewModel`

| State | Trigger | Description |
|---|---|---|
| `loading` | Initial composition | DataStore preferences Flow not yet emitted |
| `content` | First Flow emission | Preferences loaded and displayed |
| `empty` | First cold-start | DataStore returns empty before defaults written |
| `error` | IOException | DataStore storage corruption or disk full |
| `clear_confirm` | `clear_local_data_confirm` action | Bottom-sheet visible; gating destructive erasure |

**State fields:**

| Field | Type | Description |
|---|---|---|
| `settings.theme` | String | Current theme: Light / Dark / System |
| `settings.biometric_lock_enabled` | Boolean | Biometric gate on app open |
| `settings.session_timeout` | String | Inactivity timeout: 2 / 5 / 10 / 30 min |
| `settings.notify_consent_expiry` | Boolean | Consent-expiry notification flag |
| `settings.notify_security_alerts` | Boolean | Security-alert notification flag |
| `settings.app_version` | String | BuildConfig.VERSION_NAME + VERSION_CODE (read-only) |

**VM Actions:**

| Action | Signature | Side effects |
|---|---|---|
| `updateTheme` | `suspend fun updateTheme(theme: String)` | Writes theme key to DataStore atomically; dynamic theming reacts on next recomposition |
| `toggleBiometricLock` | `suspend fun toggleBiometricLock()` | Flips flag; emits BiometricUnavailable if no enrolled hardware (no DataStore write) |
| `updateSessionTimeout` | `suspend fun updateSessionTimeout(duration: String)` | Writes session_timeout from allowlist [2m, 5m, 10m, 30m] |
| `toggleConsentExpiryNotification` | `suspend fun toggleConsentExpiryNotification()` | Persists notify_consent_expiry flag |
| `toggleSecurityAlertsNotification` | `suspend fun toggleSecurityAlertsNotification()` | Persists notify_security_alerts flag |
| `navigateConsentList` | `fun navigateConsentList()` | Emits nav event → consent-list route |
| `navigateProfile` | `fun navigateProfile()` | Emits nav event → profile route |
| `clearLocalDataConfirm` | `fun clearLocalDataConfirm()` | Transitions state → `clear_confirm`; reveals `clear_local_data_sheet` |
| `dismissClearLocalData` | `fun dismissClearLocalData()` | Dismisses sheet; state → `content`; no data erased |
| `executeClearLocalData` | `suspend fun executeClearLocalData()` | Deletes Room/SQLDelight cache transactionally; resets DataStore cached-at timestamps after Room success; emits LocalDataCleared event; Open Banking consents unaffected |
| `openExternalUrl` | `fun openExternalUrl(url: String)` | Fires platform intent to system browser |
| `openOssLicences` | `fun openOssLicences()` | Emits nav event → AboutLibraries destination |
| `retryLoadSettings` | `fun retryLoadSettings()` | Re-triggers DataStore Flow collection; loading → content on success |

**Error cases:**

| Trigger | Condition | Handling | Severity |
|---|---|---|---|
| `load_settings_on_mount` | DataStore Flow throws IOException | Transition to error state; Retry button re-triggers collection | error |
| `open_external_url` | No browser installed (ActivityNotFoundException) | Snackbar shown; no crash | warning |
| `toggle_biometric_lock` | No enrolled biometrics / no hardware | Emit BiometricUnavailable; informational AlertDialog; switch stays Off | info |
| `clear_local_data` | Room delete transaction fails (IOException, disk full) | Error snackbar with Retry; DataStore timestamps NOT reset until Room succeeds | error |

---

## 4. Navigation

| Entry | Source | Trigger |
|---|---|---|
| → settings | bottom_nav (More tab, order 4) | Tap More in bottom navigation |

| From | To | Trigger |
|---|---|---|
| settings | consent-list | Tap Manage Consents row |
| settings | profile | Tap Profile row |
| settings | system browser | Tap Terms or Privacy row |
| settings | AboutLibraries | Tap OSS Licences row |
| settings (clear_confirm) | settings (content) | Dismiss or Execute via bottom-sheet |

---

## 5. API Dependencies

**Client-only feature — no server API.**

All persistence is via `androidx.datastore:datastore-preferences` (local key-value store).
Open Banking consent authorisations reside on the OBIE server and are NOT modified by any
settings action. `clear_local_data` deletes only the locally cached account and transaction
rows from Room/SQLDelight and resets DataStore cached-at timestamps.

---

## 6. Design Tokens

Design system: **Open Banking — Trust Blue** (Material 3, seed `#266489`, aesthetic: minimalist-ui)

| Token | Value | Usage in this feature |
|---|---|---|
| `colors.primary` | `#266489` | Filled confirm button, active nav indicator |
| `colors.error` | `#BA1A1A` | Confirm-clear button (`color=error`), error state icon |
| `colors.surface` | `#F7F9FF` | List item backgrounds |
| `colors.surface_container` | `#EBEEF3` | Bottom-sheet background |
| `colors.on_surface` | `#181C20` | List item primary labels |
| `colors.on_surface_variant` | `#41474D` | Supporting text, section headers |
| `colors.outline` | `#72787E` | Dividers between sections |
| `typography.titleMedium` | 16sp / 500 | List item labels |
| `typography.bodyMedium` | 14sp / 400 | Supporting text |
| `typography.labelMedium` | 12sp / 500 | Section header labels |
| `spacing.screen_padding` | 16dp | Horizontal screen padding |
| `rounded.full` | 9999dp | Filled button radius |
| `motion.durations.medium` | 300ms | Bottom-sheet enter / exit animation |
| `accessibility.min_touch_target_dp` | 48dp | All interactive rows and switches |
