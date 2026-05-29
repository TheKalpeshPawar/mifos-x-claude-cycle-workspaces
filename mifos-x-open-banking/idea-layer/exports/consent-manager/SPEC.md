# SPEC — Connected Apps (Consent Manager)

| Field         | Value                      |
|---------------|----------------------------|
| Feature       | consent-manager            |
| Flavor        | consumer                   |
| Status        | approved                   |
| Quality Score | 95                         |
| ViewModel     | ConsentManagerViewModel    |

---

## Overview

The Connected Apps screen gives Consumer persona users full visibility and control over the third-party PSD2 apps that have been granted access to their banking data. On screen entry the ViewModel calls `GET /obp/v5.1.0/my/consents` and renders a vertically scrollable list of consent cards. Each card shows the app logo (40×40dp, 10dp radius), name, grant/expiry dates, an ACTIVE or EXPIRED status badge, horizontally scrollable scope chips (Read Accounts, View Transactions, Check Balances), and either a "Revoke Access" outlined-red button (active consents) or a "Remove" text button (expired consents).

The demo dataset contains three apps: **MoneyManager Pro** (Active — granted 1 Mar 2026, expires 1 Mar 2027, scopes: Read Accounts + View Transactions + Check Balances), **TaxHelper** (Active — granted 15 Jan 2026, expires 15 Jan 2027, scopes: View Transactions + Read Accounts), and **BudgetWise** (Expired — granted 10 Oct 2025, expired 10 Apr 2026, scope: Check Balances). The expired BudgetWise card uses `#F9FAEF` fill and a muted `#44483D` text colour to signal visual demotion; its EXPIRED badge uses `#44483D` text on `#CDEDA3` (7.25:1 contrast — WCAG AA pass, corrected from prior `#E8A317` at 1.68:1 — A11Y-002 fix).

Tapping "Revoke Access" fires `RevokeConsentClicked(consentId, appName)` and transitions to the `revoke_confirm` state — an overlay scrim with a confirmation dialog ("Revoke access?") carrying Cancel (text button, `#4C662B`) and Revoke (filled button, `#BA1A1A`). Confirming calls `DELETE /obp/v5.1.0/my/consents/{consentId}` and refreshes the list. An `info_outlined` action icon on the Top App Bar opens a PSD2 information bottom sheet. Back navigation returns to Settings.

---

## Screens

| ID               | Name           | Route             | Layout | Scroll   |
|------------------|----------------|-------------------|--------|----------|
| consent-manager  | Connected Apps | /consent-manager  | Column | Vertical |

**Shell:** Top App Bar — title "Connected Apps", `arrow_back` navigation icon (→ settings), `info_outlined` action icon ("About connected apps"). No bottom navigation bar.

| Action            | Icon            | Label                   | Trigger              |
|-------------------|-----------------|-------------------------|----------------------|
| navigate_back     | arrow_back      | Back                    | navigate to settings |
| open_consent_info | info_outlined   | About connected apps    | open info bottom sheet |

---

## Components

| ID                                    | Type   | Description                                                                                                         |
|---------------------------------------|--------|---------------------------------------------------------------------------------------------------------------------|
| consent_title                         | text   | "Connected Apps" — Outfit/headline_large, #4C662B, bold; 16dp horizontal + 16dp top + 4dp bottom padding           |
| consent_subtitle                      | text   | "Manage third-party apps that have access to your account data" — Outfit/body_medium, #44483D; 16dp horizontal + bottom padding |
| **MoneyManager Pro card**             |        |                                                                                                                     |
| consent_moneymanager                  | box    | #FFFFFF fill, 16dp radius, 2dp elevation, 1dp #F9FAEF border; 16dp padding; 20dp horizontal margin, 12dp bottom margin; tappable → view_consent_detail |
| moneymanager_header_row               | stack  | Horizontal, center-aligned, 12dp spacing, 10dp bottom padding                                                      |
| moneymanager_logo                     | image  | app_logo_moneymanager — 40×40dp, 10dp radius, #DCE7C8 background                                                   |
| moneymanager_info                     | stack  | Vertical, flex:1 — contains name + dates                                                                           |
| moneymanager_name                     | text   | "MoneyManager Pro" — Outfit/title_medium, #1A1C16, semibold                                                        |
| moneymanager_dates                    | text   | "Granted 1 Mar 2026 · Expires 1 Mar 2027" — Outfit/body_small, #44483D                                            |
| moneymanager_active_badge             | box    | "ACTIVE" — #CDEDA3 fill, 10dp radius, 8dp/3dp padding, #4C662B text, Outfit/label_small, semibold                  |
| moneymanager_scopes_row               | stack  | Horizontal, 6dp spacing, 12dp bottom padding, scroll_horizontal                                                    |
| moneymanager_scope_read_accounts      | box    | "Read Accounts" chip — #CDEDA3 fill, 8dp radius, 8dp/4dp padding, #4C662B text, Outfit/label_small                 |
| moneymanager_scope_view_transactions  | box    | "View Transactions" chip — #CDEDA3 fill, 8dp radius, 8dp/4dp padding, #4C662B text, Outfit/label_small             |
| moneymanager_scope_check_balances     | box    | "Check Balances" chip — #CDEDA3 fill, 8dp radius, 8dp/4dp padding, #4C662B text, Outfit/label_small                |
| moneymanager_revoke_button            | button | "Revoke Access" — outlined, #BA1A1A border + text, 10dp radius, 14dp/8dp padding, Outfit/label_medium; align_self flex_end; triggers revoke_consent |
| **TaxHelper card**                    |        |                                                                                                                     |
| consent_taxhelper                     | box    | #FFFFFF fill, 16dp radius, 2dp elevation, 1dp #F9FAEF border; 16dp padding; 20dp horizontal margin, 12dp bottom margin; tappable → view_consent_detail |
| taxhelper_header_row                  | stack  | Horizontal, center-aligned, 12dp spacing, 10dp bottom padding                                                      |
| taxhelper_logo                        | image  | app_logo_taxhelper — 40×40dp, 10dp radius, #CDEDA3 background                                                      |
| taxhelper_info                        | stack  | Vertical, flex:1                                                                                                    |
| taxhelper_name                        | text   | "TaxHelper" — Outfit/title_medium, #1A1C16, semibold                                                               |
| taxhelper_dates                       | text   | "Granted 15 Jan 2026 · Expires 15 Jan 2027" — Outfit/body_small, #44483D                                          |
| taxhelper_active_badge                | box    | "ACTIVE" — #CDEDA3 fill, 10dp radius, 8dp/3dp padding, #4C662B text, Outfit/label_small, semibold                  |
| taxhelper_scopes_row                  | stack  | Horizontal, 6dp spacing, 12dp bottom padding, scroll_horizontal                                                    |
| taxhelper_scope_view_transactions     | box    | "View Transactions" chip — #CDEDA3 fill, 8dp radius, #4C662B text, Outfit/label_small                              |
| taxhelper_scope_read_accounts         | box    | "Read Accounts" chip — #CDEDA3 fill, 8dp radius, #4C662B text, Outfit/label_small                                  |
| taxhelper_revoke_button               | button | "Revoke Access" — outlined, #BA1A1A border + text, 10dp radius; align_self flex_end; triggers revoke_consent       |
| **BudgetWise card (expired)**         |        |                                                                                                                     |
| consent_budgetwise                    | box    | #F9FAEF fill (expired/dimmed), 16dp radius, 1dp elevation, 1dp #E1E4D5 border; 16dp padding; 20dp horizontal margin, 12dp bottom margin; tappable → view_consent_detail |
| budgetwise_header_row                 | stack  | Horizontal, center-aligned, 12dp spacing, 10dp bottom padding                                                      |
| budgetwise_logo                       | image  | app_logo_budgetwise — 40×40dp, 10dp radius, #CDEDA3 background                                                     |
| budgetwise_info                       | stack  | Vertical, flex:1                                                                                                    |
| budgetwise_name                       | text   | "BudgetWise" — Outfit/title_medium, #44483D, semibold (muted — expired)                                            |
| budgetwise_dates                      | text   | "Granted 10 Oct 2025 · Expired 10 Apr 2026" — Outfit/body_small, #44483D                                          |
| budgetwise_expired_badge              | box    | "EXPIRED" — #CDEDA3 fill, 10dp radius, 8dp/3dp padding, #44483D text (7.25:1 — WCAG AA pass; A11Y-002 fix from prior #E8A317 at 1.68:1 FAIL), Outfit/label_small, semibold |
| budgetwise_scopes_row                 | stack  | Horizontal, 6dp spacing, 12dp bottom padding                                                                       |
| budgetwise_scope_check_balances       | box    | "Check Balances" chip — #F9FAEF fill (expired muted), 8dp radius, #44483D text, Outfit/label_small                 |
| budgetwise_remove_button              | button | "Remove" — text variant, #44483D text, 10dp radius; align_self flex_end; triggers revoke_consent                   |
| **Revoke confirmation dialog**        |        |                                                                                                                     |
| revoke_confirm_dialog                 | box    | Overlay modal — #FFFFFF fill, 24dp radius, 8dp elevation, 24dp/28dp padding, 32dp horizontal margin; Escape key → dismiss_revoke_dialog; role: dialog |
| revoke_dialog_title                   | text   | "Revoke access?" — Outfit/title_large, #1A1C16, bold; 8dp bottom padding                                           |
| revoke_dialog_body                    | text   | "This will immediately remove this app's access to your account data. You can reconnect it at any time." — Outfit/body_medium, #44483D; 24dp bottom padding |
| revoke_dialog_actions                 | stack  | Horizontal, 12dp spacing, justify flex_end                                                                         |
| revoke_dialog_cancel_button           | button | "Cancel" — text variant, #4C662B text, Outfit/label_large; triggers dismiss_revoke_dialog                          |
| revoke_dialog_confirm_button          | button | "Revoke" — filled, #BA1A1A fill, #FFFFFF text, 10dp radius, Outfit/label_large; triggers confirm_revoke_consent    |
| **Empty state**                       |        |                                                                                                                     |
| empty_state_icon                      | image  | ic_link_off — 80×80dp, center-aligned, 16dp bottom padding, #E1E4D5 tint; visible in empty state only             |
| empty_state_title                     | text   | "No apps connected" — Outfit/title_medium, #44483D, semibold, center aligned; 8dp bottom padding                   |
| empty_state_body                      | text   | "Third-party apps you authorise will appear here. Visit your bank's app marketplace to connect apps." — Outfit/body_medium, #44483D, center aligned; 32dp horizontal padding |

---

## States

| ID             | Trigger                                              | Description                                                                                                        |
|----------------|------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| loading        | Screen entry / `RetryLoad` event                     | Title + subtitle visible; 3 skeleton consent cards (130dp height, #E1E4D5 fill, 16dp radius) shimmer at 200ms     |
| populated      | `ConsentsLoaded` — non-empty list                    | Full list: MoneyManager Pro (active), TaxHelper (active), BudgetWise (expired); all with badges + scope chips     |
| revoke_confirm | `RevokeConsentClicked(consentId, appName)` event     | Populated list behind overlay scrim (`#BA1A1A00` scrim); confirmation dialog visible; Escape → dismiss; Cancel → dismiss; Revoke → confirm API |
| empty          | `ConsentsLoaded` — empty list                        | Title + subtitle + ic_link_off illustration + "No apps connected" heading + body copy                             |
| error          | Network / auth failure → `LOAD_FAILED`               | Title + subtitle + cloud_off icon (error) + "Unable to load connected apps" + "Check your connection and try again" + Retry button |

---

## State Model

**ViewModel:** `ConsentManagerViewModel`
**Screen State Type:** `ConsentManagerUiState`

| Name                  | Type                     | Default       |
|-----------------------|--------------------------|---------------|
| consents              | List\<ConsentItem\>      | emptyList()   |
| uiState               | ConsentManagerUiState    | Loading       |
| revokingConsentId     | String?                  | null          |
| showRevokeDialog      | Boolean                  | false         |
| pendingRevokeConsent  | ConsentItem?             | null          |
| error                 | UiError?                 | null          |

**Events:**
- `ConsentsLoaded`
- `RevokeConsentClicked(consentId: String, appName: String)`
- `RevokeConsentConfirmed(consentId: String)`
- `RevokeConsentCancelled`
- `RevokeConsentComplete(consentId: String)`
- `RemoveExpiredConsentClicked(consentId: String)`
- `RetryLoad`
- `ConsentInfoOpened`

**Actions:** `revoke_consent`, `confirm_revoke_consent`, `dismiss_revoke_dialog`, `open_consent_info`, `view_consent_detail`

**DI Dependencies:** `ConsentRepository`

**Errors:**
- `LOAD_FAILED`: "Unable to load connected apps. Please try again."
- `REVOKE_FAILED`: "Could not revoke access. Please try again."

---

## Navigation

| From             | Action                  | To          | Type    | Description                                                        |
|------------------|-------------------------|-------------|---------|--------------------------------------------------------------------|
| consent-manager  | navigate_back           | settings    | pop     | Arrow-back tap — return to Settings screen                         |
| consent-manager  | revoke_consent          | (overlay)   | state   | Open revoke_confirm overlay — confirmation dialog appears          |
| consent-manager  | confirm_revoke_consent  | (self)      | refresh | Call DELETE consent API, dismiss dialog, refresh consent list      |
| consent-manager  | dismiss_revoke_dialog   | (self)      | state   | Dismiss dialog (Cancel tap or Escape key), return to populated     |
| consent-manager  | view_consent_detail     | (sheet)     | sheet   | Open bottom sheet with full consent detail and full scope list     |
| consent-manager  | open_consent_info       | (sheet)     | sheet   | Open PSD2 consent information bottom sheet from info icon          |

---

## API Endpoints

| Endpoint                                            | Auth        | Tag     | Purpose                                         |
|-----------------------------------------------------|-------------|---------|-------------------------------------------------|
| GET /obp/v5.1.0/my/consents                        | DirectLogin | Consent | List all PSD2 consents granted by current user  |
| DELETE /obp/v5.1.0/my/consents/{consentId}         | DirectLogin | Consent | Revoke a specific PSD2 consent by ID            |

---

## Design Tokens

| Token                               | Value           | Usage                                                                                      |
|-------------------------------------|-----------------|--------------------------------------------------------------------------------------------|
| colors.light.primary                | #4C662B         | Page title, ACTIVE badge text, active scope chip text, Cancel button text                  |
| colors.light.primary_container      | #CDEDA3         | ACTIVE badge fill, active scope chip fill, MoneyManager logo bg, EXPIRED badge fill        |
| colors.light.nav_active_indicator   | #DCE7C8         | MoneyManager Pro logo background                                                           |
| colors.light.error                  | #BA1A1A         | "Revoke Access" outlined button border + text; Revoke dialog confirm button fill           |
| colors.light.on_error               | #FFFFFF          | Revoke dialog confirm button text                                                         |
| colors.light.background             | #F9FAEF         | Screen base; expired BudgetWise card fill; expired scope chip fill; active card border     |
| colors.light.surface                | #FFFFFF         | Active consent card fill (MoneyManager Pro, TaxHelper); revoke confirm dialog fill         |
| colors.light.surface_variant        | #E1E4D5         | Expired BudgetWise card border; empty-state icon tint; skeleton card fill                  |
| colors.light.on_surface             | #1A1C16         | Active app names; dialog title "Revoke access?"                                            |
| colors.light.on_surface_variant     | #44483D         | Subtitle; grant/expiry date lines; dialog body; expired app name; expired badge text; expired chip text; Remove button; cloud_off icon |
| typography.headline_large           | Outfit 32sp/400 | "Connected Apps" page title                                                                |
| typography.title_large              | Outfit 22sp/400 | Revoke confirm dialog title "Revoke access?"                                               |
| typography.title_medium             | Outfit 16sp/500 | App names on consent cards; empty state heading "No apps connected"                        |
| typography.body_medium              | Outfit 14sp/400 | Page subtitle; dialog body text; empty state body copy                                     |
| typography.body_small               | Outfit 12sp/400 | Grant and expiry date lines on each consent card                                           |
| typography.label_large              | Outfit 14sp/500 | Dialog action buttons (Cancel, Revoke)                                                     |
| typography.label_medium             | Outfit 12sp/500 | "Revoke Access" and "Remove" button labels                                                 |
| typography.label_small              | Outfit 11sp/500 | ACTIVE / EXPIRED status badges; scope chip labels                                          |
| radius.sm                           | 8dp             | Scope chips                                                                                |
| radius.lg                           | 16dp            | Consent card corners (active + expired)                                                    |
| radius.xl                           | 24dp            | Revoke confirm dialog                                                                      |
| elevation.level1                    | 1dp             | Expired BudgetWise card                                                                    |
| elevation.level2                    | 3dp             | Active consent cards (MoneyManager Pro, TaxHelper)                                         |
| elevation.level4                    | 8dp             | Revoke confirm dialog overlay                                                              |
| motion.duration.short4              | 200ms           | Skeleton shimmer cycle duration (loading state)                                            |
| mood_gradients.trust_horizon        | #F0F1E6→#E1E4D5 | Skeleton shimmer base gradient                                                            |

---

_Generated by /idea export | 2026-05-30_
