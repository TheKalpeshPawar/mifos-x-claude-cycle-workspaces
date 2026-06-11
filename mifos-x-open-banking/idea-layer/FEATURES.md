# Features — Mifos X Open Banking

All features organized by capability and HSBC UK/CE Open Banking (OBIE Read/Write v4.0) integration points.
Updated 2026-06-11 — MIGRATION OBP → HSBC: consumer Open Banking TPP (AISP + PISP). Removed the
field-officer persona and OBP-only surfaces (login, cards, fx-rates, in-app SCA); added the consent /
authorise handoff screens and the VRP / CoF / Open Data / Events / International-payment capabilities.

The app is a single-persona consumer product. It owns no backend — every feature consumes the external
HSBC Open Banking REST API over mTLS, gated by consent + redirect-based PSU authorisation (SCA at the bank).

---

## Consent & Authorisation Features

> NEW capability cluster (vs OBP). Replaces OBP's in-app DirectLogin + password screens. The user
> authenticates at HSBC during a redirect; no username, password, or SCA code is ever entered in-app.

| Feature | Screen | API Group | Description |
|---|---|---|---|
| **splash** | splash | — | Consent/token gate — routes to onboarding or Home |
| **consent-intro** | consent-intro | — | Explain data sharing, start "Connect your HSBC account" |
| **consent-request** | consent-request | AISP | Pick permissions, `POST /aisp/account-access-consents` (status AWAU) |
| **bank-authorize-handoff** | bank-authorize-handoff | auth | Build signed authorise request, redirect to HSBC (`GET /oauth2/authorize`, PKCE S256) |
| **auth-callback** | auth-callback | auth | Deep-link return → `POST /oauth2/token` → confirm consent AUTH |
| **consent-declined** | consent-declined | — | PSU declined / callback error recovery |
| **consent-expired** | consent-expired | AISP | Re-consent when prior consent EXPD/RJCT/revoked |
| **consent-manager** | consent-manager | events, AISP | View and revoke active data-sharing consents |

---

## Account Information (AISP) Features

> Read-only. Every read requires a prior AUTH-status account-access-consent + a consent-scoped token.

| Feature | Screen | API Group | Description |
|---|---|---|---|
| **home** | home | AISP | Connected-account overview, balances, recent transactions |
| **accounts** | accounts | AISP | `GET /aisp/accounts` — authorised account list |
| **account-detail** | account-detail | AISP | `GET /aisp/accounts/{AccountId}` + balances |
| **transactions** | transactions | AISP | `GET /aisp/transactions` — history, date filter, search |
| **transaction-detail** | transaction-detail | AISP | Single transaction receipt + metadata |
| **transaction-tags** | transaction-tags | AISP | Tag/categorize transactions for personal tracking (local PFM) |
| **beneficiaries** | beneficiaries | AISP | `GET /aisp/beneficiaries` — read-only payees (no add/edit/delete under OB) |
| **standing-orders** | standing-orders, standing-order-detail | AISP | `GET /aisp/standing-orders` — read-only schedules |
| **direct-debits** | direct-debits, direct-debit-detail | AISP | `GET /aisp/direct-debits` — read-only mandates |
| **products** | products | AISP, Open Data | Product reference + comparison |
| **pfm-dashboard** | pfm-dashboard, pfm-settings | AISP | Spending insights, budgets, category breakdown |
| **business-insights** | business-insights | AISP | Business cashflow insights |

---

## Payments (PISP) Features

> Each payment runs consent → authorise (SCA at bank) → submit → status. International + scheduled +
> standing-order + file/bulk are NEW vs OBP.

| Feature | Screen | API Group | Description |
|---|---|---|---|
| **send-money** | send-money | PISP | Pick payee/account + payment kind (domestic / scheduled / standing-order / international) |
| **send-money-amount** | send-money-amount | PISP, CBPII | Amount entry + Confirmation-of-Funds check against source balance |
| **send-money-confirm** | send-money-confirm | PISP | Review → `POST /pisp/domestic-payment-consents` (AWAU) |
| **payment-authorize-handoff** | payment-authorize-handoff | auth | Build signed authorise request, redirect to HSBC (SCA at bank) |
| **payment-result** | payment-result | PISP | `POST /pisp/domestic-payments` → poll status → terminal |
| **payment-declined** | payment-declined | PISP | PSU declined / consent RJCT recovery |
| **standing-order-create** | standing-order-create | PISP | Author a domestic standing order (`POST /pisp/domestic-standing-order-consents`) |
| **standing-order-edit** | standing-order-edit | PISP | Edit amount/frequency/start-end of a standing order |

---

## Advanced Capabilities (NEW vs OBP)

| Capability | Screens | API Group | Description |
|---|---|---|---|
| **Variable Recurring Payments (VRP)** | — (step-D candidate) | VRP/PISP | Recurring / sweeping payments under a single VRP consent |
| **Confirmation of Funds (CoF)** | send-money-amount | CBPII | Pre-payment funds-available check |
| **International payments** | send-money | PISP | Cross-currency payment with ExchangeRateInformation |
| **File / bulk payment** | — (step-D candidate) | PISP | ISO 20022 pain.001 batch upload |
| **Open Data** | atm-locator, products | Open Data | Unauthenticated ATM/branch locator + product comparison |
| **Event Notification** | notifications, consent-manager | events | Real-time consent-revoked + payment status events |

---

## App & Discovery Features

| Feature | Screen | API Group | Description |
|---|---|---|---|
| **atm-locator** | atm-locator | Open Data | `GET /atms`, `GET /branches` — geolocation finder (unauthenticated) |
| **notifications** | notifications | events | In-app event feed (consent-revoked, payment status) |
| **profile** | profile | — | User-visible app profile |
| **settings** | settings | — | App theme, language, notification toggles |
| **about** | about | — | App info, version, legal links, open-source licenses |

---

## Complete Screen List (39 Screens)

Single consumer persona — no flavor split. Every screen is `has_ui` only; none owns an API/data layer
(external API consumer — see PROJECT_CONFIG.yaml `backend.owned: false`).

### Consent & Authorisation (7)

1. **splash**
2. **consent-intro**
3. **consent-request**
4. **bank-authorize-handoff**
5. **auth-callback**
6. **consent-declined**
7. **consent-expired**

### Account Information (15)

8. **home**
9. **accounts**
10. **account-detail**
11. **transactions**
12. **transaction-detail**
13. **transaction-tags**
14. **beneficiaries**
15. **standing-orders**
16. **standing-order-detail**
17. **direct-debits**
18. **direct-debit-detail**
19. **products**
20. **pfm-dashboard**
21. **pfm-settings**
22. **business-insights**

### Payments (8)

23. **send-money**
24. **send-money-amount**
25. **send-money-confirm**
26. **payment-authorize-handoff**
27. **payment-result**
28. **payment-declined**
29. **standing-order-create**
30. **standing-order-edit**

### Discovery, Consents & App (9)

31. **atm-locator**
32. **consent-manager**
33. **notifications**
34. **profile**
35. **settings**
36. **about**
37. **terms-of-service**
38. **privacy-policy**
39. **licenses**

---

## Removed in the HSBC migration (19 screens)

The OBP-era screens below have no HSBC Open Banking equivalent and were deleted:

- **Auth/password (OBP DirectLogin):** login, forgot-password, change-password, sca-challenge
  (replaced by the redirect consent/authorise handoff — SCA happens at the bank).
- **No HSBC API surface (AISP is read-only consumer data):** cards, card-detail, fx-rates.
- **Field-officer / agent banking (HSBC OB is consumer PSD2 — no officer surface):** fo-dashboard,
  customer-search, customer-detail, customer-profile, customer-onboarding, corporate-onboarding,
  kyc-review, account-applications, application-detail, agent-registration, customer-messages, meetings.

---

## Feature Quality Baseline

All features start at quality score **50/100** (scaffold). Progression:

- **≥50:** Scaffolded (template-generated)
- **≥70:** Enriched (design tokens, state models, navigation edges)
- **≥85:** Fully specced (SPEC.md, API contract, mockups)
- **≥95:** Implemented (Kotlin code, tests passing)

---

## HSBC Open Banking API Coverage (14 groups, 85 endpoints)

| API Group | OBIE Role | Endpoints | Consumer Use |
|---|---|---|---|
| Authentication & Onboarding | security | 3 | DCR, OAuth2 token, PSU authorise redirect |
| Account Information (AISP) | aisp | 18 | accounts, balances, transactions, beneficiaries, standing orders, direct debits, scheduled payments, party, products, statements |
| Confirmation of Funds (CBPII) | cbpii | 4 | pre-payment funds check |
| Variable Recurring Payments (VRP) | pisp | 6 | recurring / sweeping payments |
| Domestic Payment | pisp | 4 | single immediate payment |
| Domestic Scheduled Payment | pisp | 3 | future-dated payment |
| Domestic Standing Order | pisp | 3 | recurring schedule |
| International Payment | pisp | 4 | cross-currency payment |
| International Scheduled Payment | pisp | 3 | future-dated international |
| International Standing Order | pisp | 3 | recurring international |
| File Payment / bulk | pisp | 5 | ISO 20022 batch payment |
| Multi-Bill Payment | pisp (HSBC-specific) | 2 | UK Business bulk bill pay |
| Event Notification | events | 4 | consent-revoked + status events |
| Open Data | opendata | 6 | unauthenticated ATM/branch + product reference |

---

## Notes

- **Consent-gated:** account data is unreadable without an AUTH-status account-access-consent; every
  payment needs its own payment-consent + a fresh authorise redirect (one payment = one authorisation).
- **No in-app credentials:** the PSU authenticates and completes SCA at HSBC during the redirect.
- **External API consumer:** no owned backend/DB; `idea-layer/server/` holds Ktorfit client contracts.
- **Shared layers:** DTOs (OBIE shapes), domain models, mTLS-aware API client, token/consent cache — all KMP.
- **State management:** Store5 repositories + ViewModels per feature.
