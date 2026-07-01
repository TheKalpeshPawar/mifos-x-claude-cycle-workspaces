# mifos-x-open-banking

> UK Open Banking **AISP** reference application — Kotlin Multiplatform (Compose Multiplatform).

## What this is

A reference app that demonstrates the **full Account Information Service Provider (AISP)
capability** of the UK Open Banking (OBIE) standard, built strictly to the standard and
running against the **HSBC UK sandbox**. It is a pure API **consumer** — it reads bank
account data with the customer's consent and **never moves money** (no payment initiation).

## Standard & backend

- **Standard:** OBIE Read/Write API — Account & Transaction (AIS), v4.0 (UK Personal brand).
- **Backend:** external HSBC UK sandbox REST API. This project owns **no** backend/DB.
- **Security:** FAPI 1.0 Advanced — mTLS, Dynamic Client Registration (SSA), OAuth2
  `authorization_code` + PKCE with a signed request object, `private_key_jwt` client auth,
  app-to-app PSU authentication (SCA), and 90-day consent reconfirmation.

## Scope (full AISP surface)

Consent journey + consent dashboard, then: accounts, account detail, balances,
transactions (history/filter/detail), beneficiaries, standing orders, direct debits,
scheduled payments, statements, product, party/parties, multi-currency, ATM locator
(Open Data), offers (M&S — feature-flagged). Authored fresh via `/idea-plan`.

## Source

- Repo: https://github.com/openMF/mifos-x-open-banking (fork: TheKalpeshPawar)
- Local working copy: symlinked from `/home/kalpesh/OpenSource/Mifos/mifos-x-open-banking`
  (branch `migration/hsbc-sandbox`) — built on the de-templated `kmp-project-template` shell.
- Package: `org.mifosx.openbanking` · Platforms: Android, iOS, Desktop, Web.

## Status

Idea-layer pending — rebuilt from a clean slate on 2026-06-29. Machine-readable config:
`PROJECT_CONFIG.yaml`. HSBC sandbox material: `/home/kalpesh/OpenBankingProject/HSBC_Sandbox/`
(docs `00-HOW-TO-USE-THE-SANDBOX.md`, `01-account-information-sharing.md`); AIS swagger:
`/home/kalpesh/OpenBankingProject/specs/hsbc-sandbox/openapi/account-info-4.0-personal.yaml`.
