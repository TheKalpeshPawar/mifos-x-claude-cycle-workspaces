# SPEC — Payment Not Completed (Payment Declined)

| Field         | Value                       |
|---------------|-----------------------------|
| Feature       | payment-declined            |
| Flavor        | consumer                    |
| Status        | enriched                    |
| Quality Score | 92                          |
| ViewModel     | PaymentDeclinedViewModel    |

---

## Overview

The Payment Not Completed screen is the terminal error screen for the HSBC Open Banking PISP payment journey. It is reached from `auth-callback` when authorisation does not complete — the PSU declines at HSBC, the consent comes back with Status RJCT, the callback returns an `error` param (e.g. `access_denied`), or the downstream `/domestic-payments` submit is rejected. It is also reached directly from `payment-authorize-handoff` when the user cancels during the handoff error state.

The screen is entirely stateless with respect to network calls — all data (amount, payee, decline reason) arrives as navigation arguments resolved by `auth-callback`. No OBIE API is invoked here. This design replaces the obsolete OBP in-app `sca-challenge` error path: SCA is performed at HSBC during the authorise redirect, and a decline at that stage flows back through the deep-link callback.

The headline is deliberately calm and non-blaming: "Payment not completed". A reassurance line promoted above the explanation makes clear that no money has left the account before the PSU reads any error detail. The attempted amount and payee are shown in a details card (amount in neutral `#1A1C16`, not error red, to reinforce "not charged"). A reasons card lists three common, non-blaming causes. Two navigation CTAs are available: "Try again" pops back to `send-money-confirm` to re-stage the consent and re-authorise; "Back to home" returns to the home dashboard.

Two visual variants are declared: `content` (the calm, primary state for PSU-initiated declines) and `error` (a generic variant for unexpected or technical declines that additionally surfaces a muted technical reference note for support).

---

## Screens

| ID              | Name                  | Route             | Layout | Scroll   |
|-----------------|-----------------------|-------------------|--------|----------|
| payment-declined| Payment Not Completed | (terminal)        | Column | Vertical |

**Shell:** No top app bar. No bottom navigation bar. Terminal screen — back-stack terminated.

**Nav Parameters:**

| Param            | Type    | Required | Default | Description                                                                         |
|------------------|---------|----------|---------|-------------------------------------------------------------------------------------|
| amount           | String  | Yes      | —       | Attempted payment amount, formatted (e.g. £250.00), from PaymentDraft via nav arg   |
| currency         | String  | Yes      | —       | ISO 4217 currency of the attempted payment (e.g. GBP)                              |
| payeeName        | String  | Yes      | —       | Display name of the intended payee (e.g. Jordan Avery)                             |
| payeeBank        | String  | Yes      | —       | Payee institution name (e.g. Barclays Bank UK)                                     |
| reason           | String? | No       | null    | Human-readable decline reason; null hides the reason row                            |
| isUnexpectedError| Boolean | No       | false   | true → renders `error` state variant with the muted technical reference note        |

---

## Components

| ID                     | Type           | Description                                                                                                              |
|------------------------|----------------|--------------------------------------------------------------------------------------------------------------------------|
| declined_root          | stack (column) | #F9FAEF bg; spacing.lg padding; center-aligned both axes                                                                 |
| declined_icon          | icon           | `cancel` — 88dp, #BA1A1A; center; role image; a11y "Payment not completed"                                               |
| declined_title         | text           | "Payment not completed" — Outfit/headline_medium, #1A1C16, bold 700, center                                              |
| declined_assurance     | text           | "Good news: no money has left your account." — Outfit/title_small, #386663, semibold 600, center                         |
| declined_message       | text           | "You didn't finish authorising this payment at HSBC, so it wasn't sent…" — Outfit/body_medium, #44483D, center           |
| declined_details_card  | card (filled)  | #FFFFFF fill; 16dp radius; 1dp #FFDAD6 border; spacing.md padding; groups amount + payee + reason row                    |
| declined_amount_value  | text           | "£250.00" — Outfit/display_small, #1A1C16, bold 700, center (neutral, not error red — signals "not charged")             |
| declined_payee_value   | text           | "To Jordan Avery — Barclays Bank UK" — Outfit/body_large, #44483D, center                                                |
| declined_reason_row    | stack (row)    | `justify: space_between`; visible only when `reason != null`; groups reason label + value                                |
| declined_reason_label  | text           | "Reason" — Outfit/body_medium, #44483D                                                                                   |
| declined_reason_value  | text           | "Authorisation cancelled at HSBC" — Outfit/body_medium, #1A1C16, bold 500, align end; data-driven from nav arg           |
| declined_reasons_card  | card (filled)  | #FFFFFF fill; 16dp radius; spacing.md padding; groups "This can happen if:" heading + 3 reason items                     |
| declined_reasons_heading| text          | "This can happen if:" — Outfit/title_small, #1A1C16, bold 700; role heading level 2                                      |
| declined_reason_one    | text           | "You chose to cancel on the HSBC approval screen" — Outfit/body_medium, #44483D                                          |
| declined_reason_two    | text           | "The approval timed out before it was confirmed" — Outfit/body_medium, #44483D                                           |
| declined_reason_three  | text           | "HSBC couldn't confirm the payment from your account" — Outfit/body_medium, #44483D                                      |
| declined_status_note   | text           | "Reference: access_denied (consent RJCT)" — Outfit/body_small, #44483D, center; visible only in `error` state           |
| declined_try_again_button | button (filled) | "Try again"; #4C662B bg, #FFFFFF text; Outfit/label_large; 12dp radius; match_parent; → send-money-confirm          |
| declined_done_button   | button (text)  | "Back to home"; #386663 text; Outfit/label_large; match_parent; → home                                                   |

---

## States

| ID      | Trigger                                                              | Description                                                                                                                               |
|---------|----------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| content | Default (isUnexpectedError = false) — PSU declined / access_denied  | Full layout: icon, title, assurance, message, details card (amount, payee, reason row when reason != null), reasons card, both CTAs. `declined_status_note` hidden. |
| error   | isUnexpectedError = true — unexpected / technical decline            | Same as `content` plus `declined_status_note` (muted technical reference). Shown when the callback or /domestic-payments submit returns an unexpected error code. |

---

## State Model

**ViewModel:** `PaymentDeclinedViewModel`
**Screen State Type:** `PaymentDeclinedUiState`
**Pattern:** MVI — stateless apart from inbound nav args; no network call; no DI.

| Field            | Type    | Default       | Notes                                                                                          |
|------------------|---------|---------------|------------------------------------------------------------------------------------------------|
| amount           | String  | "£250.00"     | Attempted payment amount (formatted), from PaymentDraft via nav arg                            |
| currency         | String  | "GBP"         | ISO 4217 currency code                                                                         |
| payeeName        | String  | "Jordan Avery"| Display name of the intended payee                                                             |
| payeeBank        | String  | "Barclays Bank UK" | Payee institution name                                                                    |
| reason           | String? | null          | Human-readable decline reason; null → reason row hidden                                        |
| isUnexpectedError| Boolean | false         | true → render `error` state variant with the muted `declined_status_note`                      |

**Events:** `PaymentDeclinedEvent.NavigateToSendMoneyConfirm`, `PaymentDeclinedEvent.NavigateToHome`

**Actions:** `PaymentDeclinedAction.TryAgainClicked`, `PaymentDeclinedAction.BackToHomeClicked`

**DI:** none — stateless terminal screen.

---

## Navigation

| ID         | From             | To               | Trigger         | Type     | Notes                                                                  |
|------------|------------------|------------------|-----------------|----------|------------------------------------------------------------------------|
| nav_try_again | payment-declined | send-money-confirm | try_again_click | navigate | Re-stage the consent and re-authorise the payment from the confirm step |
| nav_done   | payment-declined | home             | done_click      | navigate | Abandon the payment; return to home dashboard                           |

---

## API Endpoints

(none — this screen performs no network calls; all data arrives via navigation arguments resolved upstream by `auth-callback`)

---

## Design Tokens

| Token                            | Value           | Usage                                                                                 |
|----------------------------------|-----------------|---------------------------------------------------------------------------------------|
| colors.light.error               | #BA1A1A         | `declined_icon` (`cancel`, 88dp)                                                      |
| colors.light.error_container     | #FFDAD6         | `declined_details_card` border colour                                                 |
| colors.light.primary             | #4C662B         | "Try again" filled button background                                                  |
| colors.light.secondary           | #386663         | `declined_assurance` text (#386663 teal/green); "Back to home" text button             |
| colors.light.background          | #F9FAEF         | Screen root background                                                                |
| colors.light.surface             | #FFFFFF         | `declined_details_card` fill; `declined_reasons_card` fill                            |
| colors.light.on_surface          | #1A1C16         | `declined_title` text; `declined_amount_value` text; `declined_reason_value` text; `declined_reasons_heading` text |
| colors.light.on_surface_variant  | #44483D         | `declined_message` body; `declined_payee_value`; `declined_reason_label`; reason list items; `declined_status_note` |
| typography.headline_medium       | Outfit 28sp/400 | `declined_title` — "Payment not completed"                                            |
| typography.display_small         | Outfit 36sp/400 | `declined_amount_value`                                                               |
| typography.title_small           | Outfit 14sp/500 | `declined_assurance`; `declined_reasons_heading`                                      |
| typography.body_large            | Outfit 16sp/400 | `declined_payee_value`                                                                |
| typography.body_medium           | Outfit 14sp/400 | `declined_message`; reason row items                                                  |
| typography.body_small            | Outfit 12sp/400 | `declined_status_note`                                                                |
| typography.label_large           | Outfit 14sp/500 | Button labels                                                                         |
| radius.md                        | 12dp            | "Try again" button corner radius                                                      |
| radius.lg                        | 16dp            | `declined_details_card` + `declined_reasons_card` corner radius                       |
| spacing.lg                       | 24dp            | Root padding; vertical section separation                                             |
| spacing.md                       | 16dp            | Card internal padding                                                                 |
| spacing.sm                       | 8dp             | Reason row top padding; payee bottom padding                                          |
| icon.size.xxl                    | 88dp            | `declined_icon` (`cancel`)                                                            |

---

_Generated by /idea export | 2026-06-14_
