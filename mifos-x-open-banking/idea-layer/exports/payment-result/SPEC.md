# SPEC — Payment Sent

| Field         | Value                     |
|---------------|---------------------------|
| Feature       | payment-result            |
| Flavor        | consumer                  |
| Status        | approved                  |
| Quality Score | 90                        |
| ViewModel     | PaymentResultViewModel    |
| Archetype     | confirmation              |

---

## Overview

The Payment Sent screen is the terminal result view of the OBIE PISP domestic-payment flow (consent → bank authorise → callback → submit `POST /pisp/domestic-payments`). It is opened with the `DomesticPaymentId` returned by the submit response plus instant-paint nav args (amount, currency, beneficiary, source label), then reads `GET /pisp/domestic-payments/{DomesticPaymentId}` on mount to confirm the settlement status. SCA was already performed at the bank during authorise — none happens here.

A green gradient hero card fills the top of the screen with a white check-circle, the headline "Payment sent", a summary line "{amount} to {beneficiary}" (e.g. "£150.00 to James Whitfield"), and a "● COMPLETED" status pill. Below it, a white details card lists the shortened Transaction ID, the source account ("From"), the Charge, and the posted time ("Just now"). "View transaction" opens transaction-detail; "Done" pops back to home. The screen is mobile-only (390px baseline) with no top app bar and no bottom navigation bar — the result is intentionally chrome-free so the success state dominates.

---

## Screens

| ID             | Name         | Route            | Layout | Scroll   |
|----------------|--------------|------------------|--------|----------|
| payment-result | Payment Sent | /payment/result  | Column | Vertical |

**Shell:** No top app bar, no bottom navigation bar. The hero gradient card is the only chrome.

---

## Components

| ID                     | Type    | Description                                                                                                       |
|------------------------|---------|-----------------------------------------------------------------------------------------------------------------|
| hero_card              | card    | Gradient-primary background, white text, 28dp bottom corner radius, 72dp top + 36dp bottom padding, centred — the success hero band |
| success_check          | icon    | 92dp white circle with a `check` glyph tinted `#4C662B` (primary); a11y "Payment confirmed"                       |
| result_title           | text    | "Payment sent" — Outfit/display_small, `#FFFFFF`, weight 700, centre-aligned; a11y role heading                  |
| result_summary         | text    | "£150.00 to James Whitfield" — Outfit/body_large, `#F5FFE6`, centre-aligned; data-driven from amount + beneficiaryName |
| status_pill            | badge   | "● COMPLETED" pill — white fill at 0.18 alpha, white text, `#B6F2C0` dot; maps `Data.Status`                     |
| details_card           | card    | White (`#FFFFFF`) card, 16dp radius, elevation 2, 20dp horizontal + 8dp vertical padding, 16dp margin            |
| transaction_id_row     | stack   | Horizontal, space-between, 14dp vertical padding — "Transaction ID" + shortened DomesticPaymentId                |
| details_divider        | divider | `#E1E4D5`, 1dp — separates the transaction-id row from the rest                                                  |
| from_row               | stack   | Horizontal, space-between, 14dp vertical padding — "From" + source account label                                 |
| charge_row             | stack   | Horizontal, space-between, 14dp vertical padding — "Charge" + summed Data.Charges                                |
| posted_row             | stack   | Horizontal, space-between, 14dp vertical padding — "Posted" + StatusUpdateDateTime (e.g. "Just now")             |
| view_transaction_button| button  | "View transaction" — filled, 12dp radius, full-width, 52dp height; on_click navigate → transaction-detail        |
| done_button            | button  | "Done" — text variant, full-width; on_click navigate → home                                                      |

---

## States

| ID      | Trigger                                            | Description                                                                                                         |
|---------|----------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| content | Default — rendered from nav args, reconciled on mount | Full hero + details card. Initial paint from nav args, then `Data.Status` from the status read maps the pill (ACSP/ACSC → "COMPLETED", RJCT → routes to payment-declined); charge_row sums Data.Charges; transaction_id_row shows the shortened DomesticPaymentId |

> The screen's declared `states` block carries a single `content` state — it is a terminal success view rendered from instant-paint nav args and reconciled against the on-mount read. The Rejected (RJCT) failure path routes to a separate screen (payment-declined), so no in-screen error state is modelled. The retry-poll and navigation events live in data-flow.yaml.

---

## State Model

**ViewModel:** `PaymentResultViewModel`

Terminal result view for the OBIE PISP flow. Opened with the `DomesticPaymentId` from the submit response (`POST /pisp/domestic-payments`) plus instant-paint nav args, then reads `GET /pisp/domestic-payments/{DomesticPaymentId}` on mount to confirm settlement status.

**Nav params:**

| Name              | Type   | Description                                                                                |
|-------------------|--------|--------------------------------------------------------------------------------------------|
| domesticPaymentId | String | `Data.DomesticPaymentId` from the submit POST — drives the status read                      |
| amount            | String | `Data.Initiation.InstructedAmount.Amount` (instant-paint, also confirmed by the read)      |
| currency          | String | `Data.Initiation.InstructedAmount.Currency` (ISO 4217)                                      |
| beneficiaryName   | String | Resolved holder name for `Data.Initiation.CreditorAccount.Name` (counterparty rule applies)|
| fromLabel         | String | Debtor (source) account label — local, not in the OBIE payment response                    |

**Status read fields:** `Data.DomesticPaymentId`, `Data.ConsentId`, `Data.Status`, `Data.StatusUpdateDateTime`, summed `Data.Charges[].Amount`.

**Actions:** `load_status`, `navigate`

**Callbacks:** `onViewTransaction` → transaction-detail; `onDone` → home

**DI Dependencies:** `PaymentsRepository`

---

## Navigation

| From           | To                  | Trigger                          | Type     |
|----------------|---------------------|----------------------------------|----------|
| payment-result | transaction-detail  | view_transaction_button tap      | navigate |
| payment-result | home                | done_button tap                  | navigate |

---

## API Endpoints

| Endpoint                                                                | Method | Auth               | Tag          | Purpose                                  |
|------------------------------------------------------------------------|--------|--------------------|--------------|------------------------------------------|
| /obie/open-banking/v4.0/pisp/domestic-payments/{DomesticPaymentId}     | GET    | Client Credentials | pisp-domestic| Read submitted payment to confirm status |

> This is a client (TPP) contract against the HSBC OBIE sandbox (`backend.owned=false`). The app consumes the ASPSP-hosted endpoint; no owned endpoints are defined for this screen.

---

## Design Tokens

| Token                           | Value           | Usage                                                            |
|---------------------------------|-----------------|-----------------------------------------------------------------|
| colors.light.primary            | #4C662B         | success_check glyph tint, view_transaction_button fill          |
| colors.light.on_primary         | #FFFFFF         | result_title, success_check circle, status_pill text            |
| gradient.primary                | earth-green     | hero_card background                                             |
| colors.light.surface            | #FFFFFF         | details_card background, success_check circle                   |
| colors.light.on_surface         | #1A1C16         | details-row value text                                          |
| colors.light.on_surface_variant | #44483D         | details-row label text                                          |
| colors.light.surface_variant    | #E1E4D5         | details_divider colour                                          |
| typography.display_small        | Outfit 36sp/700 | result_title                                                    |
| typography.body_large           | Outfit 16sp/400 | result_summary                                                  |
| typography.title_large          | Outfit 22sp/400 | view_transaction_button label                                   |
| radius.lg                       | 16dp            | details_card corner radius                                      |
| radius.md                       | 12dp            | view_transaction_button corner radius                          |
| elevation.level2                | 3dp             | details_card elevation                                          |

---

_Generated by /idea export | 2026-06-15_
