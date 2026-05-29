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

39 features defined · 3 personas · 6-phase 16-week release plan · all sections approved at quality ≥85%.

## v0.3.0 — FO MVP

**Status**: pending · target: W10

Milestone: field officer persona functional end-to-end on Android + Desktop.

Features: `fo-dashboard`, `customer-search`, `customer-detail`, `customer-profile`, `customer-onboarding`, `corporate-onboarding`, `kyc-review`, `account-applications`, `application-detail`

Exit criteria: Field officer can search customers, onboard new ones, review KYC, process applications.

## v0.4.0 — Feature Complete

**Status**: pending · target: W15

Milestone: all 45 features shipped; iOS + Web (Wasm) builds passing.

Features: `consumer-home`, `standing-order-edit`, `standing-orders`, `direct-debits`, `direct-debit-detail`, `atm-locator`, `fx-rates`, `consent-manager`, `notifications`, `pfm-dashboard`, `products`, `transaction-tags`, `customer-messages`, `meetings`, `agent-registration`

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
- Material 3 design system (light + dark) — brand-primary `#4C662B`
- WCAG AA accessibility — non-negotiable for production release

## Deferred / Future

To be populated post-v1.0 (biometric auth, real-time push notifications, production bank OAuth setup).
