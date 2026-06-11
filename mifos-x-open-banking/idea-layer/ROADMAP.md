# mifos-x-open-banking — Roadmap

> **Empty-slate state** — feature roadmap is pending product-scope definition.
> Only architectural / infrastructure milestones are listed.

## v0.1 — Empty-slate Scaffold

**Status**: complete · completed: 2026-05-22

Goal: post-template-sync infrastructure is clean and consistent; product scope is ready to be defined on top.

- [x] Replace source tree with latest `kmp-project-template` (Stream-First architecture)
- [x] Update PROJECT.md + PROJECT_CONFIG.yaml to reflect actual source state
- [x] Scaffold idea-layer foundation docs (IDEA, FEATURES, REQUIREMENTS, ROADMAP, CHANGELOG, LAYER_STATUS)
- [x] Bootstrap design-system (`design-tokens.yaml`, `DESIGN.md`, `COMPONENTS.md`, `app-shell.yaml`)
- [x] Run `/idea verify` to surface remaining gaps
- [x] Remove template residue from source: `feature/{crypto,currency-rates,emi-calculator}` modules
- [x] Remove corresponding `idea-layer/screens/{crypto,currency-rates,emi-calculator}/` directories
- [x] Remove template residue from `core/data` (CryptoRepository, CurrencyRatesRepository) and `core/database` entities
- [x] Update settings.gradle.kts and root build.gradle.kts to drop excluded modules
- [x] Re-run `/idea sync` → 0 verify failures

## v0.2 — Product Scope Definition

**Status**: complete · completed: 2026-05-27

Goal: define the actual open-banking product roster.

- [x] Run `/idea-plan` to draft product vision (problem, target users, key flows)
- [x] Run `/idea add` for each declared feature
- [x] Run `/idea-enrich` per feature to produce SPEC/MOCKUP/PROMPTS
- [x] Review with stakeholders → `/idea approve`

39 screens defined · single consumer persona · consent-driven Open Banking scope · all sections approved at quality ≥85%.

## v0.2.5 — HSBC Open Banking Migration

**Status**: complete · completed: 2026-06-11

Goal: pivot from the OBP dual-persona app to a consumer Open Banking TPP (AISP + PISP) on HSBC's UK/CE sandbox (OBIE Read/Write v4.0).

- [x] Repoint backend OBP sandbox → HSBC UK/CE Open Banking (PROJECT_CONFIG.yaml, FAPI 1.0 Advanced auth)
- [x] Import the 14 HSBC API groups (85 endpoints) into `server/api_manifest.yaml`
- [x] Re-architect entry around consent: replace DirectLogin with the OBIE DCR + redirect authorise journey
- [x] Add consent/authorise handoff screens (consent-intro, consent-request, bank-authorize-handoff, auth-callback, consent-declined, consent-expired, payment-authorize-handoff, payment-declined)
- [x] Remove OBP-only + field-officer screens (login, forgot/change-password, cards, fx-rates, in-app SCA, full FO cluster)
- [x] Rewrite vision docset (IDEA, FEATURES, ROADMAP, REQUIREMENTS, idea-plan) to the consumer Open Banking story

## v0.3.0 — Consent Onboarding + AIS

**Status**: pending · target: W10

Milestone: a consumer can connect their HSBC account by consent and view their finances end-to-end on Android + Desktop.

Features: `splash`, `consent-intro`, `consent-request`, `bank-authorize-handoff`, `auth-callback`, `consent-declined`, `consent-expired`, `home`, `accounts`, `account-detail`, `transactions`, `transaction-detail`, `beneficiaries`, `standing-orders`, `direct-debits`, `products`

Exit criteria: User completes the consent + authorise-at-bank journey, lands on Home, and browses accounts, balances, and transactions (read-only AIS).

## v0.4.0 — Payments + Advanced Capabilities

**Status**: pending · target: W15

Milestone: full PISP payment surface plus the new VRP / CoF / Open Data / Events capabilities; iOS + Web (Wasm) builds passing.

Features: `send-money`, `send-money-amount`, `send-money-confirm`, `payment-authorize-handoff`, `payment-result`, `payment-declined`, `standing-order-create`, `standing-order-edit`, `transaction-tags`, `pfm-dashboard`, `pfm-settings`, `business-insights`, `atm-locator`, `consent-manager`, `notifications`

Capabilities: domestic + scheduled + standing-order + international payments · Confirmation of Funds · Variable Recurring Payments · Open Data (ATM/branch + products) · Event Notification · consent management

Platforms: Android · iOS · Desktop · Web

## v1.0.0 — Production Release

**Status**: pending · target: W16

Milestone: all platforms pass smoke tests; release artifacts signed and ready.

- [ ] End-to-end testing on all platforms
- [ ] Performance profiling (startup, scrolling, API latency)
- [ ] Security audit (token storage, certificate pinning)
- [ ] Release builds (signed APK/AAB, IPA, Desktop installers, Wasm)
- [ ] Store metadata + screenshots

Platforms: Android · iOS · Desktop · Web
Artifacts: apk, aab, ipa, exe, msi, dmg, deb, wasm

---

## Constraints (architecture-level, apply across all future work)

- Stream-First architecture (BaseViewModel + ScreenDataStream + Store5) — NO regression to MVI
- 4-platform parity (Android · iOS · Desktop · Web) — every feature ships on all 4
- Material 3 design system (light + dark) — brand-primary `#1800B1`
- WCAG AA accessibility — non-negotiable for production release
- Consent-driven model — every account read is gated by an AUTH-status account-access-consent; every payment runs its own consent + authorise redirect (SCA at the bank, never in-app)

## Deferred / Future

To be populated post-v1.0 (production HSBC TPP enrolment with eIDAS certs, real-time push for event notifications, multi-brand host expansion beyond uk-personal, File/bulk + Multi-Bill payment screens).
