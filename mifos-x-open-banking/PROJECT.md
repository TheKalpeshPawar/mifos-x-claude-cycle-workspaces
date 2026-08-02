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

## Release

Adopted 2026-07-28 from the existing fastlane setup. Authoritative values live in
`deployment-layer/DEPLOYMENT_PROJECT_CONFIG.yaml`; this block is the `/idea-deploy`
platform switchboard.

```yaml
release:
  strategy: kmp-fastlane
  deploy_mode: local
  fastlane_setup: true
  primary_locale: en-GB
  platforms:
    android_firebase:
      enabled: true
      required_local_secrets:
        - secrets/android/firebaseAppDistributionServiceCredentialsFile.json
    android_playstore_internal:
      enabled: false        # keystore is the shared kmp-project-template key; see Known gaps
      required_local_secrets:
        - secrets/android/playStorePublishServiceCredentialsFile.json
    ios_testflight:
      enabled: false        # no AuthKey.p8, no GoogleService-Info.plist
    ios_appstore:
      enabled: false
    web:
      enabled: false        # cmp-web builds, but no deploy target chosen yet
    desktop:
      enabled: false        # cmp-desktop builds, no store/packaging configured
```

### Known gaps

- **Firebase service-account JSON is not on this machine.** Vault alias
  `firebase_service_account_json` (vault `mifos-x`) is registered but not pulled —
  Bitwarden login is outstanding. `secrets_demo/` holds a `REPLACE_WITH_*` placeholder
  only; it is not a usable credential.
- **`fastlane/FastFile` / `AppFile` / `PluginFile` are mis-cased.** Fastlane loads only
  `Fastfile` / `Appfile` / `Pluginfile`; on a case-sensitive filesystem every lane fails
  to load. Blocks all Play Store and iOS actions. Does not affect Firebase App
  Distribution, which uses the direct service-account JWT API.
- **Signing key: project-specific key generated 2026-07-28** (`keystores/upload.keystore`,
  alias `MifosXOpenBanking`, PKCS12/RSA-2048, valid to 2051), replacing the shared template
  key. **Its password is still the template default `Wizard@123`, committed in plaintext in
  both `fastlane-config/project_config.rb` and `cmp-android/build.gradle.kts`** — rotate it
  before enabling `android_playstore_internal`, since Play Store binds the signing key
  permanently on first upload. The superseded `{original,release}_keystore.keystore` remain
  git-tracked from Initial commit and should be deleted once nothing references them.
- **No `fastlane/metadata/` tree**, so all store-listing copy and screenshots are unseeded.

## Status

Idea-layer pending — rebuilt from a clean slate on 2026-06-29. Machine-readable config:
`PROJECT_CONFIG.yaml`. HSBC sandbox material: `/home/kalpesh/OpenBankingProject/HSBC_Sandbox/`
(docs `00-HOW-TO-USE-THE-SANDBOX.md`, `01-account-information-sharing.md`); AIS swagger:
`/home/kalpesh/OpenBankingProject/specs/hsbc-sandbox/openapi/account-info-4.0-personal.yaml`.
