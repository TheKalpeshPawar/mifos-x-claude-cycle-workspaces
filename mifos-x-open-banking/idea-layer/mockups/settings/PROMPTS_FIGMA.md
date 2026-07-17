# Settings — Figma Design Prompts

> Auto-generated from `screens/settings/ui.yaml`
> Design tokens: `design-tokens.yaml` (Open Banking — Trust Blue, seed #266489)
> Generated: 2026-07-16T00:00:00Z

---

## Canvas Specification

Frame size: 393×852dp (Pixel 5, logical pixels = dp at 2.75× physical density).
All measurements in dp (density-independent pixels). Clip content: on. Auto Layout enabled on all frames.

---

## Design System Summary

### Resolved Colour Palette

| Role | Token | Light Hex | Usage |
|---|---|---|---|
| Primary | `color/primary` | #266489 | Switches ON, active tab, filled buttons, icons active |
| On Primary | `color/onPrimary` | #FFFFFF | Text/icon on primary fills |
| Primary Container | `color/primaryContainer` | #C9E6FF | Permission status chip bg |
| On Primary Container | `color/onPrimaryContainer` | #004B6F | Text on primary container |
| Secondary | `color/secondary` | #50606E | — |
| Surface | `color/surface` | #F7F9FF | Screen background, top app bar |
| Surface Container Low | `color/surfaceContainerLow` | #F1F4F9 | Bottom sheet background |
| Surface Container | `color/surfaceContainer` | #EBEEF3 | Dropdown chip background |
| Surface Variant | `color/surfaceVariant` | #DDE3EA | Skeleton shimmer, dividers |
| On Surface | `color/onSurface` | #181C20 | Primary text, titles |
| On Surface Variant | `color/onSurfaceVariant` | #41474D | Supporting text, icons |
| Outline | `color/outline` | #72787E | Dividers, switch tracks OFF |
| Outline Variant | `color/outlineVariant` | #C1C7CE | Drag handle, subtle borders |
| Error | `color/error` | #BA1A1A | Destructive button fill, error icon |
| On Error | `color/onError` | #FFFFFF | Text on error fills |
| Scrim | `color/scrim` | #000000 | Modal overlay at 32% opacity |

### Type Scale (Roboto)

| Role | Size | Weight | Line Height | Usage |
|---|---|---|---|---|
| titleLarge | 22sp | 400 | 28dp | Top app bar title, bottom sheet title |
| titleMedium | 16sp | 500 | 24dp | Section header prominence (rare) |
| bodyLarge | 16sp | 400 | 24dp | List item primary label |
| bodyMedium | 14sp | 400 | 20dp | Supporting text, body copy |
| bodySmall | 12sp | 400 | 16dp | Secondary info text, version string |
| labelLarge | 14sp | 500 | 20dp | Button labels |
| labelMedium | 12sp | 500 | 16dp | Section header labels (caps) |

### Shape Tokens

Radius: extra_small=4dp · small=8dp · medium=12dp · large=16dp · extra_large=28dp · full=9999dp

---

## Frame: Loading State

Create a frame 393×852dp named "Settings/Loading". Set fill to #F7F9FF (surface).

At the top, place a Material 3 small top app bar at full width and 64dp height. Fill it with #F7F9FF. Inside, centre-align the title text "Settings" using titleLarge 22sp Roboto Regular #181C20. There are no leading or trailing icons on this bar.

Below the top app bar, fill the remaining vertical space with a vertical stack of 8 shimmer skeleton rows. Each skeleton row spans the full width minus 32dp horizontal padding (left 16dp, right 16dp), stands 56dp tall, and has a corner radius of 4dp. Apply the fill colour #DDE3EA (surfaceVariant). Between each row leave a 4dp gap. Animate all rows with a left-to-right shimmer sweep at 1.5 s duration using a gradient from #DDE3EA to #EBEEF3 and back; this represents the DataStore preferences initialising.

At the bottom of the frame, place the bottom navigation bar at full width and 80dp height (including safe area inset). Fill it with #F7F9FF. Show four nav items: Home (icon: home), Accounts (icon: account_balance), Transactions (icon: receipt_long), More (icon: more_horiz). The More item is selected — render its icon and label in #266489. The other three items render in #41474D (onSurfaceVariant). Use labelMedium 12sp 500 for all labels.

Auto Layout the entire frame as vertical, fill width, top-to-bottom.

---

## Frame: Content State

Create a frame 393×852dp named "Settings/Content". Set fill to #F7F9FF.

Place the same top app bar as described in the Loading state at the top.

Below the top app bar, create a scrollable vertical list. Set Auto Layout direction to vertical, padding 16dp on left and right, 8dp at top and 24dp at bottom, item spacing 0dp. Clip content on. The list contains all preference sections as described below.

### Appearance Section

Place a section header row: full width, 40dp height, no fill. Inside, set text "APPEARANCE" using labelMedium 12sp Roboto Medium #41474D, left-aligned with 0dp left offset (inherits container padding). This is the `appearance_header`.

Immediately below, place a list item row: full width, 56dp height, no fill, no corner radius. Auto Layout horizontal, align centre vertical, padding left 0dp right 0dp (inherits container). On the left, place the label "Theme" in bodyLarge 16sp #181C20. On the right, place a dropdown selector chip 120dp wide, 40dp tall, corner radius 4dp, fill #EBEEF3. Inside the chip, place the text "System" in bodyMedium 14sp #181C20 and a downward chevron icon 24dp #41474D. This is the `theme_dropdown` inside `theme_row`.

### Security Section

Place a section header row: "SECURITY" in labelMedium #41474D, 40dp height.

Place a list item row 56dp min height (may grow to two lines). Left side: label "Biometric lock" in bodyLarge #181C20; below it, supporting text "Require fingerprint or face ID on app open" in bodyMedium #41474D. Right side: a toggle switch in the ON state. Draw the switch track as 51dp wide, 28dp tall, corner radius 14dp, fill #266489 (primary). The thumb is a circle 20dp diameter, fill #FFFFFF, positioned to the right side of the track with 4dp inset. This is `biometric_switch` inside `biometric_row`.

Place a second list item row. Left: label "Session timeout" in bodyLarge #181C20; supporting "Auto-lock after inactivity" in bodyMedium #41474D. Right: a dropdown chip 120dp wide, 40dp tall, radius 4dp, fill #EBEEF3, showing "5 min" in bodyMedium #181C20 with a downward chevron. This is `session_dropdown` inside `session_timeout_row`.

### Permissions Section

Place a section header row: "PERMISSIONS" in labelMedium #41474D, 40dp height.

Place an info row 64dp min height. On the far left, a 24dp location_on icon in #266489 within a 40dp touch zone. Next to it, stack two text lines: top "Location" in bodyLarge #181C20; below it "Used for ATM distance sorting" in bodyMedium #41474D. On the right, place a status chip 72dp wide, 24dp tall, corner radius 9999dp, fill #C9E6FF (primaryContainer); inside the chip, text "granted" in labelSmall 11sp #004B6F (onPrimaryContainer). Beyond the chip, place a 24dp open_in_new icon in #41474D inside a 48dp touch zone. This is `location_permission_row`. The entire row is tappable (open_app_system_settings action).

### Notifications Section

Place a section header row: "NOTIFICATIONS" in labelMedium #41474D.

Place a list item row for consent expiry reminders. Left: label "Consent expiry reminders" in bodyLarge #181C20; supporting "Alert before your Open Banking consent expires" in bodyMedium #41474D. Right: toggle switch ON state (same styling as biometric_switch — track #266489, thumb #FFFFFF). This is `consent_expiry_switch` inside `consent_expiry_notif_row`.

Place a list item row for security alerts. Left: label "Security alerts" in bodyLarge #181C20; supporting "Notify for unusual access or login events" in bodyMedium #41474D. Right: toggle switch ON state. This is `security_alerts_switch` inside `security_alerts_notif_row`.

### Storage Section

Place a section header row: "STORAGE" in labelMedium #41474D.

Place an info row 72dp min height for PFM storage location. On the left, a 24dp storage icon in #41474D. Next to it, stack three text lines: "PFM data" in bodyLarge #181C20; "/data/data/org.mifosx.openbanking/files/databases/pfm_cache" in bodySmall 12sp #41474D Roboto Mono (monospace for paths); "Shared by dashboard & spending analysis" in bodySmall #41474D. No trailing icon — this row is display-only. This is `pfm_storage_location_row`.

Place a list item row for Clear PFM cache. On the left, a 24dp cleaning_services icon in #41474D, then "Clear PFM cache" in bodyLarge #181C20; supporting "Remove aggregated spending & category data" in bodyMedium #41474D. On the far right, a 24dp chevron_right icon in #41474D. This is `clear_pfm_cache_row`.

### Account Section

Place a section header row: "ACCOUNT" in labelMedium #41474D.

Place three list item rows, each 56dp min height, each with a leading icon on the left, a primary label and supporting text in the centre, and a 24dp chevron_right icon on the right:

First row (`manage_consents_row`): icon policy #41474D, label "Manage consents" in bodyLarge #181C20, supporting "View and revoke Open Banking access" in bodyMedium #41474D.

Second row (`profile_row`): icon account_circle #41474D, label "Profile" in bodyLarge #181C20, supporting "Account holder identity details" in bodyMedium #41474D.

Third row (`clear_local_data_row`): icon delete_sweep #41474D, label "Clear local data" in bodyLarge #181C20, supporting "Erase cached account and transaction data" in bodyMedium #41474D. The destructive nature of this action does not change the row colour — the confirmation bottom sheet handles the warning.

### About & Legal Section

Place a section header row: "ABOUT & LEGAL" in labelMedium #41474D.

Place four list item rows:

Row 1 (`terms_row`): icon article #41474D, label "Terms of service" in bodyLarge #181C20, trailing open_in_new icon #41474D (indicates external browser launch).

Row 2 (`privacy_row`): icon privacy_tip #41474D, label "Privacy policy" in bodyLarge #181C20, trailing open_in_new #41474D.

Row 3 (`licences_row`): icon info_outline #41474D, label "Open source licences" in bodyLarge #181C20, trailing chevron_right #41474D.

Row 4 (`app_version_row`): no icon, label "Version" in bodyLarge #181C20, trailing text "0.1.0 (build 1)" in bodySmall #41474D. No touch target on this row — it is display-only.

Place the bottom nav bar as described in the Loading state, with the More item selected.

---

## Frame: Empty State

Create a frame 393×852dp named "Settings/Empty". Set fill to #F7F9FF.

Place the top app bar (same as other states) at the top.

In the centre of the remaining space, create a centred vertical stack with Auto Layout, gap 12dp, padding 32dp. Place:

A Material icon "settings" at 48dp×48dp, fill #41474D (onSurfaceVariant).

Below it, place the title text "Settings unavailable" in headlineSmall 24sp Roboto Regular #181C20, centred.

Below that, place body text "Loading your preferences… This should be instant." in bodyMedium 14sp #41474D, centred, max width 280dp. This state appears on first cold start before DataStore emits default preferences — it is typically a single-frame flash.

Place the bottom nav bar at the bottom.

---

## Frame: Error State

Create a frame 393×852dp named "Settings/Error". Set fill to #F7F9FF.

Place the top app bar at the top.

In the centre of the remaining space, create a centred vertical stack, Auto Layout vertical, gap 12dp, padding 32dp. Place:

A Material icon "error_outline" at 48dp×48dp, fill #BA1A1A (error). This icon communicates DataStore I/O failure (storage corruption or disk full).

Below it, place the title "Settings unavailable" in headlineSmall 24sp #181C20, centred.

Below that, body text "Unable to read your preferences. Storage may be full or corrupted." in bodyMedium 14sp #41474D, centred, max width 280dp.

Below that, add a filled button (`settings_error_retry_button`): 140dp wide, 48dp tall, corner radius 9999dp (full pill), fill #266489 (primary). Inside, centre the label "Try again" in labelLarge 14sp Roboto Medium #FFFFFF. Min touch target 48dp height already satisfied.

Place the bottom nav bar at the bottom.

---

## Frame: Clear Confirm State

Create a frame 393×852dp named "Settings/ClearConfirm". This state represents the content state with a modal bottom sheet overlaid.

First, reproduce the Settings/Content frame as the background layer at full opacity.

On top of the content, place a scrim layer spanning the entire 393×852dp frame: fill #000000 at 32% opacity. This dims the settings list to focus attention on the bottom sheet.

Create a modal bottom sheet component anchored to the bottom of the frame. The sheet spans the full width (393dp) and is as tall as its content (approximately 240dp). Apply corner radius 28dp to the top-left and top-right corners only; bottom corners are square. Fill the sheet with #F1F4F9 (surfaceContainerLow). Add a drop shadow: elevation 2 (M3 level 2, approximately 3dp blur, #000000 at 15% opacity).

Inside the bottom sheet, use Auto Layout vertical, padding: top 8dp, left 24dp, right 24dp, bottom 32dp, item spacing 16dp.

At the very top of the sheet, centre a drag handle: 32dp wide, 4dp tall, corner radius 2dp, fill #C1C7CE (outlineVariant).

Below the drag handle, place the sheet title "Erase local data?" in titleLarge 22sp Roboto Regular #181C20.

Below the title, place body text explaining the action: "This will delete all cached account and transaction data from your device. Open Banking authorisations are NOT affected." Use bodyMedium 14sp #41474D. Max width: fill sheet minus 48dp horizontal padding. Allow two-line wrapping.

Below the body, place a horizontal row of two buttons using Auto Layout horizontal, fill width, gap 12dp, justify content space-between.

Left button (`cancel_clear_local_data_button`): variant text, no fill, no border. Label "Cancel" in labelLarge 14sp Roboto Medium #266489. Padding: horizontal 24dp, height 48dp.

Right button (`confirm_clear_local_data_button`): variant filled, fill #BA1A1A (error colour — signals destructive action). Corner radius 9999dp. Label "Erase all" in labelLarge 14sp Roboto Medium #FFFFFF. Width 140dp, height 48dp. On press, apply pressed-state overlay #FFFFFF at 8% opacity on top of #BA1A1A.

Place the bottom nav bar behind the scrim (same z-order as the content).

---

## Auto Layout Specifications

### Top App Bar
Direction: horizontal · Width: fill · Height: 64dp · Padding: horizontal 16dp, vertical 0dp · Alignment: centre vertical · Contains: title text left-aligned.

### Settings List (scrollable container)
Direction: vertical · Width: fill · Height: hug (clips at screen bounds) · Padding: horizontal 16dp, top 8dp, bottom 24dp · Item spacing: 0dp · Overflow: scroll vertical.

### Section Header Row
Direction: horizontal · Width: fill · Height: 40dp · Alignment: centre vertical · Padding: none (inherits container).

### List Item Row
Direction: horizontal · Width: fill · Min-height: 56dp (hug if supporting text wraps) · Alignment: centre vertical · Item spacing: 12dp · Padding: vertical 8dp.

### Info Row (location, pfm storage)
Direction: horizontal · Width: fill · Min-height: 64dp (hug) · Alignment: top (for multi-line) · Item spacing: 12dp · Padding: vertical 12dp.

### Switch Component
Direction: horizontal · Width: 51dp · Height: 28dp · Padding: 4dp (thumb inset) · Alignment: centre vertical.

### Dropdown Chip
Direction: horizontal · Width: 120dp · Height: 40dp · Padding: horizontal 12dp · Item spacing: 4dp · Alignment: centre vertical · Corner radius: 4dp.

### Bottom Sheet Container
Direction: vertical · Width: fill · Height: hug · Padding: top 8dp, horizontal 24dp, bottom 32dp (+ safe area) · Item spacing: 16dp · Corner radius: top 28dp.

### Button Row (bottom sheet)
Direction: horizontal · Width: fill · Item spacing: 12dp · Alignment: centre vertical · Justify: space-between.

---

## Component Variants

### Switch (biometric_switch, consent_expiry_switch, security_alerts_switch)
| Variant | Track Fill | Thumb Fill | Thumb Position |
|---|---|---|---|
| ON / default | #266489 (primary) | #FFFFFF | right, 4dp inset |
| ON / pressed | #004B6F (primaryContainer-dark) | #F7F9FF | right |
| OFF / default | #72787E (outline) | #FFFFFF | left, 4dp inset |
| OFF / pressed | #41474D | #F7F9FF | left |
| disabled | #DDE3EA | #C1C7CE | left |

### Dropdown Chip (theme_dropdown, session_dropdown)
| Variant | Fill | Border | Text Colour |
|---|---|---|---|
| default | #EBEEF3 (surfaceContainer) | none | #181C20 |
| hovered | #E5E8ED (surfaceContainerHigh) | none | #181C20 |
| pressed | #DDE3EA (surfaceVariant) | 1dp #C1C7CE | #181C20 |
| focused | #EBEEF3 | 2dp #266489 | #181C20 |

### List Item Row (tappable)
| Variant | Background | Text Colour |
|---|---|---|
| default | transparent | #181C20 / #41474D |
| hovered | #F1F4F9 @ 50% | #181C20 / #41474D |
| pressed | #DDE3EA @ 80% | #181C20 / #41474D |
| focused | ripple #266489 @ 12% | #181C20 / #41474D |

### Filled Button (confirm_clear_local_data_button)
| Variant | Fill | Label Colour | Shadow |
|---|---|---|---|
| default | #BA1A1A | #FFFFFF | M3 level 0 |
| hovered | #BA1A1A + 8% #FFFFFF (onError) state-layer overlay | #FFFFFF | M3 level 1 |
| pressed | #FFFFFF 8% overlay on #BA1A1A | #FFFFFF | M3 level 0 |
| disabled | #181C20 @ 12% | #181C20 @ 38% | none |

### Filled Button (settings_error_retry_button)
| Variant | Fill | Label Colour |
|---|---|---|
| default | #266489 | #FFFFFF |
| hovered | #266489 + 8% #FFFFFF (onPrimary) state-layer overlay | #FFFFFF |
| pressed | #FFFFFF 8% overlay on #266489 | #FFFFFF |
| disabled | #181C20 @ 12% | #181C20 @ 38% |

---

## Semantic Token → Figma Variable Mapping

| Token Name | Figma Variable Path | Light Value | Usage |
|---|---|---|---|
| primary | color/primary | #266489 | Switch ON, active tab, filled buttons, active icons |
| onPrimary | color/onPrimary | #FFFFFF | Label on primary fill |
| primaryContainer | color/primaryContainer | #C9E6FF | Permission status chip background |
| onPrimaryContainer | color/onPrimaryContainer | #004B6F | Text on primaryContainer |
| surface | color/surface | #F7F9FF | Screen background, top app bar |
| surfaceContainerLow | color/surfaceContainerLow | #F1F4F9 | Bottom sheet fill |
| surfaceContainer | color/surfaceContainer | #EBEEF3 | Dropdown chip fill |
| surfaceVariant | color/surfaceVariant | #DDE3EA | Skeleton shimmer, switch OFF track |
| onSurface | color/onSurface | #181C20 | Primary text, section titles |
| onSurfaceVariant | color/onSurfaceVariant | #41474D | Supporting text, inactive icons |
| outline | color/outline | #72787E | Switch OFF track, dividers |
| outlineVariant | color/outlineVariant | #C1C7CE | Subtle borders, drag handle |
| error | color/error | #BA1A1A | Destructive button fill, error icon |
| onError | color/onError | #FFFFFF | Label on error fill |
| scrim | color/scrim | #000000 | Modal scrim at 32% opacity |
| spacing/screen_padding | spacing/screenPadding | 16dp | Horizontal list padding |
| radius/extra_large | radius/extraLarge | 28dp | Bottom sheet top corners |
| radius/full | radius/full | 9999dp | Buttons, switch track |
| radius/extra_small | radius/extraSmall | 4dp | Dropdown chip, skeleton rows |
| fontFamily/brand | font/brand | Roboto | All text elements |

---

## Prototype Interaction Flow

All tap targets meet the 48dp minimum touch target requirement (WCAG 2.5.5). Interactions are derived from `action_contract` declarations in `screens/settings/ui.yaml`.

On tap of `theme_dropdown` (trailing of theme_row): Open a dropdown menu showing three options — "Light", "Dark", "System default". On selection, invoke `updateTheme(theme)` which writes the chosen value to DataStore atomically. The screen recomposes with the new theme value reflected in `theme_dropdown`. Navigate to: same screen, updated theme applied.

On tap of `biometric_switch`: Invoke `toggleBiometricLock()`. If the device has enrolled biometrics, flip the switch state and write to DataStore. If no biometrics are enrolled or the hardware is absent, present an informational AlertDialog ("Biometric lock unavailable — no enrolled biometrics found on this device") and leave the switch in the OFF state.

On tap of `session_dropdown`: Open a dropdown showing four options — "2 minutes", "5 minutes", "10 minutes", "30 minutes". On selection, invoke `updateSessionTimeout(duration)` writing the value to DataStore.

On tap of `location_permission_row`: Invoke `openAppSystemSettings()` which deep-links to the OS App Settings page for this app (Android: ACTION_APPLICATION_DETAILS_SETTINGS). Navigate to: OS system Settings — exits app context, returns on back press.

On tap of `consent_expiry_switch`: Invoke `toggleConsentExpiryNotification()` which flips the `notify_consent_expiry` flag in DataStore. The background scheduler reads this flag to decide whether to post consent-expiry reminder notifications.

On tap of `security_alerts_switch`: Invoke `toggleSecurityAlertsNotification()` which flips `notify_security_alerts` in DataStore. The FCM message handler reads this flag to gate security-event push notification display.

On tap of `clear_pfm_cache_row`: Invoke `clearPfmCache()` which deletes all aggregated spending and category rows from the Room PFM cache database (`pfm_room_cache`). After completion, show a snackbar "PFM cache cleared". Navigate to: same content state, cache now empty.

On tap of `manage_consents_row`: Invoke `navigateConsentList()`. Navigate to: `consent-list` screen using the app's NavController.

On tap of `profile_row`: Invoke `navigateProfile()`. Navigate to: `profile` screen.

On tap of `clear_local_data_row`: Invoke `clearLocalDataConfirm()` which emits a state transition to `clear_confirm`. The `clear_local_data_sheet` bottom sheet slides up from the bottom. Transition animation: bottom sheet slides in from bottom over 300 ms (M3 medium duration, emphasis easing cubic-bezier(0.2, 0.0, 0, 1.0)). The scrim fades in simultaneously.

On tap of `cancel_clear_local_data_button` (within the sheet): Invoke `dismissClearLocalData()`. The sheet slides back down and the scrim fades out. Navigate to: content state. No data is erased.

On tap of `confirm_clear_local_data_button` ("Erase all"): Invoke `executeClearLocalData()` which (1) deletes all cached account and transaction rows from Room/SQLDelight transactionally, (2) only after successful deletion, resets DataStore cached-at timestamp keys to null. On success, show a snackbar "Local data cleared" and navigate back to the content state. On Room delete failure, show an error snackbar "Could not clear data — try again" with a Retry action. Open Banking consent authorisations on the server are not affected.

On tap of `terms_row`: Invoke `openExternalUrl("https://www.openbanking.org.uk/customer-hub/terms-and-conditions/")`. Navigate to: system browser (Android Custom Tab / iOS SFSafariViewController). If no browser is installed, show a snackbar "No browser found to open link".

On tap of `privacy_row`: Invoke `openExternalUrl("https://www.openbanking.org.uk/privacy-policy/")`. Navigate to: system browser. Same error handling as terms_row.

On tap of `licences_row`: Invoke `openOssLicences()`. Navigate to: the AboutLibraries in-app Compose destination (list of open-source licences for all bundled dependencies).

`app_version_row` has no tap target or interaction. It is a static display row.

On tap of `settings_error_retry_button` (error state only): Invoke `retryLoadSettings()` which re-triggers the DataStore preferences Flow collection. The screen transitions to the Loading state while the Flow re-collects, then to Content on success. On repeated IOException, the screen returns to the Error state.

---

## Accessibility Notes

All interactive list item rows have a minimum touch target height of 48dp as required by WCAG 2.5.5 and Material 3 guidelines. The minimum 48dp dimension is satisfied by the row height or by adding invisible padding above/below.

Switch components (`biometric_switch`, `consent_expiry_switch`, `security_alerts_switch`): provide `contentDescription` as the `accessibility_label` string from `ui.yaml` (e.g. "Biometric lock toggle"). State changes must be announced by TalkBack using a state change announcement ("Biometric lock on" / "Biometric lock off").

`location_permission_row` must announce the current permission state ("Location permission: granted") and the action ("Opens device app settings") in the same TalkBack focus event.

`clear_pfm_cache_row` must use `contentDescription`: "Clear PFM cache — removes aggregated spending and category data" to prevent ambiguity when accessed by assistive technology.

`cancel_clear_local_data_button` and `confirm_clear_local_data_button` must each carry explicit `contentDescription` matching their labels. The bottom sheet itself must set `ModalBottomSheetState` with `semanticsProperties.heading = "Erase local data?"` so TalkBack announces the sheet on appearance.

`settings_error_retry_button` must include `contentDescription`: "Try again — reload settings".

Colour contrast ratios (WCAG AA):
- #181C20 on #F7F9FF: ≥ 15.8:1 (AAA)
- #41474D on #F7F9FF: ≥ 7.4:1 (AAA)
- #FFFFFF on #266489: ≥ 4.6:1 (AA)
- #FFFFFF on #BA1A1A: ≥ 5.1:1 (AA)
- #004B6F on #C9E6FF: ≥ 5.8:1 (AA)

Reduce motion: when `prefers-reduced-motion` (or the system animation scale is 0 on Android), omit the bottom sheet slide-up animation and instead show the sheet at its target position instantly. The shimmer skeleton should also be replaced with a static placeholder when reduced motion is active.

Icon-only interactive targets (`open_in_new` in location_permission_row, `chevron_right` in list rows) must not be treated as separate touch targets — the entire list row is the tappable unit. Do not place a separate click handler on the trailing icon.
