# User onboarding — Feature Specification

> Generated from `screens/user-onboarding/ui.yaml` by `/idea-feature-export`
> Schema version: 2.0.0 · Source hash: `6aca2474d208`
> Endpoints: 0 · DTOs: 0 · Components: 5 · Test scenarios: 4

## Export gate exception

This feature fails export gates **E1** (state_model has ≥1 ViewModel) and **E3** (api[] has
≥1 entry). Step 1.5 says SKIP with "run `/idea enrich` first" — but enrichment cannot add a
ViewModel that does not exist in source. `IntroScreen.kt` is a stateless composable with
`viewmodel: null`, verified during the 2026-07-28 reverse sync. The gate would never clear, so
this exports with the exception recorded rather than being skipped silently.
Recorded in `PIPELINE_STATE#capabilities.idea-feature-export.metrics.e1_e3_exceptions`.

## 1. Overview

First-run education before the PSU connects an HSBC account. Establishes UK Open Banking as
FCA-regulated and FAPI 1.0 Advanced-secured, and hands off to `login`.

| Attribute | Value |
|---|---|
| Feature ID | `user-onboarding` |
| Cluster | consent |
| Priority | must (FR-001, FR-002) |
| Status | approved · quality 95 |
| Archetype | onboarding |
| Source module | `feature/login` — **implemented** as `onboarding/IntroScreen.kt` |
| Route | `IntroRoute` (data object) — startDestination of `AuthGraphRoute` |

**No module of its own.** It ships inside `feature/login`, one of two screens in that
position (the other is `licences` inside `feature/settings`).

### Prose corrected at source 2026-07-30

`docs.yaml#description` previously described a **three-step pager** (intro →
permissions_overview → consent_explainer) with an `ob_explainer` bottom sheet, and `flow.yaml`
carried six transitions between those steps. None of it ships: `states: [intro]`,
`IntroScreen.kt`, `viewmodel: null`, and TC-ONB-003 asserts no state and no I/O.

Rather than documenting the divergence and leaving it, the source YAML was corrected in the
same pass — the description now describes the single screen, and the six phantom transitions
were dropped from `flow.yaml`, leaving only the real edge to `login`. This SPEC and the screen
YAML now agree.

## 2. Screen inventory

| Component | Type | Purpose |
|---|---|---|
| `hero_illustration` | image | decorative hero |
| `intro_headline` | text | headline |
| `intro_body` | text | what UK Open Banking is |
| `trust_chips` | chip_group | FCA-regulated / FAPI-secured trust markers |
| `continue_button` | button | primary CTA → `login` |

Single state: `intro`.

## 3. State model

**None.** No ViewModel, no state fields, no actions, no DI. The continue button is a
**nav-host callback** (`onContinue → LoginRoute`), not a dispatched action — which is why the
feature contributes zero rows to `TAG_REGISTRY.yaml`.

This is a deliberate shape, not an enrichment gap: a static education screen with no I/O has
nothing to model.

## 4. Navigation

| Origin | Trigger | Target |
|---|---|---|
| `app_launch_no_consent` | first run, or post-revoke | `user-onboarding` |
| `post_revoke_redirect` | consent revoked from the dashboard | `user-onboarding` |
| `continue_button` | "Connect with HSBC" | `login` |

**Skipped on the re-consent path** (TC-ONB-004) — a PSU reconfirming an existing connection
goes to `LoginRenewRoute` inside the authenticated host, not back through onboarding.

`flow.yaml` now declares exactly one transition — `user-onboarding → login` — plus the two
entry points above. The six phantom sub-screen transitions were removed 2026-07-30.

## 5. API dependencies

**None.** Zero endpoints, zero DTOs. `API.md` records the absence explicitly rather than being
omitted, so a reader can distinguish "no API" from "not yet exported".

## 6. Design tokens

`design-tokens.yaml` 2.1.0 — `image` hero, `chip_group` for trust markers, `button_filled`
(`primary`, pill) for the CTA. Motion dial 2: no carousel, no auto-advance.
Canonical brand spec: `design-system/DESIGN.md` 1.1.0.

## 7. Test mapping

| TC | Assertion | Expected path |
|---|---|---|
| TC-ONB-001 | hero, headline, body, trust chips and CTA render | `feature/login/src/androidUnitTest/.../IntroScreenRobolectricTest.kt` |
| TC-ONB-002 | Continue navigates to login | ↑ |
| TC-ONB-003 | **screen holds no state and performs no I/O** | ↑ |
| TC-ONB-004 | intro skipped on the re-consent path | ↑ |

TC-ONB-003 is the guard that keeps this screen stateless — it is the assertion that would fail
if someone added a ViewModel to satisfy gate E1.

## 8. Notes

`docs.yaml` declares no `flow_ref` despite `flows/onboarding-consent.yaml` existing.
