# SPEC — Review & Grant Access (Consent Request)

| Field         | Value                        |
|---------------|------------------------------|
| Feature       | consent-request              |
| Flavor        | consumer                     |
| Status        | enriched                     |
| Quality Score | 96                           |
| ViewModel     | ConsentRequestViewModel      |

---

## Overview

The Review & Grant Access screen is the consent-grant step of the OBIE account-access-consent journey. It gives the PSU a full, least-privilege breakdown of every data cluster the app will read from their HSBC account before they commit to granting access. The screen has no top-level data fetch on entry — it renders immediately in the `content` state with static but data-anchored copy.

At the top a scope summary card (`#F0F1E6` fill) shows which accounts are in scope ("all your HSBC accounts") and the consent duration ("Access until: 11 September 2026 (90 days)"), rendered from the `Data.ExpirationDateTime` the app will send. Below it, a white outlined card headed "Read-only data clusters" lists all 10 OBIE permission clusters the app requests. Three clusters carry a "Required" outlined badge (`#44483D` text, `#C5C8BA` border) — Account details (`ReadAccountsDetail`), Balances (`ReadBalances`), and Transactions (`ReadTransactionsDetail`). The remaining seven carry an "Optional" tonal badge (`#CDEDA3` fill, `#102000` text) — Payees (`ReadBeneficiariesDetail`), Standing orders (`ReadStandingOrdersDetail`), Direct debits (`ReadDirectDebits`), Scheduled payments (`ReadScheduledPaymentsDetail`), Account-holder info (`ReadParty`), Product details (`ReadProducts`), and Statements (`ReadStatementsDetail`). Each cluster row has a leading `#4C662B` icon, a body-medium description in `#1A1C16`, and its badge aligned trailing.

A `body_small` expiry note ("This access expires automatically after 90 days. You can disconnect sooner at any time from Settings.") sits below the cluster card. The primary CTA "Grant access" (filled `#4C662B`) POSTs `OBReadConsent1` to `POST /obie/open-banking/v4.0/aisp/account-access-consents`, transitions to the `submitting` state (circular spinner + "Creating your consent…"), and on a 201 `AWAU` response emits `NavigateToBankAuthorize(consentId)` to the bank-authorize-handoff screen. A "Cancel" outlined button (`#4C662B` border) returns to `consent-intro`. A muted footer "You'll approve this at HSBC. We never see your password." closes the screen.

---

## Screens

| ID              | Name                | Route             | Layout | Scroll   |
|-----------------|---------------------|-------------------|--------|----------|
| consent-request | Review & Grant Access | /consent-request | Column | Vertical |

**Shell:** No explicit Top App Bar declared in ui.yaml — standard onboarding continuation shell. No bottom navigation bar.

| Action          | Label                         | Trigger                                             |
|-----------------|-------------------------------|-----------------------------------------------------|
| grant_click     | Grant access                  | POST account-access-consents → navigate to bank-authorize-handoff |
| cancel_click    | Cancel                        | navigate back to consent-intro                      |

---

## Components

| ID                                     | Type             | Description                                                                                                                                   |
|----------------------------------------|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| consent_root                           | stack            | Column, `#F9FAEF` bg, `spacing.lg` padding — root container                                                                                  |
| consent_title                          | text             | "Review what you'll share" — Outfit/headline_medium, `#1A1C16`, heading level 1, `spacing.xs` bottom padding                                  |
| consent_subtitle                       | text             | "This app is asking to read the following information from your HSBC account. Tap Grant access to continue to HSBC's secure sign-in." — Outfit/body_medium, `#44483D`, `spacing.lg` bottom padding |
| consent_scope_card                     | card             | Filled, `#F0F1E6` bg, 12dp radius, `spacing.md` padding, `spacing.md` bottom margin — scope summary (accounts + duration)                    |
| consent_scope_accounts_row             | stack            | Horizontal row, `spacing.xs` vertical padding, center-start alignment — holds icon + text                                                    |
| consent_scope_accounts_icon            | icon             | `account_balance` — 20dp, `#386663`; a11y "Accounts in scope"                                                                               |
| consent_scope_accounts_text            | text             | "Shared with: all your HSBC accounts" — Outfit/body_medium, `#1A1C16`, weight 600, `spacing.sm` start padding                               |
| consent_scope_duration_row             | stack            | Horizontal row, `spacing.xs` vertical padding, center-start alignment — holds icon + text                                                    |
| consent_scope_duration_icon            | icon             | `schedule` — 20dp, `#386663`; a11y "Access duration"                                                                                        |
| consent_scope_duration_text            | text             | "Access until: 11 September 2026 (90 days)" — Outfit/body_medium, `#1A1C16`, weight 600, `spacing.sm` start padding                         |
| consent_clusters_card                  | card             | Outlined, `#FFFFFF` bg, `#C5C8BA` border, 12dp radius, `spacing.md` padding, `spacing.md` bottom margin — holds all 10 cluster rows          |
| consent_clusters_heading               | text             | "Read-only data clusters" — Outfit/title_medium, `#1A1C16`, bold (700), heading level 2, `spacing.sm` bottom padding                        |
| **1. Account details (Required)**      |                  |                                                                                                                                               |
| consent_cluster_accounts               | stack            | Horizontal row, `spacing.sm` vertical padding, center-start; icon + text + badge                                                            |
| consent_cluster_accounts_icon          | icon             | `account_balance_wallet` — 20dp, `#4C662B`; a11y "Account details"                                                                         |
| consent_cluster_accounts_text          | text             | "Account details — your account names, numbers, sort codes and currency" — Outfit/body_medium, `#1A1C16`, `spacing.sm` start padding         |
| consent_cluster_accounts_required      | badge            | "Required" — outlined, `#44483D` text, `#C5C8BA` border, 8dp radius, Outfit/label_small                                                    |
| consent_cluster_divider_1              | divider          | `#E1E4D5`                                                                                                                                    |
| **2. Balances (Required)**             |                  |                                                                                                                                               |
| consent_cluster_balances               | stack            | Horizontal row, `spacing.sm` vertical padding; icon + text + badge                                                                          |
| consent_cluster_balances_icon          | icon             | `savings` — 20dp, `#4C662B`; a11y "Balances"                                                                                               |
| consent_cluster_balances_text          | text             | "Balances — your current and available balance on each account" — Outfit/body_medium, `#1A1C16`                                             |
| consent_cluster_balances_required      | badge            | "Required" — outlined, `#44483D` text, `#C5C8BA` border, 8dp radius, Outfit/label_small                                                    |
| consent_cluster_divider_2              | divider          | `#E1E4D5`                                                                                                                                    |
| **3. Transactions (Required)**         |                  |                                                                                                                                               |
| consent_cluster_transactions           | stack            | Horizontal row, `spacing.sm` vertical padding; icon + text + badge                                                                          |
| consent_cluster_transactions_icon      | icon             | `receipt_long` — 20dp, `#4C662B`; a11y "Transactions"                                                                                      |
| consent_cluster_transactions_text      | text             | "Transactions — incoming and outgoing payments, dates, amounts and merchant details" — Outfit/body_medium, `#1A1C16`                        |
| consent_cluster_transactions_required  | badge            | "Required" — outlined, `#44483D` text, `#C5C8BA` border, 8dp radius, Outfit/label_small                                                    |
| consent_cluster_divider_3              | divider          | `#E1E4D5`                                                                                                                                    |
| **4. Payees (Optional)**               |                  |                                                                                                                                               |
| consent_cluster_beneficiaries          | stack            | Horizontal row, `spacing.sm` vertical padding; icon + text + badge                                                                          |
| consent_cluster_beneficiaries_icon     | icon             | `group` — 20dp, `#4C662B`; a11y "Payees"                                                                                                   |
| consent_cluster_beneficiaries_text     | text             | "Payees — the saved payees you can send money to" — Outfit/body_medium, `#1A1C16`                                                           |
| consent_cluster_beneficiaries_optional | badge            | "Optional" — tonal, `#CDEDA3` fill, `#102000` text, 8dp radius, Outfit/label_small                                                         |
| consent_cluster_divider_4              | divider          | `#E1E4D5`                                                                                                                                    |
| **5. Standing orders (Optional)**      |                  |                                                                                                                                               |
| consent_cluster_standing_orders        | stack            | Horizontal row, `spacing.sm` vertical padding; icon + text + badge                                                                          |
| consent_cluster_standing_orders_icon   | icon             | `event_repeat` — 20dp, `#4C662B`; a11y "Standing orders"                                                                                   |
| consent_cluster_standing_orders_text   | text             | "Standing orders — your scheduled recurring payments and their next due dates" — Outfit/body_medium, `#1A1C16`                              |
| consent_cluster_standing_orders_optional | badge          | "Optional" — tonal, `#CDEDA3` fill, `#102000` text, 8dp radius, Outfit/label_small                                                         |
| consent_cluster_divider_5              | divider          | `#E1E4D5`                                                                                                                                    |
| **6. Direct debits (Optional)**        |                  |                                                                                                                                               |
| consent_cluster_direct_debits          | stack            | Horizontal row, `spacing.sm` vertical padding; icon + text + badge                                                                          |
| consent_cluster_direct_debits_icon     | icon             | `sync_alt` — 20dp, `#4C662B`; a11y "Direct debits"                                                                                         |
| consent_cluster_direct_debits_text     | text             | "Direct debits — the mandates set up on your account and their recent payments" — Outfit/body_medium, `#1A1C16`                             |
| consent_cluster_direct_debits_optional | badge            | "Optional" — tonal, `#CDEDA3` fill, `#102000` text, 8dp radius, Outfit/label_small                                                         |
| consent_cluster_divider_6              | divider          | `#E1E4D5`                                                                                                                                    |
| **7. Scheduled payments (Optional)**   |                  |                                                                                                                                               |
| consent_cluster_scheduled_payments     | stack            | Horizontal row, `spacing.sm` vertical padding; icon + text + badge                                                                          |
| consent_cluster_scheduled_payments_icon | icon            | `event_upcoming` — 20dp, `#4C662B`; a11y "Scheduled payments"                                                                              |
| consent_cluster_scheduled_payments_text | text            | "Scheduled payments — one-off future-dated payments and their dates" — Outfit/body_medium, `#1A1C16`                                        |
| consent_cluster_scheduled_payments_optional | badge       | "Optional" — tonal, `#CDEDA3` fill, `#102000` text, 8dp radius, Outfit/label_small                                                         |
| consent_cluster_divider_7              | divider          | `#E1E4D5`                                                                                                                                    |
| **8. Account-holder info (Optional)**  |                  |                                                                                                                                               |
| consent_cluster_party                  | stack            | Horizontal row, `spacing.sm` vertical padding; icon + text + badge                                                                          |
| consent_cluster_party_icon             | icon             | `contact_page` — 20dp, `#4C662B`; a11y "Account-holder info"                                                                               |
| consent_cluster_party_text             | text             | "Account-holder info — the account holder's name and contact details" — Outfit/body_medium, `#1A1C16`                                       |
| consent_cluster_party_optional         | badge            | "Optional" — tonal, `#CDEDA3` fill, `#102000` text, 8dp radius, Outfit/label_small                                                         |
| consent_cluster_divider_8              | divider          | `#E1E4D5`                                                                                                                                    |
| **9. Product details (Optional)**      |                  |                                                                                                                                               |
| consent_cluster_products               | stack            | Horizontal row, `spacing.sm` vertical padding; icon + text + badge                                                                          |
| consent_cluster_products_icon          | icon             | `inventory_2` — 20dp, `#4C662B`; a11y "Product details"                                                                                    |
| consent_cluster_products_text          | text             | "Product details — the account type, rates and features of your HSBC product" — Outfit/body_medium, `#1A1C16`                              |
| consent_cluster_products_optional      | badge            | "Optional" — tonal, `#CDEDA3` fill, `#102000` text, 8dp radius, Outfit/label_small                                                         |
| consent_cluster_divider_9              | divider          | `#E1E4D5`                                                                                                                                    |
| **10. Statements (Optional)**          |                  |                                                                                                                                               |
| consent_cluster_statements             | stack            | Horizontal row, `spacing.sm` vertical padding; icon + text + badge                                                                          |
| consent_cluster_statements_icon        | icon             | `description` — 20dp, `#4C662B`; a11y "Statements"                                                                                         |
| consent_cluster_statements_text        | text             | "Statements — your account statements and the periods they cover" — Outfit/body_medium, `#1A1C16`                                           |
| consent_cluster_statements_optional    | badge            | "Optional" — tonal, `#CDEDA3` fill, `#102000` text, 8dp radius, Outfit/label_small                                                         |
| consent_expiry_note                    | text             | "This access expires automatically after 90 days. You can disconnect sooner at any time from Settings." — Outfit/body_small, `#44483D`, `spacing.md` bottom padding |
| consent_error_banner                   | card             | Filled, `#FFDAD6` bg, 8dp radius, `spacing.md` padding; visible in `error` state only — holds error icon + message                          |
| consent_error_icon                     | icon             | `error` — 20dp, `#BA1A1A`; a11y role=image                                                                                                 |
| consent_error_message                  | text             | "We couldn't start your connection. Please check your network and try again." — Outfit/body_small, `#410002`, `spacing.sm` start padding     |
| consent_submitting_spinner             | loading_indicator | Circular indeterminate, 32dp, `#4C662B`, centered; a11y "Creating your consent"; visible in `submitting` state |
| consent_submitting_message             | text             | "Creating your consent…" — Outfit/body_medium, `#44483D`, center; visible in `submitting` state                                             |
| consent_empty_icon                     | icon             | `account_balance` — 48dp, `#75796C`, centered; visible in `empty` state                                                                     |
| consent_empty_title                    | text             | "No accounts to share" — Outfit/title_medium, `#1A1C16`, bold, center; visible in `empty` state                                             |
| consent_empty_message                  | text             | "We couldn't find any HSBC accounts to connect. Check that your accounts are open and eligible for Open Banking, then try again." — Outfit/body_medium, `#44483D`, center; visible in `empty` state |
| consent_grant_button                   | button           | "Grant access" — filled, `#4C662B` bg, `#FFFFFF` text, Outfit/label_large, 8dp radius, full width; triggers POST account-access-consents; shows inline spinner when `submitting` |
| consent_cancel_button                  | button           | "Cancel" — outlined, `#4C662B` border + text, Outfit/label_large, 8dp radius, full width; navigates to consent-intro |
| consent_footer                         | text             | "You'll approve this at HSBC. We never see your password." — Outfit/body_small, `#44483D`, centered, `spacing.md` top / `spacing.xl` bottom padding |

---

## States

| ID         | Trigger                                                           | Description                                                                                                         |
|------------|-------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------|
| content    | Screen entry (initial)                                            | Title, subtitle, scope card, all 10 cluster rows, expiry note, Grant button, Cancel button, footer — full review view |
| submitting | `GrantClicked` action while POST is in-flight                     | Spinner + "Creating your consent…" visible; Grant button shows inline loading indicator; all other content hidden    |
| error      | `CreateConsentResultReceive(failure)` — 400/401/403/429/500       | Content layout + error banner (`#FFDAD6`) visible above the Grant button; banner shows mapped error message          |
| empty      | No shareable HSBC accounts found                                  | `account_balance` icon 48dp + "No accounts to share" title + explanatory body + Cancel button — Grant button hidden  |

---

## State Model

**ViewModel:** `ConsentRequestViewModel`
**Screen State Type:** `ConsentRequestUiState`

| Name              | Type                       | Default                        | Note                                                                                       |
|-------------------|----------------------------|--------------------------------|--------------------------------------------------------------------------------------------|
| uiState           | ConsentRequestScreenState  | ConsentRequestScreenState.Content | Content \| Submitting \| Error \| Empty                                                 |
| permissions       | List\<String\>             | DEFAULT_AIS_PERMISSIONS        | All 10 OBIE permission clusters (3 required + 7 optional)                                  |
| expirationDateTime | String?                   | null                           | ISO-8601 expiry; defaults to creation + 90 days                                            |
| consentId         | String?                    | null                           | Populated from `Data.ConsentId` on 201; used as `openbanking_intent_id`                    |
| consentStatus     | String?                    | null                           | `Data.Status` from `OBReadConsentResponse1`; expected `AWAU`                               |
| errorMessage      | String?                    | null                           | Resolved from OB error code on failure                                                     |
| isSubmitting      | Boolean                    | false                          | True while POST is in-flight                                                               |

**Events:**
- `ConsentRequestEvent.NavigateToBankAuthorize(consentId: String)`
- `ConsentRequestEvent.NavigateToConsentIntro`

**Actions:**
- `ConsentRequestAction.GrantClicked`
- `ConsentRequestAction.CancelClicked`
- `ConsentRequestAction.Internal.CreateConsentResultReceive(result)`

**DI Dependencies:** `ObpAuthRepository`

**Errors:**
- `BAD_REQUEST (400)`: "We couldn't start your connection. Please check your network and try again."
- `UNAUTHORIZED (401)`: "We couldn't authorise this connection. Please try again."
- `INVALID_CONSENT_STATUS (403)`: "This connection is no longer valid. Please start again."
- `TOO_MANY_REQUESTS (429)`: "Too many attempts. Please wait a moment and try again."
- `SERVER_ERROR (500)`: "Something went wrong on our end. Please try again in a moment."

---

## Navigation

| From            | Action        | To                    | Type    | Description                                                              |
|-----------------|---------------|-----------------------|---------|--------------------------------------------------------------------------|
| consent-request | grant_success | bank-authorize-handoff | push    | 201 AWAU received — emit `NavigateToBankAuthorize(consentId)`            |
| consent-request | cancel_click  | consent-intro         | pop     | Cancel — return to intro without creating a consent                      |

---

## API Endpoints

| Endpoint                                                    | Auth              | Tag                | Purpose                                                              |
|-------------------------------------------------------------|-------------------|--------------------|----------------------------------------------------------------------|
| POST /obie/open-banking/v4.0/aisp/account-access-consents  | Client Credentials (cc_access_token) | AccountInformation | Register the AIS consent — returns ConsentId + Status AWAU |

---

## Design Tokens

| Token                           | Value             | Usage                                                                                           |
|---------------------------------|-------------------|-------------------------------------------------------------------------------------------------|
| colors.light.primary            | #4C662B           | Cluster row icons; "Grant access" button fill; "Cancel" button border + text                    |
| colors.light.primary_container  | #CDEDA3           | "Optional" badge fill                                                                           |
| colors.light.background         | #F9FAEF           | Screen base                                                                                     |
| colors.light.surface            | #FFFFFF           | Clusters card fill                                                                              |
| colors.light.surface_variant    | #F0F1E6           | Scope summary card fill                                                                         |
| colors.light.on_surface         | #1A1C16           | Page title; cluster description text; scope card text                                           |
| colors.light.on_surface_variant | #44483D           | Subtitle; expiry note; footer; submitting message                                               |
| colors.light.outline            | #C5C8BA           | Clusters card border; "Required" badge border; "Cancel" button border                          |
| colors.light.surface_variant_2  | #E1E4D5           | Dividers between cluster rows                                                                   |
| colors.light.secondary          | #386663           | Scope card icons (`account_balance`, `schedule`)                                                |
| colors.light.error              | #BA1A1A           | Error banner icon                                                                               |
| colors.light.error_container    | #FFDAD6           | Error banner fill                                                                               |
| colors.light.on_error_container | #410002           | Error banner message text                                                                       |
| colors.light.on_primary         | #FFFFFF            | "Grant access" button label                                                                    |
| colors.light.tertiary           | #75796C           | Empty-state `account_balance` icon                                                              |
| colors.custom.optional_on       | #102000           | "Optional" badge text                                                                           |
| typography.headline_medium      | Outfit 28sp / 400 | "Review what you'll share" screen title                                                         |
| typography.title_medium         | Outfit 16sp / 500 | "Read-only data clusters" card heading                                                          |
| typography.body_medium          | Outfit 14sp / 400 | Subtitle; cluster descriptions; scope text; submitting message; empty-state body                |
| typography.body_small           | Outfit 12sp / 400 | Expiry note; error message; footer                                                              |
| typography.label_large          | Outfit 14sp / 500 | "Grant access" and "Cancel" button labels                                                       |
| typography.label_small          | Outfit 11sp / 500 | "Required" and "Optional" badges                                                                |
| radius.md                       | 12dp              | Scope card and clusters card corners                                                            |
| radius.sm                       | 8dp               | "Grant access" button; "Cancel" button; badge corners; error banner                             |

---

_Generated by /idea export | 2026-06-15_
