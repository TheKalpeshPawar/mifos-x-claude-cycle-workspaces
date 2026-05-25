# Feature Specification — Connected Apps (Consent Manager)

| Field | Value |
|---|---|
| Feature | consent-manager |
| Name | Connected Apps |
| Flavor | consumer |
| Status | designed |
| Quality Score | 88 |
| Contract Version | 1.1.0 |

---

## Overview

The Connected Apps screen gives consumers full visibility and granular control over which third-party applications hold active PSD2 OAuth consents to access their Open Banking account data. The screen is reachable from Settings via a back-navigable top app bar. Three real consent records are rendered in the enriched design:

- **MoneyManager Pro** — active consent (granted 1 Mar 2026, expires 1 Mar 2027). Scopes: Read Accounts, View Transactions, Check Balances. Blue logo background (#E3F2FD). Revoke Access button (outlined, red).
- **TaxHelper** — active consent (granted 15 Jan 2026, expires 15 Jan 2027). Scopes: View Transactions, Read Accounts. Amber logo background (#FFF3E0). Revoke Access button (outlined, red).
- **BudgetWise** — expired consent (granted 10 Oct 2025, expired 10 Apr 2026). Scope: Check Balances. Green logo background (#E8F5E9). Remove button (text variant, grey).

Revoking an active consent shows an in-screen confirmation dialog overlay (`revoke_confirm` state) before making the DELETE API call. An empty state is shown when no consents exist. A non-recoverable network failure renders the error state with a retry action.

---

## Screens

| Screen ID | Name | Route | Archetype | Scroll |
|---|---|---|---|---|
| consent-manager | Connected Apps | /consent-manager | index_list | vertical |

---

## Components

### Page Header

| ID | Type | Content | Style |
|---|---|---|---|
| consent_title | text | "Connected Apps" | headline_large, #1800B1, bold, px 20, pt 16, pb 6 |
| consent_subtitle | text | "Manage third-party apps that have access to your account data" | body_medium, #666666, px 20, pb 20 |

### Consent Card — MoneyManager Pro (Active)

| ID | Type | Content | Style |
|---|---|---|---|
| consent_moneymanager | box | Card container | #FFFFFF bg, radius 16, elevation 2, px 16, py 16, border #F0F0F0 1px, mx 20, mb 12 |
| moneymanager_header_row | stack | Horizontal row | orientation horizontal, align center, spacing 12, pb 10 |
| moneymanager_logo | image | app_logo_moneymanager | 40×40, radius 10, #E3F2FD bg |
| moneymanager_info | stack | Vertical info group | orientation vertical, flex 1 |
| moneymanager_name | text | "MoneyManager Pro" | title_medium, #111111, semibold |
| moneymanager_dates | text | "Granted 1 Mar 2026 · Expires 1 Mar 2027" | body_small, #888888 |
| moneymanager_active_badge | box | "ACTIVE" | #E8F5E9 bg, radius 10, px 8, py 3, #2E7D32 text, label_small semibold |
| moneymanager_scopes_row | stack | Horizontal scopes | orientation horizontal, spacing 6, pb 12, scroll_horizontal |
| moneymanager_scope_read_accounts | box | "Read Accounts" | #EDE7F6 bg, radius 8, px 8, py 4, #4527A0 text, label_small |
| moneymanager_scope_view_transactions | box | "View Transactions" | #EDE7F6 bg, radius 8, px 8, py 4, #4527A0 text, label_small |
| moneymanager_scope_check_balances | box | "Check Balances" | #EDE7F6 bg, radius 8, px 8, py 4, #4527A0 text, label_small |
| moneymanager_revoke_button | button | "Revoke Access" | outlined, #FF5252 border+text, radius 10, px 14, py 8, label_medium, align_self flex_end |

### Consent Card — TaxHelper (Active)

| ID | Type | Content | Style |
|---|---|---|---|
| consent_taxhelper | box | Card container | #FFFFFF bg, radius 16, elevation 2, px 16, py 16, border #F0F0F0 1px, mx 20, mb 12 |
| taxhelper_header_row | stack | Horizontal row | orientation horizontal, align center, spacing 12, pb 10 |
| taxhelper_logo | image | app_logo_taxhelper | 40×40, radius 10, #FFF3E0 bg |
| taxhelper_info | stack | Vertical info group | orientation vertical, flex 1 |
| taxhelper_name | text | "TaxHelper" | title_medium, #111111, semibold |
| taxhelper_dates | text | "Granted 15 Jan 2026 · Expires 15 Jan 2027" | body_small, #888888 |
| taxhelper_active_badge | box | "ACTIVE" | #E8F5E9 bg, radius 10, px 8, py 3, #2E7D32 text, label_small semibold |
| taxhelper_scopes_row | stack | Horizontal scopes | orientation horizontal, spacing 6, pb 12, scroll_horizontal |
| taxhelper_scope_view_transactions | box | "View Transactions" | #EDE7F6 bg, radius 8, px 8, py 4, #4527A0 text, label_small |
| taxhelper_scope_read_accounts | box | "Read Accounts" | #EDE7F6 bg, radius 8, px 8, py 4, #4527A0 text, label_small |
| taxhelper_revoke_button | button | "Revoke Access" | outlined, #FF5252 border+text, radius 10, px 14, py 8, label_medium, align_self flex_end |

### Consent Card — BudgetWise (Expired)

| ID | Type | Content | Style |
|---|---|---|---|
| consent_budgetwise | box | Card container | #FAFAFA bg, radius 16, elevation 1, px 16, py 16, border #EEEEEE 1px, mx 20, mb 12 |
| budgetwise_header_row | stack | Horizontal row | orientation horizontal, align center, spacing 12, pb 10 |
| budgetwise_logo | image | app_logo_budgetwise | 40×40, radius 10, #E8F5E9 bg |
| budgetwise_info | stack | Vertical info group | orientation vertical, flex 1 |
| budgetwise_name | text | "BudgetWise" | title_medium, #888888 (dimmed), semibold |
| budgetwise_dates | text | "Granted 10 Oct 2025 · Expired 10 Apr 2026" | body_small, #BBBBBB |
| budgetwise_expired_badge | box | "EXPIRED" | #FFF3E0 bg, radius 10, px 8, py 3, #E65100 text, label_small semibold |
| budgetwise_scopes_row | stack | Horizontal scopes | orientation horizontal, spacing 6, pb 12 |
| budgetwise_scope_check_balances | box | "Check Balances" | #F0F0F0 bg, radius 8, px 8, py 4, #9E9E9E text (dimmed), label_small |
| budgetwise_remove_button | button | "Remove" | text variant, #9E9E9E, radius 10, px 14, py 8, label_medium, align_self flex_end |

### Revoke Confirmation Dialog

| ID | Type | Content | Style |
|---|---|---|---|
| revoke_confirm_dialog | box | Dialog container | #FFFFFF bg, radius 24, elevation 8, px 24, py 28, mx 32 |
| revoke_dialog_title | text | "Revoke access?" | title_large, #111111, bold, pb 8 |
| revoke_dialog_body | text | "This will immediately remove this app's access to your account data. You can reconnect it at any time." | body_medium, #555555, pb 24 |
| revoke_dialog_actions | stack | Action row | orientation horizontal, spacing 12, justify flex_end |
| revoke_dialog_cancel_button | button | "Cancel" | text variant, #1800B1, label_large, px 16, py 10 |
| revoke_dialog_confirm_button | button | "Revoke" | filled, #FF5252 bg, #FFFFFF text, label_large, radius 10, px 20, py 10 |

### Empty State

| ID | Type | Content | Style |
|---|---|---|---|
| empty_state_icon | image | ic_link_off | 80×80, align_self center, pb 16, tint #CCCCCC |
| empty_state_title | text | "No apps connected" | title_medium, #444444, semibold, center, pb 8 |
| empty_state_body | text | "Third-party apps you authorise will appear here. Visit your bank's app marketplace to connect apps." | body_medium, #888888, center, px 32 |

---

## States

| ID | Trigger | Visible Components | Notes |
|---|---|---|---|
| loading | Screen enters; API call in flight | consent_title, consent_subtitle | Shows 3 skeleton cards (height 130dp each) |
| populated | API returns non-empty consent list | All 3 consent cards + header | MoneyManager Pro + TaxHelper active; BudgetWise expired |
| content | Alias for populated | — | Backward-compat alias |
| empty | API returns zero consents | consent_title, consent_subtitle, empty_state_icon, empty_state_title, empty_state_body | ic_link_off icon, no list |
| revoke_confirm | User taps Revoke Access on any active card | All populated components + revoke_confirm_dialog group | Scrim overlay #80000000; dialog on top |
| error | Network failure or API error | consent_title, consent_subtitle | cloud_off icon, "Unable to load connected apps", retry button |

---

## State Model

**ViewModel:** `ConsentManagerViewModel`

### State Fields

| Name | Type | Default | Description |
|---|---|---|---|
| consents | List\<ConsentItem\> | emptyList() | Full list of consents returned from API |
| uiState | ConsentManagerUiState | Loading | Drives which state is rendered (Loading, Populated, Empty, Error) |
| revokingConsentId | String? | null | ID of consent currently being revoked (drives loading indicator on card) |
| showRevokeDialog | Boolean | false | Whether the revoke confirmation dialog overlay is shown |
| pendingRevokeConsent | ConsentItem? | null | The consent the user tapped Revoke on; shown in dialog copy |
| error | UiError? | null | Non-null when uiState == Error |

### Error Codes

| Field | Code | Message |
|---|---|---|
| global | LOAD_FAILED | Unable to load connected apps. Please try again. |
| revoke | REVOKE_FAILED | Could not revoke access. Please try again. |

### Events

| Event | Payload | Effect |
|---|---|---|
| ConsentsLoaded | — | Sets consents list, transitions uiState to Populated or Empty |
| RevokeConsentClicked | consentId: String, appName: String | Sets pendingRevokeConsent, showRevokeDialog = true |
| RevokeConsentConfirmed | consentId: String | Calls DELETE API; sets revokingConsentId |
| RevokeConsentCancelled | — | Clears pendingRevokeConsent, showRevokeDialog = false |
| RevokeConsentComplete | consentId: String | Removes consent from list, clears revokingConsentId |
| RemoveExpiredConsentClicked | consentId: String | Calls DELETE API for expired record cleanup |
| RetryLoad | — | Re-issues GET consents API call |
| ConsentInfoOpened | — | Navigates to PSD2 info bottom sheet |

### Actions

`revoke_consent`, `confirm_revoke_consent`, `dismiss_revoke_dialog`, `open_consent_info`, `view_consent_detail`

### DI Dependencies

`ConsentRepository`

---

## Navigation

| From | Action | To | Type | Description |
|---|---|---|---|---|
| top app bar back arrow | navigate_back | settings | pop | Return to settings screen |
| moneymanager_revoke_button / taxhelper_revoke_button | revoke_consent | (same screen — revoke_confirm state) | overlay | Show revoke confirmation dialog |
| revoke_dialog_confirm_button | confirm_revoke_consent | (same screen — populated/empty after refresh) | api+dismiss | Call DELETE consent API, remove from list |
| revoke_dialog_cancel_button | dismiss_revoke_dialog | (same screen — populated state) | dismiss | Close dialog, return to list |
| consent card (tap) | view_consent_detail | (bottom sheet) | bottom sheet | Show full consent detail and scope list |
| top app bar info icon | open_consent_info | (bottom sheet) | bottom sheet | Open PSD2 consent information |

---

## API Endpoints

| Endpoint | Auth | Purpose |
|---|---|---|
| GET /obp/v5.1.0/my/consents | DirectLogin | List all PSD2 consents for the authenticated user |
| DELETE /obp/v5.1.0/my/consents/{consentId} | DirectLogin | Revoke a specific consent by ID |

---

## Design Tokens

| Token | Value | Usage |
|---|---|---|
| primary | #1800B1 | Screen title, Cancel button text |
| surface | #FFFFFF | Active consent card background, dialog background |
| surface_variant | #FAFAFA | Expired consent card background (dimmed) |
| error | #FF5252 | Revoke Access button border + text, Revoke dialog confirm button background |
| success_bg | #E8F5E9 | ACTIVE badge background |
| success_text | #2E7D32 | ACTIVE badge text |
| warning_bg | #FFF3E0 | EXPIRED badge background |
| warning_text | #E65100 | EXPIRED badge text |
| neutral | #9E9E9E | Dimmed expired scope chips, Remove button text |
| scope_chip_bg | #EDE7F6 | Active scope chip background |
| scope_chip_text | #4527A0 | Active scope chip text |
| expired_chip_bg | #F0F0F0 | Expired scope chip background |
| on_surface_medium | #666666 | Subtitle text |
| on_surface_low | #888888 | Date labels on active cards |
| on_surface_lowest | #BBBBBB | Date labels on expired cards |
| scrim | #80000000 | Revoke confirmation dialog overlay scrim |

---

*Generated by /idea export | 2026-05-25*
