# REQUIREMENTS.md — mifos-x-open-banking

> Imported from the HSBC UK Open Banking **Account & Transaction API (AIS) v4.0** spec
> (`account-info-4.0-personal.yaml`) via `/idea-import-api` on 2026-06-29.
> This project is a pure **client** of the external HSBC AIS API — these are **consumer
> contracts** for Ktorfit codegen, not an owned backend (RULE-IDEA-SERVER-DATA-001 skips
> owned-DB checks; `backend.owned: false`).

## API summary

| Field | Value |
|---|---|
| API | HSBC UK Open Banking — Account & Transaction (AIS) |
| Standard | OBIE Read/Write v4.0 |
| Brand | UK Personal (HSBC) |
| Resource base URL | `https://sandbox.ob.hsbc.co.uk/mock/obie/open-banking/v4.0/aisp` |
| OAuth2 base (v1.1) | `https://sandbox.ob.hsbc.co.uk/mock/obie/open-banking/v1.1/oauth2` |
| DCR base (v3.2) | `https://sandbox.ob.hsbc.co.uk/mock/obie/open-banking/v3.2/oauth2` |
| Resource auth | `Authorization: Bearer <token>` (FAPI 1.0 Advanced; mTLS + `x-fapi-*` headers at transport) |
| Role | AISP — read-only |

## Security & flow (FAPI 1.0 Advanced)

1. **DCR** (`POST /register`, DCR v3.2.1) — register the client once using a PS256-signed SSA → `client_id`.
2. **Client-credentials token** (`POST /oauth2/token`, `private_key_jwt`, `scope=accounts`) → stages a consent.
3. **Create consent** (`POST /account-access-consents`) with a `Permissions[]` list → `ConsentId` (`AwaitingAuthorisation`).
4. **PSU authorisation** (`GET /oauth2/authorize`, signed request object + PKCE S256, app-to-app) — PSU authenticates (SCA), approves the requested permission set, selects accounts.
5. **Token exchange** (`POST /oauth2/token`, `authorization_code`) → PSU-bound access + refresh tokens.
6. **Resource access** — `GET` the AIS resources below with the PSU bearer token.
7. **Lifecycle** — `GET`/`DELETE` consent; refresh token; 90-day reconfirmation (SCA-RTS Art 36(6)/10A).

> AIS is read-only — no detached `x-jws-signature` is required on these GETs.

## Consent permissions (`Data.Permissions[]`)

`ReadAccountsBasic` · `ReadAccountsDetail` · `ReadBalances` · `ReadBeneficiariesBasic` · `ReadBeneficiariesDetail` · `ReadDirectDebits` · `ReadPAN` · `ReadParty` · `ReadPartyPSU` · `ReadProducts` · `ReadOffers` · `ReadScheduledPaymentsBasic` · `ReadScheduledPaymentsDetail` · `ReadStandingOrdersBasic` · `ReadStandingOrdersDetail` · `ReadStatementsBasic` · `ReadStatementsDetail` · `ReadTransactionsBasic` · `ReadTransactionsCredits` · `ReadTransactionsDebits` · `ReadTransactionsDetail`

## SFR — endpoints (Account & Transaction API)

| SFR | RPC | Purpose | Path params / query | Returns (DTO) | Permission | Auth |
|---|---|---|---|---|---|:--:|
| SFR-AIS-01 | `POST /account-access-consents` | Create account-access-consent (permission list + expiry) | body `OBReadConsent1` | `OBReadConsentResponse1` | — (declares permissions) | Bearer (CC) |
| SFR-AIS-02 | `GET /account-access-consents/{ConsentId}` | Consent status | `ConsentId` | `OBReadConsentResponse1` | — | Bearer (CC) |
| SFR-AIS-03 | `DELETE /account-access-consents/{ConsentId}` | Revoke consent | `ConsentId` | — (204) | — | Bearer (CC) |
| SFR-AIS-04 | `GET /accounts` | List authorised accounts | — | `OBReadAccount6` | ReadAccountsBasic/Detail | Bearer (PSU) |
| SFR-AIS-05 | `GET /accounts/{AccountId}` | Account detail | `AccountId` | `OBReadAccount6` | ReadAccountsBasic/Detail | Bearer (PSU) |
| SFR-AIS-06 | `GET /accounts/{AccountId}/balances` | Account balances | `AccountId` | `OBReadBalance1` | ReadBalances | Bearer (PSU) |
| SFR-AIS-07 | `GET /accounts/{AccountId}/transactions` | Transactions (from/toBookingDateTime, credits/debits) | `AccountId`, query | `OBReadTransaction6` | ReadTransactionsBasic/Credits/Debits/Detail | Bearer (PSU) |
| SFR-AIS-08 | `GET /accounts/{AccountId}/beneficiaries` | Beneficiaries | `AccountId` | `OBReadBeneficiary5` | ReadBeneficiariesBasic/Detail | Bearer (PSU) |
| SFR-AIS-09 | `GET /accounts/{AccountId}/standing-orders` | Standing orders | `AccountId` | `OBReadStandingOrder6` | ReadStandingOrdersBasic/Detail | Bearer (PSU) |
| SFR-AIS-10 | `GET /accounts/{AccountId}/direct-debits` | Direct debits | `AccountId` | `OBReadDirectDebit2` | ReadDirectDebits | Bearer (PSU) |
| SFR-AIS-11 | `GET /accounts/{AccountId}/scheduled-payments` | Scheduled payments | `AccountId` | `OBReadScheduledPayment3` | ReadScheduledPaymentsBasic/Detail | Bearer (PSU) |
| SFR-AIS-12 | `GET /accounts/{AccountId}/statements` | Statements list (from/toStatementDateTime) | `AccountId`, query | `OBReadStatement2` | ReadStatementsBasic/Detail | Bearer (PSU) |
| SFR-AIS-13 | `GET /accounts/{AccountId}/statements/{StatementId}` | Statement detail | `AccountId`, `StatementId` | `OBReadStatement2` | ReadStatementsBasic/Detail | Bearer (PSU) |
| SFR-AIS-14 | `GET /accounts/{AccountId}/statements/{StatementId}/transactions` | Transactions within a statement | `AccountId`, `StatementId` | `OBReadTransaction6` | ReadTransactionsBasic/Detail | Bearer (PSU) |
| SFR-AIS-15 | `GET /accounts/{AccountId}/statements/{StatementId}/file` | Statement file / PDF | `AccountId`, `StatementId` | binary (application/pdf) | ReadStatementsBasic/Detail | Bearer (PSU) |
| SFR-AIS-16 | `GET /accounts/{AccountId}/product` | Account product (fees/rates) | `AccountId` | `OBReadProduct2` | ReadProducts | Bearer (PSU) |
| SFR-AIS-17 | `GET /accounts/{AccountId}/party` | Account holder — single party | `AccountId` | `OBReadParty2` | ReadParty | Bearer (PSU) |
| SFR-AIS-18 | `GET /accounts/{AccountId}/parties` | Account owner(s)/operator(s) — multiple parties | `AccountId` | `OBReadParty3` | ReadParty | Bearer (PSU) |
| SFR-AIS-19 | `GET /accounts/{AccountId}/offers` | Account offers (overdrafts, balance transfers) | `AccountId` | `OBReadOffer1` | ReadOffers | Bearer (PSU) |

## DTOs (OBIE response models — generated by `/idea-generate-dtos` from the swagger)

`OBReadConsent1`, `OBReadConsentResponse1`, `OBReadAccount6`, `OBReadBalance1`, `OBReadTransaction6`,
`OBReadBeneficiary5`, `OBReadStandingOrder6`, `OBReadDirectDebit2`, `OBReadScheduledPayment3`,
`OBReadStatement2`, `OBReadProduct2`, `OBReadParty2`, `OBReadParty3`, `OBReadOffer1`.

> Every response uses the OBIE envelope: top-level `Data` (payload), `Links` (`Self`/`Next`/`Prev`/`First`/`Last`
> pagination), `Meta` (`TotalPages`, `FirstAvailableDateTime`). Money is `{Amount, Currency}`.

## Out of scope (not imported)

- **PISP** (payment initiation), **CBPII** (confirmation of funds) — not an AISP capability.
- Bulk endpoints (`/balances`, `/transactions` at root) — not present in the personal v4.0 spec.
