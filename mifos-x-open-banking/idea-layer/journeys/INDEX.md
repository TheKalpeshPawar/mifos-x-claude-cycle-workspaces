# Journeys Index — mifos-x-open-banking

> Auto-maintained by `/idea journey`. 9 journeys across 2 personas.
> Last updated: 2026-05-30

---

## Consumer Persona (5 journeys)

| Journey | Screens | Tier | Status |
|---------|---------|------|--------|
| [consumer-authentication](./consumer-authentication.yaml) | splash, login, home | maximum | draft |
| [consumer-forgot-password](./consumer-forgot-password.yaml) | login, forgot-password | maximum | draft |
| [consumer-accounts-payments](./consumer-accounts-payments.yaml) | home, accounts, account-detail, transactions, transaction-detail, transaction-tags, send-money, send-money-confirm, beneficiaries | maximum | draft |
| [consumer-cards-financing](./consumer-cards-financing.yaml) | cards, card-detail, transactions, standing-orders, direct-debits, direct-debit-detail, standing-order-detail, standing-order-edit | maximum | draft |
| [consumer-insights-utilities](./consumer-insights-utilities.yaml) | pfm-dashboard, transactions, fx-rates, send-money, atm-locator, products, notifications | medium | draft |
| [consumer-profile-settings](./consumer-profile-settings.yaml) | profile, settings, change-password, consent-manager, about, privacy-policy, terms-of-service, licenses | maximum | draft |

## Field Officer Persona (3 journeys)

| Journey | Screens | Tier | Status |
|---------|---------|------|--------|
| [fo-authentication-registration](./fo-authentication-registration.yaml) | splash, agent-registration, login, fo-dashboard | maximum | draft |
| [fo-customer-lifecycle](./fo-customer-lifecycle.yaml) | customer-search, customer-onboarding, kyc-review, customer-detail, customer-profile, customer-messages, corporate-onboarding | maximum | draft |
| [fo-operations-management](./fo-operations-management.yaml) | fo-dashboard, meetings, account-applications, application-detail, customer-detail, customer-messages | maximum | draft |

---

## Coverage

All 44 screens are covered by at least one journey. Some screens appear in multiple journeys (shared screens: splash, login, home, profile, settings, fo-dashboard, customer-detail, customer-messages, transactions, send-money).

## Next Steps

- Run `/idea journey link {id}` to populate bidirectional flow.yaml back-refs
- Run `/idea journey verify` to check RULE-JOURNEY-001 J1–J7
- Run `/idea sync` to validate idea-layer health
