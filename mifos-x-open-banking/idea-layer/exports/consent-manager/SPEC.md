# SPEC — Connected Apps

| Field         | Value                      |
|---------------|----------------------------|
| Feature       | consent-manager            |
| Flavor        | consumer                   |
| Status        | approved                   |
| Quality Score | 95                         |
| ViewModel     | ConsentManagerViewModel    |

---

## Overview

The Connected Apps screen gives consumers full visibility and control over all PSD2 open banking consents they have granted to third-party applications. It lists each connected app as a card with the app name, grant/expiry dates, current status badge (ACTIVE or EXPIRED), and the set of data-access scopes (e.g. Read Accounts, View Transactions, Check Balances). Active apps have a red "Revoke Access" outlined button; expired apps have a grey "Remove" text button. Tapping "Revoke Access" transitions to a `revoke_confirm` overlay state showing a confirmation dialog with "Cancel" and "Revoke" actions before the destructive DELETE API call is made. The screen has no bottom navigation bar — it is reached from the Settings/More flow and exits via the back arrow.

The current dataset includes three apps: MoneyManager Pro (active, Read Accounts + View Transactions + Check Balances), TaxHelper (active, View Transactions + Read Accounts), and BudgetWise (expired, Check Balances).

---

## Screens

| ID              | Name           | Route             | Layout | Scroll   |
|-----------------|----------------|-------------------|--------|----------|
| consent-manager | Connected Apps | /consent-manager  | Column | Vertical |

**Shell:** Top app bar ("Connected Apps", back arrow → settings, info action button). No bottom navigation bar.

---

## Components

| ID                              | Type    | Description                                                                                           |
|---------------------------------|---------|-------------------------------------------------------------------------------------------------------|
| consent_title                   | text    | "Connected Apps" — `headline_large`, color `#4C662B`, bold; 16dp horizontal padding                  |
| consent_subtitle                | text    | "Manage third-party apps that have access to your account data" — `body_medium`, color `#44483D`      |
| consent_moneymanager            | box     | White card (`#FFFFFF`), 16dp radius, 16dp padding, `#F9FAEF` border; MoneyManager Pro active consent  |
| moneymanager_logo               | image   | App logo 40×40dp, 10dp radius, `#DCE7C8` background                                                  |
| moneymanager_name               | text    | "MoneyManager Pro" — `title_medium`, `#1A1C16`, semibold                                             |
| moneymanager_dates              | text    | "Granted 1 Mar 2026 · Expires 1 Mar 2027" — `body_small`, `#44483D`                                 |
| moneymanager_active_badge       | box     | "ACTIVE" chip — bg `#CDEDA3`, text `#4C662B`, 10dp radius, `label_small`                             |
| moneymanager_scope_read_accounts | box   | "Read Accounts" scope chip — bg `#CDEDA3`, text `#4C662B`, 8dp radius, `label_small`                 |
| moneymanager_scope_view_transactions | box | "View Transactions" scope chip — bg `#CDEDA3`, text `#4C662B`                                     |
| moneymanager_scope_check_balances | box  | "Check Balances" scope chip — bg `#CDEDA3`, text `#4C662B`                                           |
| moneymanager_revoke_button      | button  | "Revoke Access" — outlined, border `#BA1A1A`, text `#BA1A1A`, `label_medium`, 10dp radius            |
| consent_taxhelper               | box     | White card; TaxHelper active consent                                                                  |
| taxhelper_logo                  | image   | TaxHelper logo 40×40dp, 10dp radius, `#CDEDA3` background                                            |
| taxhelper_name                  | text    | "TaxHelper" — `title_medium`, `#1A1C16`, semibold                                                    |
| taxhelper_dates                 | text    | "Granted 15 Jan 2026 · Expires 15 Jan 2027" — `body_small`, `#44483D`                               |
| taxhelper_active_badge          | box     | "ACTIVE" chip — bg `#CDEDA3`, text `#4C662B`                                                         |
| taxhelper_scope_view_transactions | box  | "View Transactions" scope chip                                                                        |
| taxhelper_scope_read_accounts   | box     | "Read Accounts" scope chip                                                                            |
| taxhelper_revoke_button         | button  | "Revoke Access" — outlined, border `#BA1A1A`, text `#BA1A1A`                                         |
| consent_budgetwise              | box     | `#F9FAEF` card (expired — lighter), `#E1E4D5` border; BudgetWise expired consent                     |
| budgetwise_logo                 | image   | BudgetWise logo 40×40dp, 10dp radius, `#CDEDA3` background                                           |
| budgetwise_name                 | text    | "BudgetWise" — `title_medium`, `#44483D`, semibold (muted to signal expiry)                          |
| budgetwise_dates                | text    | "Granted 10 Oct 2025 · Expired 10 Apr 2026" — `body_small`, `#44483D`                               |
| budgetwise_expired_badge        | box     | "EXPIRED" chip — bg `#CDEDA3`, text `#44483D` (7.25:1 contrast pass), 10dp radius                   |
| budgetwise_scope_check_balances | box     | "Check Balances" scope chip — bg `#F9FAEF`, text `#44483D` (expired styling)                         |
| budgetwise_remove_button        | button  | "Remove" — text variant, `#44483D`, `label_medium`                                                   |
| revoke_confirm_dialog           | box     | White dialog, 24dp radius, elevation 8; visible in `revoke_confirm` state overlay                    |
| revoke_dialog_title             | text    | "Revoke access?" — `title_large`, `#1A1C16`, bold                                                    |
| revoke_dialog_body              | text    | "This will immediately remove this app's access to your account data. You can reconnect it at any time." — `body_medium`, `#44483D` |
| revoke_dialog_cancel_button     | button  | "Cancel" — text, color `#4C662B`; dismisses dialog, returns to `populated`                           |
| revoke_dialog_confirm_button    | button  | "Revoke" — filled, bg `#BA1A1A`, white text; calls DELETE consent API                               |
| empty_state_icon                | image   | `ic_link_off` 80×80dp, tint `#E1E4D5`                                                                |
| empty_state_title               | text    | "No apps connected" — `title_medium`, `#44483D`, semibold, centered                                  |
| empty_state_body                | text    | "Third-party apps you authorise will appear here. Visit your bank's app marketplace to connect apps." — `body_medium`, `#44483D`, centered |

---

## States

| ID             | Trigger                                     | Description                                                                          |
|----------------|---------------------------------------------|--------------------------------------------------------------------------------------|
| loading        | Screen entry                                | Title + subtitle visible; 3 skeleton cards (130dp each) with shimmer animation       |
| populated      | Consents loaded successfully                | All 3 consent cards visible with full data                                           |
| revoke_confirm | "Revoke Access" tapped                      | Populated list blurred behind scrim; confirmation dialog overlaid                    |
| empty          | No consents returned from API               | Title + subtitle + empty state illustration and copy                                 |
| error          | API failure on load                         | Title + subtitle + error state (cloud_off icon, retry button)                        |

---

## State Model

**ViewModel:** `ConsentManagerViewModel`
**Screen State Type:** `ConsentManagerUiState`

| Name                | Type               | Default          |
|---------------------|--------------------|------------------|
| consents            | List\<ConsentItem\>| `emptyList()`    |
| uiState             | ConsentManagerUiState | `Loading`     |
| revokingConsentId   | String?            | `null`           |
| showRevokeDialog    | Boolean            | `false`          |
| pendingRevokeConsent| ConsentItem?       | `null`           |
| error               | UiError?           | `null`           |

**Events:** `ConsentsLoaded`, `RevokeConsentClicked(consentId, appName)`, `RevokeConsentConfirmed(consentId)`, `RevokeConsentCancelled`, `RevokeConsentComplete(consentId)`, `RemoveExpiredConsentClicked(consentId)`, `RetryLoad`, `ConsentInfoOpened`

**Actions:** `revoke_consent`, `confirm_revoke_consent`, `dismiss_revoke_dialog`, `open_consent_info`, `view_consent_detail`

**DI Dependencies:** `ConsentRepository`

**Errors:**
- `LOAD_FAILED`: "Unable to load connected apps. Please try again."
- `REVOKE_FAILED`: "Could not revoke access. Please try again."

---

## Navigation

| From            | To       | Trigger                              | Type    |
|-----------------|----------|--------------------------------------|---------|
| consent-manager | settings | Back arrow in top app bar            | pop     |
| consent-manager | (dialog) | "Revoke Access" tap → `revoke_confirm` state overlay | state |
| consent-manager | (list)   | "Cancel" in dialog → dismiss overlay | state   |
| consent-manager | (list)   | "Revoke" confirmed → DELETE API → refresh list | state |
| consent-manager | (bottom sheet) | Info icon tap → PSD2 info sheet | modal |

---

## API Endpoints

| Endpoint                                    | Auth        | Tag     | Purpose                                          |
|---------------------------------------------|-------------|---------|--------------------------------------------------|
| GET /obp/v5.1.0/my/consents                 | DirectLogin | Consent | List all PSD2 consents granted by the consumer   |
| DELETE /obp/v5.1.0/my/consents/{consentId}  | DirectLogin | Consent | Revoke a specific PSD2 consent by ID             |

---

## Design Tokens

| Token                          | Value   | Usage                                                          |
|--------------------------------|---------|----------------------------------------------------------------|
| color.light.primary            | #4C662B | Title text, ACTIVE badge text, scope chip text, dialog Cancel button |
| color.light.primary_container  | #CDEDA3 | ACTIVE badge bg, active scope chip bg, logos bg, EXPIRED badge bg |
| color.light.background         | #F9FAEF | Screen background, expired card background                     |
| color.light.surface            | #FFFFFF | Active consent card backgrounds, dialog background             |
| color.light.on_surface_variant | #44483D | Subtitle, dates, EXPIRED badge text, expired card text         |
| color.light.error              | #BA1A1A | "Revoke Access" button border + text, dialog confirm button bg |
| color.light.surface_variant    | #E1E4D5 | Expired card border, empty state icon tint                     |
| typography.headline_large      | —       | "Connected Apps" title                                         |
| typography.title_medium        | —       | App names in consent cards                                     |
| typography.title_large         | —       | Dialog title "Revoke access?"                                  |
| typography.body_medium         | —       | Subtitle, dialog body text                                     |
| typography.body_small          | —       | Grant/expiry dates                                             |
| typography.label_small         | —       | Status badges, scope chips                                     |
| typography.label_medium        | —       | "Revoke Access" / "Remove" button text                         |
| radius.xl                      | 24dp    | Dialog border-radius                                           |
| radius.lg                      | 16dp    | Consent card border-radius                                     |
| radius.sm                      | 8dp     | Scope chip border-radius                                       |

---

_Generated by /idea export | 2026-05-29_
