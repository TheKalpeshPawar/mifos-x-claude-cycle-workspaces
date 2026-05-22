# mifos-x-open-banking — Roadmap

> **Empty-slate state** — feature roadmap is pending product-scope definition.
> Only architectural / infrastructure milestones are listed.

## v0.1 — Empty-slate Scaffold (current)

**Status**: in progress · target: 2026-Q3

Goal: post-template-sync infrastructure is clean and consistent; product scope is ready to be defined on top.

- [x] Replace source tree with latest `kmp-project-template` (Stream-First architecture)
- [x] Update PROJECT.md + PROJECT_CONFIG.yaml to reflect actual source state
- [x] Scaffold idea-layer foundation docs (IDEA, FEATURES, REQUIREMENTS, ROADMAP, CHANGELOG, LAYER_STATUS)
- [x] Bootstrap design-system (`design-tokens.yaml`, `DESIGN.md`, `COMPONENTS.md`, `app-shell.yaml`)
- [x] Run `/idea verify` to surface remaining gaps
- [ ] Remove template residue from source: `feature/{crypto,currency-rates,emi-calculator}` modules
- [ ] Remove corresponding `idea-layer/screens/{crypto,currency-rates,emi-calculator}/` directories
- [ ] Remove template residue from `core/data` (CryptoRepository, CurrencyRatesRepository) and `core/database` entities
- [ ] Update settings.gradle.kts and root build.gradle.kts to drop excluded modules
- [ ] Re-run `/idea sync` → 0 verify failures

## v0.2 — Product Scope Definition

**Status**: pending · target: TBD

Goal: define the actual open-banking product roster.

- [ ] Run `/idea-plan` to draft product vision (problem, target users, key flows)
- [ ] Run `/idea add` for each declared feature
- [ ] Run `/idea-enrich` per feature to produce SPEC/MOCKUP/PROMPTS
- [ ] Review with stakeholders → `/idea approve`

## v0.3+ — Per-feature Implementation

**Status**: pending · target: TBD

To be planned per feature once v0.2 closes.

---

## Constraints (architecture-level, apply across all future work)

- Stream-First architecture (BaseViewModel + ScreenDataStream + Store5) — NO regression to MVI
- 4-platform parity (Android · iOS · Desktop · Web) — every feature ships on all 4
- Material 3 design system (light + dark) — brand-primary `#1800B1`
- WCAG AA accessibility — non-negotiable for production release

## Deferred / Future

To be populated once product scope is set.
